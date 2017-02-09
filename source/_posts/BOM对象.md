---
title: JavaScript BOM对象
date: 2017-1-11T11:05:15.000Z
tags:
  - javascript
description: BOM(Browser Object Model) 是指浏览器对象模型，是用于描述这种对象与对象之间层次关系的模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。
photos: 'http://oizt3fjv8.bkt.clouddn.com/bom.png'
---

## 全局对象
```bash
window     当前窗口，如果文档包含框架（frame 或 iframe 标签），浏览器会为 HTML 文档创建一个 window 对象，并为每个框架创建一个额外的 window 对象。
top        最顶层浏览器窗口
parent     当前窗口的父窗口
self       当前窗口,等价于window
```

## 窗口位置
```
screen.width   浏览器屏幕宽度
screen.height  浏览器屏幕高度

pageXOffset    滚动条距离左边的位置
pageYOffset    滚动条距离顶部的位置

scrollTo(w, h) 滚动到那个位置
```
