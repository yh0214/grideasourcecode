---
title: '单元测试框架'
date: 2019-11-06 14:07:39
tags: []
published: true
hideInList: false
feature: 
---
测试是判断预期结果和实际结果是否一致，类似于条件判断 
断言 assert
```
def add(a, b):
    return a + b

expcted = 7
actual = add(3, 4)
assert actual == expcted
```
单元测试框架 同样可以使用在接口测试、ui测试
unittest python自带的一个单元测试框架
```
import unittest
def add(a, b):
    return a + b
x = 3
y = 5
expected = 8
class TestAdd(unittest.TestCase):

    def test_add_success(self):
        # 测试用例方法
        # 要准备 预期结果和世界结果
        self.assertTrue(expected == add(x, y))

    def test_add_error(self):
        self.assertEqual(7, add(x, y))
```
```
import unittest


def add(a, b):
    return a + b


x = 3
y = 5
expected = 8


class TestAdd(unittest.TestCase):  # 类名最好是Test开头
    # 测试用例的设计 前置条件 后置条件
    @classmethod
    def setUpClass(cls):
        print('测试类之前')

    @classmethod
    def tearDownClass(cls):
        print('测试类之后')

    def setUp(self):
        '''前置条件'''
        # 每个测试用例方法之前自动运行setUp里面的程序
        self.data = [
            {'a': 3, 'b': 4, 'expected': 7},
            {'a': 5, 'b': 9, 'expected': 8}
        ]
        print('用例执行前置条件')

    def tearDown(self):
        '''后置条件'''
        # 每个测试用例方法之后自动执行tearDown里面的程序
        print('用例执行后置条件')

    def test_add_success(self):  # 测试用例方法一定要test_开头
        # 断言方式有很多
        self.assertTrue(self.data[0]['expected'] == add(self.data[0]['a'], self.data[0]['b']))
        # self.assertGreater()

    def test_add_error(self):
        self.assertEqual(self.data[1]['expected'], add(self.data[1]['a'], self.data[1]['b']))


if __name__ == '__main__':
    unittest.main()
```
F表示测试用例不通过 .表示测试用例通过
运行使用unittest框架代码的两种方式 1、pycharm中右键选择Run 'Unittests in ...' 2、添加上代码unitest.main()后，使用python ...运行
可以根据python -m unittest 模块名.测试类名.测试方法运行指定的测试用例方法
unittest 用例执行顺序是用例方法名根据ASCII编码顺序执行
```
import unittest


def minus(a, b):
    return a - b


x = 3
y = 5

expected = -2


class TestMinus(unittest.TestCase):  # 类名最好是Test开头

    def test_minus_success(self):  # 测试用例方法一定要test_开头
        # 断言方式有很多
        self.assertTrue(expected == minus(x, y))

    def test_minus_error(self):
        self.assertEqual(7, minus(x, y))


if __name__ == '__main__':
    unittest.main()
```
```
# 初始化一个对象 suite 测试套件（集合）
import unittest

# 初始化测试套件
from class_14_单元测试.test_add import TestAdd
from class_14_单元测试.test_minus import TestMinus

from class_14_单元测试 import test_add
from class_14_单元测试 import test_minus

suite = unittest.TestSuite()
# 往套件里面添加测试用例

cases = [TestAdd('test_add_success'),
         TestAdd('test_add_error'),
         TestMinus('test_minus_success'),
         TestMinus('test_minus_error')]
suite.addTests(cases)

# TestLoader 用来加载测试用例的
# 可以根据模块加载，也可以根据测试类加载，也可以自己定义规则加载
# 初始化一个loader
loader = unittest.TestLoader()
# 根据测试类加载测试用例
# cases1 = loader.loadTestsFromTestCase(TestAdd)
# cases2 = loader.loadTestsFromTestCase(TestMinus)
cases1 = loader.loadTestsFromModule(test_add)
cases2 = loader.loadTestsFromModule(test_minus)
suite1 = unittest.TestSuite()
suite1.addTests(cases1)
suite1.addTests(cases2)

# 运行，测试报告文件 demo.txt

with open('demo5.txt', mode='w', encoding='utf-8') as f:
    # 初始化 runner
    runner = unittest.TextTestRunner(f, verbosity=2)
    # 运行
    runner.run(suite1)

```
自动发现测试用例
```
import os
import unittest

# 自动发现测试用例
# suite1 = unittest.TestSuite()
# 初始化 loader
loader = unittest.TestLoader()
# 自动发现测试用例
test_dir = os.path.dirname(os.path.abspath(__file__))
# discover()方法返回的结果就是一个suite，所以就不需要再定义suite了
suite1 = loader.discover(test_dir)
with open('demo6.txt', mode='w', encoding='utf-8') as f:
    runner = unittest.TextTestRunner(f, verbosity=2)
    runner.run(suite1)

```
HTMLTestRunner
```
import os
import unittest
# 导入htmltestrunner
from datetime import datetime
from class_14_单元测试.HTMLTestRunner import HTMLTestRunner


# 下载htmltestrunner  http://tungwaiyip.info/software/HTMLTestRunner.html
# 自动发现测试用例
# suite1 = unittest.TestSuite()
# 初始化 loader
loader = unittest.TestLoader()
# 自动发现测试用例
start_dir = os.path.dirname(os.path.abspath(__file__))
# discover()方法返回的结果就是一个suite，所以就不需要再定义suite了
suite1 = loader.discover(start_dir)


# html文件 模式为二进制写入模式 二进制不需要写encoding
# 测试报告放到report文件夹
# 根据时间动态生成一个文件名
report_dir = os.path.join(start_dir,'report')
if not os.path.exists(report_dir):
    os.mkdir(report_dir)

time_str = datetime.now().strftime('%Y-%m-%d %H-%M-%S')

# report/2019-11-5.html
file_name = os.path.join(report_dir,time_str + '.html')
with open(file_name, mode='wb') as f:
    runner = HTMLTestRunner(f,
                            verbosity=2,
                            title='python的第一份测试报告',
                            description='哈哈哈',
                            tester='yh')
    runner.run(suite1)

```
