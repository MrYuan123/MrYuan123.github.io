---
layout:     post
title:      "How to build python data mining platform"
subtitle:   " \"Hello World, Hello Blog\""
date:       2017-3-17 16：00
author:     "Leonard Yuan"
header-img: "../img/post-bg-kuaidi.jpg"
catalog: true
tags:
    - Data Analysis
    - Ubuntu

---

# 数据分析环境搭建

>在使用python进行数据挖掘过程中，有几个重要的第三方库经常会使用到，这几个库分别为numpy、pandas、scipy和matplotlib，本节将分别指导安装如上的几个库，用于数据挖掘使用。


### 1.安装pip(pip3)

在ubuntu操作系统之下，我们使用pip安装第三方库比较方便，因此我们需要先安装pip(pip3)，如果使用python2安装pip，如果使用python3则安装pip3。（因本机采用python3，安装pip3）。如下：

	sudo apt install python3-pip

### 2.安装第三方库

在安装pip3后，我们开始安装第三方库，指令如下：

	pip3 install pandas
	pip3 install numpy
	pip3 install scipy
	pip3 install matplotlib

**注意：如果出现访问权限不够，无法安装的情况，如下。遇到这种情况在指令前面夹sudo即可。**

<p>
<img src="/img/in_post/17.1.png"/>
</p>

在安装好如上第三方库之后，有可能会出现matplotlib库无法使用的情况，提示“python-tk package”未安装，则采取如下的处理：

	sudo apt-get install python3-tk
	pip3 install matplotlib
	pip3 install nose
	pip3 install pillow

使用指令`from PIL import Image`验证正确性。

问题解决！

### 3.程序测试

我们拿一段实例代码来测试，安装库的结果，代码如下：

	import numpy as np
	import matplotlib.pyplot as plt

	# 创建对象
	fig = plt.figure();

	# 限制坐标的范围
	ax = plt.axes(xlim=(0, 5 * np.pi), ylim=(-2, 2))

	# 用划分坐标区间，趋近曲线
	x = np.linspace(0, 5 * np.pi, 1000);

	# 函数表达式
	y = np.sin(x);

	# 绘制曲线
	ax.plot(x, y);

	# 显示图像
	plt.show()

运行结果如下：

<p>
<img src="/img/in_post/17.2.png"/>
</p>
