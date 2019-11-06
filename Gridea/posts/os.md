---
title: '包和模块'
date: 2019-10-21 09:21:51
tags: [Python]
published: true
hideInList: false
feature: 
---
模块是Python程序架构的一个核心概念
以py为后缀名的文件就是模块，含有__init__.py的目录叫做包
智能导入：alt + enter
导入方式：
1、import + 模块名，使用这种方式调用函数时必须用import后面的所有部分.函数来调用
2、import + 模块名 as 别名
3、from 包.模块名 import 函数名 
4、from 包 import 模块名
5、from 包 import 模块名 as 别名
6、from ... import * 引入所有的方法，尽量不使用此方法
别名的使用场景：
1、名字比较长 2、导入的名字和在这个文件当中存在同名的情况
包 --> 模块 --> 函数（类），变量
包是表示存储python代码的文件夹，在以前的python版本中package中有__init__.py才被认为是包，在新版本的python中package中没有__init__.py也被认为是包
模块的搜索顺序
在导入模块时：
* 搜索当前目录指定模块的文件，如果有就直接导入
* 如果没有，再搜索系统目录
* 将某个路径添加到系统系统下：sys.path.append('C:\class_09_modules')
* 每一个模块都有一个内置属性__file__ 可以查看模块的完整路径
__name__属性
* 测试模块的代码只在测试情况下被运行，而在导入时不会被执行
* __name__是一个内置属性
* 如果被其他文件导入的，__name__就是模块名
* 如果是当前执行的程序，__name__是__main__

__main__是程序入口，运行的哪一个文件，那么那一个文件就叫__main__
if __name__ == '__main__':  用来测试模块

