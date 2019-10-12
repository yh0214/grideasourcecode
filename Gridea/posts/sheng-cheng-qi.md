---
title: '生成器'
date: 2019-09-23 09:42:18
tags: []
published: true
hideInList: false
feature: 
---
生成器其实也是一个函数
```
def g():
    for x in range(10):
        yield x
```
使用了一个新的关键字yield，没有return会不会报错？
```
In[]：
r = g()
r
Out[]：<generator object g at 0x000000000613E1B0>
```
可以看到返回的是一个generator
```
In[]：dir(r)
Out[]：
['__class__',
 '__del__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__iter__',
 '__le__',
 '__lt__',
 '__name__',
 '__ne__',
 '__new__',
 '__next__',
 '__qualname__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 'close',
 'gi_code',
 'gi_frame',
 'gi_running',
 'gi_yieldfrom',
 'send',
 'throw']
```
它有'__iter__'方法，是一个可迭代对象
它有'__next__'方法，是一个迭代
使用next调用一下
```
In[]：next(r)
Out[]：0
```
```
In[]：next(r)
Out[]：1
```
返回的是函数中x的值
有一个yield关键字，这个是一个迭代器，是迭代器里面的一个特殊内容，叫生成器
执行完一次r = g()，现场应该被销毁了，但是r还是有值，还是可以继续调用next，事实上，函数的现场并没有被销毁，这就是生成器函数和普通函数不太一样的地方
看下生成器是如何工作的
```
def gen():
    print('a')
    yield 1
    print('b')
    yield 2
    return 3
```
定义了一个函数，有2个yield，1个return
```
In[]：g = gen()
g
Out[]：<generator object gen at 0x0000000003259570>
```
理论上，gen里面有return，应该有返回值，但是这个g还是一个generator，说明函数并没有被执行
接下来使用next调用
```
In[]：next(g)
Out[]：
a
1
```
在这里，执行到第一个yield，就停止执行了
再执行一次next(g)
```
In[]：next(g)
Out[]：
b
2
```
打印出了b，然后到2就又停止了，而之前的a并没有被打印出来，说明现场保留了
再执行一次next(g)
```
In[]：next(g)
Out[]：
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
 in 
----> 1 next(g)

StopIteration: 3
```
没有更多yield的时候，抛出StopIteration异常，还有一点需要注意的是，这个异常值就是它的返回值，没有返回值的话异常值就为空
总结一下：带yield语句的函数称为生成器函数，生成器函数的返回值是生成器
特点：
* 生成器函数执行的时候，不会执行函数体（注意，这里是说生成器函数执行的时候，不是生成器执行的时候）
* 当next生成器的时候，当前代码会执行到之后的第一个yield，会弹出值，并暂停函数
* 当再次执行next生成器的时候，从上次暂停处开始往下执行
* 当没有多余的yield的时候，会抛出StopIteration异常，如果函数有返回值，异常的value是函数的返回值
  
生成器是惰性求值的，先来写一个计数器
```
def counter():
    x = 0
    while True:
        x += 1
        yield x

def inc(c):
    return next(c)
```
```
In[]：c = counter()
In[]: inc(c)
Out[]：1
```
这样每次执行inc(c)都可以得到一个+1的值
还可以封装的更好
```
def inc():
    c = counter()
    return lambda : next(c)
```
还有一种更好的方法，可以把counter封装到inc里面
```
def inc():
    def counter():
        x = 0
        while True:
            x += 1
            yield x
    c = counter()
    return lambda : next(c)
```
```
In[]：incr = inc()
In[]: incr()
Out[]：1
```
```
In[]：incr()
Out[]：2
```
难点
```
def make_inc():
    def counter():
        x = 0
        while True:
            x += 1
            yield x
    c = counter()
    return next(c)
```
```
In[]：make_inc()
Out[]：1
```
```
In[]：make_inc()
Out[]：1
```
```
In[]：make_inc()
Out[]：1
```
为什么再次执行还是得到1？
每次都会初始化一个c，给它一个新的生成器，所以每次都是1
使用lambda的话，只会生成一次c，后面每次都是调用这个函数
应用
斐波那契数列
首先看使用递归实现，递归非常慢
```
def fib(n):
    if n == 0:
        return 1
    if n == 1:
        return 1
    return fib(n-1) + fib(n-2)
```
还可以使用生成器实现
```
def fib():
    a = 0
    b = 1
    while True:
        a,b = b,a + b
        yield a
```
```
In[]：
f = fib()
for _ in range(5):
    print(next(f))
Out[]：
1
1
2
3
5
```
生成器可以解决递归问题
协程是生成器的高级应用


