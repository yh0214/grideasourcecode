---
title: '匿名函数'
date: 2019-09-19 22:45:17
tags: []
published: true
hideInList: false
feature: 
---
所谓匿名函数就是没有名字的函数，用lambda这个关键字来定义
lambda后面接一个参数x，然后用冒号分隔，然后定义一个函数体
```
lambda x : x + 1
```
冒号后面是不换行的
```
In[]：(lambda x : x + 1)(3)
Out[]：4
```
```
In[]：
f = lambda x : x + 1
f(3)
Out[]：4
```
匿名函数（lambda表达式）只能写在一行上，所以也被称为单行函数
匿名函数可以不传参数，直接返回值
```
In[]：
f = lambda : 0
f()
Out[]：0
```
匿名函数传递多个参数也是可以的
```
In[]：
f = lambda x,y : x + y
f(3,5)
Out[]：8
```
匿名函数也是支持默认参数的
```
In[]：
(lambda x,y=3:x + y)(3)
Out[]：6
```
匿名函数也是支持位置可变参数的
```
In[]：
(lambda *args:args)(*range(3))
Out[]：(0, 1, 2)
```
关键字可变参数也是ok的
```
In[]：
(lambda *args,**kwargs:print(args,kwargs))(*range(3),**{str(x):x for x in range(3)})
Out[]：(0, 1, 2) {'0': 0, '1': 1, '2': 2}
```
再来看下keyword-only参数
```
In[]：
(lambda *,x : x)(x = 3)
Out[]：3
```
# 匿名函数的应用
## sorted
```
In[]：
help(sorted)
Out[]：
Help on built-in function sorted in module builtins:
sorted(iterable, /, *, key=None, reverse=False)
    Return a new list containing all items from the iterable in ascending order.
    A custom key function can be supplied to customize the sort order, and the
    reverse flag can be set to request the result in descending order.
```
里面传一个可迭代对象，key默认是None，然后reverse代表反转
假设有一个User对象，它有name和age两个属性
```
from collections import namedtuple
User = namedtuple('User',['name','age'])
```
然后创建一个User的对象列表
```
users = [User('yh',18),User('max',16),User('xxx',32)]
```
在不使用匿名函数的情况下，让users根据age来进行排序
```
In[]：
def get_age(user):
    return user.age
sorted(users,key=get_age)
Out[]：
[User(name='max', age=16), User(name='yh', age=18), User(name='xxx', age=32)]
```
在使用匿名函数的情况下，让users根据age来进行排序
```
In[]：sorted(users,key = lambda x : x.age)
Out[]：[User(name='max', age=16), User(name='yh', age=18), User(name='xxx', age=32)]
```
当函数作为参数时，需要使用匿名函数
## map


```
In[]：

Out[]：
```

```
In[]：

Out[]：
```

```
In[]：

Out[]：
```




















