---
title: JS Array
date: 2016-11-24 16:38:42
updated: 2018-10-12 12:20:00
tags: ['javascript操作手册']
description: Javascript Array对象操作总结
---

<!-- ### JS 数组操作 -->

注：

1. 标记星号是会改变原数组的操作 
2. 元素操作索引从 0 开始
3. 包含起始位置和结束位置的操作，结束位置都不包含在内，是**前闭后开区间**

#### concat（连接数组）

```javascript
// 数组连接数组
var arr = ['a', 'b'].concat(['c', 'd'])   // arr: ['a', 'b', 'c', 'd']

// 数组连接多个数组
var arr = ['a', 'b'].concat(['c'], ['d']) // arr: ['a', 'b', 'c', 'd']

// 数组连接字符串
var arr = ['a', 'b'].concat('c', 'd')  	  // arr: ['a', 'b', 'c', 'd']

// 数组连接字符串和数组
var arr = ['a', 'b'].concat(['c'], 'd')   // arr: ['a', 'b', 'c', 'd']
```

#### join（数组转为字符串）

```javascript
var arr1 = ['a', 'b']
var arr3 = arr1.join('')  // arr3: 'ab'
```

#### *pop（删除最后一个元素）

```javascript
var arr1 = ['a', 'b']
arr1.pop() // arr1: ['a']
```

#### *shift（删除第一个元素）

```javascript
var arr1 = ['a', 'b']
arr1.shift() // arr1: ['b']
```

#### *push（末尾添加元素）

```javascript
var arr1 = ['a', 'b']
arr1.push('c', 'd') // arr1: ['a', 'b', 'c', 'd']
```

#### *unshift（首部添加元素）

```javascript
var arr1 = ['a', 'b']
arr1.unshift('r') // arr1: ['r', 'a', 'b']
```

#### *reverse（数组元素颠倒）

```javascript
var arr1 = ['a', 'b']
arr1.reverse()  // arr1: ['b', 'a']
```

#### slice(start, end) （浅拷贝元素）

```javascript
var arr1 = ['a', 'b', 'c']
var arr3 = arr1.slice(1, 2) // arr3: ['b']
```

#### *splice （替换、删除元素）

```javascript
var arr1 = ['a', 'b']
指定开始删除元素的位置： arr1.splice(0) // arr1: []
删除指定位置并且指定个数的元素： arr1.splice(0, 1) // arr1: ['b']
替换指定位置指定个数的元素： arr1.splice(0, 1, 'i') // arr1: ['i'，'b']
```

#### *sort（排序）

a - b < 0，a 排在 b 前面

a - b = 0，a, b 相对位置不变

a - b > 0，b 排在 a 前面

```javascript
// 对象数组依照对象的某一个值升序排序
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]

// 数字类型比较
arr4.sort((a, b) => a.age - b.age)
// arr4: [{name: 'wu', age: 12},{name: 'wzp', age: 23},{name: 'yi', age: 35}]

// 字符串类型比较
arr4.sort((a, b) => {
  a = a.name.toUpperCase(a)
  b = b.name.toUpperCase(b)
  if (a < b) return -1
  else if (a > b) return 1
  else return 0
})
// arr4: [{name: 'wu', age: 12},{name: 'wzp', age: 23},{name: 'yi', age: 35}]
```

#### *forEach（遍历）

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
arr4.forEach((i, idx, arr) => {
  i.name = i.name + idx
})
// arr4 = [{name: 'wzp0', age: 23},{name: 'wu1', age: 12},{name: 'yi2', age: 35}]
```

#### map（映射）

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var arr5 = arr4.map((i, idx, arr) => i.name)
//arr5: ["wzp", "wu", "yi"]
```

#### filter（过滤）

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var arr5 = arr4.filter((i, idx, arr) => i.name === 'wzp')
// arr5: [{name: 'wzp', age: 23}]
```

#### some（是否包含）

返回true或false

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var flag = arr4.some((i, idx, arr) => i.age > 30)
// flag: true
```

#### every（全部通过）

返回true或false

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var flag = arr4.every((i, idx, arr) => i.age > 30)
// flag: false
```

#### find（返回第一个匹配元素）

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var hit = arr4.find((i, idx, arr) => i.age > 30)
// hit: {name: 'yi', age: 35}
```

