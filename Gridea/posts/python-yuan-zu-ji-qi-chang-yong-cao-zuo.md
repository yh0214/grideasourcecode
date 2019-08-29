---
title: 'Python元组及其常用操作'
date: 2019-08-29 13:57:16
tags: []
published: true
hideInList: false
feature: 
---
元组：tuple
tuple和list非常相似，但是tuple一旦初始化就不能修改
tuple获取元素的方法与list一样，通过索引获取
定义一个空的tuple：
```
t = ()
```
但是要定义一个只有一个元素的tuple，必须加一个逗号，来消除歧义
```
t = (1,)
```
“可变的”tuple
```
In[]：
t = ('a','b',['python','java'])
print(t)
t[2][1] = 'php'
print(t)
Out[]：
('a', 'b', ['python', 'java'])
('a', 'b', ['python', 'php'])
```








