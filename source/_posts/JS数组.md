---
title: JS数组
date: 2016-12-29 16:41:42
tags: ['js笔记']
description: Javascript Array对象操作总结
photos: http://oizt3fjv8.bkt.clouddn.com/javascript.JPG
---

## concat（合并数值）
```javascript
var arr1 = ['a', 'b']
var arr2 = ['x', 'y']
var arr3 = arr1.concat(arr2)  //arr3:["a", "b", "x", "y"]
```

## join（数组转为字符串）
```javascript
var arr1 = ['a', 'b']
var arr3 = arr1.join('')  //arr3:"ab"
```

## pop（删除最后一个元素）
```javascript
var arr1 = ['a', 'b']
arr1.pop() //arr1:['a']
```

## shift（删除第一个元素）
```javascript
var arr1 = ['a', 'b']
arr1.shift() //arr1:['b']
```

## push（末尾添加元素）
```javascript
var arr1 = ['a', 'b']
arr1.push('c') //arr1:["a", "b", "c"]
```

## unshift（首部添加元素）
```javascript
var arr1 = ['a', 'b']
arr1.unshift('r') //arr1:["r", "a", "b"]
```

## reverse（数组元素颠倒）
```javascript
var arr1 = ['a', 'b']
arr1.reverse()  //arr1: ["b", "a"]
```

## slice(start, end) （选择元素）
```javascript
var arr1 = ['a', 'b']
var arr3 = arr1.slice(1, 2) //arr3: ["b"]
```

## splice （指定位置替换、删除元素）
```javascript
var arr1 = ['a', 'b']
指定开始删除元素的位置： arr1.splice(0) //arr1: []
删除指定位置并且指定个数的元素： arr1.splice(0, 1) //arr1: ["b"]
替换指定位置指定个数的元素： arr1.splice(0, 2, 'i') //arr1: ["i"]
```

## sort（排序）
```javascript
对象数组依照对象的某一个值升序排序
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
arr4.sort(function(a, b){
  return a.age - b.age
  //arr4: [{name: 'wu', age: 12},{name: 'wzp', age: 23},{name: 'yi', age: 35}]
})
```

## forEach（遍历）
```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
arr4.forEach(function(item, index){
  console.log(item.name + index)
  //wzp0  wu1  yi2
})
```

## map（映射）
```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var arr5 = arr4.map(function(item, index){
   return item.name
})
//arr5: ["wzp", "wu", "yi"]
```

## filter（过滤）
```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var arr5 = arr4.filter(function(item, index){
    return item.name === 'wzp'
})
//arr5: [{name: 'wzp', age: 23}]
```

## some（是否包含，返回true或false）
```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var flag = arr4.some(function(item){
     return item.age > 30
})
//flag: true
```

## every（全部通过，返回true或false）
```javascript
var arr4 = [{name: 'wzp', age: 23},{name: 'wu', age: 12},{name: 'yi', age: 35}]
var flag = arr4.every(function(item){
     return item.age > 30
})
//flag: false
```

## indexOf('str', start)（是否包含数据，返回索引或-1）
```javascript
var arr1 = ['a', 'b']
var index = arr1.indexOf('b') //index: 1
```

## lastIndexOf('str', start) （从数组末尾开始找）
```javascript
var arr1 = ['a', 'b']
var index = arr1.lastIndexOf('b') //index: 1
```

## ruduce（数组求和）
```javascript
var arr3 = [1,3,4,6,2]
var sum = arr3.reduce(function(pre, cur, index){
  return pre + cur
})
//sum: 16
```
