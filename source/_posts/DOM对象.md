---
title: JavaScript DOM对象
date: 2017-1-12T11:05:15.000Z
tags:
  - javascript
description: DOM—Document Object Model,它是W3C国际组织的一套Web标准。它定义了访问HTML文档对象的一套属性、方法和事件。
photos: 'http://oizt3fjv8.bkt.clouddn.com/dom.png'
---

## 选择
```javascript
根据ID         document.getElementById('xxx')
根据类名        document.getElementsByClassName('highlight')
根据标签名      document.getElementsByTagName('td')

选择一个元素    document.querySelector(".myclass")
选择多个元素    document.querySelectorAll("div.note, div.alert")
```

## 创建
```javascript
创建元素节点    document.createElement('div')
创建文本节点    document.createTextNode('hello world!')
```

## 查找
```javascript
父节点          ele.parentElement

多个子节点      ele.children
第一个子节点    ele.firstElementChild
最后一个子节点  ele.lastElementChild
子节点个数      ele.childElementCount

前一个兄弟元素  ele.previousElementSibling
后一个兄弟元素  ele.nextElementSibling  
```
## 获取内容
```javascript
获取文本内容     el.textContent
获取Html内容     el.innerHTML
```

## 更改
```javascript
添加          ele.appendChild(el)
删除          ele.removeChild(el)
替换          ele.replaceChild(el1, el2)
克隆          el.cloneNode(true)
外部后面插入  el.insertAdjacentHTML('afterend', htmlString)
外部前面插入  el.insertAdjacentHTML('beforebegin', htmlString)
内部后面插入  parentEle.appendChild(el)
内部前面插入  parentEle.insertBefore(newEle , referenceEle)
```
## 属性
```javascript
获取属性    el.getAttribute('class')
设置属性    el.setAttribute('class', 'highlight')
移除属性    el.removeAttribute('class')
判断属性    el.hasAttribute('class')
```

## 样式
```javascript
添加类     el.classList.add(className)
移除类     el.classList.remove(className)
触发类     el.classList.toggle(className)
判断类     el.classList.contains(className)
```
