---
title: '类的继承'
date: 2019-11-06 09:40:17
tags: []
published: true
hideInList: false
feature: 
---
```
class DalaoParent:
    def __init__(self, money):
        self.money = money

    def xiaomubiao(self, money):
        print(f"大佬今年定{money}的小目标")

    def paiting(self,type):
        print('想做什么就做什么')

class Dalao(DalaoParent):
    # def __init__(self, money):
    #     self.money = money
    def paiting(self, type):
        super().paiting(type)
        print(f'想当{type}派画家')


xixi = Dalao(10000)
print(xixi.money)
xixi.xiaomubiao(20000)
xixi.paiting('野兽')

xx_parent = DalaoParent(30000)
xx_parent.paiting('抽象')
```
```
class Mobile:
    def __init__(self, brand, model, color):
        self.brand = brand
        self.model = model
        self.color = color
        print('Mobile正在初始化')

    def call(self, phone_number):
        print(f'呼叫电话号码{phone_number}')

class IphoneMobile(Mobile):
    brand = '苹果'

    def __init__(self, model, color):
        # self.model = model
        # self.color = color
        # Mobile(self.brand, model, color)
        # super().__init__(self.brand, model, color)
        # Mobile(self.brand, model, color).call('123')
        super().call('123')
        print('Iphone正在初始化')
iphone5 = IphoneMobile('5', '黑色')
```
重写 __init__方法被重写了，不会用父类里买的__init__
super()的作用 如果想使用父类里面的方法 1、Parent().方法() 2、super().方法()
多重继承
```
class Mobile:
    def __init__(self, brand, model, color):
        self.brand = brand
        self.model = model
        self.color = color
        print('Mobile正在初始化')

    def call(self, phone_number):
        print(f'呼叫电话号码{phone_number}')

    def say(self, data):
        print(f'普通手机正在说{data}')

class Game:
    def play(self, name):
        print(f'正在玩{name}')

class Voice:
    def say(self, data):
        print(f'手机正在说{data}')

class SmartPhone(Mobile, Voice, Game):
    '''智能手机'''
    # def say(self, data):
    #     print(f'智能手机正在说{data}')


smart_phone = SmartPhone("苹果", "8", "红色")
smart_phone.call('186')
smart_phone.play('王者荣耀')
smart_phone.say('666')
```
