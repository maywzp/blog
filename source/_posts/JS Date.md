---
title: JS Date
date: 2018-10-16 16:09:00
updated: 2018-10-16 16:09:00
tags: 'javascript操作手册'
description: Javascript Date对象操作总结
---

注：
展示 get\* 接口
省略 getUTC\* 接口
省略 set\* 接口
省略 setUTC\* 接口

### JS Date 操作
#### getFullYear（指定日期的年份）
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getFullYear() // 2018
```

#### getMonth（指定日期的月份）
返回值范围：0 ~ 11，0 代表一月份
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getMonth() // 9
```

#### getDate（指定日期月的第几天）
返回值范围：1 ~ 31
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getDate() // 16
```

#### getDay（指定日期周的第几天）
返回值范围：0 ~ 6，0 表示星期天
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getDay() // 2
```

#### getHours（指定日期的小时）
返回值范围：0 ~ 23
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getHours() // 12
```

#### getMinutes（指定日期的分钟数）
返回值：0 ~ 59
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getMinutes() // 16
```

#### getSeconds（指定日期的秒数）
返回值范围：0 ~ 59
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getSeconds() // 11
```

#### getMilliseconds（指定日期的毫秒数）
返回值范围：0 ~ 999
```javascript
var now = new Date('2018-10-16 12:16:11')
now. getMilliseconds() // 0
```

#### getTime（时间戳）
返回格林威治时间数值：表示 1970-01-01 00:00:00 距离指定日期的毫秒数
```javascript
var now = new Date('2018-10-16 12:16:11')
now. getTime() // 1539663371000
```

#### getTimezoneOffset（UTC日期与当前时区的时间差）
返回的是分钟数，正数表示比UTC早，负数表示比UTC时间晚
```javascript
var now = new Date('2018-10-16 12:16:11')
now.getTimezoneOffset() // -480  北京时间比UTC时间晚8个小时
```

#### toISOString（指定日期的UTC时间）
```javascript
var now = new Date('2018-10-16 12:16:11')
now. toISOString() // 2018-10-16T04:16:11.000Z
```

#### toJSON（Date 对象的字符串形式）
返回值与 toISOString 方法一样
```javascript
var now = new Date('2018-10-16 12:16:11')
now. toJSON() // 2018-10-16T04:16:11.000Z
```

### 时间格式化函数

```javascript
// dateFormat(new Date(), 'yyyy-MM-dd hh:mm:ss') => 2018-10-16 14:33:40
export const dateFormat = (date, fmt = 'yyyy-MM-dd') => {
  date = new Date(date)
  const o = {
    'M+': date.getMonth() + 1, // 月份
    'd+': date.getDate(), // 日
    'h+': date.getHours(), // 小时
    'm+': date.getMinutes(), // 分
    's+': date.getSeconds(), // 秒
    'q+': Math.floor((date.getMonth() + 3) / 3), // 季度
    S: date.getMilliseconds() // 毫秒
  }
  if (/(y+)/.test(fmt)) {
    fmt = fmt.replace(
      RegExp.$1,
      (date.getFullYear() + '').substr(4 - RegExp.$1.length)
    )
  }

  Object.keys(o).forEach(k => {
    if (new RegExp('(' + k + ')').test(fmt)) {
      fmt = fmt.replace(
        RegExp.$1,
        RegExp.$1.length === 1 ? o[k] : ('00' + o[k]).substr(('' + o[k]).length)
      )
    }
  })

  return fmt
}
```

### moment 时间插件

#### dayOfYear（当前日期在一年中的天数）

```javascript
var m = moment('2018-10-16 12:16:11')
m.dayOfYear() // 289
```

#### daysInMonth（当前月份的天数）

```javascript
var m = moment('2018-10-16 12:16:11')
m.daysInMonth() // 31
```

#### week（当前日期在一年中的周数）

```javascript
var m = moment('2018-10-16 12:16:11')
m.week() // 42
```

#### quarter（当前日期在一年中的季度）

```javascript
var m = moment('2018-10-16 12:16:11')
m.quarter() // 4
```

#### max（最大时间）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
moment.max(a, b)  // b
```

#### min（最小时间）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
moment.min(a, b)  // a
```

#### *add（时间后推）

```javascript
var m = moment('2018-10-16 12:16:11')
m.add(1, 'day').add(1, 'month')
// m: moment("2018-11-17T12:16:11.000")
```

#### *subtract（时间前推）

```javascript
var m = moment('2018-10-16 12:16:11')
m.subtract(1, 'day').subtract(1, 'month')
// m: moment("2018-09-15T12:16:11.000")
```

#### *startOf（开始时间）

```javascript
var m = moment('2018-10-16 12:16:11')
m.startOf('day') // m: moment("2018-10-16T00:00:00.000")
```

#### *endOf（结束时间）

```javascript
var m = moment('2018-10-16 12:16:11')
m.endOf('day') // m: moment("2018-10-16T23:59:59.999")
```

#### format（格式化）

```javascript
var m = moment('2018-10-16 12:16:11')
m.format('YYYY-MM-DD HH:mm:ss') // 2018-10-16 12:16:11
```

#### diff（时差）

第三个参数控制是否获得精准的数值，默认返回的数值会向下取舍，去掉小数。

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
b.diff(a, 'day')  // 5
b.diff(a, 'day', true)  // 5
```

#### toObject（将moment 对象转为包含年月日时分秒毫秒的对象）

```javascript
var m = moment('2018-10-16 12:16:11')
m.toObject()
// { years: 2018, months: 9, date: 16, hours: 12, minutes: 16, seconds: 11, milliseconds: 0 }
```

#### isBefore（之前）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
a.isBefore(b) // true
```

#### isSame（相同）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
a.isSame(b) // false
```

#### isAfter（之后）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
a.isAfter(b) // false
```

#### isBetween（之间）

```javascript
var a = moment('2018-10-01')
var b = moment('2018-10-06')
var m = moment('2018-10-16 12:16:11')
m.isBetween(a, b) // false
```

#### isLeapYear（是否是闰年）

```javascript
var m = moment('2018-10-16 12:16:11')
m.isLeapYear() // false
```

#### isDate（是否是Date对象）

```javascript
moment.isDate(new Date()) // true
```

### 输出指定范围的日期

```javascript
import moment from 'moment'

export const betweenDate = (startDate, endDate, unit = 'day', fm = 'YYYY-MM-DD') => {
  let start = moment(startDate).startOf(unit)
  let end = moment(endDate).startOf(unit)
  const result = []
  while (end.diff(start) >= 0) {
    result.push(start.format(fm))
    start.add(1, unit)
  }
  return result
}

betweenDate('2018-10-01', '2018-10-11') 
// ['2018-10-01', '2018-10-02', '2018-10-03', '2018-10-04', '2018-10-05', '2018-10-06', '2018-10-07', '2018-10-08', '2018-10-09', '2018-10-10', '2018-10-11' ]
```

