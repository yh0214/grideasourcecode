---
title: '路径处理&文件读写&异常处理'
date: 2019-10-29 15:07:46
tags: []
published: true
hideInList: false
feature: 
---
* 路径处理
  ```
  import os
  ```
* 获取当前工作的文件夹路径，此路径是指在哪里运行python文件，此方法不经常使用
  ```
  print(os.getcwd())
  ```
* 文件的绝对路径，非常有用
 ```
  print(os.path.abspath(__file__))
  ```
* 获取文件路径的文件夹路径
  ```
  dir_name = os.path.dirname(os.path.abspath(__file__))
  ```
* 路径拼接
  ```
  new_dir = os.path.join(dir_name,'data')
  ```
* 创建文件夹，使用该方法创建要一层一层创建，否则会报错
  ```
  os.mkdir(new_dir)
  ```
* 首先判断文件夹是否存在，存在则再去创建
  ```
  new_dir = os.path.join(dir_name,'data','cases')
  new_dir_data = os.path.dirname(new_dir)
  if os.path.exists(new_dir_data):
      os.mkdir(new_dir)
  else:
      print('data文件夹不存在')
  ```
* 判断是否是一个文件夹，返回True或者False
  ```
  print(os.path.isdir(new_dir))
  ```
* 判断是否是一个文件，返回True或者False
  ```
  print(os.path.isfile(new_dir))
  ```

* 打开文件 文件内容有汉字时使用utf-8打开
  ```
  f = open('demo.txt',encoding='utf-8')
  ```
* 读文件
  ```
  print(f.read())
  ```
* 一行一行读取文件
  ```
  f = open('demo.txt',encoding='utf-8')
  print(f.readlines())
  ```
* 写文件 mode为'w'，如果文件已经存在，写入内容的时候，原来的文件内容会被覆盖
* 如果不想被覆盖，mode应该使用'a'
* mode为'x'，创作模式，文件已经存在时使用x模式会报错
  ```
  f = open('demo.txt',mode='w',encoding='utf-8')
  f.write('呼呼，哈哈')
  ```
* 关闭文件，当打开文件执行了操作后，一定要记得关闭
  ```
  f.close()
  ```
* 防止忘记关闭文件
  ```
  with open('demo.txt',mode='r',encoding='utf-8') as f:
    print(f.read())
  ```
* 异常处理
try:
    执行代码
except 错误类型1：
    pass
except 错误类型2：
    pass
except (错误类型3,错误类型4):
    pass
```
try:
    1/0
    mylist = [1, 2, 3, 4, 5, 6]
    mylist[100]
except IndexError:
    print('wrong2')
except ZeroDivisionError:
    print('wrong')
```
* try：遇到错误代码就会终止分支，只会执行except ZeroDivisionError分支
* 异常处理写except Exception，不写具体错误类型，会不好定位问题
为什么进行异常处理？
为了让程序按我们的想法执行。
手动抛出异常 raise
```
class MyError(Exception):
    pass


try:
    mylist = [1, 2, 3]
    mylist[4]
    1 / 0
except (ZeroDivisionError, IndexError) as e:
    raise MyError
``` 
finally
```
try:
    mylist = [1, 2, 3]
    mylist[4]
    1 / 0
except (ZeroDivisionError, IndexError) as e:
    print('error')
finally:
    print('douhuiyuxning')
```


