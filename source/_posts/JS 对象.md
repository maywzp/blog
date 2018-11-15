---
title: JS Object
date: 2016-12-22 11:44:18
updated: 2018-10-12 11:56:00
tags: ['javascript操作手册']
---


注：标记星号是会改变原对象的操作 

#### *assign（复制对象到目标对象）

继承属性和不可枚举属性是不能拷贝的、对象浅拷贝。

```javascript
var obj = { name: 'may', age: 25 }
var obj2 = Object.assign(obj, { gender: 1 })
// obj: { name: 'may', age: 25, gender: 1 }
// obj2: { name: 'may', age: 25, gender: 1 }
```

#### *defineProperties（修改对象多个属性）

`configurable` 该属性可被改变和删除，`enumerable` 该属性可被枚举，`writable` 该属性值可写。默认值都为 `false`。

对象的属性描述符分为：数据描述符 和 存取描述符

数据描述符可选键值：`value`、`writable`

存取描述符可选键值：`get`、`set`

数据描述符 和 存取描述符 **不能共存**

```javascript
var obj = { }
Object.defineProperties(obj, {
  name: { // 数据描述符
    value: 'join',
    writable: true, // 可写
    configurable: false, // 不可删除
    enumerable: false // 不可枚举
  },
  age: (ageValue => ({ // 存取描述符
    configurable: true,
    enumerable: true,
    get() {
      return ageValue
    },
    set(val) {
      ageValue = val
    }
  }))(25)
})


obj.name // join
obj.name = 'aysa' // aysa
Object.keys(obj) // []
delete obj.name // false
```

#### *defineProperty (修改对象一个属性)

```javascript
var obj = { }
var ageValue = 25
Object.defineProperty(obj, 'name', {
  value: 'may'
})
Object.defineProperty(obj, 'age', {
  get() {
    return ageValue
  },
  set(val) {
    ageValue = val
  }
})
```

#### entries（自身可枚举属性的键值对数组）

不会返回原型对象上的属性

```javascript
var obj = { name: 'may', age: 25 }
obj.__proto__.gender =1
var et = Object.entries(obj) // et: [['name', 'may'], ['age', 25]]

// 遍历对象键值对
Object.entries(obj).forEach(([k, v]) => { console.log(`${k} ${v}`) })

// 对象转Map
var map = new Map(Object.entries(obj))
```

#### fromEntries（键值对数组转化为对象）

大部分浏览器还未支持

```javascript
var map = new Map([['name', 'may'], ['age', 25]])
var obj = Object.fromEntries(map) // obj: { name: 'may', age: 25 }
```

#### keys（返回自身可枚举属性组成的数组）

不会返回原型对象上的属性

如果获取一个对象的所有属性,，甚至包括不可枚举的，可使用 `getOwnPropertyNames` 方法

```javascript
var obj = { name: 'may', age: 25 }
obj.__proto__.gender =1
Object.keys(obj) // ['name', 'age']

for(let k in obj) {
  console.log(k) // name、age、gender
}
```

#### values（返回自身可枚举属性值组成的数组）

不会返回原型对象上的属性

```javascript
var obj = { name: 'may', age: 25 }
obj.__proto__.gender =1
Object.values(obj) // ['may', 25]
```

#### *preventExtensions（使对象不可扩展）

不能添加新属性

```javascript
var obj = { name: 'may', age: 25 }
Object.preventExtensions(obj)
obj.gender = 1 // obj: { name: 'may', age: 25 }
```

#### *freeze（浅冻结对象）

不能向这个对象添加新的属性，不能修改其已有属性的值，不能删除已有属性，以及不能修改该对象已有属性的可枚举性、可配置性、可写性。

```javascript
var obj = { name: 'may' }
Object.freeze(obj) // 冻结对象

obj.name = 'w' // error name 值并不会改变
delete obj.name // false

var arr = [1, 2]
Object.freeze(arr) // 冻结数组
arr.push(2) // error arr 不会改变


// 深度冻结
function deepFreeze(obj) {
  var propNames = Object.getOwnPropertyNames(obj)

  propNames.forEach(function(name) {
    var prop = obj[name]

    if (typeof prop == 'object' && prop !== null) deepFreeze(prop)
  })

  return Object.freeze(obj)
}

var obj = { name: 'may', internal: { a: 2 } }
deepFreeze(obj)
obj.internal.a = 3 // a 的值不会改变
```

