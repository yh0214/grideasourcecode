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
* index方法根据值返回第一个索引
* count方法返回元素在列表里的个数

index和count的时间复杂度是O(n)
# 列表修改
通过索引的方式进行赋值即可
```
In[]：
new_l = [1,2,3,2,4,3,5]
new_l[2] = 5
print(new_l)
Out[]：
[1, 2, 5, 2, 4, 3, 5]
```
超出范围还是会抛出IndexError
```
In[]：
new_l = [1,2,3,2,4,3,5]
new_l[10] = 10
Out[]：
IndexError                                Traceback (most recent call last)
<ipython-input-3-daf879895697> in <module>
      1 new_l = [1,2,3,2,4,3,5]
----> 2 new_l[10] = 10
IndexError: list assignment index out of range
```
# 列表增加
## list.append
先用help函数看下它的函数签名
```
In[]：
help(list.append)
Out[]：
Help on method_descriptor:
append(self, object, /)
    Append object to the end of the list.
```
append**原地修改list，返回值是None**,直接在最后加一位，我们称之为追加
```
In[]：
new_l = [1,2,3,2,4,3,5]
new_l.append(99)
print(new_l)
Out[]：
[1, 2, 3, 2, 4, 3, 5, 99]
```
## list.insert
在第i个元素前插入e
```
In[]：
help(list.insert)
Out[]：
Help on method_descriptor:
insert(self, index, object, /)
    Insert object before index.
```
```
In[]：
new_l = [1,2,3,2,4,3,5]
new_l.insert(1,99)
print(new_l)
Out[]：
[1, 99, 2, 3, 2, 4, 3, 5]
```
**当越界的时候，自动往左或往右插入该值，这点非常重要，它并不会报错**
```
In[]：
new_l = [1,2,3,2,4,3,5]
new_l.insert(100,99)
print(new_l)
Out[]：
[1, 2, 3, 2, 4, 3, 5, 99]
In[]：
new_l = [1,2,3,2,4,3,5]
new_l.insert(-100,99)
print(new_l)
Out[]：
[99, 1, 2, 3, 2, 4, 3, 5]
```
append和insert的效率：
* append的时间复杂度是O(1)，常数时间，效率和数据的规模无关
* insert的时间复杂度是O(n)，线性时间，效率和数据规模线性相关

**尽量使用append**
## list.extend
extend将任意可迭代对象追加到数据的末尾，**原地修改，返回None**
```
In[]：
help(list.extend)
Out[]：
Help on method_descriptor:
extend(self, iterable, /)
    Extend list by appending elements from the iterable.
```
值得注意的是，extend是把可迭代对象里的每一个值循环append到list里去，而不是像append，直接把一整个对象追加到列表的队尾
* append操作单个元素
* extend操作可迭代对象

