---
title: '装饰器'
date: 2019-10-10 13:48:00
tags: []
published: true
hideInList: false
feature: 
---
先来看一个函数，logger
```
def logger(fn):
    def warp(*args,**kwargs):
        print('call {}'.format(fn.__name__))
        ret = fn(*args,**kwargs)
        print('{} called'.format(fn.__name__))
        return ret
    return warp
```
这个函数的参数是函数，返回值也是一个函数
先定义一个加函数，作为参数传入logger
```
def add(x,y):
    return x + y
```
然后定义一个函数
```
In[]：
loged_add = logger(add)
loged_add(3,5)
Out[]：
call add
add called
8
```
loged_add = logger(add)这一步是把add函数作为参数传入logger中，这个时候没有发生任何计算，loged_add是一个函数，这个函数就是wrap
可以查看下loged_add
```
In[]：loged_add
Out[]：<function __main__.logger.<locals>.warp(*args, **kwargs)>
```
以上这种场景通常用于作为参数的函数执行前后需要一些额外操作
再引入一个东西
```
import datetime

def logger(fn):
    def wrap(*args,**kwargs):
        start = datetime.datetime.now()
        ret = fn(*args,**kwargs)
        end = datetime.datetime.now()
        print('{} called took {}'.format(fn.__name__,end-start))
        return ret
    return wrap
```
可以看看这个函数执行了多久
```
import time

def sleep(x):
    time.sleep(x)
```
```
In[]：loged_sleep = logger(sleep)
```
```
In[]：loged_sleep(3)
Out[]：sleep called took 0:00:03
```
装饰器
换一种语法糖
```
@logger
def sleep(x):
    time.sleep(x)
```
这时候，就可以将封装发生在函数定义的时候
这是python的一种语法，可以更方便的去定义我们的函数
@logger的方式和loged_add = logger(add)是等效的
参数是一个函数，返回值是一个函数的函数，就可以作为装饰器
只有用@语法来写的时候，才称为装饰器。
