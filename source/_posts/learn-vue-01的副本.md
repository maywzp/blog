---
title: learn-vue-01
date: 2018-05-30 16:35:51
update: 2018-05-30 16:35:51
tags: vue
description: 深入学习 Vue.js 第一步，学习 Object.defineProperty。Vue.js 的响应原理依赖于 Object.defineProperty，所以 Vue 不支持 IE8 及更低版本浏览器。Vue 通过设置对象的 setter/getter 方法，来监听数据的变化，通过 getter 进行依赖收集，而每个 setter 方法就是一个观察者，在数据变更时通知订阅者更新视图。
---

### 了解 Object.defineProperty API

首先，我们应该了解一下 `JS` 中的一个 `API`：

[Object.defineProperty(object, propertyname, descriptor) ](https://msdn.microsoft.com/zh-cn/library/dd548687(v=vs.94).aspx)

该方法的作用：**将属性添加到对象，或者修改现有属性的特性**

通常情况下，我们添加一个属性在对象上会这样写：

```javascript
const obj = {}
obj.name = 'jack'
```

`Object.defineProperty` 也同样能做到：

```javascript
// 使用 Object.defineProperty 增加属性
const obj = {}
let name = 'jack'
Object.defineProperty(obj, 'name', {
  configurable: true, // 该属性是否可修改，默认值：false
  enumerable: true, // 该属性是否能遍历，默认值：false
  get() {
    return name
  },
  set(newValue) {
    name = newValue
  }
})
```

这样做虽然增加了代码量，但却可以控制对象属性的读取值，执行上面代码：

```javascript
obj.name
// jack

obj.name = 'ross'
// ross
```

### 封装 defineProperty 函数

对 `Object.defineProperty`进行封装，方便调用：

```javascript
// defineProperty 函数封装
const callback = {
  target: null
}

const defineProperty = function(object, key, value, cb) {
  let array = []
  Object.defineProperty(object, key, {
    configurable: true,
    enumerable: true,
    get() {
      // 依赖收集
      if (callback.target) {
        array.push(callback.target)
      }
      return value
    },
    set(newValue) {
      if (newValue !== value) {
        // 触发事件
        array.forEach(func => func(newValue, value))
      }
      value = newValue
    }
  })
}
```

`defineProperty`函数简陋的实现了Vue里的响应式原理，即在`get`方法中收集依赖，在`set`方法中触发依赖，更新视图。

`defineProperty`函数的调用：

```javascript
const obj = {}
defineProperty(obj, 'name', 'jack')

callback.target = (newValue, oldValue) => console.log('第一个依赖函数，新值为：' + newValue)
obj.name
// jack

callback.target = (newValue, oldValue) => console.log('第二个依赖函数，新值为：' + newValue)
obj.name = 'ross'
obj.name
// 第一个依赖函数，新值为：ross
// ross

obj.name = 'titanic'
obj.name
// 第一个依赖函数，新值为：titanic
// 第二个依赖函数，新值为：titanic
// titanic
```

添加的依赖函数，将在`Object.defineProperty`的`get`方法中被收集，所以在调用`obj.name`时会将新的依赖添加到依赖数组里，在调用`obj.name = xx` 时会触发依赖列表。

### Vue 中将 data 变为可观察 (observable) 的

下面的代码简单的说明了如何把 data 的属性转化为可观察的。

```javascript
const observable = (obj, cb) => {
  Object.keys(obj).forEach(k => defineReactive(obj, k, obj[k], cb))
}

const defineReactive = (obj, key, val, cb) => {
  Object.defineProperty(obj, key, {
    configurable: true,
    enumerable: true,
    get() {
      // 依赖收集
    },
    set(newValue) {
      // 通知订阅者触发视图更新
      cb()
    }
  })
}

class Vue {
  constructor(ops) {
    this._data = ops.data
    observable(this._data, ops.render)
  }
}

const app = new Vue({
  el: '#app',
  data: {
    name: 'jack'
  },
  render() {
    console.log('视图更新')
  }
})
```

此时要触发视图的更新（`set` 方法），需要使用`app._data.name`，但为了简便易懂，我们更希望使用 `app.name`这样的方式直接触发`set`对视图进行重绘，那么我们就需要用到代理。

### 代理

代理函数，将 data 里的属性移植到 vue实例中去，采用 app.name 这种方式触发 set，而非 app._data.name

```javascript
function _proxy(data) {
  const that = this
  Object.keys(data).forEach(key => {
    Object.defineProperty(that, key, {
      configurable: true,
      enumerable: true,
      get: function proxyGetter() {
        return that._data[key]
      },
      set: function proxySetter(newValue) {
        that._data[key] = newValue
      }
    })
  })
}
```

在 `class Vue` 的 `constructor`中使用`_proxy(ops.data)`，完成代理即可使用 `app.name` 触发 `set` 更新视图。

[查看相关代码](https://github.com/maywzp/LearnVue/blob/master/demo/learn-vue-01.js)