---
title: vue2常用代码
date: 2016-11-18T16:44:28.000Z
updated: 2016-11-18T16:44:28.000Z
tags:
  - vue
description: 'Vue.js是当下很火的一个JavaScript MVVM库,它是以数据驱动和组件化的思想构建的。'
photos: 'http://oizt3fjv8.bkt.clouddn.com/vue_no2.jpg'
---

# 绑定 class

## 单个 class

```javascript
<div :class="{active: isActive}"></div>
```

## 多个 class

```javascript
<div :class="{active: isActive, 'text-danger': hasError}"></div>
```

## 绑定一个 class 对象

```javascript
<div :class="classObj"></div>
data: {
    classObj: {
        active: true,
        'text-danger': false
    }
}
```

## 结合计算属性，创造更强大的绑定

```javascript
<div :class="classObj"></div>
data: {
    isActive: true,
    error: null
},
computed: {
    classObj: function(){
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error && this.error.type === 'fatal',
      }
    }
}
```

# 绑定 style

## 直接绑定

```javascript
<div :style="{color: '#ccc', fontSize: baseSize + 'px'}"></div>
```

## 绑定一个 style 对象

```javascript
<div :style="styleObj"></dvi>
data: {
    styleObj: {
      color: '#ccc',
      fontSize: '14px'
    }
}
```

**注：通过 vue 绑定的 style 会自动添加响应的前缀**

# tab 标签切换

```javascript
v-for="(item, index) of items"
:class="{'current-tab':iscur == index}" @click="iscur = index"
v-show="iscur == index? true: false"
```

# 多事件绑定

```html
<div v-on="click: onClick, keyup: onKeyup, keydown: onKeydown"></div>
```

# v-if 切换多个元素

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

# v-for 迭代

## 数组

```html
<li v-for="(item, index) in items">{{ index }} - {{ item.message }}</li>
```

## 对象

```html
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }} : {{ value }}
</div>
```

## 渲染多个元素

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```

# 排序

```html
<li v-for="user in users | orderBy 'name'">//按名字排序用户</li>
<li v-for="user in users | orderBy 'name' -1">//降序</li>
<li v-for="user in users | orderBy 'lastName' 'firstName'">
  //使用两个键名排序
  <button @click="order = order * -1">Reverse Sort Order</button>
</li>

<li v-for="user in users | orderBy 'name' order">//动态排序</li>
```

# filter(过滤器)

```javascript
{
  {
    msg | capitalize
  }
} //过滤器函数第一个参数为表达式

new Vue({
  filters: {
    capitalize: function(value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
```

# 命令修饰符

```bash
.prevent  （阻止默认事件）
.stop     （阻止事件冒泡）
.capture  （时间捕获模式）
.self     （元素本身触发）
```

# v-model 修饰符

```javascript
v-model.lazy   （数值改变才执行，change事件中同步）
v-model.number （转化为number类型）
v-model.trim   （去掉首尾空格）
```
