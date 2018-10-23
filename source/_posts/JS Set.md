---
title: JS Set
date: 2018-10-17 19:00:00
updated: 2018-10-17 19:00:00
tags: 'javascript操作手册'
description: Javascript Set操作总结
---

new Set([iterable])  传入可迭代对象
set 对象不同于数组，其索引和值相同(idx === val)

#### has（是否存在指定值）
```javascript
var set = new Set([1, 3])
set.has(1) //true
```

#### add（添加指定值到末尾）
不能添加重复的值
```javascript
ar set = new Set([1, 3])
set.add(5)
```

#### delete（删除指定元素）

成功返回 true，失败返回 false
```javascript
var set = new Set([1, 3])
set.delete(3)
```

#### clear（清空所有元素）
```javascript
var set = new Set([1, 3])
set.clear()
```

#### forEach（遍历集合）
```javascript
var set = new Set([1, 3])
set.forEach((val, idx, all) => {
  console.log(val) // 1、3
  console.log(idx) // 1、3
  console.log(all)  //  Set([1, 3])
})
```

#### entries（返回迭代对象）
```javascript
var set = new Set([1, 3])
var setIter = set.entries()
setIter.next() // { value: [1, 1], done: false }
setIter.next() // { value: [3, 3], done: false }
```

#### values（返回值的迭代对象）
```javascript
var set = new Set([1, 3])
var setIter = set.values()
setIter.next() // { value: 1, done: false }
setIter.next() // { value: 3, done: false }
```

#### keys（返回索引的迭代对象）
其结果与 `values` 方法相同
```javascript
var set = new Set([1, 3])
var setIter = set.keys()
setIter.next() // { value: 1, done: false }
setIter.next() // { value: 3, done: false }
```

#### `[Symbol.iterator]()`（返回迭代对象）
其结果与 `values` 方法相同
```javascript
var set = new Set([1, 3])
var setIter = set[Symbol.iterator]()
setIter.next() // { value: 1,  done: false }
```