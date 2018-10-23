---
title: DOM 操作
date: 2017-1-12T11:05:15.000Z
updated: 2018-10-19 16:37:00
tags: 'javascript操作手册'
description: DOM 操作总结。
---

DOM 节点分类：

文档节点、元素节点、文本节点、属性节点、注释节点

后面的操作基于此 DOM

```html
<div class="container" name="container" style="color: #444;font-size: 16px;">
  <div class="item">item</div>
  <div class="item">item</div>
  <div class="item special">item special</div>
</div>
<script>
  var items = document.querySelectorAll('.item')
  var container = document.querySelector('.container')
    
  var insertStr = '<div class="item insert">item</div>'
  var insertEle = document.createElement('div')
  insertEle.innerText = 'item insert'
</script>
```

### 元素节点操作

#### isSameNode（是否是同一个节点）

```javascript
items[0].isSameNode(items[0]) // true
items[0].isSameNode(items[1]) // false
```

#### isEqualNode（两个节点是否相等）

```javascript
与属性顺序无关
items[0].isEqualNode(items[1]) // true
items[0].isEqualNode(items[2]) // false
```

#### compareDocumentPosition（比较两个节点相对位置）

返回值：

1：没有关系，两个节点不属于同一个文档。 

2：第一节点（P1）位于第二个节点（P2）后。

4：第一节点（P1）定位在第二节点（P2）前。

8：第一节点（P1）位于第二节点（P2）内。 

16：第二节点（P2）位于第一节点（P1）内。 

32：没有关系，或是两个节点是同一元素的两个属性。

返回值可组合，比如：20 = 16 + 4

```javascript
container.compareDocumentPosition(items[0]) // 20
items[0].compareDocumentPosition(items[1]) // 4
```

#### innerHTML（获取/设置后代 HTML）

```javascript
container.innerHTML // 获取
container.innerHTML = insertStr // 设置
```

#### replaceChild（节点替换）

```javascript
container.replaceChild(items[2], items[0]) // items[2] 替换 items[0]
```

#### removeChild（移除节点）

```javascript
container.removeChild(items[2]) // 移除 items[2]
```

#### appendChild（添加节点到末尾）

```javascript
container.appendChild(insertEle) // 添加 insertEle 节点到 container 节点末尾
```

#### insertBefore（在指定节点前插入新节点）

```javascript
container.insertBefore(insertEle, items[1]) // 添加 insertEle 节点到 items[1] 节点之前
```

#### cloneNode（克隆指定节点）

如果不指定`true`参数，只是克隆当前节点

```javascript
var cloneEle = items[2].cloneNode(true) // 复制 items[2] 节点
container.appendChild(cloneEle)
```

#### createElement（创建元素节点）

```javascript
var createEle = document.createElement('div') // 创建元素节点
var createTxt = document.createTextNode('item create') // 创建文本节点
createEle.appendChild(createTxt)
container.appendChild(createEle)
```

#### createTextNode（创建文本节点）

```javascript
var createTxt = document.createTextNode('item create') // 创建文本节点
container.appendChild(createTxt)
```

### 元素节点查询

下面👇原生的方法会将换行符也当作文本子节点处理，也包括注释节点，调用前**需清除空格和注释**

#### childNodes（返回子节点的集合）

```javascript
var children = container.childNodes
children.length // 3
```

#### firstChild（第一个子节点）

```javascript
var first = chontainer.firstChild
first.innerText // 'item'
```

#### lastChild（最后一个子节点）

```javascript
var last = container.lastChild
last.innerText // 'item special'
```

#### nextSibling（下一个兄弟节点）

```javascript
var next = items[0].nextSibling
next.innerText // 'item'
```

#### previousSibling（上一个兄弟节点）

```javascript
var prev = items[1].previousSibling
prev.innerText // 'item'
```

#### parentNode（父节点）

```javascript
var parent = items[0].parentNode
parent // 返回 container 节点
```

#### 实际推荐使用

上述方法对应的另一个版本，只返回元素节点，推荐使用，其对应关系如下：

```javascript
children 			   -> 	childNode
firstElementChild 	   -> 	firstChild
lastElementChild 	   -> 	lastChild
previousElementSibling -> 	previousSibling
nextElementSibling 	   ->   nextSibling
parentElement 		   ->   parentNode
```

### 属性节点操作

#### attributes（返回所有属性节点）

```javascript
var attr = container.attributes
attr.class.value // 'container'
```

#### getAttribute（获取指定属性值）

```javascript
container.getAttribute('class') // 'container'
```

#### getAttributeNode（获取指定属性节点）

```javascript
var attrNode = container.getAttributeNode('name')
attrNode.value // 'container
```

#### hasAttribute（是否具有指定属性）

```javascript
container.hasAttribute('name') // true
container.hasAttribute('id') // false
```

#### hasAttributes（是否至少含有一个属性）

```javascript
container.hasAttributes() // true
```

#### removeAttribute（移除指定属性）

```javascript
container.removeAttribute('name') // 移除 name 属性
```

#### removeAttributeNode（移除指定属性节点）

```javascript
var attrNode = container.getAttributeNode('name')
container.removeAttributeNode(attrNode) // 移除 name 属性节点
```

#### setAttribute（添加属性）

