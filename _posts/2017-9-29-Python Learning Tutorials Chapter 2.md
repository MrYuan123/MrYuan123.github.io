---
layout:     post
title:      "Python Learning Tutorials Chapter 2"
subtitle:   " \"人生苦短，我用python\""
date:       2017-9-29 10：00
author:     "Leonard Yuan"
header-img: "img/post-bg-miui6.jpg"
catalog: true
tags:
    - Python

---

>python学习笔记。

---

## 文件I/O处理：

读写文件是最常见的IO操作。Python内置了读写文件的函数，用法和C是兼容的。

读写文件前，我们先必须了解一下，在磁盘上读写文件的功能都是由操作系统提供的，现代操作系统不允许普通的程序直接操作磁盘，所以，读写文件就是请求操作系统打开一个文件对象（通常称为文件描述符），然后，通过操作系统提供的接口从这个文件对象中读取数据（读文件），或者把数据写入这个文件对象（写文件）。

1.读文件

要以读文件的模式打开一个文件对象，使用Python内置的open()函数，传入文件名和标示符：

	>>> f = open('/Users/michael/test.txt', 'r')

标示符'r'表示读，这样，我们就成功地打开了一个文件。

如果文件不存在，open()函数就会抛出一个IOError的错误，并且给出错误码和详细的信息告诉你文件不存在，如下：

	>>> f=open('/Users/michael/notfound.txt', 'r')
	Traceback (most recent call last):
  		File "<stdin>", line 1, in <module>
	IOError: [Errno 2] No such file or directory: '/Users/michael/notfound.txt'

如果文件打开成功，接下来，调用read()方法可以一次读取文件的全部内容，Python把内容读到内存，用一个str对象表示：

	>>> f.read()
	'Hello, world!'

最后一步是调用close()方法关闭文件。文件使用完毕后必须关闭，因为文件对象会占用操作系统的资源，并且操作系统同一时间能打开的文件数量也是有限的：

	>>> f.close()
	>
由于文件读写时都有可能产生IOError，一旦出错，后面的f.close()就不会调用。所以，为了保证无论是否出错都能正确地关闭文件，我们可以使用try ... finally来实现：

	try:
    	f = open('/path/to/file', 'r')
   	 	print f.read()
	finally:
    	if f:
    	    f.close()

但是每次都这么写实在太繁琐，所以，Python引入了with语句来自动帮我们调用close()方法：

	with open('/path/to/file', 'r') as f:
	    print f.read()

这和前面的try ... finally是一样的，但是代码更佳简洁，并且不必调用f.close()方法。

调用read()会一次性读取文件的全部内容，如果文件有10G，内存就爆了，所以，要保险起见，可以反复调用read(size)方法，每次最多读取size个字节的内容。另外，调用readline()可以每次读取一行内容，调用readlines()一次读取所有内容并按行返回list。因此，要根据需要决定怎么调用。

如果文件很小，read()一次性读取最方便；如果不能确定文件大小，反复调用read(size)比较保险；如果是配置文件，调用readlines()最方便：

	for line in f.readlines():
    	print(line.strip()) # 把末尾的'\n'删掉
	file-like Object

像open()函数返回的这种有个read()方法的对象，在Python中统称为file-like Object。除了file外，还可以是内存的字节流，网络流，自定义流等等。file-like Object不要求从特定类继承，只要写个read()方法就行。

StringIO就是在内存中创建的file-like Object，常用作临时缓冲。

## 二进制文件

前面讲的默认都是读取文本文件，并且是ASCII编码的文本文件。要读取二进制文件，比如图片、视频等等，用'rb'模式打开文件即可：

	>>> f = open('/Users/michael/test.jpg', 'rb')
	>>> f.read()
	'\xff\xd8\xff\xe1\x00\x18Exif\x00\x00...' # 十六进制表示的字节

## 字符编码

要读取非ASCII编码的文本文件，就必须以二进制模式打开，再解码。比如GBK编码的文件：

	>>> f = open('/Users/michael/gbk.txt', 'rb')
	>>> u = f.read().decode('gbk')
	>>> u
	u'\u6d4b\u8bd5'
	>>> print u

#测试

如果每次都这么手动转换编码嫌麻烦（写程序怕麻烦是好事，不怕麻烦就会写出又长又难懂又没法维护的代码），Python还提供了一个codecs模块帮我们在读文件时自动转换编码，直接读出：

	unicode：
	import codecs
	with codecs.open('/Users/michael/gbk.txt', 'r', 'gbk') as f:
    	f.read() # u'\u6d4b\u8bd5'


## 操作文件和目录

