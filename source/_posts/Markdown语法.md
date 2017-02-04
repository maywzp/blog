---
title: Markdown语法
date: 2016-10-10 10:30:09
tags: ["语法"]
description: Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。
photos: http://oizt3fjv8.bkt.clouddn.com/markdown.jpg
---

## 标题

#       一级标题
##      二级标题
###     三级标题
####    四级标题
#####   五级标题
######  六级标题

```
  #       一级标题
  ##      二级标题
  ###     三级标题
  ####    四级标题
  #####   五级标题
  ######  六级标题
```

## 列表
### 无序列表
- 文本1
- 文本2
- 文本3

```
- 文本1
- 文本2
- 文本3
```

### 有序列表
1. 文本1
2. 文本2
3. 文本3

```
1. 文本1
2. 文本2
3. 文本3
```

## 链接
### 普通链接
[百度](http://www.baidu.com)

```
[百度](http://www.baidu.com)
```
### 图片查看
![](http://ww4.sinaimg.cn/bmiddle/aa397b7fjw1dzplsgpdw5j.jpg)

```
![](http://ww4.sinaimg.cn/bmiddle/aa397b7fjw1dzplsgpdw5j.jpg)
```

## 引用
> 一盏灯，一片昏黄；一简书，一杯淡茶。

```
> 一盏灯，一片昏黄；一简书，一杯淡茶。
```

## 字体
### 粗体
**加粗**

```
  **加粗**
```
### 斜体
*斜体*

```
*斜体*
```

## 代码引用
### 单行引用
`cwd: 'tmp/fontawesome/fonts'`

```
`cwd: 'tmp/fontawesome/fonts/'`
```

### 多行引用
```
expand: true,
cwd: 'tmp/fontawesome/fonts/',
src: ['**'],
dest: 'source/css/fonts/'
```

## 表格
dog | bird | cat
----|------|----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

```
dog | bird | cat
----|------|----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz
```
