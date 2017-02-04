---
title: css问题记录
date: 2017-1-24 09:19:45
tags: ['css', '问题']
description: 积累css平时犯的错误。
photos: http://oizt3fjv8.bkt.clouddn.com/css.jpg
---

## 清除相邻行内元素之间的空隙
解决方法：
1. 浮动：float
2. 改变表现形式：display: inline-block
3. 取消元素之间的空格（有些元素不起作用）

## 手机端flex布局不能换行
解决方法：目前只能将父元素换为display:block,子元素浮动来解决

## 设置的按钮样式在手机浏览器不起作用
解决方法：取消webkit内核浏览器按钮自带样式：
`input[type="button"], input[type="submit"], input[type="reset"] {-webkit-appearance: none;}`

## Firefox浏览器按钮文字不居中
解决方法：取消mozilla内核按钮的内边距和边框
`input[type="reset"]::-moz-focus-inner,
input[type="button"]::-moz-focus-inner,
input[type="submit"]::-moz-focus-inner,
input[type="file"] > input[type="button"]::-moz-focus-inner{border:none;padding:0;}`
