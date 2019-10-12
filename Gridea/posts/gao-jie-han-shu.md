---
title: '高阶函数'
date: 2019-10-09 11:30:56
tags: []
published: true
hideInList: false
feature: 
---
首先看一个函数
```
def counter(base):
    def inc(x=1):
        nonlocal base
        base += x
        return base
    return inc
```
```
In[]：inc = counter(3)
In[]：inc(3)
Out[]：6
```
```
In[]：inc(3)
Out[]：9
```
这种返回值是一个函数或者参数是函数的情况，就称为高阶函数
第一种情况：返回值是函数
第二种情况：参数是函数
这两种情况的函数，就叫做高阶函数
高阶函数的作用
首先看一个排序函数，传入一个可迭代对象
```
def sort(it):
    ret = []
    for x in it:
        for i,e in enumerate(ret):
            if x > e:
                ret.insert(i,x)
                break
        else:
            ret.append(x)
    return ret
```
```
In[]：sort([1,4,3,8,2,9,0,7])
Out[]：[9, 8, 7, 4, 3, 2, 1, 0]
```
如果要从小到大排列，只需要将大于改成小于就好了，x<e
一般要实现顺序排列和逆序排列需要两个函数，但是可以通过加一个判断，将两个功能通过一个函数实现
```
def sort(it,r=False):
    ret = []
    for x in it:
        for i,e in enumerate(ret):
            if r:
                if x < e:
                    ret.insert(i,x)
                    break
            else:
                if x > e:
                    ret.insert(i,x)
                    break
        else:
            ret.append(x)
    return ret
```
还可以再次进行优化，将if判断抽出来，作为一个函数
```
def sort(it,r=False):
    def cmp(a,b):
        if r:
            return a < b
        else:
            return a > b
    ret = []
    for x in it:
        for i,e in enumerate(ret):
            if cmp(x,e):
                ret.insert(i,x)
                break
        else:
            ret.append(x)
    return ret
```
那将cmp函数移到外面行不行呢？可以将cmp作为一个参数传入
```
def sort(it,cmp=lambda a,b :a < b):
    ret = []
    for x in it:
        for i,e in enumerate(ret):
            if cmp(x,e):
                ret.insert(i,x)
                break        
        else:
            ret.append(x)
    return ret
```
```
In[]：sort([1,4,3,8,2,9,0,7],lambda a,b :a > b)
Out[]：[9, 8, 7, 4, 3, 2, 1, 0]

```
```
In[]：sort([1,4,3,8,2,9,0,7],lambda a,b :a < b)
Out[]：[0, 1, 2, 3, 4, 7, 8, 9]
```
函数作为返回值：通常是用于闭包的场景，需要封装一些变量
函数作为参数：通常是用于大多数逻辑固定，少部分逻辑不固定的场景














