---
title: 'Python可迭代对象与迭代器'
date: 2019-09-10 15:03:31
tags: []
published: true
hideInList: false
feature: 
---
# 可迭代对象
```
In[]：
r = range(10)
r.__iter__
Out[]：
<method-wrapper '__iter__' of range object at 0x0000000006013570>
```
有__iter__方法的对象叫可迭代对象
for in语句需要可迭代对象
# 迭代器
迭代器是可迭代对象
```
In[]：
it = iter(range(10))
it.__next__
Out[]：
<method-wrapper '__next__' of range_iterator object at 0x000000000628CD50>
```
有__next__方法的可迭代对象叫迭代器
可迭代对象可以转换为迭代器
iter函数可以把一个可迭代对象转换为迭代器













