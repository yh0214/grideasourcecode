---
title: 'Python集合运算'
date: 2019-09-04 14:29:05
tags: []
published: true
hideInList: false
feature: 
---
# 交集
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.intersection(s2)
Out[]：
{2, 3}
```
s1.intersection(s2)将得到s1集合与s2集合的交集，是**原地不修改，有返回值**
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s2.intersection_update(s1)
s2
Out[]：
{2, 3}
```
set.intersection_update方法**原地修改，返回None**
接下来看下python集合运算里的运算符重载
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1 & s2
Out[]：
{2, 3}
```
**set重载了按位与运算符&为求交集的运算**
# 差集
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.difference(s2)
Out[]：
{1}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.difference_update(s2)
s1
Out[]：
{1}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1 - s2
Out[]：
{1}
```
# 对称差集
如果把两个集合A和B看成是一个全集，对称差集就是交集的补集
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.symmetric_difference(s2)
Out[]：
{1, 4}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.symmetric_difference_update(s2)
s1
Out[]：
{1, 4}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1 ^ s2
Out[]：
{1, 4}
```
# 并集
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.union(s2)
Out[]：
{1, 2, 3, 4}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1.update(s2)
s1
Out[]：
{1, 2, 3, 4}
```
```
In[]：
s1 = {1,2,3}
s2 = {2,3,4}
s1 | s2
Out[]：
{1, 2, 3, 4}
```
# 子集、超集
判断s2是否是s1的子集
```
In[]：
s1 = {1,2,3,4}
s2 = {2,3}
s2.issubset(s1)
Out[]：
True
```
判断s1是否是s2的超集
```
In[]：
s1 = {1,2,3,4}
s2 = {2,3}
s1.issuperset(s2)
Out[]：
True
```
# 集合的应用
* 去重
* 集合运算更快

1、权限认证，例如：具有权限要求满足A、B、C中任意一项，有一个用户具有权限B、C、D，那么此用户是否有权限？
通过isdisjoin的方法，返回False即可
isdisjoin判断2个集合是否有交集，如果有交集返回False，没有交集返回True
2、有一个任务列表，存储全部的任务，有一个列表存储已经完成的任务，找出未完成的任务
用差集
# 集合的限制
**集合元素必须可hash**
```
In[]：
hash([1,2,3])
Out[]：
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-82-35e31e935e9e> in <module>
----> 1 hash([1,2,3])
TypeError: unhashable type: 'list'
In[]：
{[1,2,3]}
Out[]：
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-83-f70e4b6b8fd1> in <module>
----> 1 {[1,2,3]}
TypeError: unhashable type: 'list'
```
