---
title: canvas参考手册
date: 2016-12-8 10:37:49
updated: 2016-12-8 10:37:49
tags: ['canvas']
description: HTML5 <canvas> 标签用于绘制图像
---

## 绘制图像的方法
```javascript
ctx.fill()      填充
ctx.stroke()    绘制边框
```

## 绘制图像的样式
```javascript
ctx.fillStyle     填充的样式
ctx.strokeStyle   边框的样式
ctx.lineWidth     边框的宽度
```

## 绘制矩形
x:矩形起点横坐标
y:矩形起点纵坐标
width:矩形长度
height:矩形高度
```javascript
ctx.fillRect(x,y,width,height)     矩形填充
ctx.strokeRect(x,y,width,height)   矩形边框
ctx.clearRect(x,y,width,height)    矩形清除区域
```

## 绘制圆形
x:圆心的x坐标
y:圆心的y坐标
radius:半径
startAngle:开始角度
endAngle:结束角度
anticlockwise:是否逆时针（true）为逆时针，(false)为顺时针
```javascript
ctx.arc(x,y,radius,startAngle,endAngle,anticlockwise)
```
### 旋转角度
![](http://pic002.cnblogs.com/images/2012/407398/2012080217203994.png)


## 绘制线条
x:x坐标
y:y坐标
```javascript
ctx.moveTo(x,y)    起点
ctx.lineTo(x,y)    终点
```

## 绘制贝塞尔曲线
cp1x:第一个控制点x坐标
cp1y:第一个控制点y坐标
cp2x:第二个控制点x坐标
cp2y:第二个控制点y坐标
x:终点x坐标
y:终点y坐标
注：第二点为拐点
```javascript
ctx.bezierCurveTo(cp1x,cp1y,cp2x,cp2y,x,y)
```

## 绘制二次样条曲线
qcpx:二次样条曲线控制点x坐标
qcpy:二次样条曲线控制点y坐标
qx:二次样条曲线终点x坐标
qy:二次样条曲线终点y坐标
注：起点为上一个贝塞尔曲线的终点
```javascript
ctx.quadraticCurveTo(qcpx,qcpy,qx,qy)
```

## 渐变
xstart:渐变开始点x坐标
ystart:渐变开始点y坐标
radiusStart:发散开始圆的半径
xEnd:渐变结束点x坐标
yEnd:渐变结束点y坐标
radiusEnd:发散结束圆的半径

offset:设定的颜色离渐变结束点的偏移量(0~1)
color:绘制时要使用的颜色
```javascript
var gr = ctx.createLinearGradient(xStart,yStart,xEnd,yEnd)
var gr = ctx.createRadialGradient(xStart,yStart,radiusStart,xEnd,yEnd,radiusEnd)
gr.addColorStop(offset,color)
```
## 发散渐变偏移量图(非同心圆)
![](http://pic002.cnblogs.com/images/2012/407398/2012080314164328.png)

## 变形
### 平移
x:坐标原点向x轴方向平移x
y:坐标原点向y轴方向平移y

```javascript
ctx.translate(x,y)
```

### 缩放
x:x坐标轴按x比例缩放
y:y坐标轴按y比例缩放
```javascript
ctx.scale(x,y)
```

### 旋转
angle:坐标轴旋转x角度（角度变化模型和画圆的模型一样）
```javascript
ctx.rotate(angle)
```

## 图形组合
两个图形相互叠加
type取值：
  source-over（默认值）:在原有图形上绘制新图形
  destination-over:在原有图形下绘制新图形
  source-in:显示原有图形和新图形的交集，新图形在上，所以颜色为新图形的颜色
  destination-in:显示原有图形和新图形的交集，原有图形在上，所以颜色为原有图形的颜色
  source-out:只显示新图形非交集部分
  destination-out:只显示原有图形非交集部分
  source-atop:显示原有图形和交集部分，新图形在上，所以交集部分的颜色为新图形的颜色
  destination-atop:显示新图形和交集部分，新图形在下，所以交集部分的颜色为原有图形的颜色
  lighter:原有图形和新图形都显示，交集部分做颜色叠加
  xor:重叠飞部分不现实
  copy:只显示新图形
```javascript
ctx.globalCompositeOperation = type
```
type取值图：
![](http://pic002.cnblogs.com/images/2012/407398/2012080317515321.png)

## 阴影
```javascript
ctx.shadowOffsetX    阴影的横向位移量（默认值为0）
ctx.shadowOffsetY    阴影的纵向位移量（默认值为0）
ctx.shadowColor      阴影的颜色
ctx.shadowBlur       阴影的模糊范围（值越大越模糊）
```

## 绘制图像
### 绘图
image:Image对象
x:绘制图像的x坐标
y:绘制图像的y坐标
```javascript
context.drawImage(image,x,y)
```

image:Image对象
x:绘制图像的x坐标
y:绘制图像的y坐标
w:绘制图像的宽度
h:绘制图像的高度
```javascript
context.drawImage(image,x,y,w,h)
```
选取图像的一部分矩形区域进行绘制
image:Image对象
sx：图像上的x坐标
sy：图像上的y坐标
sw：矩形区域的宽度
sh：矩形区域的高度
dx：画在canvas的x坐标
dy：画在canvas的y坐标
dw：画出来的宽度
dh：画出来的高度
```javascript
ctx.drawImage(image,sx,sy,sw,sh,dx,dy,dw,dh)
```
先裁取图像区域，在画在画布上
![](http://pic002.cnblogs.com/images/2012/407398/2012080410231479.png)

### 平铺
type取值:
no-repeat:不平铺
repeat-x:横方向平铺
repeat-y:纵方向平铺
repeat:全方向平铺
```
ctx.createPattern(image,type)
```

### 裁剪
只绘制封闭路径区域内的图像，不绘制路径外部图像
```
ctx.clip()
```

## 绘制文字
text:要绘制的文字
x:文字起点的x坐标轴
y:文字起点的y坐标轴
```javascript
ctx.fillText(text,x,y)          填充文字
ctx.strokeText(text,x,y)        绘制文字轮廓
ctx.font                        设置字体样式
ctx.textAlign                   水平对齐方式:start、end、right、center
ctx.textBaseline                垂直对齐方式:top、hanging、middle、alphabetic、ideographic、bottom
ctx.measureText(text)           计算字体长度(px)
```

## 保存和恢复状态
```javascript
ctx.save()        保存
ctx.restore()     恢复
```

## 保存文件
Mime：
PNG图像： image/png
GIF图形： image/gif
JPEG图形：image/jpeg
```javascript
canvas.toDataURL(MIME)
```
<!-- ## 基本属性
```
fillStyle         填充样式
strokeStyle       线条样式
shadowColor       阴影的颜色
shadowBlur        阴影的模糊程度
shadowOffsetX     阴影的水平偏移量
shadowOffsetY     阴影的垂直偏移量
```

## 基本方法
```
createLinearGradient()         创建线性渐变
createPattern()                重复元素
creatRadialGradient()          创建环形渐变
addColorStop()                 渐变对象停止的颜色和位置
```

## 线条样式
```
lineCap       线条结束端点的样式
lineJoin      线条相交点的样式
lineWidth     线条粗细
lineLimit     最大斜接长度
```

## 矩形
```
rect()          创建矩形
fillRect()      矩形填充
strokeRect()    矩形绘制
clearRect()     清除矩形区域
```

## 路径
```
fill()                填充当前绘图
stroke()              绘制已定义的路线
beginPath()           起始一条路线
moveTo()              把路径移动到指定点
closePath()           重当前点回到起始点
lineTo()              添加一个新点并创建线条
clip()                从原始画布剪切任意形状和尺寸的区域
quadraticCurveTo()    创建二次贝塞尔曲线
bezierCurveTo()       创建三次贝塞尔曲线
arc()                 创建弧线
arcTo()               创建两切线之间的弧/曲线。
isPointInPath()       如果指定的点位于当前路径中，则返回 true，否则返回 false。
```

## 转换
```
scale()           缩放
rotate()          旋转
translate()       重新映射画布上的 (0,0) 位置
transform()       替换绘图的当前转换矩阵
setTransform()    将当前转换重置为单位矩阵,然后运行 transform()
```

## 文本
### 属性
```
font            字体属性
textAlign       对齐方式
textBaseline    文本基线
```
### 方法
```
fillText()      在画布上绘制"被填充的"文本
strokeText()    在画布上绘制文本（无填充）
measureText()   返回包含指定文本宽度的对象
```

## 图像绘制
```
drawImage()      向画布上绘制图像、画布或视频
```

## 像素操作
### 属性
```
width        返回 ImageData 对象的宽度
height       返回 ImageData 对象的高度
data         返回 ImageData 对象的数据
```
### 方法
```
createImageData()  创建ImageData对象
getImageData()     返回 ImageData 对象
putImageData()     把图像数据放回画布上
```
## 合成
```
globalAlpha                绘图的当前 alpha 或透明值
globalCompositeOperation   新图像如何绘制到已有的图像上
```

## 其他方法
```
save()           保存当前状态
restore()        返回之前保存状态
createEvent()
getContext()
toDataURL()
``` -->
