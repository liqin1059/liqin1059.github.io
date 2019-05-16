---
layout: post
title: Jquery类级别（$.extend）
date: 2017-04-18 14:31:30
categories: 控件
tags: []
---
## 类级别（$.extend）

	$.extend({
	    add:function(a,b){
	return a+b;
	},
	    minus:function(a,b){
	return a-b;
	}
	});
	//调用
	var i = $.add(3,2);
	var j = $.minus(3,2);


## 对象级别（$.fn.extend）

	$.fn.extend ({
	changeColor:function(){

	    this.css("color","red");
	},
	changeFont:function(){

	     this.css("font-size","24px");
	},
	check:function(){
	    return this.each(function(){
	    this.checked = true;

	    });

	          }

	});
	//调用
	$(function(){
	$("a").changeColor();
	$("a").changeFont();
	$("input").check();
	});
## 作用域
	(function($){


	})(jQuery);

	//兼容写法
	;(function($){
	})(jQuery);



