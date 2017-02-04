---
title: node环境配置
date: 2016-12-02
tags: ['node', '配置']
description: windows和CentOS node环境配置
photos: http://oizt3fjv8.bkt.clouddn.com/nodeno2.jpg
---
## Windows安装node

1. node中文官网下载msi安装包 http://nodejs.cn/
2. 双击安装，默认安装路径即可
3. 默认安装位置 C:\Program Files\nodejs
4. 安装完成运行node -v即可查看node版本号
5. 安装的Node已集成npm，无需额外下载，更换淘宝镜像，加快npm包下载速度：
```bash
npm config set registry https://registry.npm.taobao.org
npm info underscore （如果上面配置正确这个命令会有字符串response）
```
6. 安装常用模块express：`npm install express -g`


## CentOS安装node
1. 获取node：`curl --silent --location https://rpm.nodesource.com/setup_4.x | bash -`
2. 安装node：`yun install -y nodejs`
3. 安装npm：`yun install npm`
4. 更新node：
安装n模块：`npm install -g n`
更新版本：n 4.4.3 或 n stable更新到最新稳定版
**注：用n模板更新node由于不是国内的服务器更新容易中断，最好搭建vpn，此外中断失败会导致node不能用，先使用 n - 4.4.3 命令去除安装的版本重新安装**

## 安装node插件
### 安装pm2（让node程序在服务器上一直运行）
```bash
npm -g install pm2
pm2 start server.js
```
