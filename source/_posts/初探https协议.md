---
title: 初探https协议
date: 2017-02-16 17:13:33
tags: ["http"]
description: HTTPS（全称：Hyper Text Transfer Protocol over Secure Socket Layer），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。
photos: http://oizt3fjv8.bkt.clouddn.com/https.jpg
---
**http协议之上加入TLS或SSL协议形成https**
如下图所示：
![](http://oizt3fjv8.bkt.clouddn.com/https_no1.jpg)

## HTTP与HTTPS的区别

区别            |HTTP      |HTTPS
------------|-------- |----------
ca申请证书   |不需要   |需要
信息传输方式 |明文传输  |ssl加密传输
端口         |80      |443
链接方式     |无状态   |加密传输、身份认证

## HTTPS开发注意事项
1. HTTPS网站不允许调用HTTP网站上的资源
2. HTTPS无法调用HTTP服务器的接口
3. 资源引入换为使用相对协议，如`//ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.js`
