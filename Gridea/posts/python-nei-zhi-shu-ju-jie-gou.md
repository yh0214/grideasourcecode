---
title: 'Python列表及其常用操作'
date: 2019-08-28 14:07:15
tags: []
published: true
hideInList: false
feature: 
---
# 概念
在其他语言里，会叫这种数据类型为数组，array，在python里，我们叫列表，list
列表是一种数据结构
列表是一个序列，用于顺序的存储数据。
序列是python中最基本的数据结构。
序列中的每个元素都分配一个数字：索引
```
l = list()
l = []
l = [1,2,3]
l = list(range(1,10))
```
通常在定义列表的时候用\[]，在转化可迭代对象为列表的时候用list函数
# 访问列表
定义一个1-9的列表
```
l = list(range(1,10))
```
通过下标访问，下标从0开始
```
l[0]
```
当下标超出范围时，会抛出IndexError
```
l[100]
```
负数索引从右边开始，并且索引从-1开始
## list.index
也可以通过help函数查看所有方法的函数签名，也就是函数说明
```
In[]：help(list.index)
Out[]：
Help on method_descriptor:
index(self, value, start=0, stop=9223372036854775807, /)
    Return first index of value.
    Raises ValueError if the value is not present.
```
这里函数签名中，stop有个默认值，也就是到列表哪一个位置结束，这也是它的最大值了，超出了可能就内存溢出。
"list.index"方法返回查找到的第一个索引
```
l = list(range(1,10))
l.index(4)
new_l = [1,2,3,2,4,3,5]
new_l.index(2)
new_l.index(2,2,3)
new_l.index(2,-1)
new_l.index(2,-4,-1)
```
list.index的start和end参数可以为负数，但是在查找过程中还是从左到右的顺序
当查找不到元素时，抛出错误ValueError。
### list.index函数解读
实现list.index函数：
```
def index(lst,val,start=0,end=-1):
    i = start
    for x in lst[start:end]:
        if x == val:
            return i
        i += 1
    raise ValueError()
```
## list.count
查看一下list.count的函数签名
```
In[]：help(list.count)
Out[]：
Help on method_descriptor:
count(self, value, /)
    Return number of occurrences of value.
```
list.count，统计你要查询的字符在列表里出现的次数
```
new_l = [1,2,3,2,4,3,5]
new_l.count(5)
new_l.count(10)
```
### list.count函数解读
实现list.count函数：
```
def count(lst,value):
    c = 0
    for x in lst:
        if x == value:
            c += 1
    return c
```
## 总结
* list通过索引访问元素



















