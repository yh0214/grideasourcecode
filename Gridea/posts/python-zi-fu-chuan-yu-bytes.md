---
title: 'Python字符串与bytes'
date: 2019-09-03 16:10:40
tags: []
published: true
hideInList: false
feature: 
---
# 定义
* str是文本序列
* bytes是字节序列

## 区别
* 文本是有编码的，例如：utf8、gbk
* 字节没有编码
* 文本的编码指的是字符如何使用字节来表示

## 编码
* 单字节编码，例如：ascii
* 多字节编码，例如：utf8

**注意：python3中，字符串默认使用utf8编码**
而把字符串经过编码后的数据类型，我们称为bytes
以下这段编码就是用utf8编码表示的字节：
```
In[]：
s = '人人都是Pythonista'
s.encode()
Out[]：
b'\xe4\xba\xba\xe4\xba\xba\xe9\x83\xbd\xe6\x98\xafPythonista'
```
bytes是可以转化成字符串的
```
In[]：
s = '人人都是Pythonista'
bt = s.encode()
bt.decode()
Out[]：
'人人都是Pythonista'
```
**在python3中，socket只能用bytes**
**注意：在python2中不区分bytes和str**
# bytes
## bytes定义
str的所有操作，bytes都支持
* bytes由str通过encode方法转化得到
* 通过b前缀定义bytes

```
In[]：
bt = b'abc'
type(bt)
Out[]：
bytes
```
## bytes操作
bytes的操作除了encode外，str操作都有对应bytes的版本，但是传入参数也必须是bytes，如果传入字符串会报错
栗子（使用socket发送十六进制报文）：
1. 将字符串转换为十六进制字节
2. 将十六进制字节转换为字符串
```
In[]：
a = 'aabbccddeeff'
a_bytes = bytes.fromhex(a)
print(a_bytes)
aa = a_bytes.hex()
print(aa)
Out[]：
b'\xaa\xbb\xcc\xdd\xee\xff'
aabbccddeeff
```
# bytearray
bytearray是bytes的可变版本
str和bytes是不可变的
bytearray是可变类型，进行一次替换
```
In[]：
ba = bytearray(b'abc')
ba[0] = int(b'D'.hex(),16)
ba
Out[]：
bytearray(b'Dbc')
```
这里要注意几个地方
* bytearray更新的时候，也是一个一个字节更新的，不是一个字符串
* 要把字节转换成十六进制数进行更替
## 使用场景
图像处理
修改图片时，图片保存成了字节，需要一个可变版本的bytes
## bytearray的方法
相对bytes来说，多了insert，append，extend，pop，remove，clear，reverse
其实就是多了list的那些方法，并且可以索引操作
但是和修改bytearray一样，所有的方法中，都需要用int来表示，而非bytes本身
int必须在0~256这个范围内，即8位的无符号整数



























