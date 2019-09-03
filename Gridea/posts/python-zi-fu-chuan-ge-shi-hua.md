---
title: 'Python字符串格式化'
date: 2019-09-03 14:29:12
tags: []
published: true
hideInList: false
feature: 
---
# print style字符串格式化
通过在字符串后面追加一个百分号，再追加一个元组，元组里面加上你要组合的字符串
传入参数顺序替换占位符，返回替换后的字符串
```
In[]：
'i use %s,i am %d' % ('python',18)
Out[]：
'i use python,i am 18'
```
**注意：当在拼接sql的时候，一定要用这种print style，%的方式可以帮助我们避免恶意攻击者sql注入**
# format方法
format方法使用{}作为占位符
format可以在占位符里面加数字，指定format参数的位置
```
In[]：
s = 'i use {1},i am {0}'
s.format(18,'python')
Out[]：
'i use python,i am 18'
```
参数可以通过指定位置方式多次使用
```
In[]：
'{0}{0}'.format('python')
Out[]：
'pythonpython'
```
可以在占位符里加标识符，来使用关键字参数
```
In[]：
'{who} {do} {what}'.format(who='everyone',do='use',what='python')
Out[]：
'everyone use python'
```
同时支持使用位置和关键字参数
**位置参数必须要在前面，关键字参数在后面**
```
In[]：
'{0} {who} {do} {what}'.format('今天',who='everyone',do='use',what='python')
Out[]：
'今天 everyone use python'
```
若要打印{}，则在外面加一层{}即可
```
In[]：
'{{}}'.format()
Out[]：
'{}'
```
```
In[]：
'{{{}}}'.format(18)
Out[]：
'{18}'
```
# f前缀
python3.6开始新增了一项新的前缀，f前缀
```
In[]：
who = 'everyone'
do = 'use'
what = 'python'
f'{who} {do} {what}'
Out[]：
'everyone use python'
```
当在代码块的上文中已经提及了这些变量，可以直接用f前缀加上这些变量来组合
举个栗子：
```
In[]：
token = 'asdfasdfasdfasdf'
user_id = 1
dt = '2019-09-03'
url = f'http://you-are-one.com/?token={token}&user_id={user_id}&dt={dt}'
url
Out[]：
'http://you-are-one.com/?token=asdfasdfasdfasdf&user_id=1&dt=2019-09-03'
```





















