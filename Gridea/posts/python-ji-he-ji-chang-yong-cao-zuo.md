---
title: 'Python集合及常用操作'
date: 2019-09-04 09:36:03
tags: []
published: true
hideInList: false
feature: 
---
# 定义与初始化
集合没有重复元素
set()可以对可迭代对象进行转化
```
In[]：
s = {1,2,3}
s
Out[]：
{1, 2, 3}
```
# 集合增加
```
In[]：
s = {0,1,2}
s.add(3)
s
Out[]：
{0, 1, 2, 3}
```
在增加已存在元素时，set集合并不会被追加新元素
```
In[]：
s = {0,1,2,3}
s.add(3)
s
Out[]：
{0, 1, 2, 3}
```
再来看一个方法
```
In[]：
help(set.update)
Out[]：
**Help on method_descriptor:
update(...)
    Update a set with the union of itself and others.**
```
update方法会把自己和别人联合起来，但是会去重，**没有返回值，原地修改**
```
In[]：
s = {0,1,2,3}
s.update(range(4,7))
s
Out[]：
{0, 1, 2, 3, 4, 5, 6}
```
```
In[]：
s = {0,1,2,3,4,5,6}
s.update(range(4,9))
s
Out[]：
{0, 1, 2, 3, 4, 5, 6, 7, 8}
```
# 集合删除
## set.remove
```
In[]：
help(set.remove)
Out[]：
Help on method_descriptor:
remove(...)
    Remove an element from a set; it must be a member.
    If the element is not a member, raise a KeyError.
```
我们看remove的函数签名，2个点：
* 会从集合中删除你传入的变量，但是这个变量必须是集合中已有的元素
* 如果这个元素不存在，是会抛出异常的
```
In[]：
s = set(range(9))
s.remove(0)
s
Out[]：
{1, 2, 3, 4, 5, 6, 7, 8}
```
remove**原地修改，不返回值**
## set.pop
```
In[]：
help(set.pop)
Out[]：
Help on method_descriptor:
pop(...)
    Remove and return an arbitrary set element.
    Raises KeyError if the set is empty.
```
从函数签名得知，pop和remove有一个区别，就是pop会return这个删除的值
同时，如果集合为空了，还要pop的话，会抛出KeyError信息
## set.discard
```
In[]：
help(set.discard)
Out[]：
Help on method_descriptor:
discard(...)
    Remove an element from a set if it is a member.
    If the element is not a member, do nothing.
```
discard可以指定删除哪个元素，而不是像pop那样，只能从队首或者队尾删除
**原地修改，不返回值**
discard删除不存在的元素时，什么也不做
# 修改
集合不能修改单个元素
# 查找
**集合不能通过索引访问，因为集合不是一个线性结构**
# 成员运算符
因为集合的成员运算和其他线性结构的时间复杂度不同
做一个简单的效率计算
使用%%timeit，这是ipython提供的一个magic
```
In[]：
lst = list(range(1000000))
s = set(range(1000000))
In[]：
%%timeit
-1 in lst
Out[]：
8.91 ms ± 126 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
In[]：
%%timeit
-1 in s
Out[]：
32.3 ns ± 0.193 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)
```
在list里面做100次循环，得到平均值是8.91ms上下浮动126us，但是在set中，效率是32.3ns上下浮动0.193ns
再来看一个：
```
In[]：
lst = list(range(100))
s = set(range(100))
In[]：
%%timeit
-1 in lst
Out[]：
885 ns ± 3.95 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
In[]：
%%timeit
-1 in s
Out[]：
32.2 ns ± 0.182 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)
```
做成员运算时，**列表的效率和列表的规模有关**
做成员运算时，**集合的效率和集合的规模无关**
成员运算
* 集合的效率：O(1)
* 列表的效率：O(n)

所以可能的话，当你要做成员运算的时候，就把列表、元组转化成集合做







