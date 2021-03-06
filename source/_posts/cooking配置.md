---
title: cooking配置
date: 2016-12-25
updated: 2016-12-25
tags: ['自动化工具', '配置']
---

cooking 是一个基于 webpack 但是提供更简单的配置项，同时内置了许多常用配置的构建工具。

## 安装

Webpack 配置较繁琐，实际项目中使用 cooking npm 来搭建项目环境
参考手册：[http://cookingjs.github.io/zh-cn/intro.html](http://cookingjs.github.io/zh-cn/intro.html)
安装：`npm i cooking-cli -g`
创建 vue 项目：`npm init vue`
执行项目：`cooking watch`
生产环境代码构建：`cooking build`

## cooking.config.js 文件配置

### 配置多文件入口

```javascript
entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
template: [{
  filename: 'index.html',
  template: 'src/index.tpl',
  chunks: ['index', 'vendor', 'manifest']
}, {
  filename: 'search.html',
  template: 'src/search.tpl',
  chunks: ['search', 'vendor', 'manifest']
}],
```

### 配置 host

```javascript
devServer: {
   hostname: '192.168.1.155', （换为本地IP）
   port: 2001,
   protocol: 'http:',
}
```

### 配置 postcss、less、lint

```javascript
postcss: [
   require('autoprefixer')
 ],
extends: ['vue', 'lint', 'less', 'autoprefixer']
```

### 全局 jQuery

```javascript
cooking.add(
  'plugins.Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    'window.jQuery': 'jquery'
  })
)
```

### 添加 loader

```javascript
cooking.add('loader.file', {
  test: /\.swf$/,
  loaders: ['file?name=[path][name].[ext]']
})
```
