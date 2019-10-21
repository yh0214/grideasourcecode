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
```
help(functools.wraps)
Help on function wraps in module functools:

wraps(wrapped, assigned=('__module__', '__name__', '__qualname__', '__doc__', '__annotations__'), updated=('__dict__',))
    Decorator factory to apply update_wrapper() to a wrapper function
    
    Returns a decorator that invokes update_wrapper() with the decorated
    function as the wrapper argument and the arguments to wraps() as the
    remaining arguments. Default arguments are as for update_wrapper().
    This is a convenience function to simplify applying partial() to
    update_wrapper().
```
看看如何使用
```
import datetime
import functools
def logger(fn):
    @functools.wraps(fn)
    def wrap(*args,**kwargs):
        start = datetime.datetime.now()
        ret = fn(*args,**kwargs)
        end = datetime.datetime.now()
        print('{} called took {}'.format(fn.__name__,end - start))
        return ret
    return wrap
```
```
import time
@logger
def sleep(x):
    time.sleep(x)
```
```
In[]:sleep(3)
Out[]:sleep called took 0:00:03.000353
```
这个就是copy_properties的由来
柯里化其实是一个数学的概念，目的是让多个参数变成单个参数
带参数的装饰器
假如需要记录大于某个时间的操作，并且可以对这个时间做控制，通过参数传递进来
```
import functools
import datetime
def logger(s):
    def _logger(fn):
        @functools.wraps(fn)
        def wrap(*args,**kwargs):
            start = datetime.datetime.now()
            ret = fn(*args,**kwargs)
            end = datetime.datetime.now()
            if (end - start).total_seconds() > s:
                print('call {} took {}'.format(fn.__name__,end - start))
            return ret
        return wrap
    return _logger
```
(end - start).total_seconds()将时间格式的时间差转为数字格式
```
import time
@logger(1)
def sleep(x):
    time.sleep(x)
```
执行时间大于1s的操作进行记录
```
In[]:sleep(2)
Out[]:call sleep took 0:00:02
```
```
In[]:sleep(1)
Out[]:
```
```
In[]:sleep(3)
Out[]:call sleep took 0:00:03
```
sleep(2)和sleep(3)执行完后进行了记录，sleep(1)执行完没有进行记录
@logger(1)拆开就是logger(1)(sleep)
带参数的装饰器：一个函数，返回一个不带参数的装饰器
多参数
```
import functools
import datetime
def logger(s,p = lambda name,t : print('call {} took {} '.format(name,t))):
    def _logger(fn):
        @functools.wraps(fn)
        def wrap(*args,**kwargs):
            start = datetime.datetime.now()
            ret = fn(*args,**kwargs)
            end = datetime.datetime.now()
            if (end - start).total_seconds() > s:
                p(fn.__name__,end - start)
            return ret
        return wrap
    return _logger
```
```
import time
@logger(1)
def sleep(x):
    time.sleep(x)
```
```
In[]：sleep(2)
Out[]：call sleep took 0:00:02 
```
```
import time
@logger(1,p = lambda name,t : print('hahahaha'))
def sleep(x):
    time.sleep(x)
```
```
In[]：sleep(2)
Out[]：hahahaha
```
超时后的打印逻辑可以进行自定义了
作为装饰器，可以有多层，但是超过两层时首先要命名一个变量，然后再使用@变量()就可以了
例如有logger _logger __logger三层时
```
import functools
import datetime
def logger(s):
    def _logger(p = lambda name,t : print('call {} took {} '.format(name,t))):
        def __logger(fn):
            @functools.wraps(fn)
            def wrap(*args,**kwargs):
                start = datetime.datetime.now()
                ret = fn(*args,**kwargs)
                end = datetime.datetime.now()
                if (end - start).total_seconds() > s:
                    p(fn.__name__,end - start)
                return ret
            return wrap
        return __logger
    return _logger
```
```
import time
logger2s = logger(1)
@logger2s()
def sleep(x):
    time.sleep(x)
```
```
In[]:sleep(3)
Out[]:call sleep took 0:00:03 
```


















