---
title: JS Number
date: 2018-10-13 08:45:00
updated: 2018-10-13 08:45:00
tags: 'javascript操作手册'
description: Javascript Number操作总结
---

注：js 数字的范围：-2e53 -1 ~ 2e53 - 1

#### isNaN（是否是NaN）

```javascript
Number.isNaN(20) // false
Number.isNaN(NaN) // true
Number.isNaN(Number('a')) // true
```

#### isFinite（是否是有穷数）

```javascript
Number.isFinite(2) // true
Number.isFinite(Infinite) // false
Number.isFinite('2') // false
```

#### isInteger（是否是整数）

```javascript
Number.isInteger(2) // true
Number.isInteger(2.56) // false
Number.isInteger('a') // false
```

#### isSafeInteger（是否是安全整数）

```javascript
Number.isSafeInteger(Math.pow(2, 53) - 1) // true
Number.isSafeInteger(Math.pow(-2, 53) + 1) // true
Number.isSafeInteger('a') // false
Number.isSafeInteger(Infinity) // false
Number.isSafeInteger(NaN) // false
```

#### parseFloat（转化为浮点数）

```javascript
Number.parseFloat('3.14') // 3.14
Number.parseFloat(3) // 3
Number.parseFloat('a') // NaN
```

#### parseInt（转化为整数）

```javascript
Number.parseInt('3.14') // 3
Number.parseInt(2.1) // 2
Number.parseInt('a') // NaN
```

#### toFixed（返回四舍五入指定位数的字符串）

```javascript
var num = 2.5879
num.toFixed(2) // '2.59'
```

#### toPrecision（返回指定有效数个数的字符串）

同 `toFixed` 不精准

```javascript
var num = 2.5879
num.toPrecision(3) // '2.59'
```

#### toExponential（将数值转换为指数计数法）

参数：小数点位数

```javascript
var a = 289.1
a.toExponential(2) // '2.89e+2'

// 指数转化为数值
function toNonExponential(num) {
  var m = num.toExponential().match(/\d(?:\.(\d*))?e([+-]\d+)/);
  return num.toFixed(Math.max(0, (m[1] || '').length - m[2]));
}

toNonExponential(2.89e+2) // 289
```


