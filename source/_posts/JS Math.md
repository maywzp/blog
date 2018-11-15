---
title: JS Math
date: 2018-10-16 10:21:00
updated: 2018-10-16 10:21:00
tags: 'javascript操作手册'
description: Javascript Math对象操作总结
---

注：math 的所有函数都能传 数字字符串

#### Math.abs（绝对值）

```javascript
Math.abs('1.2') // 1.2
Math.abs(-1.2) // 1.2
Math.abs('a') // NaN
```

#### Math.ceil（向上取整）

```javascript
Math.ceil('1.25') // 2
Math.ceil(1.25) // 2
Math.ceil(-1.25) // -1
Math.ceil('a') // NaN
```

#### Math.floor（向下取整）

```javascript
Math.floor('1.25') // 1
Math.floor(1.25) // 1
Math.floor(-1.25) // -2
Math.floor('a') // NaN
```

#### Math.trunc（只返回整数部分，去除小数）

```javascript
Math.trunc('2.52') // 2
Math.trunc(-2.13) // -2
Math.trunc(0.2) // 0
Math.trunc('a') // NaN
```

#### Math.max（最大值）

```javascript
Math.max(-3, -1, 0, 3) // 3
Math.max('-3', '-1', '0', '3') // 3
Math.max(-3, -1, 0, 'a') // NaN
```

#### Math.min（最小值）

```javascript
Math.min(-3, -1, 0, 3) // -3
Math.min('-3', '-1', '0', '3') // -3
Math.min(-3, -1, 0, 'a') // NaN
```

#### Math.random（返回 0~1 之间的随机数）

```javascript
Math.random() // 0.7930965120699416

// 返回指定范围的随机数
function randomNum(n, m) {
  return Math.random() * (m - n) + n
}

// 返回指定长度的随机数
function randNum(len) {
  let rand = ''
  for (let i = 0; i < len; i++) {
    rand += Math.floor(Math.random() * 10)
  }
  return Number(rand)
}
```

#### Math.round（四舍五入后的整数）

```javascript
Math.round(1.5) // 2
Math.round(-1.5) // -1
Math.round(-1.51) // -2
Math.round('a') // NaN

// 返回指定精度的数字
function round(number, precision) {
  return Math.round(+number + 'e' + precision) / Math.pow(10, precision)
}

round(1.089, 2) // 1.09
```

#### Math.sign（判断数值正负）

返回值：1 整数、0 零、-1 负数

```javascript
Math.sign(4.2) // 1
Math.sign(0) // 0
Math.sign(-4.2) // -1
Math.sign('a') // NaN
```

#### Math.pow(x, y) （x 的 y 幂方）

```javascript
Math.pow(2, 3) // 8
Math.pow(10, 2) // 100
Math.pow('2', '3') // 8
Math.pow('2', 'a') // NaN
```

#### Math.sqrt（平方根）

```javascript
Math.sqrt(25) // 5
Math.sqrt('6') // 2.449489742783178
Math.sqrt(0) // 0
Math.sqrt(-4) // NaN
```

#### Math.cbrt（立方根）

```javascript
Math.cbrt(8) // 2
Math.cbrt(0) // 0
Math.cbrt(-8) // -2
```

#### Math.log10（以 10 为底的对数）

```javascript
Math.log10(100) // 2
Math.log10(1) // 0
Math.log10(0) // -Infinity
Math.log10(-100) // NaN
```

#### Math.log2（以 2 为底的对数）

```javascript
Math.log2(4) // 2
Math.log2(-4) // NaN
Math.log2(0) // -Infinity
```

#### Math.log（一个数的自然对数）

自然对数以常数 e 为底数的对数

```javascript
Math.log(2) // 0.6931471805599453
Math.log(-2) // NaN

// 以 x 为底 y 的对数（即 logx y）
function getBaseLog(x, y) {
  return Math.log(y) / Math.log(x)
}

getBaseLog(2, 8) // 3
```

#### Math.PI

```javascript
Math.PI // 3.141592653589793
```

#### Math.sin（正弦）

```javascript
Math.sin(Math.PI / 6) // 0.49999999999999994
```

#### Math.cos（余弦）

```javascript
Math.cos(Math.PI / 3) // 0.5000000000000001
```

#### Math.tan（正切）

```javascript
Math.tan(Math.PI / 4) // 0.9999999999999999
```

#### 三角函数特数值

![](http://oizt3fjv8.bkt.clouddn.com/2018-10-15-145507.png)
