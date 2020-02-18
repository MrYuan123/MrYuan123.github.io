---
layout:     post
title:      "How to install ubuntu OS (under Windows)"
subtitle:   " \"Hello World, Hello Blog\""
date:       2017-3-17 16：00
author:     "Leonard Yuan"
header-img: "../img/post-bg-e2e-ux.jpg"
catalog: true
tags:
    - data_analysis
    - ubuntu
    - Windows

---

# Windows10下重装ubuntu操作系统


>简介：
实力证明，在不了解、不知情的情况下，程序员最好不要对自己的电脑作大死，否则但来的麻烦能让你焦头烂额。上学期初为了提升linux下程序开发的相关经验，将电脑改为windows10和ubuntu双系统，学期末做大死，随意更改了ubuntu下图形界面相关文件的访问权，造成了好端端的图形界面版本的ubuntu变成了命令行版，着实尴尬。所以重新安装bantu操作系统，并整理成教程，以备不时之需（不过应该不会再作死了吧？我猜！）

## 一、实验相关参数

电脑：华硕
ubuntu版本:ubuntu-16.04.2-desktop-amd64

## 二、安装步骤

### 1.初次安装windows+ubuntu双系统

初次安装双系统的教程在**百度**都很详细，比较推荐下面的几个教程：

[windows+ubuntu系统安装教程1](http://jingyan.baidu.com/article/90bc8fc85ec19cf652640c5f.html)

[windows+ubuntu系统安装教程2](http://www.jianshu.com/p/2eebd6ad284d)

在初次安装双系统时，首先安装windows操作系统，此处不再赘述。在安装windows操作系统后，需要在磁盘空间中分配出一定的磁盘空间来安装ubuntu操作系统，windows操作系统中找到磁盘管理，如下：

<p>
<img src="/img/in_post/1.png"/>
</p>


我们点击某个磁盘分区，从中分出安装ubuntu操作系统的磁盘空间，并右击选择删除盘，供之后的安装使用。

**注意:**
windows下进行磁盘分配的时候，如果发现磁盘的格式为dynamic，而不是basic时，就有点麻烦。这种磁盘格式下，ubuntu安装会失败。惟一的办法只能是重新对整个磁盘进行格式化为basic格式、分区。推荐工具为DiskGenius。对磁盘进行格式化分区之后，重新安装windows操作系统，再重复如上ubuntu安装教程。

### 2.windows下重装ubuntu操作系统

此条适合于作死破坏了原有ubuntu操作系统，导致无法正常登录的同学。首先使用软碟通制作ubuntu操作系统的安装U盘,制作ubuntu安装U盘教程如下：

[ubuntu安装U盘制作教程](http://jingyan.baidu.com/article/a3761b2b66fe141577f9aa51.html)

图例1：

<p>
<img src="/img/in_post/2.png"/>
</p>

图例2：

<p>
<img src="/img/in_post/3.png"/>
</p>


在制作好安装U盘后，我们重启电脑，在电脑没有进入windows操作系统之前(即没有出现windows操作系统图标之前)，长按esc或者F12进入磁盘选择界面（部分电脑快捷键不同），选择自ubuntu安装盘启动。

如图：

<p>
<img src="/img/in_post/4.png"/>
</p>

**注意:
在安装过程中可能出现无论怎么按esc键都无法进入磁盘启动选择界面的情况，这种情况一般是由于windows操作系统中电池管理中设置快速启动所致，关闭即可。**

进入安装U盘后，逐步执行（参照首次安装教程）。当执行到如下步骤时，注意选择“卸载Ubuntu并重新安装”，在选择此项确定后会跳出警告说“有可能破坏原有操作系统的引导”，**继续确认**，进入安装界面，经过漫长的等待之后，完成安装。

<p>
<img src="/img/in_post/5.png"/>
</p>

### 3.恢复windows操作系统引导

在正确安装ubuntu操作系统之后，我们可能会发现在启动操作系统之后，ubuntu启动选项中的windows引导消失了，如下：

<p>
<img src="/img/in_post/6.png"/>
</p>

在这种情况下，我们需要进入ubuntu操作系统中恢复windows操作系统引导，步骤如下：

**1.Ubuntu live CD启动之后，进入终端，输入如下：**

	sudo fdisk -l   
	mkdir /media/tempdir   
	mount /dev/sda3 /media/tempdir   
	grub-install --root-directory=/media/tempdir /dev/sda   

**2.重启，就能看到grub2的引导界面了，选择进入Ubuntu**

	sudo update-grub2

**在成功安装之后，就可以尽情在ubuntu下玩耍啦！！！！**

<p>
<img src="/img/in_post/7.png"/>
</p>
