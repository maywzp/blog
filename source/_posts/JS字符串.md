---
title: JS字符串
date: 2016-12-29 16:44:28
tags: ["js笔记"]
---

## concat（合并字符串）
```javascript
var str1 = 'a'
var str2 = 'b'

var str3 = str1.concat(str2)  //str3: 'ab'
```
## split(分隔符, 指定长度)（字符串转数组）
```javascript
var str1 = 'firstname'
var str2 = str1.split('', 4)  //str2: ["f", "i", "r", "s"]
```

## slice(start, end)（提取字符）
```javascript
var str1 = 'firstname'
var str2 = str1.slice(0, 6)  //str2: 'firstn'
```

## substr(start, length)（提取字符）
```javascript
var str1 = 'firstname'
var str2 = str1.substr(0, 4)  //str2: 'firs'
```

## substring(start, end)（提取字符:不能使用负数）
```javascript
var str1 = 'firstname'
var str2 = str1.substring(0, 4)  //str2: 'firs'
```

## toLowerCase() （转换为小写）
```javascript
var str1 = 'FsGd'
var str2 = str1.toLowerCase() //str2: 'fsgd'
```

## toUpperCase() （转换为大写）
```javascript
var str1 = 'FsGd'
var str2 = str1.toUpperCase() //str2: 'FSGD'
```

## charAt(index)（返回指定位置的字符）
```javascript
var str1 = 'firstname'
var at = str1.charAt(4) //at: 't'
```

## at(index)（返回指定位置的字符:可识别Unicode编码大于0xFFFF的字符）
```javascript
var str1 = 'firstname'
var at = str1.at(4) //at: 't'
```

## indexOf('str', start)（是否包含字符，返回索引或-1）
```javascript
var str1 = 'firstname'
var index = str1.indexOf('a')  //index: 6
```

## lastIndexOf('str', start)（是否包含字符，返回索引或-1）
```javascript
var str1 = 'firstname'
var index = str1.lastIndexOf('a')  //index: 6
```

## includes('str', start) （是否包含字符，返回true或false）
```javascript
var str1 = 'firstname'
var flag = str1.includes('name')  //flag: true
```

## startWith('str', start)（字符是否在源字符串头部）
```javascript
var str1 = 'firstname'
var flag = str1.startWith('first')  //flag: true
```

## endWith('str', start)（字符是否在源字符串尾部）
```javascript
var str1 = 'firstname'
var flag = str1.endWith('name')  //flag: true
```

## repeat(number) （将源字符串重复n次）
```javascript
var str1 = 'end'
var str2 = str1.repeat(3)  //str2: 'endendend'
```
