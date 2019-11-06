---
title: '类的创建&调用'
date: 2019-10-30 08:48:14
tags: []
published: true
hideInList: false
feature: 
---
类，一群有共同的特征和行为的事物
类名，标识符，大驼峰命名法
类的表示方法
```
class DaLao:
    pass
```
特征又被称为属性，类属性，类成员都具备的共同点。
特征由变量表示，变量写在类下面
```
class DaLao:
    haird = "low"
    eyed = "class"
    fav_shoes = "tuo shoes"


print(DaLao.haird)
print(DaLao.eyed)
```
对象：某个类下面具体的一个个体
在类里面定义的函数称为方法
初始化方法也叫构造函数 只能返回None
初始化对象的时候自动调用__init__方法
实例 = 对象
类变量 = 类属性
实例变量 = 实例属性
实例变量是表示某一个对象拥有的特征
```
class SingleDog:
    freedom = True
    favor = "吃狗粮"
    sports_hobby = "睡觉"

    def __init__(self,name,favor_game):
        self.name = name
        self.favor_game = favor_game
        print('hello')


single_dog = SingleDog('huhu','abc')
print(single_dog)
```
























