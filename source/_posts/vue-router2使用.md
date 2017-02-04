---
title: vue-router2使用
date: 2016-11-19 10:47:15
tags: ['vue']
description: vue-router是vue.js官方的路由插件,它和vue.js是深度集成的,适合用于构建单页面应用。
photos: http://oizt3fjv8.bkt.clouddn.com/vue-router.png
---

## 定义路由（routes.js）
路由懒加载
```javascript
const Login = resolve => require(['./pages/login.vue'], resolve)

export const routes = [
  {path: '/', name: '登录', component: Login},
]
```
子路由
```javascript
{path: '/main', name: '主页面', component: Main,
  children: [
    {path: '/', name: '', component: NewsList},
    {path: 'newsList', name: '新闻列表', component: NewsList},
    {path: 'newsAdd', name: '添加新闻', component: NewsAdd},
    {path: 'newsAdd/:id', name: '添加新闻', component: NewsAdd},
  ]
}
```

## 引入vue-router（main.js）
```javascript
import Vue from 'vue'
import { routes } from './routes'
import VueRouter from 'vue-router'
Vue.use(VueRouter)
```
## 使用vue-router
```javascript
<router-link to='/'></router-link>
Js跳转：this.$router.push({path: '/' });
```
