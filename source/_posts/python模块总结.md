---
title: python模块总结
date: 2020-03-29 17:05:56
tags: 
    - python
category: #分类(分层)
    - python
index_img: https://cdn-ali-img-shstaticbz.shanhutech.cn/bizhi/staticwp/202205/7b1d1b735095c31f76061f1ea52b2a0d--1172751072.jpg
---

模块的调用及创建

## 模块的导入

### 模块导入的方式

```python
import math				# 导入一个模块
import math, turtle		# 这种方式可以导入多个模块
import math as mth		# 导入模块并赋予新的名字(调用时使用新的名字)
from math import pi		# 导入模块中指定的成员(这样导入后可以直接使用)
form math import *		# 导入模块中所有的成员(不建议使用)

```


### 模块的加载

导入一个math模块，无论写了多少import语句，都只会加载一次，如果想要重新加载，可以使用这样的方式:

```python
import importlib	# 需要导入这个模块
importlib.reload(math)	# 然后调用这个方法
```





## package的使用

### 包的结构
将模块放在一起就形成了“包”，包的文件夹里必须有__init__.py的文件，这个文件就是包的标识，一般用于定义form xxx import * 所导入的成员。
包的下面可以有子包，就像文件夹一样，文件夹下可以有文件夹。



### 子包的引用

```python
form .. import xx	# ..表示上级目录
form . import xx	# .表示同级目录
```



### sys.path和模块搜索路径

模块搜索路径(由上到下的顺序进行搜索)：

​	1.内置模块

​	2.当前目录

​	3.程序主目录(也就是项目目录)

​	4.pythonpath目录(需要设置pythonpath环境变量)

​	5.标准链接库目录

​	6.第三方库目录(site-packages)

	7. .pth文件里面的内容(前提是这个文件存在)
 	8. 通过sys.path.append()临时添加的目录

 使用sys.path修改搜索目录：

```python
import sys
sys.path.append('d:/')
```