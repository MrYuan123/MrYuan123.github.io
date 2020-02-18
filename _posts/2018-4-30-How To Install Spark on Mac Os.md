---
layout:     post
title:      "How To Install Spark On Mac os"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-4-30 22：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Mac OS
    - Big Data

---

# How To Install Spark on Mac os

## 1. Introduction

Today, I will introduce the way to install spark on mac os. I will achieve the calculation of the data of MovieLens, it is the part of my undergraduate project. The topic of my undergraduate project is `Design and Implementation of Recommendation System Based on Collaborative Filtering Algorithm`. Because I choose MovieLens as my DataSet(190mb), so I have to use spark as analytics engine for large-scale data processing. Thus, it is neccessary to install Spark on mac os.

So, ler's start.

## 2. Install Java JDK

We must install java JDK at first, we should download `.dmg` from official website, the link is shown as follow:

[Download .dmg files](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

The website is shown like this:

![](/img/in_post/install_spark/download_java.png)

Choose `MAC OS X x64`, then download it. When download process is finished, click `.dmg` files, and follow hints to finish install process.

![](/img/in_post/install_spark/install_java.png)

Then you can use command `java -version` to confirm whether it is successful to install java JDK.

![](/img/in_post/install_spark/java_version.png)

Aferwards, we start settle environment variables. First of all, we need to find `profile` files, its path is `/etc/profile`. We can use vim or something else to revise `profile`, we must add the path of java into profile, you should add following text:

	JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home"
	export JAVA_HOME
	CLASS_PATH="$JAVA_HOME/lib"
	PATH=".$PATH:$JAVA_HOME/bin"

After you save profile, use command `source /etc/profile ` to make sure your revise to be valid. Finally, you can use following command to get the path of java:

	$ echo $JAVA_HOME
	/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home

From now, we can use java JDK on you mac os.

## 3. Install Scala

I will add details.

## 4. Install Spark



## 5. Introduction of Using Spark
