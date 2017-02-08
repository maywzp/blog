---
title: css效果-文字
date: 2016-10-19T11:05:15.000Z
tags:
  - css
description: css实现一些特殊的文字效果。
photos: 'http://oizt3fjv8.bkt.clouddn.com/css_no6.jpg'
---

## [凸版印刷效果](http://play.csssecrets.io/letterpress)
知识点：`text-shadow` 实现：

```
background: hsl(210, 13%, 30%);
color: hsl(210, 13%, 60%);
text-shadow: 0 -1px 1px black;
```

## [空心文字](http://play.csssecrets.io/stroked-text)
实现：

```
text-shadow: 1px 1px black,
            -1px -1px black,
            1px -1px black,
            -1px 1px black;
```

## [文字发光](http://play.csssecrets.io/glow)

```css
a{
  color: #ffc;
  text-decoration: none;
  transition: 1s;
}
a:hover {
  text-shadow: 0 0 0.1em, 0 0 0.3em;
}
```

## [文字凸起](http://play.csssecrets.io/extruded)
实现：
```
text-shadow: 0 1px hsl(0,0%,85%),
             0 2px hsl(0,0%,80%),
             0 3px hsl(0,0%,75%),
             0 4px hsl(0,0%,70%),
             0 5px hsl(0,0%,65%),
             0 5px 10px black;
```
