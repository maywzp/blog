---
title: javascript 继承的实现
date: 2018-10-25 18:44:37
updated: 2018-10-25 18:44:37
tags: '知识点'
---

继承是指一个对象直接使用另一对象的属性和方法。

Javascript 在`ES6`之前并没有像其他面向对象编程语言（如：C++、Java）有“类”(class)的概念，虽然设计了构造函数，但只能创建对象的副本，无法共享属性和方法。所以在`ES6`之前，js对象的继承主要还是通过`prototype`属性实现。

下面展示几种原始的继承方法：

## 构造函数的继承
要使用到的构造函数
```javascript
function Animal() {
  this.species = '动物'
}

function Cat(name, color) {
  this.name = name
  this.color = color
}
```

### 构造函数绑定

使用 call 或 apply 方法，将父对象的构造函数绑定到子对象上

```javascript
function Cat(name, color) {
  Animal.call(this, arguments)
  this.name = name
  this.color = color
}

var cat1 = new Cat('大毛', '黄色')
cat1.species	// 动物
```

### prototype 模式

如果"猫"的 prototype 对象，指向一个 Animal 的实例，那么所有"猫"的实例，就能继承 Animal 了

```javascript
Cat.prototype = new Animal()
Cat.prototype.constructor = Cat
var cat1 = new Cat('大毛', '黄色')
cat1.species	// 动物
```

**注意：改变了对象的 prototype ，需要手动将 新 prototype 对象的 constructor 属性指向原来的构造函数。**

```javascript
o.prototype = {}
o.prototype.constructor = o
```

### 直接继承 prototype

将 Cat 的 prototype 对象，然后指向 Animal 的 prototype 对象

缺点：Cat.prototype 和 Animal.prototype 现在指向了同一个对象

​	    Animal.prototype.constructor === Cat

```javascript
function Animal(){ }
Animal.prototype.species = '动物'

Cat.prototype = Animal.prototype;
Cat.prototype.constructor = Cat;
var cat1 = new Cat('大毛', '黄色')
cat1.species	// 动物
```

### 利用空对象作为中介

```javascript
var F = function() {}
F.prototype = Animal.prototype
Cat.prototype = new F()
Cat.prototype.constructor = Cat
```

封装：

uber 属性 指向父对象的 prototype 属性，可以直接调用父对象的方法

```javascript
function extend(Child, Parent) {
  var F = function() {}
  F.prototype = Parent.prototype
  Child.prototype = new F()
  Child.prototype.constructor = Child
  Child.uber = Parent.prototype
}
```

### 拷贝继承

```javascript
function Animal(){ }
Animal.prototype.species = '动物'

function extend2(Child, Parent) {
  var p = Parent.prototype
  var c = Child.prototype
  for (var i on p) {
    c[i] = p[i]
  }
  c.uber = p
}
```

## 非构造函数继承

```javascript
var Chinese = {
  nation:'中国'
}

var Doctor ={
  career:'医生'
}
```

### object() 方法

```javascript
function object(o) {
  function F() {}
  F.prototype = o
  return new F()
}

var Doctor = object(Chinese)
```

### 浅拷贝

```javascript
function extendCopy(p) {
  var c = {}
  for (var i in p) {
    c[i] = p[i]
  }
  c.uber = p
  return c
}
```

### 深拷贝

```javascript
function deepCopy(p, c) {
  var c = c || {}
  for(var i in p) {
    if (typeof p[i] === 'object') {
      c[i] = (p[i].constructor === Array) ? [] : {}
      deepCopy(p[i], c[i])
    } else {
      c[i] = p[i]
    }
  }
  return c
}
```

## ES6 Class
类的所有方法实际上都定义在类的prototype属性上面。
```javascript
class Animal {
  constructor() {
    this.species = '动物'
  }
}

class Cat extends Animal {
  constructor(name, color) {
    super()
    this.name = name
    this.color = color
  }
  getColor() {
    return this.color
  }
}

var cat1 = new Cat('大毛','黄色')
cat1.species	// 动物
```