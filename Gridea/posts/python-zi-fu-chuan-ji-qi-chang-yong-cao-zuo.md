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









