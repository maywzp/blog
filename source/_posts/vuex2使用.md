---
title: vuex2使用
date: 2016-11-20T09:12:51.000Z
updated: 2016-11-20T09:12:51.000Z
tags:
  - vue
description: 'Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态,并以相应的规则保证状态以一种可预测的方式发生变化。'
photos: 'http://oizt3fjv8.bkt.clouddn.com/vuex.jpg'
---

# 四大要素

```bash
State（定义数据）
Mutations（同步操作，改变state数据）
Actions（异步操作，触发mutation）
Getters（数据格式处理，返回所需数据）
```

# 引入 vuex

```javascript
import Vue from 'vue'
import Vuex from 'vuex'
import * as getters from './getters'
import * as actions from './actions'
Vue.use(Vuex)
```

# 使用 vuex

Computed 计算属性里引入 getters 中的数据 Methods 中引入 actions 中的方法

```javascript
import { mapGetters, mapActions } from 'vuex'
mounted(){
  this.fetchBooks()
  let books = this.books
},
computed: {
  ...mapGetters([
    'books',
  ])
},
 methods: {
  ...mapActions([
    'fetchBooks',
  ]),
}
```
