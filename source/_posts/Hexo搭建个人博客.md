---
title: Hexo配置
date: 2016-10-8 11:16:16
tags: '配置'
description: Hexo 是一个简单地、轻量地、基于Node的一个静态博客框架，可以方便的生成静态网页托管在github和Heroku上，引用Hexo作者 @tommy351 的话：快速、简单且功能强大的 Node.js 博客框架。A fast, simple & powerful blog framework, powered by Node.js.
photos: http://oizt3fjv8.bkt.clouddn.com/hexo.png
---
## Hexo简介
> [hexo](https://github.com/hexojs/hexo) 是一款基于Node.js的静态博客框架。
> 中文文档：    [https://hexo.io/zh-cn/docs/configuration.html](https://hexo.io/zh-cn/docs/configuration.html)



## 常用命令
```
hexo new "postName"      #新建文章
hexo new page "pageName" #新建页面
hexo generate            #生成静态页面至public目录
hexo server              #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy              #将.deploy目录部署到GitHub
hexo help                #查看帮助
hexo version             #查看Hexo的版本
```

## 部署
修改_config.yml文件
```
deploy:
  type: git
  repository: https://github.com/username/username.github.io.git
  branch: master
```
