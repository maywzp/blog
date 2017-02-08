---
title: css效果-变形
date: 2016-10-16 11:05:15
tags: ['css']
description: css元素变形。
photos: http://oizt3fjv8.bkt.clouddn.com/css_no5.jpg
---

## 功能
1. 旋转
transform:rotate(45deg);
![](http://www.wzsky.net/img/uploadimg/20120312/1008380.png)

2. 缩放
transform:scale(0.8, 1);

3. 倾斜
transform:skew(30deg, 0deg);
![](http://www.wzsky.net/img/uploadimg/20120312/1008382.png)

4. 移动
translate(50px, 50px);
![](http://www.wzsky.net/img/uploadimg/20120312/1008383.png)

5. 指定变形的基准点
transorm-origin:left bottom;
![](http://www.wzsky.net/img/uploadimg/20120312/1008384.png)

## 3D变换
### 3D旋转
rotateX()：以方框X轴，从下向上旋转
![](http://images0.cnblogs.com/blog/707050/201507/112302140801561.jpg)
rotateY()：以方框y轴，从左向右旋转
![](http://images0.cnblogs.com/blog/707050/201507/112302149394133.jpg)
rotateZ()：以方框中心为原点，顺时针旋转
![](http://images0.cnblogs.com/blog/707050/201507/112302154554574.jpg)

x：是一个0到１之间的数值，主要用来描述元素围绕X轴旋转的矢量值；
y：是一个０到１之间的数值，主要用来描述元素围绕Y轴旋转的矢量值；
z：是一个０到１之间的数值，主要用来描述元素围绕Z轴旋转的矢量值；
a：是一个角度值，主要用来指定元素在3D空间旋转的角度，如果其值为正值，元素顺时针旋转，反之元素逆时针旋转。

下面介绍的三个旋转函数功能等同：
rotateX(a)函数功能等同于rotate3d(1,0,0,a)
rotateY(a)函数功能等同于rotate3d(0,1,0,a)
rotateZ(a)函数功能等同于rotate3d(0,0,1,a)

### 3D效果详解
参考资料：[张金鑫-CSS3 3D transform变换](http://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/)
perspective（透视，视角）：值为0就在屏幕前，值越大距离屏幕焦点越远。
translateZ(让元素在自己的眼前或近或远)：translateZ值越小，则元素大小越小（因为元素远去，我们眼睛看到的就会变小）；translateZ值越大，该元素也会越来越大，当translateZ值非常接近perspective的值时，该元素的大小就会撑满整个屏幕，超过perspective值的时候，该元素看不见了--我们是看不见眼睛后面的东西的！
[demo](http://www.zhangxinxu.com/study/201209/transform-perspective-translateZ.html)
perspective-origin:改变3D焦点位置
transform-style: preserve-3d  子元素根据焦点展示不同的3D效果
[3D效果的应用-旋转木马效果](http://www.zhangxinxu.com/study/201209/pictures-3d-slide-view.html)

## [变形](http://play.csssecrets.io/parallelograms-pseudo)
任意变形一个元素而不改变它的内容
知识点：`将其伪元素变形`
实现：
```css
.box{
  position: relative;
  border: 0;
  background: transparent;
}

.box::before {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -1;
    background: #58a;
    transform: skew(45deg);
}
```

## [菱形的实现](http://play.csssecrets.io/diamond-clip)
知识点：`clip-path裁剪`

实现
```css
img{
  -webkit-clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
}

img:hover {
	-webkit-clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
	clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```

## [梯形的实现](http://play.csssecrets.io/trapezoid-tabs)
知识点：`3D效果`
```css
.box{
   position: relative;
}
.box::before{
  content: '';
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -1;
    border-radius: .5em .5em 0 0;
    box-shadow: 0 0.15em white inset;
    transform: scale(1.1, 1.3) perspective(.5em) rotateX(5deg);
    transform-origin: bottom;
}
```
