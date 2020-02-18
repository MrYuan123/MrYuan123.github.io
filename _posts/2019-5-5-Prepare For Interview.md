---
layout:     post
title:      "Prepare For Interview"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-5-5 14：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Interview
    - Computer Science
---

# 面试知识汇总

## 状态码系列

### 1. 1XX：通知
1XX系列状态码仅在与http服务器沟通时使用

- 100：继续（客户端应当继续发送请求）
- 101：转换协议（在发送完这个响应最后的空行后，服务器将会切换到在Upgrade 消息头中定义的那些协议）

### 2. 2XX：成功
- 200：请求成功
- 202：请求被接受，但处理尚未完成 处理方式：阻塞等待
- 204：服务端已经实现了请求，但是没有返回新的信息。处理方式，丢弃

### 3. 3XX：重定向
- 300：该状态码不被HTTP/1.0的应用程序直接使用， 只是作为3XX类型回应的默认解释。存在多个可用的被请求资源。 处理方式：若程序中能够处理，则进行进一步处理，如果程序中不能处理，则丢弃
- 301：请求到的资源都会分配一个永久的URL，这样就可以在将来通过该URL来访问此资源 处理方式：重定向到分配的URL
- 302：请求到的资源在一个不同的URL处临时保存 处理方式：重定向到临时的URL
- 304：自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容
- 301和302的区别：302重定向只是`暂时`的重定向，搜索引擎会抓取新的内容而保留旧的地址，因为服务器返回302，所以，搜索搜索引擎认为新的网址是暂时的。而301重定向是`永久`的重定向，搜索引擎在抓取新的内容的同时也将旧的网址替换为了重定向之后的网址。

### 4. 4XX：客户端错误
- 401：请求要求身份验证。 对于需要登录的网页，服务器可能返回此响应
- 403：服务器已经理解请求，但是拒绝执行它
- 404：请求失败，请求所希望得到的资源未被在服务器上发现
- 405：客户端试图使用一个本资源不支持的HTTP方法
- 406：当客户端对表示有太多要求，以至于服务器无法提供满足要求的表示，服务器可以发送这个响应代码
- 409：Conflict。你请求的操作会导致服务器的资源处于一种不可能或不一致的状态

### 5. 5XX： 服务端错误
- 500：代表了服务器在处理请求的过程中有错误或者异常状态发生
- 503：HTTP服务器正常，只是下层web服务服务不能正常工作。最可能的原因是资源不足：服务器突然收到太多请求，以至于无法全部处理

## Redis
- 一种key-value存储系统，通常被称为数据结构服务器，因为值（value）可以是：
	- 字符串(String)
		- SET(), GET(),
	- 哈希(Hash)
		- HMSET(), HGETALL(), HDEL(), HMGET()
	- 列表(list)
		- LPUSH(), LPOP(), LRANGE()
	- 集合(sets)
		- SADD(), SPOP(), SMEMBERS()
	- 有序集合(sorted sets)
		- Redis 有序集合和集合一样也是string类型元素的集合,且不允许重复的成员。不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。有序集合的成员是唯一的,但分数(score)却可以重复，集合时通过哈希表来实现的
		- ZADD(), ZRANGE(), ZCOUNT()
