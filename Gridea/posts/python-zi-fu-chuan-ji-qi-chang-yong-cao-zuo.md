---
title: 'Python字符串及其常用操作'
date: 2019-08-29 15:04:43
tags: []
published: true
hideInList: false
feature: 
---
# 定义
单/双引号只能定义单行字符串，不能定义多行字符串
三引号可以定义多行字符串
# 转义
转义符号用“\”
转义符号还可以使用前缀关键字r，它代表的意思是：后面的字符串是raw string
特别是写正则的时候需要加上r前缀
u前缀代表unicode字符串
b前缀代表bytes
# 下标操作
字符串可以使用下标访问
**字符串是不可变的**
**字符串是迭代器，是可迭代对象**
list()可以将字符串转化为列表
```
In[]：
s = 'python'
list(s)
Out[]：
['p', 'y', 't', 'h', 'o', 'n']
```
count()可以计算字符串中某个字符出现的次数
```
In[]：
s = '霍霍霍霍霍元甲'
s.count('霍')
Out[]：
5
```
index()可以搜索字符串中某个字符的位置
```
In[]：
s = '霍霍霍霍霍元甲'
s.index('霍')
Out[]：
0
```
# 字符串的操作
## join
join是字符串的方法，参数是可迭代对象，接受者是分隔符
```
In[]：
l = ['i','use','python']
','.join(l)
Out[]：
'i,use,python'
```
## 字符串分割
### str.split
```
In[]：
help(str.split)
Out[]：
Help on method_descriptor:
split(self, /, sep=None, maxsplit=-1)
    Return a list of the words in the string, using sep as the delimiter string.
    sep
      The delimiter according which to split the string.
      None (the default value) means split according to any whitespace,
      and discard empty strings from the result.
    maxsplit
      Maximum number of splits to do.
      -1 (the default value) means no limit.
```
str.split()，默认使用空格分割，当遇到多个空格，默认会当作一个空格处理
```
In[]：
s = "life        is short"
s.split()
Out[]：
['life', 'is', 'short']
```
但是，当指定了一个空格为分隔符，一个空格就当作一个空格处理
```
In[]：
s = "life        is short"
s.split(' ')
Out[]：
['life', '', '', '', '', '', '', '', 'is', 'short']
```
参数maxsplit表示从左到右分割多少次，默认为-1，表示分割所有分隔符
```
In[]：
s = "life        is short"
s.split(maxsplit=1)
Out[]：
['life', 'is short']
```
分隔符可以是任意字符串
```
In[]：
s = "life        is short"
s.split('is')
Out[]：
['life        ', ' short']
```
### str.rsplit
```
In[]：
help(str.rsplit)
Out[]：
Help on method_descriptor:
rsplit(self, /, sep=None, maxsplit=-1)
    Return a list of the words in the string, using sep as the delimiter string.
      sep
        The delimiter according which to split the string.
        None (the default value) means split according to any whitespace,
        and discard empty strings from the result.
      maxsplit
        Maximum number of splits to do.
        -1 (the default value) means no limit.
    Splits are done starting at the end of the string and working to the front.
```
rsplit就是从右往左分割的
### str.splitlines
```
In[]：
help(str.splitlines)
Out[]：
Help on method_descriptor:
splitlines(self, /, keepends=False)
    Return a list of the lines in the string, breaking at line boundaries.
    Line breaks are not included in the resulting list unless keepends is given and
    true.
```
splitlines()方法比较简单，但是很实用，就是在读文件的时候，可以快速分割行
按行分割，并且返回值不带换行符
```
In[]：
s = '''life
is
short
'''
s.splitlines()
Out[]：
['life', 'is', 'short']
```
按行分割，并且返回值带换行符
```
In[]：
s = '''life
is
short
'''
s.splitlines(True)
Out[]：
['life\n', 'is\n', 'short\n']
```
### str.partition
```
In[]：
help(str.partition)
Out[]：
Help on method_descriptor:
partition(self, sep, /)
    Partition the string into three parts using the given separator.
    This will search for the separator in the string.  If the separator is found,
    returns a 3-tuple containing the part before the separator, the separator
    itself, and the part after it.
    If the separator is not found, returns a 3-tuple containing the original string
    and two empty strings.
```
partition其实就是split的指定分隔符，maxsplit=1的特殊版本
```
In[]：
s = 'life is short'
s.partition(' ')
Out[]：
('life', ' ', 'is short')
```
* 总是返回一个三元组（由三个元素构成的）
* 按照传入的分隔符分割一次
* 返回结果是head,sep,tail
rpartition是partition从右往左的版本
通常在对配置文件做操作的时候，我们会用partition
## 大小写转换
### str.upper & str.lower
```
In[]：
s = 'tEst'
s.upper()
Out[]：
'TEST'
```
```
In[]：
s = 'tEst'
s.lower()
Out[]：
'test'
```
upper和lower两个方法都是**原地不修改，有返回值**
### str.swapcase
大小写互换，**原地不修改，有返回值**
```
In[]：
s = 'tEst'
s.swapcase()
Out[]：
'TeST'
```
## 排版
### str.title
每个单词首字母大写，**原地不修改，有返回值**
```
In[]：
s = 'tEst hello'
s.title()
Out[]：
'Test Hello'
```
### str.capitalize
一句话的首字母大写，**原地不修改，有返回值**
```
In[]：
s = 'life is short'
s.capitalize()
Out[]：
'Life is short'
```
### str.center
在指定支付长度中居中，**原地不修改，有返回值**
```
In[]：
s = 'test'
s.center(100)
Out[]：
'                                                test                                                '
```
```
In[]：
s = 'test'
s.center(100,'-')
Out[]：
'------------------------------------------------test------------------------------------------------'
```
### str.zfill
用0补足，**原地不修改，有返回值**
```
In[]：
s = 'tEst'
s.zfill(50)
Out[]：
'0000000000000000000000000000000000000000000000tEst'
```
## 修改
### str.replace
replace返回一个新的字符串，原地不修改，有返回值
```
In[]：
s = 'life is short'
s.replace('short','long')
Out[]：
'life is long'
```
### str.strip
去除字符串前后的空格
```
In[]：
s = '   life is short   '
s.strip()
Out[]：
'life is short'
```
其实strip去除的是空白字符，不只是空格
```
In[]：
s = '\t\n\r life is short '
s.strip()
Out[]：
'life is short'
```
而且strip可以去除指定的字符，但是仅限于前后
```
In[]：
s = '#-#   life is short  #-#'
s.strip('#')
Out[]：
'-#   life is short  #-'
```
还可以去除多个字符，按照先后顺序
```
In[]：
s = '###  H is happy H #'
s.strip('#H ')
Out[]：
'is happy'
```
### str.lstrip
只移除左边的
```
In[]：
s = '###life is short'
s.lstrip('#')
Out[]：
'life is short'
```
只移除右边的
```
In[]：
s = 'life is short###'
s.rstrip('#')
Out[]：
'life is short'
```
### str.ljust
用来填充字符，原字符串在左边
```
In[]：
s = 'life is short'
s.ljust(50)
Out[]：
'life is short                                     '
```
可以指定填充字符
```
In[]：
s = 'life is short'
s.ljust(50,'$')
Out[]：
'life is short$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$'
```
### str.rjust
用来填充字符，原字符串在右边
```
In[]：
s = 'life is short'
s.rjust(50,'$')
Out[]：
'$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$life is short'
```
## 查找
### str.find
从左往右查找，找到第一个子串，返回子串首字母的索引
```
In[]：
s = 'life is short'
s.find('f')
Out[]：
2
```
当子串不存在的时候返回-1
```
In[]：
s = 'life is short'
s.find('F')
Out[]：
-1
```
start参数和stop参数是开始查找的索引和结束查找的索引，左闭右开，不包含end参数，end=-1代表的就是最后
### str.rfind
find从右往左的版本
```
In[]：
s = 'life is funny'
s.rfind('f')
Out[]：
8
```
### str.index
index查找，子串不存在时，抛出ValueError
find查找时，子串不存在，返回-1
这是index和find的唯一区别
### str.rindex
rindex是index从右往左的版本
### str.count
计算参数在字符串中的个数，当count计算的值不存在的时候返回0
count同样也是有start参数和end参数的
```
In[]：
s = '###life is funny###'
s.count('#')
Out[]：
6
```
### str.startswith
判断字符串是否以某个前缀开始，返回结果是bool值
start参数，end参数和find一样
```
In[]：
s = '###life is funny###'
s.startswith('#')
Out[]：
True
```
### str.endswith
endswith判断字符串是否以某个后缀结束，返回bool
start参数，end参数和find一样
```
In[]：
s = '###life is funny###'
s.endswith('#')
Out[]：
True
```
### is*
is\*的意思就是，字符串的方法里有一串以is开头的方法，代表的意思就是“是否是xxx”
isalnum判断是否是只含有字母
```
In[]：
s = 'qwer'
s.isalnum()
Out[]：
True
```
isdecimal判断是否是数字
```
In[]：
s = '12345'
s.isdecimal()
Out[]：
True
```
isidentifier判断是否是字母或者下划线开头，且包含字母数字和下划线
```
In[]：
s = '_is1'
s.isidentifier()
Out[]：
True
```









