---
title: wireshark抓包工具的使用
date: 2017-02-15 15:20:18
tags: ['http']
description: wireshark是非常流行的网络封包分析软件，功能十分强大。可以截取各种网络封包，显示网络封包的详细信息。
photos: http://oizt3fjv8.bkt.clouddn.com/wireshark.jpg
---

## Wireshark抓包窗口显示模块
```bash
过滤器区（Display Filter）: 过滤条件
封包列表区（Packet List Pane）: 显示捕获的包
封包详情区（Packet Detail Pane）：显示封包中的字段
16进制数据区（Dissector Pane）: 显示16进制数据
地址栏（Miscellaneous）：地址栏，杂项
```
![](http://oizt3fjv8.bkt.clouddn.com/wireshark_no1.jpg)

## 过滤器的使用
过滤器可通过`Save`按钮保存
多条过滤条件：`and`连接
常用过滤条件：
```bash
//ip过滤
源ip：  ip.src == 192.168.1.155
目的ip: ip.dst == 180.163.251.208

//端口过滤
端口：    tcp.port == 8080
源端口：  tcp.srcport == 8080
目的端口：tcp.dstport == 8080

//协议过滤
直接写协议： http

//请求方式过滤
GET请求：  http.request.method == "GET"
POST请求： http.request.method == "POST"
```

##  封包列表显示信息
```bash
No              编号          
Time            时间戳
Source          源地址
Destination     目标地址
Protocol        协议
Length          长度
Info            封包信息
```

## 封包详情信息
```bash
Frame                           物理层的数据帧概况
Ethernet II                     数据链路层以太网帧头部信息
Internet Protocol Version 4     网络层IP包头部信息
Transmission Control Protocol   传输层数据段头部信息
Hypertext Transfer Protocol     应用层的信息
```
wireshark与对应的OSI七层模型:
![](http://oizt3fjv8.bkt.clouddn.com/wireshark_no2.png)
wireshark捕获到的TCP信息
![](http://oizt3fjv8.bkt.clouddn.com/wireshark_no3.png)
