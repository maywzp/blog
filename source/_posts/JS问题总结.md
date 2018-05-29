---
title: JS问题总结
date: 2017-1-06 14:15:32
updated: 2017-1-06 14:15:32
tags: ['javascript', '问题']
description: 积累JavaScript平时犯的错误。
photos: http://oizt3fjv8.bkt.clouddn.com/javascript_no4.jpg
---

## ajax方法错误常见问题
### 后台接收参数为乱码
解决方法1：ajax方法加入头部信息：
`headers : {'Content-Type': 'application/json;charset=utf-8'}`
### 状态值为200,（方法已调通），但仍然进入error函数
解决方法：指定返回值类型，
返回string： dataType: ‘string’
返回JSON： dataType: ‘json’
### 中文乱码解决方案
解决方法：
加码(必须套两层)。
`login_name = encodeURI(encodeURI(login_name));  `
解码
`js:   loginName = decodeURI(decodeURI(loginName));`
`Java：loginName = java.net.URLDecoder.decode(loginName,"UTF-8");`

## 图片上传常见错误
### enctype错误
解决方案：设置enctype：`enctype="multipart/form-data"`
### 后端接收值为空
解决方案：input的name值与后台接收参数值不匹配


## 表单提交常见问题
### 点击按钮直接提交表单而不进入ajax方法
解决方案：阻止按钮的默认事件：`e.preventDefault()`
### 防止表单反复提交
解决方案：提交完表单后，禁用提交按钮
