---
title: JS String
date: 2016-11-29 10:47:28
updated: 2018-10-12 17:35:00
tags: ['javascript操作手册']
description: Javascript String操作总结
---

#### Unicode编码值

汉字：[0x4e00,0x9fa5]（或十进制[19968,40869]）

数字：[0x30,0x39]（或十进制[48, 57]）

大写字母：[0x41,0x5a]（或十进制[65, 90]）

小写字母：[0x61,0x7a]（或十进制[97, 122]）

#### fromCharCode（根据Unicode值创建字符串） 

最大支持16位的数字 

```javascript
var str = String.fromCharCode(65,66,67) // str: ABC
```

#### fromCodePoint（根据Unicode值创建字符串） 

最大支持21位的数字 

```javascript
var str = String.fromCodePoint(65,66,67) // str: ABC 
```

#### charAt（返回指定位置字符）

```javascript
var str = 'No safe wading in an unknown water'
str.charAt(0)  // N
```

#### charCodeAt（返回指定位置字符的Unicode码）

```javascript
var str = 'No safe wading in an unknown water'
str. charCodeAt(0)  // 78
```

#### codePointAt（返回指定位置字符的Unicode码）

更加精准

```javascript
var str = 'No safe wading in an unknown water'
str. codePointAt(0)  // 78
```

#### split(分隔符, 指定长度)（字符串转数组）

```javascript
var str = 'firstname'
str.split('', 4)  // ['f', 'i', 's', 't']
```

#### slice(start, end)（提取字符）

```javascript
var str = 'firstname'
str.slice(0, 6)  // 'firstn'
```

#### substr(start, length)（提取字符）

```javascript
var str = 'firstname'
str.substr(0, 4)  // 'firs'
```

#### substring(start, end)（提取字符:不能使用负数）

```javascript
var str = 'firstname'
str.substring(0, 4)  // 'firs'
```

#### toLowerCase（转换为小写）

```javascript
var str = 'FsGd'
str.toLowerCase() // 'fsgd'
```

#### toUpperCase （转换为大写）

```javascript
var str = 'FsGd'
str.toUpperCase() // 'FSGD'
```

#### startsWith（是否以指定值开头）

```javascript
var str = 'No safe wading in an unknown water'

str.startsWith('No') // true
```

#### endsWith（是否以指定值结尾）

```javascript
var str = 'No safe wading in an unknown water'

str.endsWith('water') // true
```

#### includes（是否包含指定值）

```javascript
var str = 'No safe wading in an unknown water'

str.includes('in') // true
```

#### indexOf（返回第一次出现指定值的索引）

如未找到该值，返回 -1

```javascript
var str = 'No safe wading in an unknown water'

str.indexOf('in') // 11
```

#### lastIndexOf（返回最后出现指定值的索引）

如未找到该值，返回 -1

```javascript
var str = 'No safe wading in an unknown water'

str.lastIndexOf('in') // 15
```

#### repeat（重复字符串次数）

```javascript
var str = 'may'

str.repeat(3) // 'maymaymay'
```

#### trim（返回去除前后空格后的字符串）

```javascript
var str = ' hellow world '
str.trim() // hellow world
```

