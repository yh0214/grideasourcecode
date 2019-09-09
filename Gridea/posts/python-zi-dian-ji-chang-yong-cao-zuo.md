---
title: 'Python字典及常用操作'
date: 2019-09-04 16:58:27
tags: []
published: true
hideInList: false
feature: 
---
# 定义
定义字典的方法：
第一种：直接使用dict()来定义
```
In[]：
d = dict(
name = 'yh',
address = '呼呼')
d
Out[]：
{'name': 'yh', 'address': '呼呼'}
```
第二种：直接使用花括号括起来
```
In[]：
d = {'a':1,'b':2}
d
Out[]：
{'a': 1, 'b': 2}
```
第三种：
1、可迭代对象的元素必须是一个二元组
2、二元组的第0个元素是字典的key，第一个元素为字典的value
```
In[]：
d = dict([('a',1),('b',2)])
d
Out[]：
{'a': 1, 'b': 2}
```
第四种：传入的可迭代对象元素为key，值为None
```
In[]：
d = dict.fromkeys(range(5))
d
Out[]：
{0: None, 1: None, 2: None, 3: None, 4: None}
```
传入的可迭代对象的元素为key，值为abc
```
In[]：
d = dict.fromkeys(range(5),'abc')
d
Out[]：
{0: 'abc', 1: 'abc', 2: 'abc', 3: 'abc', 4: 'abc'}
```
定义一个空字典可以使用{}或者dict()，定义一个空集合需要使用set()
# 增加
第一种：直接使用key作为下标，对某个不存在的下标赋值
```
In[]：
d = {'a':1,'b':2}
d['c'] = 3
d
Out[]：
{'a': 1, 'b': 2, 'c': 3}
```
第二种：通过update方法同时更新多个键值对，也可以将一个新的字典更新到另一个字典里
```
In[]：
d = {'a':1,'b':2}
d.update([('c',3),('p',4)])
d
Out[]：
{'a': 1, 'b': 2, 'c': 3, 'p': 4}
```
直接传入字典更加方便，若key已存在，则会更新对应的值
```
In[]：
d = {'a':1,'b':2}
d.update({'c':3,'d':4})
d
Out[]：
{'a': 1, 'b': 2, 'c': 3, 'd': 4}
```
# 修改
当key存在的时候，对下标赋值，会修改这个key对应的value
也可以使用update修改
```
In[]：
d = {'a':1,'b':2}
d['a'] = 3
d
Out[]：
{'a': 3, 'b': 2}
```
```
In[]：
d = {'a':1,'b':2}
d.update({'b':4})
d
Out[]：
{'a': 1, 'b': 4}
```
# 删除
## dict.pop
pop需要传入一个key，如果key存在会返回这个key的value
```
In[]：
d = {'a':1,'b':2}
d.pop('a')
Out[]：
1
```
如果key不存在会抛出KeyError，并且会把这个键一起返回
```
In[]：
d = {'a':1,'b':2}
d.pop('c')
Out[]：
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-20-72feaa87d842> in <module>
      1 d = {'a':1,'b':2}
----> 2 d.pop('c')
KeyError: 'c'
```
但是当删除了不存在的key，并且指定了默认值的时候，就不会抛出KeyError
```
In[]：
d = {'a':1,'b':2}
d.pop('c','default')
Out[]：
'default'
```
## dict.popitem
随机返回删除的一个kv对的二元组
```
In[]：
d = {'a':1,'b':2}
d.popitem()
Out[]：
('b', 2)
```
## dict.clear
清空一个字典
```
In[]：
d = {'a':1,'b':2}
d.clear()
d
Out[]：
{}
```
## del
del语句是删除一个键的引用，相当于dict.pop(key)
但是通常不用del，都用pop
# 访问
## 单个元素的访问
直接使用下标访问，当Key不存在的时候抛出KeyError
```
In[]：
d = {'a':1,'b':2}
d['a']
Out[]：
1
```
get方法访问不存在的key的时候会返回默认值，未设置时为None，设置时返回设定值
```
In[]：
d = {'a':1,'b':2}
d.get('c','default')
Out[]：
'default'
```
## 字典的遍历
直接使用for in遍历字典，遍历的是字典的key
遍历字典的值可以使用values
```
In[]：
d = {'a':1,'b':2,'c':3}
for v in d.values():
    print(v)
Out[]：
1
2
3
```
d.items()使用最多，返回一个可迭代对象，元素是字典的所有kv对
```
In[]：
d = {'a':1,'b':2,'c':3}
for k,v in d.items():
    print(k,'=>',v)
Out[]：
a => 1
b => 2
c => 3
```
# 字典的限制
* 字典的key不能重复
* 字典的key需要可hash
* 字典也不能做字典的key