- 在Redis中可以进行数据的备份操作，即使用`save`命令就可以在redis目录中创建`.rdb`文件，之后可以使用config命令进行恢复
-  Redis使用`MULTI`进入事务模式，就是在没有进行`EXEC`命令之前，输入的指令不会执行，当EXEC 被调用时，所有的命令才会被一次性执行
-  执行 EXEC 后：所有的命令都会被执行，甚至是那些错误的命令。换句话说，就算有命令失败，队列中的其他命令也会被执行
-  Redis命令在事务中可能会执行失败，但是Redis事务`不会回滚`，而是继续会执行余下的命令
-  对Redis的分布式的使用，在Redis中有分布式锁，使用分布式锁能够将系统设计成分布式的模式
-  Redis的安装：[Redis的安装](http://www.runoob.com/redis/redis-install.html)

## 后端开发常用Linux命令

- netstat：显示路由表、实际的网络连接以及每一个网络接口设备的状态信息
- ipcs：显示所有的ipc设施，ipc（进程间通信）
- tail -f catalina.out：查看日志
- rm -rf 文件名：删除文件
- touch 文件名：创建文件
- cat：查看文件命令，一次性查看所有内容
- ssh：用户通过SSH客户端可以连接到运行了SSH服务器的远程机器上，传输的数据是加密和压缩的
- scp：在linux下远程拷贝文件的命令
- ps：查看进程运行状态
- file：获取文件的基本信息
- tar: 对文件进行打包
- chmod: 改变文件的权限
- mv: 既可以用于重命名，也可以用于move

## 最重要的几个排序算法

- 参考网页：[几种排序的实现方法](https://www.cnblogs.com/onepixel/articles/7674659.html)
- 快速排序(就是将一个数组，以某个数字为分界线，大于它的放在右边，小于它的，放在左边，最后完成排序)

			class Solution {
			    public void sort(int[] array, int lo, int ro){
			        if(lo>=ro)
			            return array;
			        int index = parition(array, lo, ro);
			        sort(array, lo, index);
			        sort(array, index + 1, ro);
			    }

			    public int parition(int[] array, lo, ro){
			        int key = array[lo];
			        while(lo < ro){
			            while(array[ro] > key &&lo < ro)
			                ro --;
			            array[lo] = array[ro];

			            while(array[lo] < key && lo < ro)
			                lo ++;
			            array[ro] = array[lo];
			        }
			        array[ro] = key;
			        return ro;
			    }
			}

- 归并排序（使用的是递归的方式，首先将数组分为两个部分，对左右两个部门分别进行排序，最后再合并到一块，所以分为divide和merge两个部分）
- 冒泡排序最简单，不看了
- 选择排序，就是每次选择队列中的最小值，放在对应的位置，一直到把所有的队列中元素遍历完

		class Solution {
		    public int[] sort(int[] array){
		        int minIndex;
		        for(int m = 0; m < array.length - 1; m++){
		            minIndex = m;
		            for (int n = 0; n < array.length; n++){
		                if(array[n] < array[minIndex])
		                    minIndex = n;
		            }
		            int temp = array[n];
		            array[m] = array[minIndex];
		            array[minIndex] = temp;
		        }
		        return array;
		    }
		}

- 插入排序：很简单，就是每次为新的元素寻找位置，然后将该元素插到已经排好的队列中去
- 桶排序：就是将元素按分的组添加进去，然后对桶内的元素进行排序，最后将不为空的桶相互连接起来，获得最终的结果
- 希尔排序

## 可能会考的算法题

### 1. 使用两个栈实现一个队列（232）
- 思路就是两个栈里面的元素相互导，设置两个栈sin和sout分别表示入队列和出队列，只有在sout为空的情况下，就将sin中的元素出栈入栈，倒转push进去，那么此时sout出栈的第一个元素就是队列的第一个元素
- 试题地址：[Leetcode地址](https://leetcode.com/problems/implement-queue-using-stacks/)

### 2. 一个队列实现一个栈（225）
- 就是每次在push的时候就进行队列中的元素重新从队头挪到队尾，使得保证每次pop()的时候都是最后进去的元素
- 试题地址：[Leetcode地址](https://leetcode.com/problems/implement-stack-using-queues/)

### 3. 36进制加法
- 这个关键就是进位问题的处理，通过一个循环，当进位，加数有任意一个不为空的时候，就进行加法操作，然后保留进位

### 4. z字型遍历
- Leetcode原题：[Leetcode Z字型遍历](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

### 5. 将算术问题转换成图的问题
-  Leetcode原题：[Leetcode 279.Perfect Square](https://leetcode.com/problems/perfect-squares/)

### 6. 数组中第k大元素
- 最简单方法，优先队列

		class Solution {
		    public int findKthLargest(int[] nums, int k) {
		        PriorityQueue<Integer> result = new PriorityQueue<Integer>();
		        for(Integer m: nums){
		            result.offer(m);
		            if(result.size() > k)
		                result.poll();
		        }
		        return result.peek();
		    }
		}
- 使用快速排序的思路来解这道题

		class Solution {
		    public int findKthLargest(int[] nums, int k) {
		        return parition(nums, 0, nums.length - 1, k);
		    }

		    public int parition(int[] nums, int start, int end, int k){
		        int index = backTrack(nums, start, end);
		        if(index + 1 == k)
		            return nums[index];
		        else if(index + 1 > k)
		            return parition(nums, start, index - 1, k);
		        else{
		            return parition(nums, index + 1, end, k - index + 1);
		        }
		    }
		    public int backTrack(int[] nums, int start, int end){
		        int key = nums[start];
		        while(start < end){
		            while(nums[end] > key && start < end)
		                end--;
		            nums[start] = nums[end];

		            while(nums[start] < key && start < end)
		                start ++;
		            nums[end] = nums[start];
		        }
		        nums[end] = key;
		        return end;
		    }
		}

## 可能的面试题

### 计算机网络相关
- TCP和UDP有什么区别？
	- TCP协议是有连接的，有连接的意思是开始传输实际数据之前TCP的客户端和服务器端必须通过三次握手建立连接，会话结束之后也要结束连接。而UDP是无连接的 	- TCP协议保证数据按序发送，按序到达，提供超时重传来保证可靠性，但是UDP不保证按序到达，甚至不保证到达，只是努力交付，即便是按序发送的序列，也不保证按序送到
	- TCP协议所需资源多，TCP首部需20个字节（不算可选项），UDP首部字段只需8个字节
	- TCP有流量控制和拥塞控制，UDP没有，网络拥堵不会影响发送端的发送速率
	- TCP是一对一的连接，而UDP则可以支持一对一，多对多，一对多的通信
	- TCP面向的是字节流的服务，UDP面向的是报文的服务
- TCP为啥是可靠的
	- TCP在传输过程中，通信双方按照协议进行通信；将数据截断为合理的长度；超时重发；首部校验，若发现有改动则抛弃该包；通过可变大小的窗口协议进行流量控制
 	- 针对乱序：在三次握手时，序列号被初始化，传输过程中将继续使用这个序列号，每传送一个包，序列号进行加1；TCP也会进行重新排序
	- 针对丢包：收到一个数据包过后，会用ACK应答码进行确认，发送方可以针对未确认的包进行重传
	- 针对重复：若已收到过该序列号的包，则丢弃
- http和https的区别
	- http协议的数据是未加密的，明文传输的，因此在传输的过程中会出现安全问题。HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，要比http协议安全，可防止数据在传输过程中不被窃取、改变，确保数据的完整性
- http请求过程
	- 相关网页：[http请求的过程](https://www.cnblogs.com/xuzekun/p/7527736.html)
	- http请求的具体过程
		- 对网址先进行域名解析，获取对应的IP地址（这个是逐层去找的）
		- 根据IP地址，找到对应的服务器，三次握手
		- 服务器响应HTTP请求，浏览器得到html代码
		- 浏览器解析html代码，并请求html中需要的资源
		- 浏览器对网页进行渲染
- https的加密过程
	- 具体过程的解释网页：[https通过SSL加密的过程](https://www.cnblogs.com/xiohao/p/9054355.html)
	- 客户端发出请求获得CA证书和加密相关信息，通过非对称密钥机制保证双方身份认证，并完成建立连接，在实际数据通信时通过对称密钥机制保障数据安全性
	- 对称加密：两边密钥一致；非对称加密：加密的密钥公开，解密的密钥是保密的
- TCP协议的三次握手
	- 见计算机网络复习
- TCP协议的四次挥手
	- 见计算机网络复习
- TCP拥塞控制机制
	- 见计算机网络复习
- TCP协议如何进行流量控制的
- ARP是什么？ARP内部如何实现？
- HTTP、TCP、IP三层协议中，接收端如何判断已接受完对端发送来的数据
	- HTTP协议的服务端响应报文里有Content-Length字段，明确了报文的长度。客户端应该是通过这个来判断的(另外个人觉得状态码也是传输的依据)
	- TCP协议里接收方要回传确认号。如果双方各自向对方请求下一个数据包，却没有响应对方的请求，那么说明数据传完了。有时数据发送方如果发送完毕，会发出中断连接请求。对方也就知道已经发送完毕了
	- IP协议是无连接协议，不会考虑对方是否“发送完毕”。如果IP数据报被分片发送，那么只有最后一个分片的“还有分片（M）”flag置为0，之前的分片相应flag都置为1

### 计算机组成原理与操作系统
- 软硬中断的差别
	- 硬中断是由外部事件引起的因此具有随机性和突发性；软中断是执行中断指令产生的，无面外部施加中断请求信号，因此中断的发生不是随机的而是由程序安排好的
	- 硬中断的中断响应周期，CPU需要发中断回合信号（NMI不需要）；软中断的中断响应周期，CPU不需发中断回合信号
	- 硬中断的中断号是由中断控制器提供的（NMI硬中断中断号系统指定为02H）；软中断的中断号由指令直接给出，无需使用中断控制器
	- 硬中断是可屏蔽的（NMI硬中断不可屏蔽）；软中断不可屏蔽
- 并发和并行的区别
	- 并发：处理器同时处理多个任务，实际同一时刻只有一个任务在执行
	- 并行：多核多处理器同时处理多个任务
- 线程与进程的区别与联系
	- 相关地址：[进程与线程的区别](https://blog.csdn.net/kuangsonghan/article/details/80674777)
	- 进程是资源的分配和调度的一个独立单元，而线程是CPU调度的基本单元
	- 同一个进程中可以包括多个线程，并且线程共享整个进程的资源（寄存器、堆栈、上下文），一个进行至少包括一个线程
	- 进程结束后它拥有的所有线程都将销毁，而线程的结束不会影响同个进程中的其他线程的结束
	- 线程是轻两级的进程，它的创建和销毁所需要的时间比进程小很多，所有操作系统中的执行功能都是创建线程去完成的
	- 线程中执行时一般都要进行同步和互斥，因为他们共享同一进程的所有资源。系统在运行的时候会为每个进程分配不同的内存空间；而对线程而言，除了CPU外，系统不会为线程分配内存（线程所使用的资源来自其所属进程的资源），线程组之间只能共享资源
	- 线程有自己的私有属性TCB，线程id，寄存器、硬件上下文，而进程也有自己的私有属性进程控制块PCB，这些私有属性是不被共享的，用来标示一个进程或一个线程的标志

### HashMap相关
- HashMap不安全的原因
	- HashMap为什么不安全的原因：[HashMap不安全的原因](https://www.jianshu.com/p/e2f75c8cce01), HashMap使用的是桶索引和链表来完成哈希冲突的解决的，但是多线程中这种方法有问题
	- put的时候导致的多线程数据不一致，类似于a刚刚获得了桶的链表地址，但是cpu调度转交给了别的线程，别的线程b成功将具有相同哈希值的数据放了进去，那么当此时a如果再去继续完成操作的话，就会出现数据不一致的情况
	- HashMap的get操作可能因为resize而引起死循环（cpu100%）。就是两个线程同时进行resize操作，就会造成死循环
- `HashMap`使用的是数组（桶）和链表来实现的，（Java8中还用到了红黑树）`不同的key可能具有相同的hashCode`，这时候就出现哈希冲突了，也叫做哈希碰撞，为了解决哈希冲突，HashMap采用了链地址方法的方法，是的一个桶里面链接多个数值
![](/img/in_post/base_knowledge.images/1.png)
- `HashTable`和`HashMap`几乎是相同的，主要区别是线程安全性和速度。HashTable容器使用`synchronized`来保证线程安全，但在线程竞争激烈的情况下HashTable的效率非常低下。就是在其他线程在进行操作的时候，其他线程都得等着
- `ConcurrentHashMap`使用`锁分段技术`。首先将数据分成一段一段地存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据的时候，其他段的数据也能被其他线程访问
- rehash：在HashMap进行扩容的时候，需要对里面的元素进行rehash，这个过程是需要重新计算hash值的

## 琐碎及其他

- 什么是浏览器缓存：
	- 浏览器缓存就是把一个已经请求过的Web资源（如html页面，图片，js，数据等）拷贝一份副本储存在浏览器中。缓存会根据进来的请求保存输出内容的副本。当下一个请求来到的时候，如果是相同的URL，缓存会根据缓存机制决定是直接使用副本响应访问请求，还是向源服务器再次发送请求
- 消息队列
	- 消息队列实际上是`操作系统`在`内核`为我们创建的一个队列，通过这个队列的标识符key,每一个进程都可以打开这个队列，每个进程都可以通过这个队列向这个队列中插入一个结点或者获取一个结点来完成不同进程间的通信
- 并发与并行的区别
	- 并发的实质是一个物理CPU(也可以多个物理CPU) 在若干道程序之间多路复用，并发性是对有限物理资源强制行使多用户共享以提高效率。 并行性指两个或两个以上事件或活动在同一时刻发生。在多道程序环境下，并行性使多个程序同一时刻可在不同CPU上同时执行
- 操作系统的中断原理
	- 相关网页：[操作系统的中断原理](https://www.jianshu.com/p/4efd858c6520)
- Scrapy主要组件
	- 引擎
	- 调度器（URL的优先队列）
	- 下载器
	- 爬虫（相当于解析器）
	- 项目管道（对提取的实体进行持久化，有效性验证，数据清洗的）
	- 下载器中间件（处理Scrapy引擎与下载器之间的请求及响应）
	- 爬虫中间件（介于Scrapy引擎和爬虫之间的框架，主要工作是处理蜘蛛的响应输入和请求输出）
	- 调度中间件（介于Scrapy引擎和调度之间的中间件）
	- Scrapy主要介绍：[Scrapy简介](https://www.cnblogs.com/kongzhagen/p/6549053.html)
![](/img/in_post/base_knowledge.images/2.png)
- 红黑树
	- 一种特殊的自适应平衡二叉树
	- 每个节点或者是黑色，或者是红色
	- 根节点是黑色
	- 每个叶子节点（NIL）是黑色
	- 如果一个节点是红色的，则它的子节点必须是黑色的
	- 从一个节点到该节点的子孙节点的所有路径上包含相同数目的黑节点

## 排序算法的特点

- 排序算法的复杂度

![](/img/in_post/base_knowledge.images/3.png)

- 插入排序：当待排序的数据基本有序时，插入排序的效率比较高，只需要进行很少的数据移动
- 归并排序的时间复杂度为O(nlogn), 它的主要缺点是所需的额外空间与待排序数组的尺寸成正比
- 堆排序就是基于优先队列实现的，优先队列可以分为最大优先队列和最小优先队列，最大优先队列主要支持两种操作：插入元素和删除最大元素，最小优先队列则支持插入元素和删除最小元素
- 排序算法中的稳定性表示：如果一个排序算法能够保留数组中重复元素的相对位置则可以被称为是稳定的
- 堆排序的相关链接：[堆排序的简介](https://www.cnblogs.com/0zcl/p/6737944.html)
- 应用场景
	- 冒泡排序：优化后的冒泡排序可用于当数据已经基本有序，且数据量较小时
	- 插入排序：若数组基本有序且数据规模较小时，选用插入排序较好
	- 希尔排序：数据量较小且基本有序时
	- 选择排序：当数据规模较小时，选择排序性能较好
	- 堆排序：堆排序适合处理数据量大的情况，数据呈流式输入时用堆排序也很方便
	- 归并排序：数据量较大且要求排序稳定时
	- 快速排序：快速排序适合处理大量数据排序时的场景

![](/img/in_post/base_knowledge.images/4.png)
