---
layout: post
title: 移动端常见问题
date: 2017-05-13 12:31:30
categories: 移动端
tags: [移动端]
---

## 移动端字体
三大手机系统的字体：

- ios 系统

默认中文字体是Heiti SC
默认英文字体是Helvetica
默认数字字体是HelveticaNeue
无微软雅黑字体

- android 系统

默认中文字体是Droidsansfallback
默认英文和数字字体是Droid Sans
无微软雅黑字体

- winphone 系统

默认中文字体是Dengxian(方正等线体)
默认英文和数字字体是Segoe
无微软雅黑字体

各个手机系统有自己的默认字体，且都不支持微软雅黑
如无特殊需求，手机端无需定义中文字体，使用系统默认
英文字体和数字字体可使用 Helvetica ，三种系统都支持


- 移动端定义字体的代码
    body{font-family:Helvetica;}

## 移动端字体选择
- px/rem
对于只需要适配手机设备，使用px即可
对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备
- rem配置参考：
    html {font-size:10px}
    @media screen and (min-width:480px) and (max-width:639px) {
        html {
            font-size: 15px
        }
    }
    @media screen and (min-width:640px) and (max-width:719px) {
        html {
            font-size: 20px
        }
    }
    @media screen and (min-width:720px) and (max-width:749px) {
        html {
            font-size: 22.5px
        }
    }
    @media screen and (min-width:750px) and (max-width:799px) {
        html {
            font-size: 23.5px
        }
    }
    @media screen and (min-width:800px) and (max-width:959px) {
        html {
            font-size: 25px
        }
    }
    @media screen and (min-width:960px) and (max-width:1079px) {
        html {
            font-size: 30px
        }
    }
    @media screen and (min-width:1080px) {
        html {
            font-size: 32px
        }
    }


## Retina 显示屏
- 什么是Retina 显示屏，带来了什么问题
retina：一种具备超高像素密度的液晶屏，同样大小的屏幕上显示的像素点由1个变为多个，如在同样带下的屏幕上，苹果设备的retina显示屏中，像素点1个变为4个
在高清显示屏中的位图被放大，图片会变得模糊，因此移动端的视觉稿通常会设计为传统PC的2倍
那么，前端的应对方案是：
设计稿切出来的图片长宽保证为偶数，并使用backgroud-size把图片缩小为原来的1/2
//例如图片宽高为：200px*200px，那么写法如下
    .css{width:100px;height:100px;background-size:100px 100px;}
其它元素的取值为原来的1/2，例如视觉稿40px的字体，使用样式的写法为20px
    .css{font-size:20px}


## viewport模板
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="utf-8">
    <meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
    <meta content="yes" name="apple-mobile-web-app-capable">
    <meta content="black" name="apple-mobile-web-app-status-bar-style">
    <meta content="telephone=no" name="format-detection">
    <meta content="email=no" name="format-detection">
    <title>标题</title>
    <link rel="stylesheet" href="index.css">
    </head>
    <body>
    这里开始内容
    </body>
    </html>

## IE/Chrome
- 优先使用最新版本 IE 和 Chrome

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />

## 添加到主屏后的标题（IOS）

    <meta name="apple-mobile-web-app-title" content="标题"/> 


## 启用 WebApp 全屏模式（IOS）
当网站添加到主屏幕后再点击进行启动时，可隐藏地址栏（从浏览器跳转或输入链接进入并没有此效果）
    <meta name="apple-mobile-web-app-capable" content="yes" /> 
    <meta name="apple-touch-fullscreen" content="yes" />



## 百度禁止转码
通过百度手机打开网页时，百度可能会对你的网页进行转码，往你页面贴上它的广告，非常之恶心。不过我们可以通过这个meta标签来禁止它：

    <meta http-equiv="Cache-Control" content="no-siteapp" />


## 设置状态栏的背景颜色（IOS）
- 设置状态栏的背景颜色
只有在 `"apple-mobile-web-app-capable" content="yes"` 时生效

    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" /> 

