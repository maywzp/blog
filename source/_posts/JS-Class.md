---
title: JS Class
date: 2018-10-29 11:17:21
updated: 2018-10-29 11:17:21
tags: '知识点'
---

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，通过 class 关键字，可以定义类。
实际上 `class` 只是一个语法糖，在 ES6 之前就可以做到的，新的语法只是让结构更加清晰。
ES6 之前类的实现方法，可参考 [javascript 继承的实现](https://maywzp.github.io/2018/10/25/javascript-%E7%BB%A7%E6%89%BF/)

### 实例属性

实例对象上的属性，可以在实例中使用，也可在类内部使用。

### 静态属性

Class 自身的属性，通过 `Class.propName` 读写。

### 私有方法

在 Class 内部使用的方法，不能再外部使用。
实现方法：

1. 命名增加下划线，如：\_bar()，但这种方法只是命名上识别出它是私有方法，其实外部还是可以调用。
2. 将私有方法移除类，在内部要调用时使用。
3. 使用 Symbol 类型，为私有方法命名一个 Symbol 值，如：`const bar = Symbol('bar'); [bar]()`。

### 静态方法

使用 static 关键字定义，不会被实例继承，可被子类继承，通过类直接调用。
静态方法的 this 指的是类，不是实例。

### get/set 拦截属性存取行为

Class 可以对某个属性设置 get 和 set，拦截该属性的存取行为。

### new.target

一般用于构造函数之中，返回当前被调用的 Class

### super

super 关键字用于访问和调用一个对象的父对象上的函数。
super 的使用：

1. 在子类的 constructor 函数中使用 `super()` 调用父类构造函数。
2. 子类公有方法 调用 super 公有方法
3. 子类静态方法 调用 super 静态方法。

### 代码示例

```javascript
const bar = Symbol('bar')

class Animal {
  // species = '动物'  注：实例属性也可这样定义
  constructor() {
    // 可使用 defineProperty 自定义属性
    Object.defineProperty(this, 'prop', {
      configurable: true,
      writable: false,
      value: 1
    })

    // new.target 判断当前被调用的 Class
    if (new.target === Animal) {
      this.target = 'Animal'
    } else if (new.target === Cat) {
      this.target = 'Cat'
    } else {
      this.target = ''
    }

    this.species = '动物' // 实例属性
  }

  // 静态方法
  static getSpecies() {
    return `static species: animal`
  }

  // 公有方法
  getSelfSpecies() {
    return `species: ${this.species}`
  }

  // 私有方法
  [bar]() {}
}

Animal.environment = '非洲'

class Cat extends Animal {
  // 继承
  constructor(name) {
    super() // 父类，可传参
    this.name = name
  }

  // 拦截已定义属性
  get name() {
    return `get name value`
  }
  set name(val) {
    console.log(`set cat name: ${val}`)
  }

  // 拦截一个新属性
  get getName() {
    return `get cat name: ${this.name}`
  }

  // 静态方法 调用 super 静态方法
  static getSuperSpecies() {
    return super.getSpecies()
  }

  // 公有方法 调用 super 公有方法
  getParentSpecies() {
    return super.getSelfSpecies() + ' too'
  }
}

Cat.category = '猫科动物' // 静态属性

cat = new Cat() // set cat name: undefined
cat.name = '大毛' // set cat name: 大毛
cat.name // get name value
cat.getName // get cat name: 大毛

Cat.category // 猫科动物
```
