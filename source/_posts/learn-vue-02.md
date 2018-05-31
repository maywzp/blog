---
title: learn-vue-02
date: 2018-05-31 11:53:01
update: 2018-05-31 11:53:01
tags: vue
description: 深入学习Vue.js第二步，实现可维护依赖收集类Dep。当对data上的对象进行修改值的时候会触发它的setter，那么取值的时候自然就会触发getter事件，所以我们只要在最开始进行一次render，那么所有被渲染所依赖的data中的数据就会被getter收集到Dep的subs中去。在对data中的数据进行修改的时候setter只会触发Dep的subs的函数。
---

在上一篇中简单的实现了Vue 响应式的依赖收集和触发，详情点击 [learn-vue-01](https://maywzp.github.io/2018/05/30/learn-vue-01/)

但我们只是将依赖放在一个数组里面，虽然好理解但却不好维护，本节我们来实现一个可维护依赖的类。

### 确定功能

**类的属性：**

target: 函数，存放需要添加的依赖

**实例的属性及方法：**

subs：Array，存放依赖

addSub：Function，添加依赖

removeSub：Function，删除依赖

notify：Function，执行依赖

### 实现

封装 `Dep`类，进行依赖维护。

```javascript
class Dep {
  // static target = null

  constructor() {
    this.subs = []
  }

  addSubs(sub) {
    this.subs.push(sub)
  }

  removeSubs(sub) {
    const index = this.subs.indexOf(sub)
    if (index > -1) {
      this.subs.splice(index, 1)
    }
  }

  notify(newVal, oldVal) {
    this.subs.forEach(func => func(newVal, oldVal))
  }
}

Dep.target = null
```

对上篇中的 `defineReactive`进行改进：

```javascript
const defineReactive = function (obj, key, val) {
  const dep = new Dep()
  Object.defineProperty(obj, key, {
    configurable: true,
    enumerable: true,
    get() {
      if (Dep.target) {
        dep.addSubs(Dep.target)
      }
      return val
    },
    set(newVal) {
      if (newVal !== val) {
        dep.notify(newVal, val)
      }
      val = newVal
    }
  })
}
```

调用 `defineReactive` 函数：

```javascript
const obj = {}
defineReactive(obj, 'name', 'jack')

Dep.target = (newValue, oldValue) =>
  console.log('第一个依赖函数，新值为：' + newValue)
obj.name
// jack

Dep.target = (newValue, oldValue) =>
  console.log('第二个依赖函数，新值为：' + newValue)
obj.name = 'ross'
obj.name
// 第一个依赖函数，新值为：ross
// ross

Dep.target = null
obj.name = 'titanic'
obj.name
// 第一个依赖函数，新值为：titanic
// 第二个依赖函数，新值为：titanic
// titanic
```

上面的代码还是存在两个问题：

1. 虽然对添加依赖和处理依赖进行了解耦，但还是不完全的解耦，在执行依赖仍需传入新值和旧值。
2. 可以看到我们并没有去使用 `removeSub` 方法去移除依赖，因为移除依赖一般都是在外部执行了，但我们目前是将 `Dep`的实例放在`defineReactive`内部，所以外部还是不能移除已经没有用的依赖。

要解决上面两个问题，需要使用 `Vue` 中的 `Watch` 类处理，这个之后再说。

[查看相关代码](https://github.com/maywzp/LearnVue/blob/master/demo/learn-vue-02.js)