- content 参数：
default ：状态栏背景是白色。
black ：状态栏背景是黑色。
black-translucent ：状态栏背景是半透明。 如果设置为 default 或 black ,网页内容从状态栏底部开始。 如果设置为 black-translucent ,网页内容充满整个屏幕，顶部会被状态栏遮挡。


## 移动端手机号码识别（IOS）
- 在 iOS Safari （其他浏览器和Android均不会）上会对那些看起来像是电话号码的数字处理为电话链接，比如：
7位数字，形如：1234567
带括号及加号的数字，形如：(+86)123456789
双连接线的数字，形如：00-00-00111
11位数字，形如：13800138000
可能还有其他类型的数字也会被识别。我们可以通过如下的meta来关闭电话号码的自动识别：
    <meta name="format-detection" content="telephone=no" />
- 开启电话功能
    <a href="tel:123456">123456</a>
- 开启短信功能：
    <a href="sms:123456">123456</a>     

## 移动端邮箱识别（Android）
与电话号码的识别一样，在安卓上会对符合邮箱格式的字符串进行识别，我们可以通过如下的meta来管别邮箱的自动识别：

    <meta content="email=no" name="format-detection" /> 


同样地，我们也可以通过标签属性来开启长按邮箱地址弹出邮件发送的功能：

    <a mailto:dooyoe@gmail.com>dooyoe@gmail.com</a>
    




## ios系统中元素被触摸时产生的半透明灰色遮罩怎么去掉
ios用户点击一个链接，会出现一个半透明灰色遮罩, 如果想要禁用，可设置`-webkit-tap-highlight-color的alpha`值为0，也就是属性值的最后一位设置为0就可以去除半透明灰色遮罩

    a,button,input,textarea{-webkit-tap-highlight-color: rgba(0,0,0,0)}
    


## 部分android系统中元素被点击时产生的边框怎么去掉
android用户点击一个链接，会出现一个边框或者半透明灰色遮罩, 不同生产商定义出来额效果不一样，可设置`-webkit-tap-highlight-color`的alpha值为0去除部分机器自带的效果
    
    a,button,input,textarea{
        -webkit-tap-highlight-color: rgba(0,0,0,0)
        -webkit-user-modify:read-write-plaintext-only; 
    }
    

`-webkit-user-modify`有个副作用，就是输入法不再能够输入多个字符
另外，有些机型去除不了，如小米2
对于按钮类还有个办法，不使用a或者input标签，直接用div标签


## winphone系统a、input标签被点击时产生的半透明灰色背景怎么去掉
    
    <meta name="msapplication-tap-highlight" content="no">
    


## webkit表单元素的默认外观怎么重置
    
    .css{-webkit-appearance:none;}
    

