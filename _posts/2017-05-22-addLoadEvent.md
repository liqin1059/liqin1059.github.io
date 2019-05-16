---
layout: post
title: javascript封装带参addLoadEvent函数
date: 2017-05-22 12:31:30
categories: javascript
tags: [addLoadEvent]
---
为了解决window.onload事件,javascript通过封装带参addLoadEvent函数
> 不带参数版本

```
function addLoadEvent(func){
	var oldonload = window.onload; //将现有的事件处理函数的值存入变量中
	if(typeof window.onload!='function){
		winodw.onload = func; //如果这个事件处理函数没有绑定任何函数，就把新函数添加给它
	}else{
		window.onload = function(){
		oldonload();
		func(); //如果已经绑定了函数，就把新函数追加到现有指令的末尾
		}
	}
}
addLoadEvent(func);
```

> 带参数版本

```
 function addLoadEvent(func){
	var ages = [ ].slice.call(arguments,1);
	var oldonload = window.onload;
		if(typeof window.onload = 'fucntion'){
			window.onload = function(){
			func.apply(this,ages);
		}else{
			window.onload = function(){
			oldonload.apply(this);
			func.apply(this.ages);
		}
	}
 }
addloadEvent(function(a,b){
alert(a);
alert(b);

},"abcd",123);
```








