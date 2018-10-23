---
title: JS 正则
date: 2018-10-23 12:13:22
updated: 2018-10-23 12:13:22
tags: 'javascript操作手册'
---

以下方法使用下面数据

```javascript
var str = 'The Quick Brown Fox Jumps Over The Lazy Dog'
var reg = /quick\s(brown).+?(jumps)/ig
```

#### 方法

##### exec

查找匹配，返回一个数组（详细匹配信息），未匹配返回 null

```
reg.exec(str)	// => ['Quick Brown Fox Jumps', 'Brown', 'Jumps' ...]
```

##### test

测试是否匹配，返回 true 或者 false

```javascript
reg.test(str)	// => true
```

##### match

查找匹配，返回一个数组，未匹配返回 null

```javascript
str.match(reg) // => ['Quick Brown Fox Jumps']
```

##### search

测试匹配，返回匹配到的位置索引，失败返回 -1

```javascript
str.search(reg) // => 4
```

##### replace

替换匹配

```javascript
str.replace(reg, 'a') // => 'The a Over The Lazy Dog'
```

##### split

分割字符串，返回 数组

```javascript
str.split(reg)	// =>  ["The ", "Brown", "Jumps", " Over The Lazy Dog"]
```



以下正则为全局匹配

#### 特殊符号

##### \

非特殊字符换化为特殊字符；特殊字符转化为字面量

```javascript
单独的 b 表示字母 b，/b 就转化为特殊字符了
* 表示 0 个或多个，\* 就匹配 * 字符
```

##### ^

配置输入的开始

```javascript
/^A/ 并不会匹配 "an A" 中的 A，但会匹配 "An E" 中的 A
```

##### $

配置输入的结束

```javascript
/t$/ 不会匹配 "eater" 中的 t，但会匹配 "eat" 中的 t
```

##### *

匹配前一个表达式 0 次或多次，等价于 {0,}

```javascript
/bo*/ 会匹配 "booed" 中的 'boo' 和 'bird' 中的 'b'
```

##### +

匹配前一个表达式 1 次或者多次，等价于{1,}

```javascript
/a+/ 会匹配 "candy" 中的 'a'，"caaaat" 中的 'aaaa'
```

##### ?

匹配前一个表达式 0 次或者 1 次，等价于 {0, 1}

```javascript
/e?el?/ 会匹配 "angle" 中 'le', "sole" 中的 'e'
```

##### .

匹配除换行符之外的任何单个字符

```javascript
/.n/ 将会匹配 "nay, an apple is on the tree" 中的 'an' 和 'on'，但是不会匹配 'nay'
```



#### 特殊字符

##### \b

匹配一个词的边界（一个词的边界就是一个词不被另外一个词跟随的位置或者不是另一个词汇字符前边的位置）

```javascript
/\bm/ 匹配 "moon" 中得 'm'

/oo\b/ 并不匹配 "moon" 中得 'oo'，因为 'oo' 被一个词汇字符 'n' 紧跟着。

/oon\b/ 匹配 "moon" 中得 'oon'，因为 'oon' 是这个字符串的结束部分。这样他没有被一个词汇字符紧跟着。
```

##### \B

匹配一个非单词边界 (一个字符串的开始和结尾都被认为是非单词)

```javascript
/\B../ 匹配 "noonday" 中得 'oo', 而 /y\B./ 匹配 "possibly yesterday" 中得 'ye'
```

##### \d

匹配一个数字，等价于 [0-9]

```javascript
\d 匹配 "B2 read" 中的 2
```

##### \D

匹配一个非数字，等价于 `[^0-9]`

```javascript
/\D/ 匹配 "B2 read" 中的 B r e a d
```

##### \s

匹配一个空白字符，包括空格、制表符、换行符和换页符

```javascript
/\s\w*/ 匹配 "foo bar" 中的 'bar'
```

##### \S

匹配一个非空白字符

```javascript
/\S\w/ 匹配 "foo bar" 中的 'foo' 和 'bar'
```

##### \w

匹配一个单字符：字母、数字和下划线，等价于 [A-Za-z0-9_]

##### \W

匹配一个非单字符：字母、数字和下划线，等价于` [^A-Za-z0-9_]`



#### 特殊运算符

##### {n}

