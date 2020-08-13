---
layout: post
title: addEventListener
date: 2019-12-30 12:31:30
categories: javascript
tags:
---
DOM方法 addEventListener() 和 removeEventListener()是用来分配和删除事件的函数。 这两个方法都需要三个参数，分别为：
- 事件名称（String）
- 要触发的事件处理函数(Function)
- 指定事件处理函数的时期或阶段(boolean)。

<!-- more -->
## DOM事件流如图：
<center><img src="/assets/img/addeventlistener.gif" alt=""></center>

由图可知捕获过程要先于冒泡过程

- 第三个参数设置为true就在捕获过程中执行
- 第三个参数设置为false就在冒泡过程中执行处理函数
