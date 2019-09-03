---
title: 'Python线性结构与切片'
date: 2019-09-03 17:29:44
tags: []
published: true
hideInList: false
feature: 
---
# 定义
线性结构共同特点：
* 可迭代
* 可以用len方法获取长度
* 可以通过索引访问
* 可以切片

# enumerate
```
In[]：
enumerate((1,2,3))
Out[]：
<enumerate at 0x6059750>
```
返回一个可迭代对象，再来看看这个可迭代对象是什么
```
In[]：
list(enumerate((1,2,3)))
Out[]：
[(0, 1), (1, 2), (2, 3)]
```
实现一个enumerate函数
```
In[]：
def new_enumerate(iterator):
    i = 0
    for v in iterator:
        yield i,v
        i += 1
list(new_enumerate((1,2,3)))
Out[]：
[(0, 1), (1, 2), (2, 3)]
```
需要同时获取索引和value时用这个函数
# 迭代器




```
In[]：

Out[]：

```