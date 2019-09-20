---
title: '函数的执行流程 & 递归函数'
date: 2019-09-19 22:24:55
tags: []
published: true
hideInList: false
feature: 
---
函数的执行流程
当调用函数的时候，解释器会把当前现场压栈，然后执行被调函数。被调函数执行完成，解释器弹出当前栈顶，恢复现场
递归函数
程序调用自身的编程技巧称为递归
```
def fib(n):
    if n == 0:
        return 1
    if n == 1:
        return 1
    return fib(n-1) + fib(n-2)
```
**递归函数必须要有退出条件**