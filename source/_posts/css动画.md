---
title: css动画
date: 2017-02-08T11:05:15.000Z
updated: 2017-02-08T11:05:15.000Z
tags:
  - css
description: css实现一些特殊的动画效果。
photos: 'http://oizt3fjv8.bkt.clouddn.com/css_no9.png'
---

# [打字动画](http://play.csssecrets.io/typing)
实现：

```css
@keyframes typing {
    from { width: 0 }
}

@keyframes caret {
    50% { border-right-color: transparent; }
}

h1{
    width: 15ch;
    white-space: nowrap;
    overflow: hidden;
    border-right: .05em solid;
    animation: typing 8s steps(15),
               caret 1s steps(1) infinite;
}
```

```html
<h1>CSS is awesome!</h1>
```

## [环形旋转动画](http://play.csssecrets.io/circular)
实现：

```css
@keyframes spin {
    from {
        transform: rotate(0turn)
                   translateY(-150px) translateY(50%)
                   rotate(1turn)
    }
    to {
        transform: rotate(1turn)
                   translateY(-150px) translateY(50%)
                   rotate(0turn);
    }
}

.item {
    animation: spin 3s infinite linear;
}

.item {
    display: block;
    width: 50px;
    margin: calc(50% - 25px) auto 0;
    border-radius: 50%;
    overflow: hidden;
}

.box {
    width: 300px;
    height: 300px;
    padding: 20px;
    border-radius: 50%;
    background: #fb3;
}
```

```html
<div class="box">
  <img src='http://lea.verou.me/book/adamcatlace.jpg' class="item">
</div>
```
