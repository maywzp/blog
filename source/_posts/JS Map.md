---
title: JS Map
date: 2018-10-17 19:00:00
updated: 2018-10-17 19:00:00
tags: 'javascript操作手册'
description: Javascript Map操作总结
---

#### has（是否存在指定键）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
map.has('name') // true
```

#### set（添加键值对）
```javascript
var map = new Map([['name', 'may']])
map.set('age', 25)
```

#### get（返回指定值）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
map.get('name') // 'may'
```

#### delete（删除指定元素）
```javascript
成功返回 true，失败返回 false
var map = new Map([['name', 'may'], ['age', 25]])
map.delete('name') // true
```

#### clear（清空所有元素）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
map.clear()
```

#### forEach（遍历）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
map.forEach((val, key, all) => {
  console.log(val) // 'may'、25
  console.log(key) // 'name'、'age'
})
```

#### entries（返回迭代对象）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
var mapIter = map.entries()
mapIter.next() // { value: ['name', 'may'], done: false }
mapIter.next() // { value: ['age', 25], done: false }
```

#### values（返回值的迭代对象）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
var mapIter = map.values()
mapIter.next() // {value: 'may', done: false}
mapIter.next() // {value: 25, done: false}
```

#### keys（返回键的迭代对象）
```javascript
var map = new Map([['name', 'may'], ['age', 25]])
var mapIter = map.keys()
mapIter.next() // {value: 'name', done: false}
mapIter.next() // {value: 'age', done: false}
```