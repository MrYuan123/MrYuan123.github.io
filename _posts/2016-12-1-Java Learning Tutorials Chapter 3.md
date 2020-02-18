---
layout:     post
title:      "Java Learning Tutorials Chapter 3"
subtitle:   " \"Hello World, Hello Blog\""
date:       2016-12-1 18：00
author:     "Leonard Yuan"
header-img: "img/home-bg-o.jpg"
catalog: true
tags:
    - Java

---

>java学习笔记。

---

# 一、接口和多态

## 1.接口

### A.接口的相关概念

- 接口是描述类的部分行为的一组操作（包括操 作名、参数类型和返回值类型），用于定义多个不相关类的共同行为；

- **接口的抽象程度比抽象类更进一步，其完全禁 止了所有的函数定义；**

- 也可以包含基本数据类型的数据成员，但它们 都默认为static和final；

### B.接口的相关语法
接口关键字用`interface`声明接口；接口的数据成员一定要赋初值，并此值不能再被更改。
接口中的方法必须是“抽象方法”，可以省略public和abstract等关键字。这种方法可以更加方便地实现不同常量共享，可以最大限度地利用动态绑定，隐藏实现细节。如定义一个关于保险的接口具体的代码如下：

	public interface Insurable{
		public int getNumber();
		public int getCoverageAmount();
		public double calculatePremium();
		public Date getExpiryDate();
	}

抽象类和接口之间拥有一定的相似之处，但是也有很大的不同。抽象类描述的是本质上相同的类之间的共同行为，定 义了一种继承关系；接口描述的是看上去不相关 的类之间的共同行为，定义了一种契约关系（类要实现接口。

### C.接口的实现

在实际的操作中，接口定义的操作必须通过类实现使用`implements`关键字来实现具体的操作，语法如下：

	public class 类名称 implements 接口名{
		具体的实现
	}

必须注意的点：

- 在定义的类中必须实现接口中定义的所有抽象方法；

- 对于来自接口的方法必须声明成public

- 一个类可以实现多个接口，而一个接口也可以被多个类实现，每个的实现方法各不一样。

在实际操作中，我们可以通过如下方法实现接口，首先先定义接口（此接口为交通工具基本操作接口。如下：

	public interface MovableObject {
		public boolean start();
		public void stop();
		public boolean turn(int degrees);
		public double fuelRemaining();
		public void changeSpeed(double kmPerHour);
	}

然后通过定义类来实现接口中的方法，如下：

	public class Plane implements MovableObject {

		public int seatCapacity;
		public Company owner;
		public Date lastRepairDate;

		//实现MovalbelObject接口的所有方法
		public boolean start() {  //启动飞机，成功则返回true  }
		public void stop() {  //停止 }
		public boolean turn(int degrees) { //转向，成功则返回true}
		public double fuelRemaining() {  //返回燃料剩余量 }
		public void changeSpeed(double kmPerHour)  {  //改变速度 }

		//plane类自己的方法：
		public Date getLastRepairDate() {   //...   }
		public double calculateWindResistance() {  //....}

	}

### D.多重继承

**java的设计以简单为导向，不允许一个类有多个父类。但一个类可以实现多个接口，通过这种机制可以实现多重继承。**

接口可以通过扩展的技术来派生出新的接口，原来的接口叫做`基本接口`或者`父接口`。派生出的类叫做`派生接口`或者`子接口`。（使用在继承类时使用的extends）

	interface 字接口 extends 父接口{
		//........
	}


## 2.塑型

### A.基本概念

	对于基本数据类型：
	相容类型之间存储容量低的自动向存储容量高的类型转换；
	如下：
	(int)871.34354;     // 结果为 871
	(char)65;           // 结果为‘A’

	对于引用变量：
	a.被塑型成更一般的类：
	Employee  emp;
	emp = new Manager();
	//将Manager类型的对象直接赋给Employee类的引用变量
	//系统会自动将Manage对象塑型为Employee类；

	b.塑型为对象所属类实现的接口类型:
	Insurable item = new Manager();

对于塑型后的对象，可以还原成原来的类型*方法如下：

	Employee  emp;
	Manager man;
	emp = new Manager();
	man = (Manager)emp;
	//将emp强制塑型为本来的类型

当一个类被塑型成其父类时它提供的方法会减少。如果塑型前后的类中都有相同的方法则从对象创建时所属类开始，沿类层次向上查找。

## 3.多态的概念

## 4.多态的应用

## 5.构造方法与多态

## 6.内部类