#### findIndex（返回第一个匹配元素的索引）

```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var hitIndex = arr4.findIndex((i, idx, arr) => i.age > 30)
// hitIndex: 2
```

#### indexOf(‘str’, start)（从开头查找元素）

返回第一个匹配元素索引或 -1

```javascript
var arr1 = ['a', 'b']
var index = arr1.indexOf('b') // index: 1
```

#### lastIndexOf(‘str’, start) （从末尾查找元素）

返回最后一个匹配元素索引或 -1

```javascript
var arr1 = ['a', 'b']
var index = arr1.lastIndexOf('b') // index: 1
```

#### includes（是否包含元素）

参数：searchElement 要查找的元素，fromIndex 从该索引出开始查找

```javascript
var arr1 = ['as', 'b']
arr1.includes('a', 0) // false
arr1.includes('as', 0) // true
```

#### reduce（累加器）

回调函数包含四个参数：acc 累加器，cur 当前值，idx 当前元素索引，arr 原数组

**最好给累加器一个初始值。**

如果不给初始值，acc 默认值为数组第一个元素，cur 从数组第二个元素开始，idx 从 1 开始。

```javascript
// 普通数组
var arr3 = [1,3,4,6,2]
var sum = arr3.reduce((cur, next, idx, arr) => cur + next) // sum: 16
var sum = arr3.reduce((acc, cur, idx, arr) => acc + cur, 0) // sum: 16

// 对象数组
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var totalAge = arr4.reduce((acc, cur) => acc + cur.age, 0) // totalAge: 70

// 二维数组转化为一位数组
var arr5 = [[1, 3], [5, 7], [8, 9]]
var flatten = arr5.reduce((flat, next) => flat.concat(next), [])
// flatten: [1, 3, 5, 7, 8, 9]
```

#### reduceRight (累加器，从右到左)

参数同 `reduce` 方法

#### isArray（是否是数组）

```javascript
var arr = [1, 2]
var flag = Array.isArray(arr) // true
```

#### from （类数组转化为数组）

参数：arrayLike 类数组，mapFn 遍历函数

```javascript
Array.from('foo') // ['f', 'o', '0']

var s = new Set([2, 4, 6])
Array.from(s) // [2, 4, 6]

var m = new Map([['name', 'wzp'], ['age', 25]])
Array.from(m) // [['name', 'wzp'], ['age', 25]]

Array.from([1, 2, 3], x => x + x) // [2, 4, 6]
```

#### of (创建数组)

参数：数组的值

```javascript
Array.of(7) // [7]
Array.of(1, 2, 3) // [1, 2, 3]
```

#### *copyWithin(target, start, end)（数组内浅复制元素）

参数：target 替换目标索引，start 开始复制索引，end 结束复制索引（不包含该位置）

复制后原数组被修改，数组长度维持不变

```javascript
var arr = [1, 2, 3, 4, 5]
arr.copyWithin(0, 3, 4) // [4, 2, 3, 4, 5]
arr.copyWithin(0, 3) // [4, 5, 3, 4, 5]
```

#### *fill （用一个固定的值填充数组）

参数：value 填充的值，start 起始索引， end 终止索引（不包含该位置）

```javascript
var arr = [1, 3, 4, 2]
arr.fill(9) // arr: [9, 9, 9, 9]
arr.fill(9, 1, 2) // arr: [1, 9, 4, 2]
```

#### entries（返回可迭代对象）

```javascript
var arr = ['a', 'b', 'c']
var iterator = arr.entries()
iterator.next() // { value: [0, 'a'], done: false }
```

#### keys（返回包含每个索引的可迭代对象）

```javascript
var arr = ['a', 'b', 'c']
var keysIterator = arr.keys()
keysIterator.next() // { value: 0, done: false }
```

#### values（返回包含每个值的可迭代对象）

```javascript
var arr = ['a', 'b', 'c']
var valuesIterator = arr.values()
valuesIterator.next() // { value: 'a', done: false }
```

#### `[@@iterator]()` （**iterator** 方法）

返回值与 `values` 方法一样

```javascript
var arr = ['a', 'b', 'c']
var iterator = arr[Symbol.iterator]()
iterator.next() // { value: 'a', done: false }
```


