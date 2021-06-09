---
title: __name__ == '__main__'的作用
date: 2020-03-26 10:37:50
tags:
	- python
categories: #分类(分层)
    - python
index_img: //i.loli.net/2020/03/25/7DaRgZ981F6mPVs.jpg
---

技术性总结

## __name__ == '__main__'的作用


###  摘要
<!-- more -->

这句话d的作用相当于是程序的入口，有点类似于Java中的main方法，直接运行java文件便会执行main方法里面的函数及变量，从其他类进行导入创建实例化对象的时候需要自行调用，main方法里面的内容不会执行，但python中没有统一的入口，都是从脚本第一行开始运行。
```python
    通常的写法:
    if __name__ == '__main__'
```
以下面代码为例，如果我们是直接运行某个.py文件(python xxx.py)，下面代码就会执行，如果是当作模块去引用这个文件的话，下面代码并不会执行。引用从别人博客看到的一句话：
> 通俗的理解__name__ == '__main__'：例如小明.py，在朋友眼中，你是小明(__name__ == '小明')；在你自己眼中，你是你自身(__name__ == '__main__')。

先创建一个test1.py，然后直接运行
```python
    print(__name__)  # 运行结果：__main__
```
然后再创建一个test2.py，调用test1
```python
	import test1
	
	print(test1.__name__)  # 运行结果：test1
```
### 计算圆的面积的例子
先创建一个pi_cal.py
```python
    PI = 3.14  # 定义一下PI的大小

    def printText():
        print("PI:", 3.14)

    printText()

    # 运行结果：PI:3.14
```
然后我们创建一个area.py用来计算圆的面积，导入pi_cal.py中的PI变量用于计算。
```python
    from pi_cai.py import PI    # 只导入PI变量

    def calculate(radius):   # 传入半径
        return PI * (radius ** 2)
    
    def main():
        print("圆的面积：", calculate(2))
    
    main()

    # 运行结果：PI:3.14   圆的面积:12.56
```
很明显的，pi_cal.py中的printText()函数也执行了，我们只想要导入PI，并不想执行一次printText()函数，所以我们可以加上 **if __name__ == '__main__'，这样子的话就以模块进行导入时便不会执行不想要的函数了。
```python
    def printText():
        print("PI:", 3.14)

    if __name__ == '__main__':
        printText()
```
还看到一种用法觉得很不错：
> 这个功能还有一个用处：调试代码的时候，在”if __name__ == '__main__'“中加入一些我们的调试代码，我们可以让外部模块调用的时候不执行我们的调试代码，但是如果我们想排查问题的时候，直接执行该模块文件，调试代码能够正常运行！