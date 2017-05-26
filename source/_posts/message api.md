---
title: Message API
date: 2017-05-26 10:47:28
tags: ['javascript']
description: Web Workers 为 Web 前端网页上的脚本提供了一种能在后台进程中运行的方法。一旦它被创建，Web Workers 就可以通过 postMessage 向任务池发送任务请求，执行完之后再通过 postMessage 返回消息给创建者指定的事件处理程序 ( 通过 onmessage 进行捕获 )。
photos: http://oizt3fjv8.bkt.clouddn.com/message_api.jpg
---

## 使用
```javascript
const sourceDomain = 'http://a.cn'
const targetDomain = 'http://b.cn'

// a.cn
const poper = window.open(targetDomain)

// TODO 周期性的发送消息
setInterval(function() {
  poper.postMessage({ message: 'I am a' }, targetDomain)
}, 6000)

// TODO 监听消息反馈
window.addEventListener('message', function(event) {
  if(event.origin !== targetDomain) return
  const mes = event.data
  return mes
}, false)


// b.cn
window.addEventListener('message', function(event) {
  if(event.origin !== sourceDomain) return
  const mes = event.data
  event.source.postMessage({ message: 'I am b' }, event.origin)
  return mes
},false)
```