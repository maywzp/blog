---
title: http入门解析
date: 2017-02-15 13:47:28
updated: 2017-02-15 13:47:28
tags: ['http']
---

超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的 WWW 文件都必须遵守这个标准。设计 HTTP 最初的目的是为了提供一种发布和接收 HTML 页面的方法。1960 年美国人 Ted Nelson 构思了一种通过计算机处理文本信息的方法，并称之为超文本（hypertext）,这成为了 HTTP 超文本传输协议标准架构的发展根基。

## 网络模型分成

OSI 模型分为七层

```bash
物理层             将数据转换为可通过物理介质传送的电子信号
数据链路层          数据分帧，并处理流控制
网络层             寻址和路由管理
传输层             建立主机端到端的链接
会话层             建立、维护和管理会话
表示层             处理数据格式、数据加密
应用层             提供应用程序间通信
```

TCP/IP 模型分为四层

```bash
网络接口层         负责监视数据在主机和网络之间的交换
网际交互层         解决主机到主机的通信问题
传输层             为应用层实体提供端到端的通信功能
应用层             为用户提供所需要的各种服务
```

图文展示：
![](http://oizt3fjv8.bkt.clouddn.com/http_no1.png)

## http 发展历史

1991 年，HTTP/0.9 版本（最早的版本）：只有一个`GET`命名，服务器只能返回 HTML 格式的字符串；
1996 年 5 月，HTTP/1.0 版本，内容大大增加，引入`POST`和`HEAD`命令，HTTP 请求和回应的格式发生变化；
1997 年 1 月，HTTP/1.1 版本，引入持久连接，TCP 连接默认不会关闭，可以被多个请求复用；引入管道机制，同一个 TCP 连接里面，客户端可以同时发送多个请求；增加`PUT`、`PATCH`、`HEAD`、 `OPTIONS`、`DELETE`方法；
2015 年，HTTP/2 版本发布，同一个连接的多个请求或回应不用按照顺序对应；引入头信息压缩机制，避免带宽的浪费；服务器可以推送消息。
**HTTP 协议采用 TCP/IP 模型**
![](http://oizt3fjv8.bkt.clouddn.com/tcpip.jpg)

## 通用 http 头部信息

Cache-Control(缓存),值:

```bash
public          所有内容都将被缓存(客户端和代理服务器都可缓存)
private         内容只缓存到私有缓存中(仅客户端可以缓存，代理服务器不可缓存)
no-cache        响应消息不能缓存
no-store        请求和响应消息都不使用缓存
max-age         缓存的内容将在 xxx 秒后失效
```

Date(消息发送的时间)
Pragma(特殊指令)，常用值：`no-cache`
Connection(连接状态)，常用值：`close(关闭)`、`keep-alive(保持连接)`
Transfer-Encoding()
Expires(缓存失效时间)，优先级较高

## http 请求头部信息

Host(主机头)
Referer(源资源地址)
User-Agent(用户信息)
Accept(客户端接受信息类型)，MIME 类型，`/`表示任何类型
Accept-Charset(接受的字符集)
Accept-Encoding(接受的内容编码)
Accept-Language(接收的语言)
Authorization(权限验证)
If-Modified-Since(文档之前一次被修改的时间)
Cookie(缓存)
If-None-Match(判断请求资源是否改变)

## http 响应头部信息

Allow(允许请求的方法)
Content-Encoding(文档编码方式)
Content-Length(内容长度)
Content-Type(内容类型),MIME 类型
Last-Modified(文档最后被修改的时间)
Refresh(多久刷新页面)
Server(服务器名)

## http 请求方法

```bash
GET             获取
POST            更新
PUT             创建
DELETE          删除
HEAD            获取报头
OPTIONS         返回服务器针支持的HTTP请求方法，查看服务器的性能
CONNECT         代理服务器使用
TRACE           回显服务器收到的请求，用于测试
```
