---
title: learn-vue-03
date: 2018-05-31 17:21:41
update: 2018-06-01 11:26:41
tags: vue
description: 深入学习Vue.js第三步，实现Watcher类。订阅者，当依赖收集的时候会addSub到subs中，在修改data中数据的时候会触发dep对象的notify，通知所有Watcher对象去修改对应视图。
---

在[上一篇](https://maywzp.github.io/2018/05/31/learn-vue-02/)中实现了`Dep`类，对依赖进行管理，但还遗留了两个问题没解决：

1.  解耦不完全，需要传递参数
2.  外部无法移除依赖

### 思考

如何解决第一个问题？

因为我们依赖的是一个函数，为了执行函数，我们只能传入参数。我们可以把某个对象的值、对应值变化时需要执行的函数抽象为一个对象，把这个对象当作依赖。

如何解决第二个问题？

因为`dep`实例只能在`defineReactive`函数中使用，没有暴露出去，要在外部使用`dep`实例中的方法，需要把`dep`的引用保存在依赖对象中。

综上所述，需要的这个依赖对象，即为`Vue`中的`Watcher`

### Watcher 类的实现

no1. 封装 Watcher

```javascript
class Watcher {
  constructor(obj, key, cb) {
    this.obj = obj
    this.getter = key
    this.cb = cb
    this.dep = null
    this.val = this.get()
  }

  get() {
    Dep.target = this
    // 此处调用 ojb 的 get 方法，同时注入依赖
    const val = this.obj[this.getter]
    Dep.target = null
    return val
  }

  update() {
    const val = this.obj[this.getter]
    const oldVal = this.val
    this.val = val
    this.cb.call(this.obj, val, oldVal)
  }

  addDep(dep) {
    this.dep = dep
  }
}
```

no2. 改进 Dep

```javascript
class Dep {
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

  notify() {
    this.subs.forEach(watcher => watcher.update())
  }
}
Dep.target = null
```

no3. 改进 defineReactive

```javascript
const defineReactive = function(obj, key, val) {
  const dep = new Dep()
  Object.defineProperty(obj, key, {
    configurable: true,
    enumerable: true,
    get() {
      if (Dep.target) {
        // 之前添加的依赖是函数，此时添加的依赖是一个对象
        dep.addSubs(Dep.target)
        // 添加 Watcher 对 dep 的引用
        Dep.target.addDep(dep)
      }
      return val
    },
    set(newVal) {
      if (newVal !== val) {
        val = newVal
        // 不需要传入参数
        dep.notify()
      }
    }
  })
}
```

no4. 使用

```javascript
// defineReactive 函数的调用
const obj = {}
defineReactive(obj, 'name', 'jack')

obj.name
// jack

const watcher1 = new Watcher(obj, 'name', (newValue, oldValue) =>
  console.log('添加的第一个 watch 函数，新值为：' + newValue)
)
obj.name = 'ross'
obj.name
// 添加的第一个 watch 函数，新值为：ross
// ross

const watcher2 = new Watcher(obj, 'name', (newValue, oldValue) =>
  console.log('添加的第二个 watch 函数，新值为：' + newValue)
)
obj.name = 'titanic'
obj.name
// 添加的第一个 watch 函数，新值为：titanic
// 添加的第二个 watch 函数，新值为：titanic
// titanic

// 移除 watcher2
watcher2.dep.removeSubs(watcher2)
obj.name = 'boom'
// 添加的第一个 watch 函数，新值为：boom
```

首先定义一个对象 `obj`，使用`defineReactive`函数拦截 `name`属性的读写。

再定义一个`Dep`类，向外暴露一个 `Dep.target` 属性，此属性接受要注入的依赖，同时具备`addSub`、`removeSub`、`notify`三个方法管理`name`属性的依赖。

最后定义一个`Watcher`类，传入 `obj` 对象、`name` 属性和依赖函数，并提供`get`方法注入依赖，`update`方法执行依赖，同时将 `Dep`实例挂载到`Watcher`实例上，实现外部管理依赖。

三个步骤无间的配合，实现过程实在是巧妙，不得不为尤大大点赞。

虽然我们对依赖的处理进行了完全的解耦，但还是此时的`Watcher`类仍然存在问题：

1.  我们只是简单的监听了单个属性，但一般视图层的渲染是依赖于多个属性。
2.  多个属性可能属于同一个`Watcher`，换句话说多个`Dep`依赖于同一个`Watcher`，那么`Watcher`应该如何保存这些`Dep`。

### 多属性监听及多依赖处理

```javascript
class Watcher {
  constructor(obj, getter, cb) {
    this.obj = obj
    this.getter = getter
    this.cb = cb
    this.deps = []
    this.val = this.get()
  }

  get() {
    Dep.target = this
    const val = this.getter.call(obj)
    Dep.target = null
    return val
  }

  update() {
    const val = this.getter.call(obj)
    const oldVal = this.val
    this.val = val
    this.cb.call(this.obj, val, oldVal)
  }

  addDep(dep) {
    this.deps.push(dep)
  }

  teardown() {
    const i = this.deps.length
    while (i--) {
      this.deps[i].removeSub(this)
    }
    this.deps = []
  }
}
```

之前在添加依赖时，只是在获取对应属性的值时添加，即下面这段代码：

```javascript
const val = this.obj[this.getter]
```

现在我们将添加依赖的属性改为一个函数，由外部决定哪些属性需要监听，即：

```javascript
const val = this.getter.call(obj)
```

此时外面传入的函数中带有获取`name`属性值，我们就可为`name`属性添加依赖，比如：

```javascript
const watcher = new Watcher(ojb, function() { return this.name }, function(newVal, oldVal) => console.log('可添加多属性的依赖') )
```

为了解决多`Dep`依赖同一个`Watcher`，我们将`Watcher`的`dep`该为一个数组，并提供一个清除所有依赖的方法：

```javascript
class Watcher {
  constructor() {
    // ...
    this.deps = []
    // ...
  }
  // ...
  addDep(dep) {
    this.deps.push(dep)
  }

  teardown() {
    const i = this.deps.length
    while (i--) {
      this.deps[i].removeSub(this)
    }
    this.deps = []
  }
}
```

最后附上改进后的调用结果：

```javascript
const obj = {}
defineReactive(obj, 'num1', 2)
defineReactive(obj, 'num2', 4)

const watcher = new Watcher(
  obj,
  function() {
    return this.num1 + this.num2
  },
  function(newValue, oldValue) {
    console.log(`这是一个监听函数，${obj.num1} + ${obj.num2} = ${newValue}`)
  }
)

obj.num1 = 3
// 这是一个监听函数，3 + 4 = 7
obj.num2 = 10
// 这是一个监听函数，3 + 10 = 13

const watcher2 = new Watcher(
  obj,
  function() {
    return this.num1 * this.num2
  },
  function(newValue, oldValue) {
    console.log(`这是一个监听函数，${obj.num1} * ${obj.num2} = ${newValue}`)
  }
)

obj.num1 = 4
// 这是一个监听函数，4 + 10 = 14
// 这是一个监听函数，4 * 10 = 40
obj.num2 = 11
// 这是一个监听函数，4 + 11 = 15
// 这是一个监听函数，4 * 11 = 44

// 测试取消
watcher2.teardown()

obj.num1 = 5
// 这是一个监听函数，5 + 11 = 16
obj.num2 = 12
// 这是一个监听函数，5 + 12 = 17
```

[点击查看相关代码](https://github.com/maywzp/LearnVue/blob/master/demo/learn-vue-03.js)
