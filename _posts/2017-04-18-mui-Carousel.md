---
layout: post
title: mui轮播图
date: 2017-04-18 14:31:30
categories: 插件
tags: [移动端]
---
今天用mui的框架的时候，写轮播图花了好多时间，最后发现调用js应该在文档最后，不能在文档前加载调用轮播的对象，以下是mui的轮播调用代码
	<script>
	mui.init({
	swipeBack:true // 启用右滑关闭功能
	});
	var slider = mui("#slider");
	slider.slider({
	 interval:3000
	});
	</script>
