---
layout:     post
title:      "About MapReduce"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-1-30 18：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Big Data
    - MapReduce

---

>It is about MapReduce.

---

# MapReduce Notes

## 一、基础知识

### 1.1 MapReduce简介

MapReduce是一个编程模型，也是一个处理和生成超大数据集的算法模型的相关实现。用户首先创建一个Map函数处理一个基于 key/value pair的数据集合，输出中间的基于key/value pair的数据集合；然后再创建一个Reduce函数用来合并所有的具有相同中间key值的中间value值。MapReduce架构的程序能够在大量的普通配置的计算机上实现并行化处理。通过MapReduce架构可以使得程序开发人员充分利用分布式系统的计算资源。

MapReduce原版论文中提到：

> The issues of how to parallelize the computation, distribute the data, and handle failures conspire to obscure the original simple computation with large amounts of complex code to deal with theseissues.

因此，MapReduce模型旨在通过分布式计算的方式来解决大量数据单机计算时的弊端。通过这种抽象模型，使用者不必关心并行计算、容错、数据分布等相关的问题，所有的问题被封装在库中（与面向对象的编程语言的思路相像）。

### 1.2 简要思路

首先先简单介绍一下分布式计算的简要思路。假设这里有涉及到10000道数学题的复杂问题，如何完成这项浩大的工程呢？大致有两种思路：

>1.找一个计算能力非常强的人进行计算，但对于这个人自己的计算能力和出错率要求很高；
>1.找100个计算能力进行计算，然后将他们的计算结果进行汇总和整理，最后得出计算结果。

前一种大致与我们现在的超级计算机的思路相同，它自身拥有着很多好处，比如计算方便，运算速度快等等，但是缺点也很明显，那就是**贵**！后者基本上就是我们所说的分布式计算的思路，MapReduce模型就是按照这样的思路进行设计的。

## 二、MapReduce详述

### 2.1 角色设定

MapReduce模型的基本思路是：利用一个输入key/value pair集合来产生一个输出的key/value pair集合。MapReduce库的用户用两个函数表达这个计算：Map和Reduce。

Map：Map函数主要用于根据输入的key/value pair值的集合产生key/value pair值的集合，相当于在实际分布式计算中的小喽啰。它们负责在获取原始的数据后进行计算并形成相应的中间值集合；

Reduce：Reduce函数接受一个中间key的值I和相关的一个value值的集合。Reduce函数合并这些value值，形成一个较小的value值的集合。
