---
title: vue问题总结
date: 2017-1-18 10:12:14
updated: 2017-1-18 10:12:14
tags: ['vue', '问题']
description: 积累vue平时犯的错误。
photos: http://oizt3fjv8.bkt.clouddn.com/vue_no3.jpg
---

## 前端进行用户身份验证

解决方法：用户登录成功在 sessionStorage 中保存用户信息，在 router.beforeEach()方法中验证 sessionStorage 是否存在用户信息，如不存在跳转到登录页面，另外不合法的路由也定位到登录页面：`{path: '*', redirect: '/Login'}`

##　跨域调后台方法
解决方法：

1. webpack 配置文件中配置 node 服务的反向代理：

```javascript
devServer: {
  proxy: {
    '/api/*': {
        target: 'http://api.chinaeid.cn',
        secure: false,
    }
  },
},
```

2. 服务器设置 cors 允许跨域请求：

```java
response.addHeader("Access-Control-Allow-Origin", "*");
 response.addHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
 response.addHeader("Access-Control-Allow-Headers", "Content-Type");
// response.addHeader("Access-Control-Allow-Credentials", "true");
 response.addHeader("Access-Control-Max-Age", "1800");//30 min
```

## 数据循环绑定时数据的格式化

解决方法：注册过滤器
注册全局过滤器：`Object.keys(filters).forEach(k => Vue.filter(k, filters[k]))`
注册组件局部过滤器：`filters: { fun(val){} }`

## vuex 刷新页面数据丢失

解决方法：将数据保存在 sessionStorage 或者 localStorage 中进行中转

## 解决 ajax 异步问题，保证数据获取到在执行其他相关函数

解决方法：返回 Promise 对象，再用 then()方法执行其他操作

```javascript
return new Promise((resolve, reject) => {
  $.ajax({
    type: 'GET',
    url: '/api/focus/get/type',
    data: {},
    dataType: 'json'
  })
    .done(data => {
      resolve(data) //成功
    })
    .fail(err => {
      reject(err) //失败
    })
})
```
