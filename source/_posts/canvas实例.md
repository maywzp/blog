---
title: canvas实例
date: 2017-01-16 11:37:49
tags: ['canvas']
description: HTML5 <canvas> 标签用于绘制图像
---

## 矩形
```javascript
var c = document.getElementById('myCanvas');
var ctx = c.getContext('2d');

ctx.fillStyle = "#f00" //默认值：black
ctx.fillRect(0, 0, 100, 100);

ctx.strokeStyle = "#ff0"; //默认值：black
ctx.lineWidth = 5;
ctx.strokeRect(120, 0, 100, 100);

ctx.clearRect(35, 35, 30, 30);
```

## 线条
```javascript
ctx.moveTo(0, 0);       //开始坐标
ctx.lineTo(200, 100);   //结束坐标
ctx.stroke();          //绘制线条
```

## 圆形
arc(x,y,r,start,stop)
```javascript
ctx.beginPath();
ctx.arc(95, 50, 40, 0, 2*Math.PI);    //绘制圆形
ctx.closePath();
ctx.stroke();
```

## 弧线
```javascript
ctx.beginPath();
ctx.arc(150, 75, 50, 0, Math.PI/2);

ctx.strokeStyle = 'rgb(250,0,0)';
ctx.stroke();
```

## 扇形
```javascript
ctx.beginPath();
ctx.sector(150, 75, 50, 0, Math.PI/2);
ctx.closePath();
ctx.fillStyle = 'rgb(250,0,0)';
ctx.fill();

CanvasRenderingContext2D.prototype.sector = function(x, y, radius, sDeg, eDeg) {
  // 初始保存
  this.save();
  // 位移到目标点
  this.translate(x, y);
  this.beginPath();
  // 画出圆弧
  this.arc(0,0,radius,sDeg, eDeg);
  // 再次保存以备旋转
  this.save();
  // 旋转至起始角度
  this.rotate(eDeg);
  // 移动到终点，准备连接终点与圆心
  this.moveTo(radius,0);
  // 连接到圆心
  this.lineTo(0,0);
  // 还原
  this.restore();
  // 旋转至起点角度
  this.rotate(sDeg);
  // 从圆心连接到起点
  this.lineTo(radius,0);
  this.closePath();
  // 还原到最初保存的状态
  this.restore();
  return this;
}
```

## 贝塞尔曲线
```javascript
ctx.bezierCurveTo(10, 10, 100, 30, 150, 100);
ctx.stroke();
ctx.quadraticCurveTo(50, 100, 150, 150);
ctx.stroke();
```

## 文本
font - 定义字体
fillText(text,x,y) - 在 canvas 上绘制实心的文本
strokeText(text,x,y) - 在 canvas 上绘制空心的文本
```javascript
ctx.font="30px Arial";
ctx.fillText("Hello World",10,50); //实心文本
ctx.strokeText("Hello World",10,50); //空心文本
```

## 渐变
createLinearGradient(x,y,x1,y1) - 创建线条渐变
createRadialGradient(x,y,r,x1,y1,r1) - 创建一个径向/圆渐变
### 线性渐变
```javascript
var gl = ctx.createLinearGradient(0, 0, 0, 150);
gl.addColorStop(0, "red");
gl.addColorStop(0.5, "green");
gl.addColorStop(1, "yellow");

ctx.fillStyle = gl;
ctx.fillRect(0, 0, 300, 150);
```
### 同心圆渐变
```javascript
var gl = ctx.createRadialGradient(150, 75, 30, 150, 75, 75);
gl.addColorStop(0, "red");
gl.addColorStop(0.5, "green");
gl.addColorStop(1, "yellow");

ctx.fillStyle = gl;
ctx.arc(150, 75, 75, 0, Math.PI*2);
ctx.fill();
```

### 发散渐变
```javascript
var gl = ctx.createRadialGradient(50, 75, 10, 150, 75, 30);
gl.addColorStop(0, "red");
gl.addColorStop(0.5, "green");
gl.addColorStop(1, "yellow");

ctx.fillStyle = gl;
ctx.rect(0, 0, 300, 150);
ctx.fill();
```

## 阴影
```javascript
ctx.shadowOffsetX = 10;
ctx.shadowOffsetY = 10;
ctx.shadowColor = 'rgba(100,100,100,0.5)';
ctx.shadowBlur = 1.5;

ctx.fillStyle = 'rgba(255,0,0,0.5)';
ctx.fillRect(100, 50, 100, 50);
```
## 创建图像
drawImage(image,x,y)
```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
var img=document.getElementById("scream");
ctx.drawImage(img,10,10);
```
