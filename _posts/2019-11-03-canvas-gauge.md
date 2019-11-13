---
title: canvas实现仪表盘动画
categories: canvas
tags: 大数据
---
canvas实现仪表盘动画:chart_with_downwards_trend:
涉及到canvas圆、弧线、弧线运动、三角形运动、圆形运动



<img src="/assets/img/gauge.gif"/>

## 首先了解一下 canvas arc()方法

<img src="/assets/img/arc.png"/>

## canvas进度条
```
var canvas = document.getElementById(id);
var ctx = canvas.getContext('2d');
var percent = progress; // 最终百分比
var circleX = canvas.width / 2; // 中心x坐标
var circleY = canvas.height / 2; // 中心y坐标
var radius = 100; // 圆环半径
var lineWidth = 18; // 圆形线条的宽度
var fontSize = 32; // 字体大小
```
- 移动端cavans模糊问题解决
```
var getPixelRatio = function(context) {
  var backingStore = context.backingStorePixelRatio ||
      context.webkitBackingStorePixelRatio ||
      context.mozBackingStorePixelRatio ||
      context.msBackingStorePixelRatio ||
      context.oBackingStorePixelRatio ||
      context.backingStorePixelRatio || 1;
  return (window.devicePixelRatio || 1) / backingStore;
};
var ratio = getPixelRatio(ctx);
canvas.style.width = canvas.width + 'px';
canvas.style.height = canvas.height + 'px';
canvas.width = canvas.width * ratio;
canvas.height = canvas.height * ratio;
ctx.scale(ratio, ratio);
```

## 两端圆点
```
// function smallcircle1(cx, cy, r) {
//   ctx.beginPath();
//   ctx.lineWidth = 1;
//   ctx.fillStyle = 'transparent';
//   ctx.arc(cx, cy, r, 0, Math.PI * 2);
//   ctx.fill();
// }
function smallcircle2(cx, cy, r, color) {
  ctx.beginPath();
  // ctx.moveTo(cx + r, cy);
  ctx.lineWidth = 1;
  ctx.fillStyle = color || pointColor;
  ctx.arc(cx, cy, r, 0, Math.PI * 2);
  ctx.fill();
}
```

##  画圆

```javascript
function circle(cx, cy, r) {
  ctx.beginPath();
  // ctx.moveTo(cx + r, cy);
  ctx.lineWidth = lineWidth;
  ctx.strokeStyle = '#DDE0EA';
  ctx.arc(cx, cy, r, Math.PI * 3 / 4, Math.PI * 1 / 4);
  // 圆弧两端的样式
  ctx.lineCap = 'round';
  ctx.stroke();
}
```

##  画弧线
- 涉及canvas弧度计算知识

<img src="/assets/img/canvas-arc.png"/>

```javascript
function sector(cx, cy, r, startAngle, endAngle) {
  ctx.beginPath();
  // ctx.moveTo(cx, cy + r); // 从圆形底部开始画
  ctx.lineWidth = lineWidth;
  // 渐变色 - 可自定义
  var linGrad = ctx.createLinearGradient(
    circleX - radius - lineWidth, circleY, circleX + radius + lineWidth, circleY
  );
  // linGrad.addColorStop(0.5, '#9bc4eb');
  linGrad.addColorStop(0.0, startColor);
  linGrad.addColorStop(1.0, endColor);
  ctx.strokeStyle = linGrad;
  // 圆弧两端的样式
  ctx.lineCap = 'round';
  // 圆弧
  ctx.arc(
    cx, cy, r,
    startAngle,
    (Math.PI * 3 / 4) + endAngle / 100 * (Math.PI * 3 / 2),
    false
  );
  ctx.stroke();
}
```

##  三角形

- 三角形旋转角度计算

<img src="/assets/img/canvas-arc.png"/>

<img src="/assets/img/angle.png"/>

```javascript
function triangle() {
  ctx.beginPath();
  ctx.moveTo(140 + Math.cos(2 * Math.PI / 360 * (135 + process * 2.7)) * 54, 140 + Math.sin(2 * Math.PI / 360 * (135 + process * 2.7)) * 54); // 135->405 process从0到100
  ctx.lineTo(140 + Math.cos(2 * Math.PI / 360 * (45 + process * 2.7)) * 31, 140 + Math.sin(2 * Math.PI / 360 * (45 + process * 2.7)) * 31);// 45->315 process从0到100
  ctx.lineTo(140 + Math.cos(2 * Math.PI / 360 * (225 + process * 2.7)) * 31, 140 + Math.sin(2 * Math.PI / 360 * (225 + process * 2.7)) * 31); // 225->495 process从0到100
  ctx.fillStyle = startColor;// 以纯色填充
  ctx.fill(); // 闭合形状并且以填充方式绘制出来
}
```

##  刷新

```javascript
function loading() {
  if (process >= percent) {
    clearInterval(circleLoading);
  }
  //  清除canvas内容
  ctx.clearRect(0, 0, circleX * 2, circleY * 2);
  // 中间透明圆
  smallcircle2(140, 140, 53, '#DDE0EA');
  // 三角形
  triangle();
  // 中间圆
  smallcircle2(140, 140, 45, startColor);
  // 中间的字
  ctx.font = fontSize + 'px Arial';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillStyle = '#FFFFFF';
  ctx.fillText(parseFloat(process).toFixed(0) + '%', circleX, circleY);
  // 圆形轨道
  circle(circleX, circleY, radius);
  // 圆弧
  sector(circleX, circleY, radius, Math.PI * 3 / 4, process);
  // 两端圆点
  // 起点
  // smallcircle1(140+Math.cos(2*Math.PI/360*120)*100, 140+Math.sin(2*Math.PI/360*120)*100, 5);
  // 端点
  smallcircle2(140 + Math.cos(2 * Math.PI / 360 * (135 + process * 2.7)) * 100, 140 + Math.sin(2 * Math.PI / 360 * (135 + process * 2.7)) * 100, 5);
  // 控制结束时动画的速度
  if (process / percent > 0.90) {
    process += 0.30;
  } else if (process / percent > 0.80) {
    process += 0.55;
  } else if (process / percent > 0.70) {
    process += 0.75;
  } else {
    process += 1.0;
  }
};
```

## 进度

```javascript
var process = 0.0;
var circleLoading = window.setInterval(function() {
  loading();
}, 20);
```
