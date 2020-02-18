---
layout:     post
title:      "Java Learning Tutorials Chapter 2"
subtitle:   " \"Hello World, Hello Blog\""
date:       2016-11-17 18：00
author:     "Leonard Yuan"
header-img: "img/home_pg1.jpg"
catalog: true
tags:
    - Java

---

>java学习笔记。

---

# java学习笔记2

## 一.类的继承

**Java只支持类的单继承，每个子类只能 有一个直接父类。**

## 1.继承的基本性质：

- 父类是所有子类的公共属性及方法的集合，子类则是父类的特殊化；
- 只需指明新类与现有类的不同，即增加 自己的属性和方法即可；
- 继承介于类之间，而不是对象之间；


## 2.类的分类

类主要有基类和派生类两种；

## 3.继承类的基本语法格式

	class childClass extends parentClass {
	//类体
	}
	其中extends表示继承父类的属性和行为；
	parentClass表示被继承的父类名称；

## 4.成员的继承方法

- 子类的对象可以使用其父类中声明为`公有（及保护）`的属性和方法，就如同在其自己的类中声明一样；
- 子类不能直接访问从父类中继承的私有 属性及方法，但可以使用公有（及保护）方法进行访问；
- 类对从父类继承来的属性变量及方法可以重新加以定义。如果派生类某成员名和基类某成员名同名，派生类同名变量成员隐藏基类成员，派生类同名 方法成员覆盖基类成员；
- 当子类执行继承自父类的操作时，处理的是继 承自父类的变量，而当子类执行它自己声明的方法时，所操作的就是它自己声明的变量，而把继承自父类的变量“隐藏”起来了；
- 子类不能继承父类中的静态属性，但可以对父类中的静态属性进行操作;

## 5.被隐藏的父类属性的访问

- 调用从父类继承的方法，则操作的是从父类继承的属性 ；
- 使用super.属性;
-
## 6.方法覆盖

定义一个与父类的方法相同参数、相同返回值、相同方法名的方法，这样就可以覆盖掉继承于父类的方法。这种方法适用于当不需要从父类继承的某方法，或者具有相同功能，但不同算法的方法。

**当成员被覆盖时，可以使用super.的方法进行访问**

# 二.object类的使用

## 1.基本概述

-  Java程序中所有类的直接或间接父类，类库中 所有类的父类，处在类层次最高点;
- 包含了所有Java类的公共属性，其构造方法是 Object( );

## 2.在object类包含主要方法

	public final Class getClass()：
	获取当前对象所属的类信息，返回Class对象
	public String toString()：
	返回当前对象本身的有关信息，按字符串对象返回
	public boolean equals(Object obj)：
	比较两个对象是否是同一对象，是则返回true
	protected Object clone( )：
	生成当前对象的一个拷贝，并返回这个复制对象
	Public int hashCode()：
	返回该对象的哈希代码值
	protected void finalize() throws Throwable ：
	定义回收当前对象时所需完成的资源释放工作

## 3.相等和同一的概念

两个对象具有相同的类型、相同的属性，称为二者相等；

两个引用变量指向同一个对象，则称为两个变量同一；

**注：使用等号“==”或者使用“equals()函数”可以判断对象是否同一的，所以对于两个具有相同变量的对象的判断，最终的结果只能是“no”；**

对于这种情况，可以通过重写equals()的方法来实现对象相等的判断；

重写的示例equals()显示如下：

	public boolean equals(Object obj) {
		if (obj instanceof Apple) {
			 Apple a = (Apple) obj;
			return (color.equals(a.getColor()) && (ripe == a.getRipe()));
		 }
		return false;
		}
	}

## 4.getclass()方法

通过Class 对象，你可以查询Class对象的各种 信息：比如它的名字，它的基类，它所实现接 口的名字等。

	void PrintClassName(Object obj) {
		 System.out.println("The Object's class is " + obj.getClass().getName()); }

## 5.终结类和终结方法

主要特点：

- 被final修饰符修饰的类和方法；

- 终结类不能被继承（即不能有派生类）；

- 终结方法不能被当前类的子类重写；

# 三.抽象类和抽象方法

## 1.抽象类

抽象类的主要特点：

- 代表一个抽象概念的类;

- 没有具体实例对象的类，**不能使用new方法进行实例化**;

- 类前需加修饰符`abstract`;

- 可包含常规类能够包含的任何东西，例如构造方法，非抽象方法;

- 也可包含抽象方法，这种方法只有方法的声明， 而没有方法的实现;

抽象类声明的语法形式为:
	abstract class Employee{
	 . . .
	}

如果使用语法`new Employee()`将会发生错误（因为抽象类不能实例化）；

## 2.抽象方法

- 声明的语法形式为 public abstract  returnType methodName(...);

- 仅有方法头，而没有方法体和操作实现，具体实现由当前类的不同子类在它们各自 的类声明中完成 ；

- 抽象类可以包含抽象方法；

## 3.关于申明相关

- 一个抽象类的子类如果不是抽象类，则它**必须为父类中的所有抽象方法书写方法体**，即重写父类中的所有抽象方法；

- 只有抽象类才能具有抽象方法，即如果 一个类中含有抽象方法，则必须将这个 类声明为抽象类 ；

- 除了抽象方法，抽象类中还可以包括非 抽象方法；

# 二.java程序开发中用到的包和类

## 1.比较常用的类

	数据类型包裹类   --实现数据类型包裹类和基本数据类型的转换
	常量字符串类String
	变量字符串类StringBuffer
	数学类(Math)
	系统和运行时类System、Runtime
	类操作类（Class、ClassLoader）
	Date类
	Calendar类
	GregorianCalendar类
	StringTokenizer类

这些类，在实际操作中可以查询其提供的功能；在此不再赘述。

## 2.自定义包

自定义包的基本概念：

- 包是一组类的集合，利用包来管理类， 可实现类的共享与复用

- 同一包中的类在缺省情况下可以互相访问，通常把需要在一起工作的类放在一个包里；

- 在实际使用中，用户可以将自己的类组织成包结构。

关于自定义包的定义和使用：

	对自定义包的定义使用package语句；
	必须为Java源文件的第一条语句，前面只能有注释或空行；
	一个文件中最多只能有一条。

	如果其他人想使用定义的包，可以使用两种方法：
	1.使用import语句引入 import mypackage.*;
	2.不使用import语句，则需要使用全名：
	  mypackage.MyClass m = new mypackage.MyClass();
