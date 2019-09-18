---
title: 'Python解析式'
date: 2019-09-10 11:17:16
tags: []
published: true
hideInList: false
feature: 
---
解析式分为：
* 列表解析式
* 生成器解析式
* 集合解析式
* 字典解析式

# 列表解析式
## 定义
通用语法：'[expr for e in iterator]'
列表解析式的优点：
代码简介，可读性强
效率比普通的迭代稍高，但不是数量级上的，只是稍微有一点
```
In[]：
%%timeit
ret = []
for i in range(10000):
    ret.append(i)
Out[]：
551 µs ± 10.6 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
In[]：
%%timeit
ret = [i for i in range(10000)]
Out[]：
278 µs ± 2.23 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```
## 解析式变体
带if语句的列表解析
```
In[]：
lst = list(range(10))
ret = []
for x in lst:
    if x % 2 == 0:
        ret.append(x)
ret
Out[]：
[0, 2, 4, 6, 8]
In[]：
ret = [x for x in lst if x % 2 == 0]
ret
Out[]：
[0, 2, 4, 6, 8]
```
事实上也可以是多个if的组合
```
In[]：
lst = list(range(10))
ret = [x for x in lst if x > 0 if x < 5]
ret
Out[]：
[1, 2, 3, 4]
```
等效于：
```
In[]：
ret = []
for x in lst:
    if x > 0:
        if x < 5:
            ret.append(x)
ret
Out[]：
[1, 2, 3, 4]
```
解析式前面有没有可能放两个元素呢？
```
In[]：
[x,y for x in range(5) for y in range(5,10)]
Out[]：
 File "<ipython-input-19-2ffe676038e5>", line 1
    [x,y for x in range(5) for y in range(5,10)]
           ^
SyntaxError: invalid syntax
```
可以将其用一个元组封装起来
```
In[]：
[(x,y) for x in range(5) for y in range(5,10)]
Out[]：
[(0, 5),
 (0, 6),
 (0, 7),
 (0, 8),
 (0, 9),
 (1, 5),
 (1, 6),
 (1, 7),
 (1, 8),
 (1, 9),
 (2, 5),
 (2, 6),
 (2, 7),
 (2, 8),
 (2, 9),
 (3, 5),
 (3, 6),
 (3, 7),
 (3, 8),
 (3, 9),
 (4, 5),
 (4, 6),
 (4, 7),
 (4, 8),
 (4, 9)]
```
## 三元表达式
语法：'x if cond else y'
* 当条件（cond）满足时，返回x
* 当条件不满足时，返回y

```
In[]：
[x**2 if x % 2 == 0 else x**3 for x in range(10)]
Out[]：
[0, 1, 4, 27, 16, 125, 36, 343, 64, 729]
```
三元表达式只能使用双分支if else
# 生成器解析式
列表解析式中的中括号变成小括号，就称为生成器解析式了
生成器解析式返回的是一个生成器
生成器的有点是：
* 不占内存
* 惰性求值

```
In[]：
def fn(x):
    print('executed')
    return x
g = (fn(x) for x in range(10))
next(g)
Out[]：
executed
0
```
* 生成器都是迭代器
* 生成器是无法使用下标访问的

# 集合解析
```
In[]：
s = {x for x in range(10)}
print(s)
print(type(s))
Out[]：
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
<class 'set'>
```
# 字典解析
```
In[]：
d = {str(x):x for x in range(10)}
print(d)
print(type(d))
Out[]：
{'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
<class 'dict'>
```










