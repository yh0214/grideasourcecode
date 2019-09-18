---
title: 'Python函数的基础'
date: 2019-09-16 10:11:16
tags: []
published: true
hideInList: false
feature: 
---
函数是Python里组织代码的最小单元
定义函数的时候，并不会执行函数体
当调用函数的时候，才会执行其中的语句块
Python在导入模块的时候，是会去执行一遍该文件
# 函数参数
位置参数
关键字参数
注意：**当位置参数和关键字参数混合使用时，位置参数必须在前面，否则会报语法错误**
默认参数
参数可以有默认值，当一个参数有默认值时，调用时如果不传递此此参数，会有默认值
注意：带默认值的参数必须在不带默认值的参数之后
位置可变参数
在参数前面加一个星号
```
In[]：
def sum(*lst):
    ret = 0
    for x in lst:
        ret += x
    return ret
print(sum(1,2,3))
Out[]：
6
```
关键字可变参数
```
In[]：
def connect(**kwargs):
    print(type(kwargs))
    print(kwargs)
connect(host='127.0.0.1',port=3601)
Out[]：
<class 'dict'>
{'host': '127.0.0.1', 'port': 3601}
```
注意：当位置可变参数和关键字可变参数一起使用时，位置可变参数必须在前面
通常来说：
默认参数靠后
可变参数靠后
默认参数和可变参数不同时出现















