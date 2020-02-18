---
layout:     post
title:      "Database Review"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-5-5 14：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Interview
    - Database
---

# 数据库复习

[数据库面试问题集合](https://www.cnblogs.com/qinghe123/p/8663573.html)
## 基础知识

- MySQL如何分页
	-	mysql数据库做分页用limit关键字，它后面跟两个参数startIndex和pageSize
- ACID
	- A: 事务的原子性, 一个事务要么全部执行，要么都不执行
	- C: 事务的一致性, 事务的运行并不改变数据库中数据的一致性
	- I: 事务的独立性也有称作隔离性
	- D: 事务的持久性是指事务执行成功以后,该事务所对数据库所作的更改便是持久的保存在数据库之中
-  主键、外键和索引的区别
![](/img/in_post/db.images/1.png)
- 触发器
	- 在数据库中，使用触发器可以定义在进行数据库操作前后的行为。触发器无法被用户所调用，它只有在数据表进行操作行为前后被动触发
- 数据库中，char和varchar的区别：一个12字节，另外一个不固定长度
- 数据库范式
	- 第一范式：强调的是列的原子性，即列不能够再分成其他几列
	- 第二范式：一是表必须有主键；二是没有包含在主键中的列必须完全依赖于主键，而不能只依赖于主键的一部分
	- 第三范式：非主键列必须直接依赖于主键，不能存在传递依赖

- join操作
	- left join(左联接)： 返回包括左表中的所有记录和右表中联结字段相等的记录。
	- right join(右联接)： 返回包括右表中的所有记录和左表中联结字段相等的记录。
	- inner join(等值连接)： 只返回两个表中联结字段相等的行。
- 存储过程：存储过程是一个预编译的SQL语句，优点是允许模块化的设计，就是说只需创建一次，以后在该程序中就可以调用多次
- 事务：事务就是被绑定在一起作为一个逻辑工作单元的SQL语句分组，如果任何一个语句操作失败那么整个操作就被失败，以后操作就会回滚到操作前状态，或者是上有个节点
- 主键和外键的区别：主键在本表中是唯一的、不可唯空的，外键可以重复可以唯空；外键和另一张表的主键关联，不能创建对应表中不存在的外键
- 处理关系型数据库，还有另外几种非关系型数据库：
	- 键值(Key-Value)存储数据库（一般使用到Hash表）-- Redis
	- 列存储(Wide-Column)数据库（一个key指向多个列）
	- 文档型(Document)数据库--MongoDB
	- 图形数据库----Neo4j
- NoSQL不能用SQL语句进行查询，只能通过该语言定义的操作语句进行增删改查
## MySQL的数据引擎

[MySQL底层实现](https://blog.csdn.net/gitchat/article/details/78787837)里面有B-树不查询的过程

- InnoDB 和 Myisam 都是用 B+Tree 来存储数据的
- MySQL存储引擎主要有两种：`MyISAM`和`InnoDB`
- 两种存储引擎的区别：
	- Innodb引擎提供了对数据库ACID事务的支持，提供了行级锁和外键约束，由于锁的粒度更小，写操作不会锁定全表，所以在并发较高时，使用Innodb引擎会提升效率
	- MyIASM引擎没有提供对数据库事务的支持，也不支持行级锁和外键，在写操作的时候，需要将整个表都锁起来
	- 在读操作远远多于写操作的情况下（且不需要事务支持的），MyISAM是更好的选择
	- MyISAM允许没有任何索引和主键的表存在。InnoDB要求表必须有主键，InnoDB如果没有设定主键或者非空唯一索引，就会自动生成一个6字节的主键(用户不可见)
- MySQL 的 InnoDB 存储引擎在设计时是将根节点常驻内存的，因此力求达到树的深度不超过 3，也就是说 I/O 不需要超过 3 次

## 索引

- 几种关键的索引 [索引相关知识](https://blog.csdn.net/u012006689/article/details/73195837)
	- 聚集索引：就是按照每张表的主键构造一棵B+树，同时叶子节点中存放的即为整张表的行记录数据（意思就是这表就是建在聚集索引上的）
	- 辅助索引，也叫非聚集索引。和聚集索引相比，叶子节点中并不包含行记录的全部数据
	- 覆盖索引：InnoDB存储引擎支持覆盖索引，即从辅助索引中就可以得到查询的记录，而不需要查询聚集索引中的记录
	- 联合索引：联合索引是指对表上的多个列进行索引
- 聚集索引：表数据按照索引的顺序来存储的。非聚簇索引的意思与之相反
- 索引是对数据库表中一列或多列的值进行排序的一种结构，是帮助MySQL高效获取数据的数据结构。MyIASM和Innodb都使用了B+树这种数据结构做为索引
- 主键创建后一定包含一个唯一性索引，唯一性索引并不一定就是主键。唯一性索引列允许空值，而主键列不允许为空值
- 主键列在创建时，已经默认为空值 + 唯一索引了
- mysql数据库都有哪些索引
	- 普通索引：普通索引仅有一个功能：加速查找
	- 唯一索引：唯一索引两个功能：加速查找和唯一约束（可含null）
	- 外键索引：外键索引两个功能：加速查找和唯一约束（不可为null）
	- 联合索引：联合索引是将n个列组合成一个索引，应用场景：同时使用n列来进行查询
- B-树
![](/img/in_post/db.images/2.png)
- B+Tree 在 B-Tree 的基础上有两点变化
	- 数据是存在叶子节点中的
	- 数据节点之间是有指针指向的，每个数据页通过一个双向链表来进行链接
	- 可以对 B+Tree 进行两种查找运算：一种是对于主键的范围查找和分页查找，另一种是从根节点开始，进行随机查找
![](/img/in_post/db.images/3.png)
- 在 B+Tree 中，所有数据记录节点都是按照键值大小顺序存放在同一层的叶子节点上，而非叶子节点上只存储 key 值信息，这样可以大大加大每个节点存储的 key 值数量，降低 B+Tree 的高度。
- 当经常进行order by、group by、distinct等字段操作的时候，使用索引会效率更高

### 两种引擎的索引实现
- MyISAM索引实现: 是使用B+树来实现索引的，MyISAM索引文件和数据文件是分离的，索引文件仅保存数据记录的地址。由于数据与索引不在一起，所以 Myisam 是`非聚簇索引`???。在MyISAM的辅助索引中存储的是主键的地址
- Innodb的索引文件本身就是数据文件，即B+Tree的数据域存储的就是实际的数据，这种索引就是聚集索引。InnoDB的`辅助索引`数据域存储的也是相应记录`主键的值`而不是地址，所以当以辅助索引查找时，会先根据辅助索引找到主键，再根据`主键索引`找到实际的数据

## 锁

- 锁的粒度
	- 表锁
	- 页锁
	- 列锁
	- （数据库锁）
- 类型维度
	- 共享锁（读锁/S锁）
	- 排它锁（写锁/X锁）
	- 意向共享锁（IS）：事务打算给数据行加行共享锁，事务在给一个数据行加共享锁前必须先取得该表的IS锁
	- 事务打算给数据行加行排他锁，事务在给一个数据行加排他锁前必须先取得该表的IX锁

## 事务的隔离

- 如果不考虑事务的隔离问题，会产生如下的问题：
	- 脏读
	- 不可重复读
	- 幻读
- 事务的隔离相关链接：[数据库事务的隔离](https://www.cnblogs.com/Andya/p/7426436.html)
- 事务的隔离级别
	- Read uncommitted(未授权读取、读未提交) -- 会出现`脏读`的情况
	- Read committed（授权读取、读提交）-- 解决了`脏读`，但是出现了`不可重复读`的情况
	- Repeatable read（可重复读取）-- 避免了脏读和不可重复读，但是会出现`幻读`情况
	- Serializable（序列化）-- 避免所有问题