打开Python交互式命令行，我们来看看如何使用os模块的基本功能：

	>>> import os
	>>> os.name # 操作系统名字
	... 'posix'

如果是posix，说明系统是Linux、Unix或Mac OS X，如果是nt，就是Windows系统。
----------------------------略（后续学习）

## 正则表达式

1.分组

除了简单地判断是否匹配之外，正则表达式还有提取子串的强大功能。用()表示的就是要提取的分组（Group）。比如：

^(\d{3})-(\d{3,8})$分别定义了两个组，可以直接从匹配的字符串中提取出区号和本地号码：

	>>> m = re.match(r'^(\d{3})-(\d{3,8})$', '010-12345')
	>>> m
	<_sre.SRE_Match object at 0x1026fb3e8>

	>>> m.group(0)
	'010-12345'

	>>> m.group(1)
	'010'

	>>> m.group(2)
	'12345'

## 贪婪匹配

最后需要特别指出的是，正则匹配默认是贪婪匹配，也就是匹配尽可能多的字符。举例如下，匹配出数字后面的0：

	>>> re.match(r'^(\d+)(0*)$', '102300').groups()
	('102300', '')

由于\d+采用贪婪匹配，直接把后面的0全部匹配了，结果0*只能匹配空字符串了。

必须让\d+采用非贪婪匹配（也就是尽可能少匹配），才能把后面的0匹配出来，加个?就可以让\d+采用非贪婪匹配：

	>>> re.match(r'^(\d+?)(0*)$', '102300').groups()
	('1023', '00')

## 面向对象的编程

	class Student(object):

    	def __init__(self, name, score):
        	self.name = name
        	self.score = score

    	def print_score(self):
        	print '%s: %s' % (self.name, self.score)

注意到\__init\__方法的第一个参数永远是self，表示创建的实例本身，因此，在\__init\__方法内部，就可以把各种属性绑定到self，因为self就指向创建的实例本身。

有了\__init\__方法，在创建实例的时候，就不能传入空的参数了，必须传入与\__init\__方法匹配的参数，但self不需要传，Python解释器自己会把实例变量传进去：

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线"\__"，在Python中，实例的变量名如果以"\__"开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问。

	class Student(object):
    	def get_name(self):
			return self.__name
		def get_score(self):
			return self.__score

需要注意的是，在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用\__name\__、\__score\__这样的变量名。


双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问\__name是因为Python解释器对外把\__name变量改成了\_Student\__name，所以，仍然可以通过\_Student\__name来访问\__name变量：

	>>> bart._Student__name
	'Bart Simpson'

但是强烈建议你不要这么干，因为不同版本的Python解释器可能会把__name改成不同的变量名。

## 继承和多态

	class Animal(object):
		def run(self):
			print 'Animal is running...'

	class Dog(Animal):
    	pass

	class Cat(Animal):
    	pass

如上是继承的方式。

当子类和父类都存在相同的**run()**方法时，我们说，子类的run()覆盖了父类的run()，在代码运行的时候，总是会调用子类的run()。这样，我们就获得了继承的另一个好处：多态。

判断一个变量是否是某个类型可以用**isinstance()**判断：

	>>> isinstance(a, list)
	True

	>>> isinstance(b, Animal)
	True

	>>> isinstance(c, Dog)
	True

当我们拿到一个对象的引用时，如何知道这个对象是什么类型、有哪些方法呢？

### 1. type函数

首先，我们来判断对象类型，使用type()函数，基本类型都可以用type()判断；

### 2. 使用isinstance()

对于class的继承关系来说，使用type()就很不方便。我们要判断class的类型，可以使用isinstance()函数。我们回顾上次的例子，如果继承关系是：

> object -> Animal -> Dog -> Husky

那么，isinstance()就可以告诉我们，一个对象是否是某种类型。先创建3种类型的对象：

	>>> a = Animal()
	>>> d = Dog()
	>>> h = Husky()

然后，判断：

	>>> isinstance(h, Husky)
	True


### 3. 使用dir()

如果要获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法：

	>>> dir('ABC')
	['__add__', '__class__', '__contains__', '__delattr__', '__doc__',
	'__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__',
	'__getnewargs__', '__getslice__', '__gt__', '__hash__', '__init__',
	'__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__',
	 '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__',
	'__setattr__', '__sizeof__', '__str__', '__subclasshook__',
	'_formatter_field_name_split', '_formatter_parser', 'capitalize',
	'center', 'count', 'decode', 'encode', 'endswith', 'expandtabs', 'find',
	 'format', 'index', 'isalnum', 'isalpha', 'isdigit', 'islower',
	'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip',
	'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition',
	'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip',
	'swapcase', 'title', 'translate', 'upper', 'zfill']
