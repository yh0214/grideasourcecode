---
title: 'Python解构与封装'
date: 2019-09-04 08:34:40
tags: []
published: true
hideInList: false
feature: 
---
# 解构
先来看一个栗子：
```
In[]：
x = 1
y = 2
x,y = y,x
print(x,y)
Out[]：
2 1
```
结构顾名思义，把一个整体拆成多个小个体
```
In[]：
lst = [1,2]
first,second = lst
print(first,second)
Out[]：
1 2
```
这样的一个过程我们称之为解构
**解构**：按照元素顺序，把**线性结构**的元素赋值给变量
# 封装
封装是解构的逆向操作
```
In[]：
t = 1,2
t
Out[]：
(1, 2)
```
# python3中解构的变化
## 八大变体
第一种变体：head代表第一个元素，tail是最后一个元素，mid是中间所有元素：
```
In[]：
lst = list(range(10))
head,*mid,tail = lst
print(head)
print(mid)
print(tail)
Out[]：
0
[1, 2, 3, 4, 5, 6, 7, 8]
9
```
第二种变体：加星号的tail是除了第一个外的所有元素：
```
In[]：
lst = list(range(10))
head,*tail = lst
print(head)
print(tail)
Out[]：
0
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```
第三种变体：加星号的head是除了最后一个外的所有元素
```
In[]：
lst = list(range(10))
*head,tail = lst
print(head)
print(tail)
Out[]：
[0, 1, 2, 3, 4, 5, 6, 7, 8]
9
```
第四种变体：左边只有一个加星号的变量，**这个是不行的**
```
In[]：
lst = list(range(10))
*lst2 = lst
Out[]：
*lst2 = lst
  File "<ipython-input-14-d0dbc72204e9>", line 5
SyntaxError: starred assignment target must be in a list or tuple
```
第五种变体：左边有两个或两个以上加星号的，**是不行的**
```
In[]：
lst = list(range(10))
head,*m1,*m2,tail = lst
Out[]：
  File "<ipython-input-15-8f61a35156b2>", line 5
SyntaxError: two starred expressions in assignment
```
第六种变体：左边加上一些其他变量
```
In[]：
lst = list(range(10))
first,second,*other,last = lst
print(first)
print(second)
print(other)
print(last)
Out[]：
lst = list(range(10))
first,second,*other,last = lst
print(first)
print(second)
print(other)
print(last)
lst = list(range(10))
first,second,*other,last = lst
print(first)
print(second)
print(other)
print(last)
0
1
[2, 3, 4, 5, 6, 7, 8]
9
```
第七种变体：当左边变量超过右边元素个数的时候，**是不允许的**
```
In[]：
lst = list(range(2))
v1,v2,v3 = lst
Out[]：
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-20-cc6bc96adc53> in <module>
      1 lst = list(range(2))
----> 2 v1,v2,v3 = lst
ValueError: not enough values to unpack (expected 3, got 2)
```
第八种变体：当左边变量数小于右边变量数，且左边没有加星号的变量，**是不允许的**
```
In[]：
lst = list(range(10))
v1,v2,v3 = lst
Out[]：
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-21-03d03897cf0b> in <module>
      1 lst = list(range(10))
----> 2 v1,v2,v3 = lst
ValueError: too many values to unpack (expected 3)
```
**小结：**
元素按照顺序赋值给变量
变量和元素必须匹配
加星号变量，可以接受任意个数的元素
加星号的变量不能单独出现






















