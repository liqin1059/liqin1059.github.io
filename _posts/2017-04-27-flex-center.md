---
layout: post
title: flex垂直居中
date: 2017-04-17 12:31:30
categories: css3
tags: [盒子]
---

## flex垂直居中

	display:flex;
	flex-direction:column;
	align-items:center;
	justify-content:center;

（兼容ios时遇到过问题）
## 顺便写一下transform的垂直居中方法

父元素

	position:relative;
子元素

	position:absolute;
	left:50%;
	top:50%;
	transform:translate(-50%,-50%);
