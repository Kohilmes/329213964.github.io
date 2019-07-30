---
layout: post
title: "JavaSwing打jar包"
date: 2019-07-30
categories: Java Swing exe4j
tags: Java Swing exe4j Idea
---

* content 
{:toc}
今天把一年前写的小游戏打了个包 

发在了https://tutor.foxcii.com/games/iwanna-version1.0.zip

如果系统没有jre环境则需选择https://tutor.foxcii.com/games/iwanna-version1.1.zip



![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/Swing/iwannaindex.png)



在打成jar包访问图片资源等时需要注意

```java
new ImageIcon("src/images/stone.png")
```

将访问不到对应图片资源

应以如下写法改写

```java
new ImageIcon(getClass().getResource("/images/stone.png"));
```



因为这个问题，打了好几次包都是这样

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/_posts/images/Swing/iwannaindex-empty.jpg)



导致一度以为是项目的frame与panel等组件排版或是线程安排有问题，直到今天才得以真相大白



打包后如没有jre环境配置则会出现以下情况

![](https://raw.githubusercontent.com/329213964/329213964.github.io/master/posts/images/Swingiwanna-jre.png)

如果将jre打包发送 则项目容量会相当大，这个问题有待解决；