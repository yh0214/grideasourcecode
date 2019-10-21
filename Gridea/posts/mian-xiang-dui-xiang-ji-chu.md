---
title: '面向对象基础'
date: 2019-10-16 09:07:30
tags: []
published: true
hideInList: false
feature: 
---
面向对象（OOP）是一种编程范式
范式可以认为是一组方法论
编程范式就是一组如何组织代码的方法论
OOP的世界观：
世界是由对象组成的
对象具有运动规律和内部状态
对象之间可以相互作用
OOP的特征：
封装
继承
多态
类的定义
```
class Door:
    def __init__(self,number,status):
        self.number = number
        self.status = status

door = Door(10001,'closed')
```
```
In[]：door.number
Out[]：10001
```
看一下self
```
class D:
    def __init__(self):
        print(id(self))
```
```
In[]：d = D()
Out[]：101570264
```
```
In[]：id(d)
Out[]：101570264
```
这个self就是d，而且是先有的self
__init__函数并不是来生成对象的，只是来初始化类
类中定义方法及调用
```
class Door:
    def __init__(self,number,status):
        self.number = number
        self.status = status
    
    def open(self):
        self.status = "opening"

    def close(self):
        self.status = "closed"
```
```
door = Door(10001,'closed')
```
```
In[]：door.status
Out[]：'closed'
```
```
door.open()
```
```
In[]：door.status
Out[]：'opening'
```
```
door.close()
```
```
In[]：door.status
Out[]：'closed'
```