```javascript
如果属性已存在，则更新相应的属性
container.setAttribute('id', 'container') // 设置 属性 id=container
```

#### setAttributeNode（添加属性节点）

```javascript
var classNode = items[2].getAttributeNode('class')
items[0].setAttributeNode(classNode.cloneNode(true)) // items[0] 与 items[2] 的 class 相同了
```

### 元素节点样式

#### style（获取/设置当前元素内嵌样式）

```javascript
container.style.fontSize // '16px' 获取

container.style.fontSize = '20px' // 设置

container.style.setProperty('font-size', '20px') // 使用 setProperty 设置

container.style.removeProperty('font-size') // 移除某个样式
```

#### className（获取/设置节点样式类名）

```javascript
items[2].className // 'item special'  获取

items[2].className = 'item' // 设置
```

#### classList（管理节点样式类）

推荐使用 `classList` 而非 `className` 管理样式类

```javascript
contains.classList.contains('container') // 是否具有指定类

container.classList.add('custom-class-1', 'custom-class-2') // 添加类

container.classList.remove('custom-class-1', 'custom-class-2') // 移除类

container.classList.replace('container', 'custom-container') // 类名替换

container.classList.toggle('toggle') // 切换类
container.classList.toggle('toggle'， true)   // 添加类
container.classList.toggle('toggle'， false)  // 移除类

```

getComputedStyle（获取元素所有样式）

包括：类 和 内嵌样式。只读

```javascript
var computedStyle = window.getComputedStyle(container)
computedStyle.fontSize // '16px'
```

### 元素节点属性

#### contentEditable（获取/设置是否可编辑）

```javascript
container.contentEditable // 'inherit' 获取

container.contentEditable = true // 设置
```

#### isContentEditable（判断是否可编辑）

与 `contentEditable` 不同的是，该属性只返回 `true` 或者 `false`

```javascript
container.isContentEditable // false
```

#### toString（返回节点字符串）

```javascript
container.toString() // '[object HTMLDivElement]'
container.getAttributeNode('name').toString() // '[object Attr]'
container.nextSibling.toString() // '[object Text]'
```

#### id（获取/设置节点id）

```javascript
container.id = 'container' // 设置

container.id // 'container' 获取
```

#### title（获取/设置节点title）

```javascript
container.title = '容器' // 设置

container.title // '容器' 获取
```

#### dataset（获取/设置 data- 开头的属性）

```javascript
container.dataset.userName = 'may' // 设置  data-user-name = 'may'

container.dataset.userName // 'may'  获取 data-user-name
```

#### nodeName（当前元素节点标签名）

返回的标签名都是大写的

```javascript
container.nodeName // 'DIV'
```

#### nodeType（节点类型）

常见值：

1：元素节点

2：属性节点

3：文本节点

```javascript
container.nodeType // 1
```

#### nodeValue（获取/设置文本节点值）

```javascript
container.nextSibling.nodeValue = 'next' // 设置

container.nextSibling.nodeValue // 'next' 获取
```

#### tagName（当前节点的标签名）

在 XML 文档中，会保留标签的原始大小写；在 HTML 文档中，以大写形式返回，与`nodeName`返回值一致。

```javascript
container.tagName // 'DIV'
```

#### tabIndex（使用tab键触发焦点读取顺序）

可读可写

 支持 tabIndex 的元素：`a` `area` `button` `input` `object` `select` `textarea`

#### textContent（返回当前节点及其后代的文本内容）

```javascript
container.textContent // 'item item item special'
```

### 节点位置

#### Element.getBoundingClientRect()

返回元素的大小以及相对于**浏览器可视窗口**的位置

```javascript
var rect = container.getBoundingClientRect()
rect // {x: 8, y: 8, width: 812, height: 66, top: 8, bottom: 74, left: 8, right: 820}
```

#### Element.scrollHeight（当前元素内容高度）

包含溢出不可见的部分

#### Element.scrollWidth（当前元素内容宽度）

包含溢出不可见的部分

#### Element.scrollLeft（当前元素的左侧部分不可见内容的长度）

元素内容左边缘到可见区域左边

#### Element.scrollTop（当前元素的上面部分不可见内容的高度）

即元素内容顶部到可见区域顶部的距

#### Element.clientHeight（内部高度）

内部高度 = 内容高度 + 内边距 

不包含 滚动条、边框、外边距 值返回整数，如果是小数会四舍五入

#### Element.clientWidth（内部宽度）

内部宽度 = 内容宽度 + 内边距 

不包含 滚动条、边框、外边距 值返回整数，如果是小数会四舍五入

#### Element.offsetHeight（外部高度）

外部高度 = 内容高度 + 内边距 + 滚动条 + 边框 

不包括 外边距 值返回整数，如果是小数会四舍五入

#### Element.offsetWidth（外部宽度）

外部宽度 = 内容宽度 + 内边距 + 滚动条 + 边框 

不包括 外边距 值返回整数，如果是小数会四舍五入

#### Element.offsetTop（祖先元素顶部的距离）

此时的祖先元素是指 层级最近、包含定位样式 的祖先元素

#### Element.offsetLeft（祖先元素左边的距离）

此时的祖先元素是指 层级最近、包含定位样式 的祖先元素