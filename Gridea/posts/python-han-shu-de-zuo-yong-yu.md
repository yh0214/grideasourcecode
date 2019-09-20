---
title: 'Python函数的作用域'
date: 2019-09-16 17:02:19
tags: []
published: true
hideInList: false
feature: 
---
# 定义
一个变量的可见范围叫做这个变量的作用域
# 全局作用域
# 局部作用域
变量的作用域为变量定义同级的作用域，也就是在哪一个级别定义的，在哪一个级别就可见
# 上、下级作用域
上级作用域对下级作用域是只读的，read-only的
不同作用域变量不可见，但是下级作用域可以对上级作用域的变量只读可见
# 全局变量global
global关键字可以提升变量作用域为全局变量
global的提升只对本作用域有用，那么我们需要让他在其他局部作用域有用，就需要再标记
# 闭包函数
```
def counter():
    c = [0]
    def inc():
        c[0] += 1
        return c[0]
    return inc
f = counter()
f()
```
这种形式我们称为闭包，函数已经结束，但是函数内部部分变量的引用还存在
理论上执行完f = counter()后，这个c已经没有了，但是我们通过inc可以继续访问，这种就称为闭包
# 局部变量
```
def counter():
    x = 0
    def inc():
        nonlocal x
        x += 1
        return x
    return inc
f = counter()
f()
```
nonlocal关键字用来标记一个变量由他的上级作用域定义，通过nonlocal标记的变量可读可写


















