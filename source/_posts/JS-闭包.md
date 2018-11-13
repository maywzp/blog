---
title: JS 闭包
date: 2018-11-06 10:08:27
updated: 2018-11-06 10:08:27
tags: '知识点'
---

闭包：定义在一个函数内部的函数

用途：
1. 读取函数内部变量
2. 使变量的值在内存中不被释放

示例：

```javascript
function t1() {
  for (var i = 0; i < 5; i++) {
    setTimeout(() => { console.log(i) }, i * 1000)
  }
}

function t2() { // 闭包
  for (var i = 0; i < 5; i++) {
    ;(i => {
      setTimeout(() => { console.log(i) }, i * 1000)
    })(i)
  }
}

function t3() { // 块级作用域
  for (let i = 0; i < 5; i++) {
    setTimeout(() => { console.log(i) }, i * 1000)
  }
}
```

```javascript
function f() {
  var i = 0
  return (x = 1) => i = i + x
}
```