#### *seal（密封对象）

阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。

```javascript
var obj = { name: 'may' }

Object.seal(obj)
obj.age = 1 // obj: { name: 'may' }
obj.name = 'join' // obj: { name: 'join' }
delete obj.name // false
```

#### isFrozen（对象是否冻结）

一个对象是冻结的是指它不可扩展，所有属性都是不可配置的，且所有数据属性（即没有getter或setter组件的访问器的属性）都是不可写的

```javascript
var obj = { name: 'may' }

Object.isFrozen(obj) // false
Object.isFrozen(Object.freeze(obj)) // true
```

#### isSealed（对象是否密封）

密封对象是指那些不可扩展的，所有自身属性都不可配置且不可删除（但不一定是不可写）的对象

```javascript
var obj = { name: 'may' }

Object.isSealed(obj) // false
Object.isSealed(Object.seal(obj)) // true
```

#### isExtensible（对象是否可扩展）

冻结对象 和 密封对象 不可扩展

```javascript
var obj = { name: 'may' }

Object.isExtensible(obj) // true

// 变为不可扩展
Object.preventExtensions(obj)
Object.isExtensible(obj) // false

// 密封对象
var sealed = Object.seal(obj)
Object.isExtensible(sealed) // false

// 冻结对象
var frozen = Object.freeze(obj)
Object.isExtensible(frozen) // false
```

#### propertyIsEnumerable（指定属性是否可枚举）

不包含原型链上的属性

```javascript
var obj = { name: 'may' }

obj.propertyIsEnumerable('name') // true
obj.propertyIsEnumerable('length') // false

var arr = ['a', 'b']
arr.propertyIsEnumerable(0) // true
arr.propertyIsEnumerable('length') // false
```

#### getOwnPropertyDescriptor（获取对象一个属性的属性描述符）

```javascript
var obj = { name: 'may' }
var o = Object.getOwnPropertyDescriptor(obj, 'name')
// o: { value: 'may', writable: true, enumerable: true, configurable: true }
```

#### getOwnPropertyDescriptors（获取对象自身属性的描述符）

```javascript
var obj = { name: 'may' }
var o = Object.getOwnPropertyDescriptors(obj)
// o: { name: { value: 'may', writable: true, enumerable: true, configurable: true } }
```

#### getOwnPropertyNames（获取对象自身属性属性名）

包含不可枚举属性，不包括Symbol值作为名称的属性

```javascript
var obj = { name: 'may', age: 25 }
var keys = Object.getOwnPropertyNames(obj) // ['name', 'age']

var arr = ['a', 'b']
var keys = Object.getOwnPropertyNames(arr) // ['0', '1', 'length']
```

#### getOwnPropertySymbols（返回对象所有 Symbol 属性的数组）

```javascript
var obj = { name: 'may' }
var age = Symbol('age')
obj[age] = 25
var os = Object.getOwnPropertySymbols(obj) // os: [Symbol('age')]
```

#### getPrototypeOf（返回对象原型）

```javascript
var obj = { name: 'may' }
Object.prototype === Object.getPrototypeOf( obj ) // true

Object.prototype === obj.__proto__ // true
```

#### is（判断两个值是否相同）

```javascript
Object.is('foo', 'bar') // false
Object.is([1], [1]) // false
Object.is('a', 'a') // true
```

#### hasOwnProperty（对象自身是否存在指定属性）

不包括原型链上属性

```javascript
var obj = { name: 'may' }

obj.hasOwnProperty('name') // true
obj.hasOwnProperty('toString') // false
```

#### isPrototypeOf（一个对象是否在另一个对象的原型链上）

```javascript
function Foo() {}
function Bar() {}

var bar = new Bar()
Foo.prototype = bar
var foo = new Foo()

bar.isPrototypeOf(foo) // true
```