对比栗子：
```
In[]：
new_l = [0,1,2]
new_l.append([1,2,3])
print(new_l)
Out[]：
[0, 1, 2, [1, 2, 3]]
In[]：
new_l = [0,1,2]
new_l.extend([1,2,3])
print(new_l)
Out[]：
[0, 1, 2, 1, 2, 3]
```
**list.extend经常用在两个列表的相加上**
## list + list
两个列表的相加还可以直接用加号
```
In[]：
l = [0,1,2,3,4]
a = l + ['a','b','c']
print('a:',a)
print('l:',l)
Out[]：
a: [0, 1, 2, 3, 4, 'a', 'b', 'c']
l: [0, 1, 2, 3, 4]
```
**这种方法有返回值，但是不修改list本身，返回一个新的list**，这种操作叫list的连接操作
# 列表删除
## list.remove
```
In[]：
help(list.remove)
Out[]：
Help on method_descriptor:
remove(self, value, /)
    Remove first occurrence of value.
    Raises ValueError if the value is not present.
```
删除第一个匹配的元素
```
In[]：
l = [1,2,3,2,3,4,3,5,3,4]
l.remove(2)
print(l)
Out[]：
[1, 3, 2, 3, 4, 3, 5, 3, 4]
```
**原地修改，返回None，根绝值删除元素**
当值不存在时，抛出ValueError
```
In[]：
l = [1,2,3,2,3,4,3,5,3,4]
l.remove(10)
Out[]：
ValueError                                Traceback (most recent call last)
<ipython-input-5-13fc432ba077> in <module>
      1 l = [1,2,3,2,3,4,3,5,3,4]
----> 2 l.remove(10)
ValueError: list.remove(x): x not in list
```
## list.pop
```
In[]：
help(list.pop)
Out[]：
Help on method_descriptor:
pop(self, index=-1, /)
    Remove and return item at index (default last).
    Raises IndexError if list is empty or index is out of range.
```
不传入参数，则默认返回并删除最后一个值
传入index参数，返回并删除index所在的值
```
In[]：
l = [3,2,4,3,5,3,4]
l.pop(3)
print(l)
Out[]：
3
[3, 2, 4, 5, 3, 4]
```
**注意：这个传入的参数是index，不是元素的值**
当索引不存在时，抛出IndexError
```
In[]：
l = [3,2,4,3,5,3,4]
l.pop(100)
Out[]：
IndexError                                Traceback (most recent call last)
<ipython-input-10-85aba9b20ee8> in <module>
      1 l = [3,2,4,3,5,3,4]
----> 2 l.pop(100)
IndexError: pop index out of range
```
这里需要注意几点：
* pop不传递index参数，时间复杂度是O(1)
* pop传递index参数，时间复杂度是O(n)
* pop根据索引删除元素，并且返回删除的元素
* remove根据值删除元素，返回None

## list.clear
```
In[]：
help(list.clear)
Out[]：
Help on method_descriptor:
clear(self, /)
    Remove all items from list.
```
删除所有元素
```
In[]：
l = [3,2,3,5,3,4]
l.clear()
print(l)
Out[]：
[]
```
使用clear后，列表对象还存在，只是里面的值都被清空了
# 其它操作
## 求list的长度
len(l)
```
In[]：
l = [3,2,3,5,3,4]
len(l)
Out[]：
6
```
## 反转列表
l.reverse()
```
In[]：
l = [0,1,2,3,4,5,6]
l.reverse()
print(l)
Out[]：
[6, 5, 4, 3, 2, 1, 0]
```
## 列表排序
l.sort()
```
In[]：
l = [2,5,3,6,1,4,8,9]
l.sort()
print(l)
Out[]：
[1, 2, 3, 4, 5, 6, 8, 9]
```
**原地修改，返回None**
**逆序排序，l.sort(reverse=True)**
```
In[]：
l = [2,5,3,6,1,4,8,9]
l.sort(reverse=True)
print(l)
Out[]：
[9, 8, 6, 5, 4, 3, 2, 1]
```
## 列表拷贝
### 引用传递
```
In[]：
a = [1,2,3]
b = a
print(b)
b[1] = 99
print(b)
print(a)
Out[]：
[1, 2, 3]
[1, 99, 3]
[1, 99, 3]
```
### 浅复制（浅拷贝）
```
In[]：
l = [1,2,3,4,5]
l2 = l.copy()
l2[0] = 'a'
print(l)
print(l2)
Out[]：
[1, 2, 3, 4, 5]
['a', 2, 3, 4, 5]
```
如果列表存在嵌套列表
```
In[]：
l = [1,[1,2,3],4]
l2 = l.copy()
l2[1][1] = 'a'
print(l2)
print(l)
Out[]：
[1, [1, 'a', 3], 4]
[1, [1, 'a', 3], 4]
```
### 深复制（深拷贝）
使用深拷贝需要引入copy模块，使用deepcopy
```
In[]：
from copy import deepcopy
l = [1, [1, 'a', 3], 4]
l2 = deepcopy(l)
l2[1][1] = 'b'
print(l2)
print(l)
Out[]：
[1, [1, 'b', 3], 4]
[1, [1, 'a', 3], 4]
```





