---
title: 'Python字符串及其常用操作'
date: 2019-08-29 15:04:43
tags: []
published: true
hideInList: false
feature: 
---
字符串可以使用索引访问
字符串是不可变的
字符串是可迭代对象
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
join是字符串的方法，参数是可迭代对象，接受者是分隔符
```
In[]：
l = ['i','use','python']
','.join(l)
Out[]：
'i,use,python'
```
字符串分割
















