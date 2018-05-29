---
title: vue2学习笔记
date: 2016-11-16 16:44:28
updated: 2016-11-16 16:44:28
tags: ['vue']
description: Vue.js是当下很火的一个JavaScript MVVM库,它是以数据驱动和组件化的思想构建的。
photos: http://oizt3fjv8.bkt.clouddn.com/vue_no1.jpg
---

## vue生命周期
![](http://oizt3fjv8.bkt.clouddn.com/vue_kill.png)

## 数据响应
###  对象
vue是通过递归遍历初始数据中的所有属性，并用object.defineProperty把它们转化为getter和setter来实现数据观察的。
如果有一个属性不存在初始数据中，那么就无法观测这个属性；
```JavaScript
//对象添加和删除属性
obj.$add(key, value)
obj.$set(key, value)
obj.$delete(key)
```

### 数组
变异方法（对下面这些方法进行了拦截，调用这些方法会数组会响应）：
`push、pop、shift、unshift、splice、sort、reverse方法`
非变异方法：
`filter、concat、slice`
上述方法返回的数组是一个不同的实例，所以要用新数组代替旧数组：
```javascript
arr = arr.filter(function(index){
  return arr[index].match(/hello/)
})
```
通过索引修改数组数据，vue无法侦测到这类操作
```javascript
//扩展方法
arr.$set(index, value)
arr.$remove(index | value)
```

## 数据监视
### computed与methods
 ```javascript
 computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
 }

 methods: {
  reverseMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
 ```

上述代码实现相同的功能
区别：computed基于它的依赖缓存，依赖不变不会重新取值
methods 每当重新渲染都会执行函数

### computed与watch
区别：computed属性用于数据的计算，返回计算后的数据
watch用于响应数据的变化，执行一些操作，改变数据值，可以无返回值

watch监视数据的变化，第一个参数为当前数据的值
用于一个数据会根据其他数据变化而变化，多数情况下可以使用computed属性代替
```javascript
data: {
  name: 'wzp',
  realName: ''
}
watch: {
  //监视name属性，当name改变时realName 变化
  name: function(val){
    this.realName = val + 'no1'
  }
}
```

## 注意事项
- vue实例直接代理data属性：data.a == vm.a == this.a
- vue暴露的其他属性方法要加前缀 $,与data属性区分
- v-html 插入的dom数据绑定会被忽略
- Mustache风格不能再HTML属性中使用,要换为v-bind指令
- <div :id="'box' + product.id"></div>
- <button :disabled="is"></button>
- 注意在 JavaScript 中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。