n是一个正整数，匹配了前面一个字符刚好发生了n次

```javascript
/a{2}/ 不会匹配“candy”中的'a',但是会匹配“caandy”中所有的a，以及“caaandy”中的前两个'a'。
```

##### {n, m}

n 和 m 都是整数。匹配前面的字符至少n次，最多m次。如果 n 或者 m 的值是0， 这个值被忽略

```javascript
/a{1,3}/ 并不匹配“cndy”中的任意字符，匹配“candy”中得a，匹配“caandy”中的前两个a，也匹配“caaaaaaandy”中的前三个a。注意，当匹配”caaaaaaandy“时，匹配的值是“aaa”，即使原始的字符串中有更多的a
```

##### (x)

匹配 'x' 并且记住匹配项 (*捕获括号*)

```javascript
模式/(foo) (bar) \1 \2/中的 '(foo)' 和 '(bar)' 匹配并记住字符串 "foo bar foo bar" 中前两个单词。模式中的 \1 和 \2 匹配字符串的后两个单词。注意 \1、\2、\n 是用在正则表达式的匹配环节。在正则表达式的替换环节，则要使用像 $1、$2、$n 这样的语法，例如，'bar foo'.replace( /(...) (...)/, '$2 $1' )
```

##### (?:x)

匹配 'x' 但是不记住匹配项 (*非捕获括号*)

```javascript
 /(?:foo){1,2}/。如果表达式是 /foo{1,2}/，{1,2}将只对 ‘foo’ 的最后一个字符 ’o‘ 生效。如果使用非捕获括号，则{1,2}会匹配整个 ‘foo’ 单词
```

##### x(?=y)

匹配 'x' 仅仅当 'x' 后面跟着 'y' (*正向肯定查找*)

```javascript
/Jack(?=Sprat)/ 会匹配到 'Jack' 仅仅当它后面跟着 'Sprat'
/Jack(?=Sprat|Frost)/ 匹配 ‘Jack’ 仅仅当它后面跟着 'Sprat' 或者是 ‘Frost’
```

##### x(?!y)

匹配 'x' 仅仅当 'x' 后面不跟着 'y' (*正向否定查找*)

```javascript
/\d+(?!\.)/匹配一个数字仅仅当这个数字后面没有跟小数点的时候。正则表达式/\d+(?!\.)/.exec("3.141")匹配‘141’但是不是‘3.141’
```

##### x|y

匹配 x 或者 y

```javascript
/green|red/ 匹配“green apple”中的‘green’和“red apple”中的‘red’
```

##### [x,y,z]

一个字符集合。匹配方括号的中任意字符。可以使用破折号（-）来指定一个字符范围。对于点（.）和星号（*）这样的特殊符号在一个字符集中没有特殊的意义

```javascript
[abcd] 和[a-d]是一样的。他们都匹配"brisket"中得‘b’,也都匹配“city”中的‘c’。/[a-z.]+/ 和/[\w.]+/都匹配“test.i.ng”中得所有字符
```

##### [^x,y,z]

一个反向字符集

```javascript
[^abc] 和 [^a-c] 是一样的。他们匹配"brisket"中得‘r’，也匹配“chop”中的‘h’
```



#### 平衡组

##### (?'group')

把捕获的内容命名为 group，并压入堆栈。

##### (?'-group')

把推栈上弹出最后入栈名为 group 的捕获内容，如果推栈本来为空，则本分组的匹配失败

##### (?(group)yes|no)

如果推栈上存在名为 group 的捕获内容，则进行 yes 部分的匹配，否则进行 no 部分的匹配

##### (?!)

 零宽负向先行断言，由于没有后缀表达式，试图匹配总是失败

```javascript
var reg = /<[^<>]*(((?'Open'<)[^<>]*)+((?'-Open'>)[^<>]*)+)*(?(Open)(?!))>/
var regHtml = /<div[^>]*>[^<>]*(((?'Open'<div[^>]*>)[^<>]*)+((?'-Open'<\/div>)[^<>]*)+)*(?(Open)(?!))<\/div>./
```



#### 运用

##### 使用括号的子字符串匹配

```javascript
var re = /(\w+)\s(\w+)/
var str = "John Smith"
var newstr = str.replace(re, "$2, $1")
console.log(newstr)	// => 'Smith, John'
```


