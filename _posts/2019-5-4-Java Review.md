---
layout:     post
title:      "Java Review"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-5-4 14：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Interview
    - Java
---


# Java面试复习

## 数据类型和基础面试问题

- 在Java中设置了两种存储大数的方式，一种是`BigInteger`，另外一种是`BigDecimal`。如果不考虑存储空间的话，最好使用这两种存储方式，因为在商业计算中，它们的精度高

		BigDecimal BigDecimal(String s);
[大数操作讲解](https://www.cnblogs.com/javahr/p/8321683.html)
- 在Java中能够实现byte和String之间的转换，在转换的过程中要考虑编码的问题

		String string = "hello world";
		byte[] bytes = string.getBytes();
		String s = new String(bytes);
[byte与String的转换](https://www.cnblogs.com/keeplearnning/p/7003415.html)

- Java的int为32位的，如果被强制转换为byte，因为byte为8位，所以转换过程中会将前24位被省略
- Java中的++不是线程安全的，因为这个操作是由多个指令完成的，有可能会出现多个线程交叉的情况
- +=是一种能够进行强制类型转换的算术操作，如果执行的话，会将被加数转换成目的类型
- 因为浮点数不能被完全表示出来，所以不能用`==`来比较浮点数，一般通过差值来进行比较
- 无论是32或者64位Java虚拟机，int的长度都为32位
- JRE、JDK、JVM 及 JIT
	- JRE代表Java运行时（Java run-time），是运行Java应用所必须的
	- JDK代表Java开发工具（Java development kit），是Java程序的开发工具，如Java编译器，它也包含JRE
	- JVM代表Java虚拟机（Java virtual machine）
	- JIT代表即时编译（Just In Time compilation），当代码执行的次数超过一定的阈值时，会将 Java字节码转换为本地代码
- hashCode()和.equals()的关系：当使用equals()判断的对象，一定是拥有一样的hashcode
- finalize()：Java技术允许使用finalize()方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的，但是什么时候调用 finalize没有保证
-  ArrayList和LinkedList的区别
	- 一个是数组实现的，一个是双向链表实现的，因此各自因为不同数据结构的特性体现了不同的特性
- Java中的TreeMap是通过红黑树实现的
- HashSet内部是采用HashMap来实现的，在HashSet中只允许出现一个null的key
- 容器类一共分类两种
	- Collection
		- List
		- Set
	- Map
		- HashTable
		- HashMap
		- WeakHashMap
- 在Java中，DateFormat的所有实现，都是不安全的
- 重写与重载的区别
	- 重写：重写（override）是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。即外壳不变，核心重写
	- 重载：重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同
- Java中的基础数据类型：byte、short、int、long、float、double、char、boolean
- Java面向对象的特性
	- 封装
		- 就是将同一事物的特性与功能封装到一起
		- 隐藏细节，明确分工，减少耦合
	- 继承
		- 继承所表达的就是一种对象类之间的相交关系
		- 继承避免了对一般类和特殊类之间共同特征进行的重复描述。
	- 多态
		- 主要体现在`重载`和`重写`
		- 多态的实现方式：接口实现，继承父类重写方法，同一类中进行方法重载
		- 多态在虚拟机中是通过一种叫做动态绑定技术(dynamic binding)实现的，执行期间判断所引用对象的实际类型，根据实际类型调用对应的方法
- UML图
	- 静态图：用例图，类图，对象图，包图，构件图，部署图
	- 动态图：状态图，活动图，协作图，序列图
	- [相关链接](https://www.cnblogs.com/jiangds/p/6596595.html)

## 2. 热门面试题

- 线程：线程是操作系统能够进行运算调度的最小单位，它被包含在进程之中，是进程中的实际运作单位
- 线程和进程有什么区别：线程是进程的子集，一个进程可以有很多线程，每条线程并行执行不同的任务。不同的进程使用不同的内存空间，而所有的线程共享一片相同的内存空间
- Thread 类中的start()和run()方法有什么区别：start()方法被用来启动新创建的线程，而且start()内部调用了run()方法，这和直接调用run()方法的效果不一样。当你调用run()方法的时候，只会是在原来的线程中调用，没有新的线程启动，start()方法才会启动新线程
- String, StringBuilder, StringBuffer
	- String是不可变的，所以在操作的过程中都是创建一个新的String类型的新对象，StringBuffer、StringBuilder可以在原有对象的基础上进⾏操作
	- StringBuffer是线程安全的，StringBuilder是非线程安全的。但是StringBuilder的性能是优于StringBuffer
- String str="i"与 String str=new String("i")不一样：内存的分配⽅方式不不⼀一样。String str="i"的⽅方式，Java虚拟机会将其分配到常量量池中;⽽而 String str=new String("i")则会被分到堆内存中
- 字符串的反转可以通过StringBuilder或者StringBuffer的reverse()方法来实现
- 普通类和抽象类的区别
	- 普通类不能包含抽象方法，抽象类可以包含抽象⽅法
	- 抽象类不能直接实例化，普通类可以直接实例化
- 抽象类不能使用final来修饰，因为final修饰的类不能被继承
- BIO、NIO、AIO 有什什么区别??????
- 容器类一共分类两种
	- Collection
		- List
			- LinkedList   
			- ArrayList
			- Vector
				- Stack
		- Set
	- Map
		- HashTable
		- HashMap
		- WeakHashMap
- Java中Collection和Collections的区别
	- java.util.Collection是一个集合接口（集合类的一个顶级接口）。它提供了对集合对象进行基本操作的通用接口方法
	- Collections则是集合类的一个工具类/帮助类，其中提供了一系列静态方法，用于对集合中元素进行排序、搜索以及线程安全等各种操作
- HashMap散列图、Hashtable散列表是按“有利于随机查找的散列(hash)的顺序”。并非按输入顺序。遍历时只能全部输出，而没有顺序
- 如何决定使用HashMap还是TreeMap
	- 对于在 Map 中插⼊入、删除、定位⼀个元素这类操作，HashMap是最好的选择，因为相对⽽言 HashMap的插⼊入会更快，但如果你要对一个key集合进⾏有序的遍历，那TreeMap是更好的选择
-  HashSet底层使用HashMap来实现
-  ArrayList和LinkedList的区别是什么
	- 数据结构实现:ArrayList 是动态数组的数据结构实现，而 LinkedList 是双向链表的数据结构实现
	- 随机访问效率:ArrayList ⽐ LinkedList 在随机访问的时候效率要高，因为 LinkedList 是线性的数据存储⽅式，所以需要移动指针从前往后依次查找
	- 增加和删除效率:在⾮⾸首尾的增加和删除操作，LinkedList要比ArrayList效率要高，因为 ArrayList增删操作要影响数组内的其他数据的下标
- ArrayList和Vector(动态数组)的区别
	- 线程安全:Vector使⽤用了Synchronized来实现线程同步，是线程安全的，⽽ArrayList是⾮线程安全的
	- 性能: ArrayList在性能⽅面要优于Vector
	- 扩容: ArrayList和Vector都会根据实际的需要动态的调整容量，只不过在Vector扩容每次会增加 1倍， ⽽ArrayList只会增加50%
- Array和ArrayList的区别
	- Array 可以存储基本数据类型和对象，ArrayList 只能存储对象
	- Array 是指定固定⼤小的，⽽而 ArrayList ⼤小是⾃动扩展的
- Java中集合类的线程安全：Vector、Hashtable、Stack 都是线程安全的，⽽而像 HashMap 则是⾮非线程安全的，不过在JDK1.5之后随着Java.util.concurrent并发包的出现，它们也有了自⼰对应的线程安全类，⽐如HashMap对应的线程安全类就是ConcurrentHashMap
- 迭代器Iterator
	- 提供遍历任何Collection的接口

			List<String> list = new ArrayList<>();
		 	Iterator<String> it = list. iterator();
			while(it. hasNext()){
	  			String obj = it. next();
	   			System. out. println(obj);
	   		}
- Iterator和ListIterator的区别
	- Iterator可以遍历Set和List集合，⽽ListIterator只能遍历List
	- Iterator只能单向遍历，⽽ListIterator可以双向遍历
	- ListIterator从 Iterator 接⼝继承，然后添加了了⼀些额外的功能，比如添加⼀个元素、替换一个元素、获取前⾯或后⾯元素的索引位置
-  可以使用Collections. unmodifiableCollection(Collection c)来创建一个只读集合
-  守护线程
	- 守护线程是运行在后台的一种特殊进程。它独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。在`Java中垃圾回收线程`就是特殊的守护线程
- 反射
	- 反射是在运⾏行状态中，对于任意一个类，都能够知道这个类的所有属性和⽅方法;对于任意一个对象，都能够调⽤它的任意⼀个⽅方法和属性;这种动态获取的信息以及动态调用对象的⽅法的功能称为Java 语言的反射机制
- Java序列化
	- 对象序列化机制（object serialization）是Java语言内建的一种对象持久化方式，通过对象序列化，可以把对象的状态保存为字节数组，并且可以在有需要的时候将这个字节数组通过反序列化的方式再转换成对象。对象序列化可以很容易的在JVM中的活动对象和字节数组（流）之间进行转换
- Java 序列列化是为了了保存各种对象在内存中的状态，并且可以把保存的对象状态再读出来。比如将对象进行文件写入，然后日后再读出来
	- 比如将session进行序列化
	- 想把的内存中的对象状态保存到一个⽂文件中或者数据库中时候
- Java中的动态代理
- 对象拷贝
	- 实现对象克隆的方式
		- 实现Cloneable接口并重写Object类中的clone()方法
		- 实现Serializable接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆
	- 深克隆和浅克隆的区别
		- 浅克隆：当对象被复制时只复制它本身和其中包含的值类型的成员变量，而引⽤类型的成员对象并没有复制
		- 深克隆: 除了了对象本身被复制外，对象所包含的所有成员变量也将复制
- Java中的异常主要分为：`Error`和`Exception`
- Java中的ArrayList，LinkedList都是线程不安全的

## Java多线程

- 基本线程类指的是：继承Thread类，实现Runnable接口，Callable接口
- 线程的五个状态：创建，就绪，运行，阻塞，终止。只有在就绪状态的时候，才有可能转成
- 一共有三种实现多线程的方式
	- 继承Thread类
	- 实现Runnable接口
	- 实现Callable接口（与Future，线程池结合使用）
- 多线程中几个重要的函数
	- sleep()：让当前执行的线程休眠
	- join()：等待该进程终止
	- yield():暂停当前正在执行的线程对象，并执行其他线程（但无法保证一定达到了让步的目的）
- 线程锁
	- 通过加锁，使得在同一时刻只允许一个线程对某个对象进行操作
	- `synchronized`关键字被用于线程间同步的实现
- 线程的run()和start()有什么区别
	- start()方法用于启动线程，run()方法用于执⾏线程的运⾏时代码。run()可以重复调⽤，⽽ start()只能调⽤⼀次
- Java程序中保证多线程的运⾏安全
	- 使⽤安全类，⽐如 Java. util. concurrent下的类
	- 使⽤⾃动锁synchronized
	- 使⽤手动锁Lock
- synchronized和volatile的区别
	- volatile 是变量修饰符;synchronized 是修饰类、⽅方法、代码段
	- volatile仅能实现变量的修改可⻅性，不能保证原子性;⽽synchronized则可以保证变量的修改可⻅性和原子性
	- volatile不会造成线程的阻塞;synchronized可能会造成线程的阻塞
- synchronized和Lock的区别
	- synchronized可以给类、方法、代码块加锁;⽽lock只能给代码块加锁
	- synchronized不需要手动获取锁和释放锁，使⽤简单，发⽣异常会自动释放锁，不会造成死锁;⽽而 lock需要自⼰己加锁和释放锁，如果使用不当没有unLock()去释放锁就会造成死锁
	- 通过Lock可以知道有没有成功获取锁，⽽synchronized却⽆法办到
- sleep和wait的区别
	- sleep(): 是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复，调用sleep不会释放对象锁。sleep()使当前线程进入停滞状态（阻塞当前线程），让出CUP的使用、目的是不让当前线程独自霸占该进程所获的CPU资源，以留一定时间给其他线程执行的机会
	- wait()方法是Object类里的方法；当一个线程执行到wait()方法时，它就进入到一个和该对象相关的等待池中，同时失去（释放）了对象的机锁
- 线程创建的相关知识：[Java多线程的创建方式](https://www.cnblogs.com/felixzh/p/6036074.html)

## Java Web

- JSP的4个作用域
	- page: 代表与一个⻚面相关的对象和属性
	- request:
	- session:
	- application:
- session和cookie的区别
	- 存储位置不同: session存储在服务器端;cookie存储在浏览器端
	- 安全性不同:cookie安全性一般，在浏览器存储，可以被伪造和修改
	- 容量和个数限制:cookie有容量限制，每个站点下的cookie也有个数限制
	- 存储的多样性:session可以存储在Redis中、数据库中、应⽤程序中;⽽cookie只能存储在浏览器中
- 防止SQL注入的方式
	- 使⽤预处理`PreparedStatement`
	- 使用正则表达式过滤掉字符中的特殊字符
- XSS攻击
	- 跨站脚本攻击，攻击者往Web⻚里插⼊入恶意的脚本代码(css 代码、Javascript 代码等)，当⽤户浏览该⻚面时，嵌⼊入其中的脚本代码会被执行，从⽽达到恶意攻击⽤户的目的，如盗取⽤户cookie、破坏⻚面结构、重定向到其他⽹站等
- try-catch-finally结构中，无论catch中返回与否，finally里面的必须执行。即使是catch中 return了，catch中的return会等finally中的代码执行完之后，才会执⾏
- http中的301和302: 301对搜索引擎优化(SEO)更加有利;302有被提示为网络拦截的⻛险
- tcp为什么是三次握手，而不是两次握手？
	- 为了实现可靠数据传输， TCP 协议的通信双方， 都必须维护一个序列号， 以标识发送出去的数据包中， 哪些是已经被对方收到的。 三次握手的过程即是通信双方相互告知序列号起始值， 并确认对方已经收到了序列号起始值的必经步骤
	- 如果只是两次握手， 至多只有连接发起方的起始序列号能被确认， 另一方选择的序列号则得不到确认
	- 相关链接： [三次握手而不是两次握手的原因？](https://blog.csdn.net/lengxiao1993/article/details/82771768)
- tcp粘包？？
- GET和POST的区别
	- 区别：[post和get方式的区别](https://www.cnblogs.com/logsharing/p/8448446.html)

**Spring MVC**

- AOP
	- 面向切面的编程，通过预编译⽅式和运⾏期动态代理实现程序功能的统⼀维护的⼀种技术
	- [AOP的原理](https://blog.csdn.net/q982151756/article/details/80513340)
- Spring MVC组件
	- 前置控制器DispatcherServlet
	- 映射控制器HandlerMapping
	- 处理器Controller
	- 模型和视图ModelAndView
	- 视图解析器ViewResolver
- @Autowired
	- 它可以对类成员变量、方法及构造函数进⾏行标注，完成自动装配的⼯作，通过@Autowired的使⽤用
来消除set/get方法
- hibernate的查询⽅式
	- hql
	- 原⽣SQL
	- 条件查询Criteria
- Hibernate中每个实体类必须提供一个无参构造函数，否则会抛出异常


## JVM

**Java程序的编译和执行过程**

- 了解Java程序的编译和执行过程对理解JVM的回收过程很有用
- 相关链接：[Java程序编译和运行的过程](https://www.cnblogs.com/qiumingcheng/p/5398610.html)
- JVM组成部分
	- 类加载器(ClassLoader)
	- 运行时数据区(Runtime Data Area)
	- 执⾏引擎(Execution Engine)
	- 本地库接⼝(Native Interface)

**Java对象在JVM内存中的管理（对理解垃圾回收机制很重要）**

- JVM内存分为堆、栈和方法区三个区域
- `堆`存储的信息：堆空间用于存储使用new关键字所创建的对象（延伸到对对象的垃圾回收）
- `栈`存储信息：栈空间用于存储程序运行时在方法中声明的所有局部变量。局部变量被定义在方法中，方法被调用时，存在栈中，方法调用结束后，从栈中清除。成员变量是放在堆中的，对象被收回的时候，成员变量失效
- `方法区`存储信息：方法区用于存放类的信息，Java程序运行时，首先会通过类装载器载入文件的字节码信息，经过解析后将其装入方法区。类的各种信息（包括方法）都在方法区存储
- 类和对象在内存空间中的关系
	- 当类的信息被加载到方法区时，除了类的类型信息以外，同时类的方法定义也被加载到方法区
	- 类在实例化对象时，多个对象会拥有各自在堆中的空间，但所有实例对象是共用在方法区中的一份方法定义的

**JVM的内存回收机制**

- 相关链接：[JVM的内存回收机制](https://www.cnblogs.com/aspirant/p/8662690.html)
- Java中的引用类型
	- 强引用：发⽣gc的时候不会被回收
	- 软引用：有⽤但不不是必须的对象，在发⽣内存溢出之前会被回收
	- 弱引用:有⽤但不不是必须的对象，在下⼀次GC时会被回收
	- 虚引用(幽灵引用/幻影引用):⽆法通过虚引用获得对象，⽤PhantomReference实现虚引⽤，虚引⽤的用途是在gc时返回一个通知
-  Java的内存结构：
	- 程序计数器
	- 虚拟机栈
	- 本地方法栈
	- 堆区
	- 方法区
	- 其中`程序计数器`、`虚拟机栈`、`本地方法栈`3个区域随线程而生、随线程而灭，因此这几个区域的内存分配和回收都具备确定性，就不需要过多考虑回收的问题，因为方法结束或者线程结束时，内存自然就跟随着回收了。而Java堆区和方法区则不一样，这部分内存的分配和回收是动态的，正是垃圾收集器所需关注的部分
- 判断对象能否被收回的方式
	- 引用计数算法（就是通过对堆中的对象都采用一个引用计数，当计数为0的情况下表示可以被收回）
	- 可达性分析算法(就是从某个回收节点开始，进行类似图的遍历，当所有引用点)
- 实际上在对象被正式回收的过程之前，还有两次的标记过程：
	- 第一次标记：如果对象在进行可达性分析后发现没有与GC Roots相连接的引用链，那它将会被第一次标记
	- 第一次标记后接着会进行一次筛选，筛选的条件是此对象是否有必要执行finalize()方法。在finalize()方法中没有重新与引用链建立关联关系的，将被进行第二次标记
	- 两次标记之后，对象将会被正式收回
- 方法区如何判断是否需要回收`无用的类`：
	- 该类所有的实例都已经被回收，也就是Java堆中不存在该类的任何实例
	- 加载该类的ClassLoader已经被回收
	- 该类对应的java.lang.Class对象没有在任何地方被引用，无法在任何地方通过反射访问该类的方法
- 常用的垃圾收集算法
	- 标记-清除算法（Mark-Sweep）：从GC ROOT开始扫描，对存活的对象进行标记，标记结束后清除没有被标记的对象（高效，但是容易造成内存碎片）
	- 标记-整理算法(Mark-compact)：就是将标记后的整体向左端移动，并更新对应的指针
	- 分代回收算法：根据对象存活的生命周期将内存划分为若干个不同的区域，一般分为老年代和新生代，在堆区之外还有一个持久区
-  GC触发的类型
	-  Scavenge GC：就是当新的对象创建，发现申请空间失败的时候，会对年轻代的分区进行扫描清理
	-  Full GC：Full GC因为需要对整个堆进行回收，所以比Scavenge GC要慢，因此应该尽可能减少Full GC的次数

**Java的类加载机制**

- 类加载的相关链接：[Java 类加载机制](http://www.cnblogs.com/aspirant/p/7200523.html)
- 类加载器除了用于加载类外，还可用于确定类在Java虚拟机中的唯一性。如果两个类不是被同一个类加载器加载，那么它们一定是不同的
- 类加载中的双亲委派机制：指每次收到类加载请求时，先将请求委派给父类加载器完成。如果父类加载器无法完成这个加载，子类尝试自己加载
- 类加载的过程主要分为7步：加载，验证，准备，解析，初始化，使用，卸载

## Java设计模式

- 单例模式
	- 就是实例只创建一次，即整个应用中只有一个该类的实例存在
	- 如果考虑单例模式多线程下的安全性的话：[单例模式的线程安全性](https://www.cnblogs.com/hupp/p/4487521.html)
- 工厂模式
	- 定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行
- 建造者模式
	- 使用多个简单的对象一步一步构建成一个复杂的对象。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式

类加载分为以下 5 个步骤:

加载:根据查找路路径找到相应的 class ⽂文件然后导⼊入;

检查:检查加载的 class ⽂文件的正确性;

准备:给类中的静态变量量分配内存空间; 解析:虚拟机将常量量池中的符号引⽤用替换成直接引⽤用的过程。符号引⽤用就理理解为⼀一个标示，⽽而在直接引⽤用直 接指向内存中的地址;

初始化:对静态变量量和静态代码块执⾏行行初始化⼯工作。


## Java线程池
- 相关链接：[Java线程池](https://www.cnblogs.com/aspirant/p/6920418.html)
- 相关链接：[线程池的执行过程](https://mp.weixin.qq.com/s/mh_1fGYEYKCC8Zqv8sMsMQ)
- 定义：java.util.concurrent.Executors提供了一个 java.util.concurrent.Executor接口的实现用于创建线程池
- 基本组成部分：
	- 线程池管理器（ThreadPool）：用于创建并管理线程池，包括 创建线程池，销毁线程池，添加新任务
	- 工作线程（PoolWorker）：线程池中线程，在没有任务时处于等待状态，可以循环的执行任务
	- 任务接口（Task）：每个任务必须实现的接口，以供工作线程调度任务的执行，它主要规定了任务的入口，任务执行完后的收尾工作，任务的执行状态等
	- 任务队列（taskQueue）：用于存放没有处理的任务。提供一种缓冲机制
- 线程池的作用：线程池作用就是限制系统中执行线程的数量
- 使用线程池的原因：
	- 减少了创建和销毁线程的次数，每个工作线程都可以被重复利用，可执行多个任务
	- 可以根据系统的承受能力，调整线程池中工作线线程的数目
- 有时间配置一个线程池的时候会比较复杂，那么可以使用其中的工厂类，来生成一下常见的线程池
	- newSingleThreadExecutor：创建一个单线程的线程池。这个线程池只有一个线程在工作，也就是相当于单线程串行执行所有任务。如果这个唯一的线程因为异常结束，那么会有一个新的线程来替代它。此线程池保证所有任务的执行顺序按照任务的提交顺序执行
	- newFixedThreadPool：创建固定大小的线程池。每次提交一个任务就创建一个线程，直到线程达到线程池的最大大小。线程池的大小一旦达到最大值就会保持不变，如果某个线程因为执行异常而结束，那么线程池会补充一个新线程。在某个线程被显式地关闭之前，池中的线程将一直存在
	- newCachedThreadPool：创建一个可缓存的线程池。如果线程池的大小超过了处理任务所需要的线程，那么就会回收部分空闲（60秒不执行任务）的线程，当任务数增加时，此线程池又可以智能的添加新线程来处理任务。此线程池不会对线程池大小做限制
	- newScheduledThreadPool： 创建一个大小无限的线程池
- 代码样例：

		Thread t1=new MyThread();
		Thread t2=new MyThread();
		Thread t3=new MyThread();
		ExecutorService pool=Executors.newSingleThreadExecutor();
		// ExecutorService pool=Executors.newCachedThreadPool();
		// ScheduledThreadPoolExecutor exec =new ScheduledThreadPoolExecutor(1);
		pool.execute(t1);
		pool.execute(t2);
		pool.execute(t3);

- 如果不用工厂类来完成线程池的构建的话，一般会使用`ThreadPoolExecutor`来进行线程池的定义
- 线程池定义中的参数：
	- corePoolSize：池中所保存的线程数，包括空闲线程
	- maximumPoolSize：池中允许的最大线程数
	- keepAliveTime：当线程数大于核心时，此为终止前多余的空闲线程等待新任务的最长时间
	- unit：keepAliveTime 参数的时间单位
	- workQueue：执行前用于保持任务的队列。此队列仅保持由 execute方法提交的 Runnable任务
	- threadFactory：执行程序创建新线程时使用的工厂
	- handler：由于超出线程范围和队列容量而使执行被阻塞时所使用的处理程序
- maximumPoolSize(最大线程数) = corePoolSize(核心线程数) + noCorePoolSize(非核心线程数)
- 线程池的执行过程：
![](1.png)
- shutdown()有什么功能:
	- 阻止新来的任务提交，对已经提交了的任务不会产生任何影响。当再将执行execute提交任务时，如果测试到状态不为RUNNING，则抛出rejectedExecution，从而达到阻止新任务提交的目的
- shutdownNow()的功能：
	- 阻止新来的任务提交，同时会中断当前正在运行的线程，即workers中的线程
- 线程池定义中有几种queue的方式：
	- 直接提交
	- 无界队列
	- 有界队列
	- （重点在于无界队列和有界队列的）