## webkit表单输入框placeholder的颜色值能改变么
    
    input::-webkit-input-placeholder{color:#AAAAAA;}
    input:focus::-webkit-input-placeholder{color:#EEEEEE;}
    

## webkit表单输入框placeholder的文字能换行么
ios可以，android不行~


## 关闭iOS键盘首字母自动大写
在iOS中，默认情况下键盘是开启首字母大写的功能的，如果启用这个功能，可以这样：
    
    <input type="text" autocapitalize="off" />
    

## 关闭iOS输入自动修正
和英文输入默认自动首字母大写那样，IOS还做了一个功能，默认输入法会开启自动修正输入内容，这样的话，用户经常要操作两次。如果不希望开启此功能，我们可以通过input标签属性来关闭掉：
    
    <input type="text" autocorrect="off" /> 
    


## 禁止文本缩放
当移动设备横竖屏切换时，文本的大小会重新计算，进行相应的缩放，当我们不需要这种情况时，可以选择禁止：
    
    html {-webkit-text-size-adjust: 100%;}
    
需要注意的是，PC端的该属性已经被移除，该属性在移动端要生效，必须设置 `meta viewport`。


## 移动端如何清除输入框内阴影
在iOS上，输入框默认有内部阴影，但无法使用 box-shadow 来清除，如果不需要阴影，可以这样关闭：
    
    input,
    textarea {
    　　border: 0; 
    　　-webkit-appearance: none; 
    }
    



## 屏幕旋转的事件和样式

`window.orientation`，取值：正负90表示横屏模式、0和180表现为竖屏模式；
    
    window.onorientationchange = function(){
                switch(window.orientation){
                    case -90:
                    case 90:
                    alert("横屏:" + window.orientation);
                    case 0:
                    case 180:
                    alert("竖屏:" + window.orientation);
                    break;
                }
    } 
    
- 样式

//竖屏时使用的样式

    @media all and (orientation:portrait) {
        .css{}
    }

//横屏时使用的样式
    @media all and (orientation:landscape) {
        .css{}
    }
    

## audio元素和video元素在ios和andriod中无法自动播放

应对方案：触屏即播 

    $('html').one('touchstart',function(){
        audio.play()
    })
    
## 摇一摇功能
HTML5 deviceMotion：封装了运动传感器数据的事件，可以获取手机运动状态下的运动加速度等数据。

## 手机拍照和上传图片
    
`<input type="file">`的`accept`属性

    <!-- 选择照片 -->
    <input type=file accept="image/*">

    <!-- 选择视频 -->
    <input type=file accept="video/*">
    
使用总结：
ios 有拍照、录像、选取本地图片功能
部分android只有选取本地图片功能
winphone不支持
input控件默认外观丑陋


## 消除transition闪屏
    
    .css{
        
        -webkit-transform-style: preserve-3d;
        
        -webkit-backface-visibility: hidden;
    }
    


开启硬件加速
解决页面闪白
保证动画流畅
    
    .css {
       -webkit-transform: translate3d(0, 0, 0);
       -moz-transform: translate3d(0, 0, 0);
       -ms-transform: translate3d(0, 0, 0);
       transform: translate3d(0, 0, 0);
    }
    

设计高性能CSS3动画的几个要素
尽可能地使用合成属性transform和opacity来设计CSS3动画，
不使用position的left和top来定位
利用translate3D开启GPU加速


##  android 上去掉语音输入按钮
    
    input::-webkit-input-speech-button {display: none}
    

## 模拟按钮hover效果
移动端触摸按钮的效果，可明示用户有些事情正要发生，是一个比较好体验，但是移动设备中并没有鼠标指针，使用css的hover并不能满足我们的需求，还好国外有个激活css的active效果，代码如下，

    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="utf-8">
    <meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
    <meta content="yes" name="apple-mobile-web-app-capable">
    <meta content="black" name="apple-mobile-web-app-status-bar-style">
    <meta content="telephone=no" name="format-detection">
    <meta content="email=no" name="format-detection">
    <style type="text/css">

    a{-webkit-tap-highlight-color: rgba(0,0,0,0);}
    .btn-blue{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;}
    .btn-blue:active{background-color: #357AE8;}

    </style>
    </head>
    <body>

    <div class="btn-blue">按钮</div>

    <script type="text/javascript">
    document.addEventListener("touchstart", function(){}, true)
    </script>
    </body>
    </html>
    




## 框架
- 移动端基础框架
    zepto.js 语法与jquery几乎一样，会jquery基本会zepto~

    iscroll.js 解决页面不支持弹性滚动，不支持fixed引起的问题~ 实现下拉刷新，滑屏，缩放等功能~

    underscore.js 该库提供了一整套函数式编程的实用功能，但是没有扩展任何JavaScript内置对象。

    fastclick 加快移动端点击响应时间
    
    animate.css CSS3动画效果库

    Normalize.css Normalize.css是一种现代的、CSS reset为HTML5准备的优质替代方案

- 滑屏框架
适合上下滑屏、左右滑屏等滑屏切换页面的效果
    slip.js
    iSlider.js
    fullpage.js
    swiper

- 瀑布流框架
`masonry`
工具推荐
caniuse 各浏览器支持html5属性查询
paletton 调色搭配

