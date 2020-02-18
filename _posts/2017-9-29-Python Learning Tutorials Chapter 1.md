---
layout:     post
title:      "Python Learning Tutorials Chapter 1"
subtitle:   " \"人生苦短，我用python\""
date:       2017-9-29 9：00
author:     "Leonard Yuan"
header-img: "img/post-bg-rwd.jpg"
catalog: true
tags:
    - Python

---

>python学习笔记。

---

# python学习教程1

## 参数

1.在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。


2.默认参数一定要用不可变对象，如果是可变对象，程序运行时会有逻辑错误！
要注意定义可变参数和关键字参数的语法：

>*args是可变参数，args接收的是一个tuple；
>
>**kw是关键字参数，kw接收的是一个dict。

## 切片

1.tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple：

	>>> (0, 1, 2, 3, 4, 5)[:3]
	>>> (0, 1, 2)

**注：当对tuple进行操作时，使用的仍然是[ ：]，而不是变换为（ ： ）**

## 迭代：

1.list这种数据类型虽然有下标，但很多其他数据类型是没有下标的，但是，只要是可迭代对象，无论有无下标，都可以迭代，比如dict就可以迭代：

	>>> d = {'a': 1, 'b': 2, 'c': 3}
	>>> for key in d:
	>>>    print(key)
	... a c b

因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。

## 列表生成式

for循环其实可以同时使用两个甚至多个变量，比如dict的items()可以同时迭代key和value：

	>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
	>>> for k, v in d.items():
	>>>    print(k, '=', v)
	... y = B x = A z = C

因此，列表生成式也可以使用两个变量来生成list：

	>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
	>>> [k + '=' + v for k, v in d.items()]
	>>> ['y=B', 'x=A', 'z=C']

**isinstance(x, str)**

此函数是用于判断X是否属于定义的类型str，其中可使用类型中可以定义多个类型**isinstance(x,(int,str))**。

## 生成器

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：

	>>> L = [x * x for x in range(10)]
	>>> L
	... [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

	>>> g = (x * x for x in range(10))
	>>> g
	... <generator object <genexpr> at 0x1022ef630>

创建L和g的区别仅在于最外层的[]和()，L是一个list，而g是一个generator。

我们可以直接打印出list的每一个元素，但我们怎么打印出generator的每一个元素呢？

如果要一个一个打印出来，可以通过next()函数获得generator的下一个返回值：

	>>> g = (x * x for x in range(10))
	>>> for n in g:
	>>>     print(n)
 	... 0

注:以上是使用迭代来打印的全过程

斐波拉契数列用列表生成式写不出来，但是，用函数把它打印出来却很容易：

	def fib(max):
    	n, a, b = 0, 0, 1
    	while n < max:
        	print(b)
        	a, b = b, a + b
        	n = n + 1
    	return 'done'

以上为函数执行斐波那契数列的过程。

值得注意的是：

a , b = b , a + b

表示a=b  b=a(原来)+b

最难理解的就是generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。

上面的函数和generator仅一步之遥。要把fib函数变成generator，只需要把print(b)改为yield b就可以了：

	def fib(max):
    	n, a, b = 0, 0, 1
    	while n < max:
    	    yield b
    	    a, b = b, a + b
    	    n = n + 1
    	return 'done'

如上是将函数转变为generator的全过程。

## isinstance()判断

我们已经知道，可以直接作用于for循环的数据类型有以下几种：

- 一类是集合数据类型，如list、tuple、dict、set、str等；

- 一类是generator，包括生成器和带yield的generator function。

这些可以直接作用于for循环的对象统称为可迭代对象：Iterable。

可以使用isinstance()判断一个对象是否是Iterable对象：

	>>> from collections import Iterable

	>>> isinstance([], Iterable)
	True

	>>> isinstance({}, Iterable)
	True

	>>> isinstance('abc', Iterable)
	True

	>>> isinstance((x for x in range(10)), Iterable)
	True

	>>> isinstance(100, Iterable)
	False

**可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。**

可以使用isinstance()判断一个对象是否是Iterator对象：
isinstance((x for x in range(10)), Iterator)

你可能会问，为什么list、dict、str等数据类型不是Iterator？

这是因为Python的Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过next()函数实现按需计算下一个数据，所以Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算。

## 函数式编程

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

函数式编程的一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！
Python对函数式编程提供部分支持。由于Python允许使用变量，因此，Python不是纯函数式编程语言。

既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

一个最简单的高阶函数：

	def add(x, y, f):
       return f(x) + f(y)

map()函数和reduce()函数的区别：

	map()作为高阶函数，事实上它把运算规则抽象了，因此，我们不但可以计算简单的f(x)=x2，
	还可以计算任意复杂的函数，比如，把这个list所有数字转为字符串：

	>>> list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
	['1', '2', '3', '4', '5', '6', '7', '8', '9']

reduce把结果继续和序列的下一个元素做累积计算，其效果就是：

reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

**参考资料**

**http://my.oschina.net/davehe/blog/122418**

如上网址介绍lambda函数的使用方法

**http://www.jb51.net/article/37287.htm**

介绍用于删除字符串中字符或者字符串的几个函数

## filter()函数的使用

Python内建的filter()函数用于过滤序列。

和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

相当于用于剔除序列中不符合条件的元素

## 返回函数

但是，如果不需要立刻求和，而是在后面的代码中，根据需要再计算怎么办？可以不返回求和的结果，而是返回求和的函数！

	def lazy_sum(*args):
    	def sum():
    	    ax = 0
    	    for n in args:
    	        ax = ax + n
    	    return ax
    	return sum

当我们调用lazy_sum()时，返回的并不是求和结果，而是求和函数：

	>>> f = lazy_sum(1, 3, 5, 7, 9)
	>>> f
	<function sum at 0x10452f668>

调用函数f时，才真正计算求和的结果：

	>>> f()
	25

**注意调用的方式**

返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量。

## 匿名函数

当我们在传入函数时，有些时候，不需要显式地定义函数，直接传入匿名函数更方便。

在Python中，对匿名函数提供了有限支持。还是以map()函数为例，计算f(x)=x2时，除了定义一个f(x)的函数外，还可以直接传入匿名函数：

	>>> map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9])
	[1, 4, 9, 16, 25, 36, 49, 64, 81]

匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果。

用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数：

	>>> f = lambda x: x * x
	>>> f
	<function <lambda> at 0x10453d7d0>
	>>> f(5)
	25

同样，也可以把匿名函数作为返回值返回，比如：

	def build(x, y):
    	return lambda: x * x + y * y

上面的函数调用时，应为：

	f=build( 2, 4)
	print f()

注：在使用匿名函数时，注意调用的方式，以及在lambda后面不加参数。

## 装饰器

由于函数也是一个对象，而且函数对象可以被赋值给变量，所以，通过变量也能调用该函数。

	>>> def now():
	...     print '2013-12-25'
	...
	>>> f = now
	>>> f()

函数对象有一个__name__属性，可以拿到函数的名字：

	>>> now.__name__
	'now'
	>>> f.__name__
	'now'

现在，假设我们要增强now()函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改now()函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）。
注意：name左右的下划线不是一个，而是两个，切记！

## 偏函数

functools.partial就是帮助我们创建一个偏函数的，不需要我们自己定义int2()，可以直接使用下面的代码创建一个新的函数int2：

	>>> import functools
	>>> int2 = functools.partial(int, base=2)
	>>> int2('1000000')
	64
	>>> int2('1010101')
	85

所以，简单总结functools.partial的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单。
