---
title: '类的方法&变量'
date: 2019-10-30 11:07:07
tags: []
published: true
hideInList: false
feature: 
---
```
class Mobile:
    has_logo = True
    has_ram = True

    def __init__(self,model,brand):
        # 把参数转化成实例变量
        self.mobile_model = model
        self.brand = brand

    def capture(self):
        # 实例方法中使用类变量
        print(self.has_logo)
        print("{}正在照相".format(self.brand))

    def beautify_cap(self):
        self.capture()
        print("修照片")

    @classmethod
    def if_logo(cls):
        # 类方法
        # 类方法很少使用
        print(cls.has_logo)

    @staticmethod
    def check_weather():
        print("今天天气......")
```
对象的实例化
```
iphone5 = Mobile('5', '苹果')
```
怎么去使用类的变量 类的变量包含类变量和实例变量
```
print(iphone5.mobile_model)
print(iphone5.brand)
```
类外面使用类变量
```
print(Mobile.has_logo)
print(iphone5.has_logo)
```
对象调用实例方法
iphone5.capture()

类变量和实例变量有什么区别？
类变量能同时被类和实例访问，实例变量只能被实例自己访问

实例属性放在__init__中定义，self.相关的属性优先放在__init__中定义

静态方法和这个类以及对象没有关系，但是有关联
静态方法和普通函数相比，好处是方便管理
例子
```
class InterViewer:

    def __init__(self, name):
        self.name = name

    def offer(self, money, time):
        print("{} 收了一个大 offer：月薪{},k {}天到岗".format(self.name, money, time))
        return '拿 offer'

    def eat(self, food):
        print("{} 最喜欢吃 {}".format(self.name, food))

    def interviwing(self):
        print("正在面试")


cainiao = InterViewer('菜鸟')
print(cainiao.offer(50, 1))
cainiao.interviwing()
```
```
class FileHandler:
    def __init__(self,filename,encoding='utf-8'):
        self.filename = filename
        self.encoding = encoding

    def read_file(self):
        with open(self.filename, mode='r', encoding=self.encoding) as f:
            a = f.read()
        return a

    def write_file(self, data,mode='w'):
        with open(self.filename, mode=mode, encoding=self.encoding) as f:
            f.write(data)


handler = FileHandler('demo.txt')
print(handler.read_file())

handler.write_file('147258369',mode='a')
```













