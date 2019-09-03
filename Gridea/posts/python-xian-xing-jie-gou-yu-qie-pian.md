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
可迭代对象可以通过iter方法转换为迭代器
next可以迭代迭代器，不可以迭代可迭代对象
当next将迭代器的元素都迭代过一遍后，再迭代一次就会抛出StopIteration
```
In[]：
it = iter(list((1,2,3)))
next(it)
Out[]：
1
```
# 切片操作
lst\[start:stop\]，可以访问这个list一段，从start开始，到stop结束，不包含stop，并且是原地不修改，有返回值
* start超出索引范围时，start = 0
* stop超出索引范围时，stop = -0
* 当start>=stop时，返回空列表
* 负数索引，实际上等于len(lst) + index


```
In[]：

Out[]：

```