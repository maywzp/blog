---
title: css效果-背景与边框
date: 2016-10-15T11:05:15.000Z
tags:
  - css
description: css实现一些特殊的背景及边框效果。
photos: 'http://oizt3fjv8.bkt.clouddn.com/css_no4.jpg'
---

# [半透明边框](http://play.csssecrets.io/translucent-borders)
知识点：

```bash
background-clip(规定背景的绘制区域)：
  border-box    背景被裁剪到边框盒。
  padding-box    背景被裁剪到内边距框。
  content-box    背景被裁剪到内容框。
```

实现：

```
border: 12px solid rgba(0,0,0,0.5);
background: white;
background-clip: padding-box;
```

# [多重边框](http://play.csssecrets.io/multiple-borders)
知识点： `box-shadow实现多重阴影。` `outline实现两层边框`
实现：
方案一

```
background: yellowgreen;
box-shadow: 0 0 0 10px #655,
          0 0 0 15px deeppink,
          0 2px 5px 15px rgba(0,0,0,.6);
```

方案二

```
outline: 5px solid deeppink;
```

# [灵活的背景定位](http://play.csssecrets.io/)
知识点： `background-position指定偏移量`

```bash
background-origin相对于什么位置来定位:
  padding-box    背景图像相对于内边距框来定位。
  border-box    背景图像相对于边框盒来定位。
  content-box    背景图像相对于内容框来定位。

calc()的运算:
  使用“+”、“-”、“*” 和 “/”四则运算
  可以使用百分比、px、em、rem等单位
  可以混合使用各种单位进行计算
```

实现：
方案一

```
background:url('xx') no-repeat bottom right #58a;
background-position: right 20px bottom 10px;
```

方案二

```
padding: 10px 20px;
background:url('xx') no-repeat bottom right #58a;
background-origin: content-box;
```

方案三

```
background:url('xx') no-repeat #58a;
background-position: calc(100% - 20px) calc(100% - 10px);
```

# [边框内圆角](http://play.csssecrets.io/inner-rounding)
知识点： `box-shadow、outline多重边框`
实现：

```
outline: 6px solid #655;
box-shadow: 0 0 0 4px #655;
border-radius: 8px;
background: tan;
```

# 背景条纹
知识点：`css渐变、background-size`

## [水平条纹](http://play.csssecrets.io/horizontal-stripes)
实现：

```
//两条条纹
background: linear-gradient(#fb3 50%, #58a 0); //一样高的条纹
background-size: 100% 30px; //条纹高度为15px

//三条条纹
background: linear-gradient(#fb3 33.3%,#ff0 0,#ff0 66.6%,#58a 0);
background-size: 100% 30px;
```

## [垂直条纹](http://play.csssecrets.io/vertical-stripes)
实现：

```
background: linear-gradient(to right, #fb3 50%, #58a 0);//一样宽的条纹
background-size:30px 100%; //条纹宽度为15px
```

## [斜向条纹](http://play.csssecrets.io/diagonal-stripes)
实现：
普通：

```
background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
background-size:42px 42px; //斜向条纹宽度为15px,背景大小：2*15/cos45°=42
```

增强版：

```
//创建重复的线性渐变
background: repeating-linear-gradient(45deg, #fb3 0, #fb3 25%, #58a 0, #58a 50%);
background-size:42px 42px;
```

## [毛玻璃效果](http://play.csssecrets.io/frosted-glass)
实现：

```css
body, .box::before {
    background: url("http://csssecrets.io/images/tiger.jpg") 0 / cover fixed;
}
.box{
    position: relative;
    background: hsla(0,0%,100%,.25) border-box;
    overflow: hidden;
    border-radius: .3em;
    box-shadow: 0 0 0 1px hsla(0,0%,100%,.3) inset,
                0 .5em 1em rgba(0, 0, 0, 0.6);
    text-shadow: 0 1px 1px hsla(0,0%,100%,.3);
}
.box::before {
    content: '';
    position: absolute;
    top: 0; right: 0; bottom: 0; left: 0;
    margin: -30px;
    z-index: -1;
    -webkit-filter: blur(20px);
    filter: blur(20px);
}
```

# [折角效果](http://play.csssecrets.io/folded-corner-realistic)
实现：

```css
.box{
    position: relative;
    background: #58a;
    background: linear-gradient(-150deg, transparent 1.5em, #58a 0);
    border-radius: .5em;
}

.box::before {
    content: '';
    position: absolute;
    top: 0; right: 0;
    width: 1.73em; height: 3em;
    background: linear-gradient(to left bottom, transparent 50%, rgba(0,0,0,.2) 0, rgba(0,0,0,.4)) 100% 0 no-repeat;
    transform: translateY(-1.3em) rotate(-30deg);
    transform-origin: bottom right;
    border-bottom-left-radius: .5em;
    box-shadow: -.2em .2em .3em -.1em rgba(0,0,0,.15)
}
```

minxin

```less
@mixin folded-corner($background, $size, $angle: 30deg) {
  position: relative;
  background: $background;
  background: linear-gradient($angle - 180deg, transparent $size, $background 0);
  border-radius: .5em;

  $x: $size / sin($angle);
  $y: $size / cos($angle);

  &::before {
      content: '';
      position: absolute;
      top: 0; right: 0;
      background: linear-gradient(to left bottom, transparent 50%, rgba(0,0,0,.2) 0, rgba(0,0,0,.4)) 100% 0 no-repeat;
      width: $y;
      height: $x;
      transform: translateY($y - $x) rotate(2*$angle - 90deg);
    transform-origin: bottom right;
      border-bottom-left-radius: inherit;
      box-shadow: -.2em .2em .3em -.1em rgba(0,0,0,.15);
  }
}

//调用
.box{
  @include(folded-corner(#58a, 2em, 40deg));
}
```

## [蒙版](http://play.csssecrets.io/dimming-box-shadow)
知识点：`通过box-shadow添加蒙版`
实现：

```css
.modal{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate3d(-50%, -50%, 0);
  filter: blur(3px); /*弱化背景，不需要可以删除*/
  box-shadow: 0 0.2em 0.5em rgba(0, 0, 0, 0.55), 0 0 0 50vmax rgba(0,0,0,.8);
}
```
