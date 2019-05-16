---
layout: post
title: mui消息提示框
date: 2017-05-07 12:31:30
categories: 控件
tags: []
---
mui消息提示框

## alert


	<script type="text/javasript" charset="UTF-8">
	//mui初始化
	mui.init({
	  swipeBack:true;//启动右滑关闭
	});
	document.getElementById("alertBtn").addEventListener('tap',function(){
	  mui.alert('mui弹出框','弹出框标题',function(){
	  //添加关闭以后的操作
	});

	});
	</script>



## confirm

	<script type="text/javasript" charset="UTF-8">
	//mui初始化
	mui.init({
	  swipeBack:true;//启动右滑关闭
	});
	document.getElementById("confirmBtn").addEventListener('tap',function(){
	  var btnArray = ['否','是']; 
	  mui.alert('mui confirm框','弹出框标题',btnArray,function(e){
	  //添加关闭以后的操作
	   if(e.index == 1){
	  //如果是数组的第二个,添加操作
	  
	  }else{
	  //其他，添加操作
	}
	});

	});
	</script>//btnArray可以使选项为多个，返回值也有多个


## prompt

	<script type="text/javasript" charset="UTF-8">
	//mui初始化
	mui.init({
	  swipeBack:true;//启动右滑关闭
	});
	document.getElementById("promptBtn").addEventListener('tap',function(e){
	//修复iOS 8.x平台存在的bug，使用plus.nativeUI.prompt会造成输入法闪一下没了 
	 var btnArray = ['取消','确认'];
	mui.prompt('请输入内容','prompt标题','placeholder',btnArray,function(e){
	  if(e.index == 1){
	  //点击了第二个按钮
	}else{
	//点击了第一个按钮
	}

	});

	});
	</script>


## toast

	<script type="text/javasript" charset="UTF-8">
	//mui初始化
	mui.init({
	  swipeBack:true;//启动右滑关闭
	});
	document.getElementById("alertBtn").addEventListener('tap',function(){
	  mui.toast('mui淡出弹出框');

	});
	</script>
