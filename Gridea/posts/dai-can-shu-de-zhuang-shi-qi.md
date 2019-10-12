---
title: '带参数的装饰器'
date: 2019-10-12 13:57:56
tags: []
published: true
hideInList: false
feature: 
---
首先看一下装饰器的副作用
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
```
import time
@logger
def sleep(x):
    time.sleep(x)
```
使用装饰器定义一个sleep函数，查看它的'__name__'
```
In[]:sleep.__name__
Out[]:'wrap'
```
是wrap而不是sleep，这就是使用了装饰器后的副作用
如何解决？
首先可以使用赋值
```
import datetime
def logger(fn):
    def wrap(*args,**kwargs):
        start = datetime.datetime.now()
        ret = fn(*args,**kwargs)
        end = datetime.datetime.now()
        print('{} called took {}'.format(fn.__name__,end-start))
        return ret
    wrap.__name__ = fn.__name__
    wrap.__doc__ = fn.__doc__
    return wrap
```
```
import time
@logger
def sleep(x):
    time.sleep(x)
```
```
In[]:sleep.__name__
Out[]:'sleep'
```
其次也可以写一个函数
```
def copy_properties(src,dst):
    dst.__name__ = src.__name__
    dst.__doc__ = src.__doc__
```
```
import datetime

def logger(fn):
    def wrap(*args,**kwargs):
        start = datetime.datetime.now()
        ret = fn(*args,**kwargs)
        end = datetime.datetime.now()
        print('{} called took {}'.format(fn.__name__,end-start))
        return ret
    copy_properties(fn,wrap)
    return wrap
```
柯里化
```
def copy_properties(src):
    def _copy(dst):
        dst.__name__ = src.__name__
        dst.__doc__ = src.__doc__
        return dst
    return _copy
```
copy_properties返回的是一个装饰器，可以这么来写
```
import datetime

def logger(fn):
    @copy_properties(fn)
    def wrap(*args,**kwargs):
        start = datetime.datetime.now()
        ret = fn(*args,**kwargs)
        end = datetime.datetime.now()
        print('{} called took {}'.format(fn.__name__,end-start))
        return ret
    return wrap
```
再看下sleep.__name__
```
In[]:sleep.__name__
Out[]:'sleep'
```
functools







