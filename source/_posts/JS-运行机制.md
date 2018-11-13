---
title: JS 运行机制
date: 2018-11-12 16:22:07
updated: 2018-11-13 15:03:30
tags: '知识点'
---

### 多进程的浏览器

浏览器的进程包括：

#### Browser 进程

浏览器的主进程（负责协调、主控），只有一个。作用有:

- 负责浏览器界面显示，与用户交互。如前进，后退等
- 负责各个页面的管理，创建和销毁其他进程
- 将 Renderer 进程得到的内存中的 Bitmap，绘制到用户界面上
- 网络资源的管理，下载等

#### 第三方插件进程

每种类型的插件对应一个进程，仅当使用该插件时才创建

#### GPU 进程

最多一个，用于 3D 绘制等

#### 浏览器渲染进程（浏览器内核，Renderer 进程）

默认每个 Tab 页面一个进程，互不影响。主要作用为:

- 页面渲染，脚本执行，事件处理等

### 多线程的浏览器内核

对于普通的前端操作来说，主要用到的是渲染进程。
渲染进程常驻线程包括：

#### GUI 渲染线程

负责渲染浏览器界面，解析 HTML，CSS，构建 DOM 树和 RenderObject 树，布局和绘制等。

当界面需要重绘（Repaint）或由于某种操作引发回流(reflow)时，该线程就会执行

注意，GUI 渲染线程与 JS 引擎线程是互斥的，当 JS 引擎执行时 GUI 线程会被挂起（相当于被冻结了），GUI 更新会被保存在一个队列中等到 JS 引擎空闲时立即被执行。

#### JS 引擎线程

也称为 JS 内核，负责处理 Javascript 脚本程序。（例如 V8 引擎）

JS 引擎线程负责解析 Javascript 脚本，运行代码。

JS 引擎一直等待着任务队列中任务的到来，然后加以处理，一个 Tab 页（renderer 进程）中无论什么时候都只有一个 JS 线程在运行 JS 程序

同样注意，GUI 渲染线程与 JS 引擎线程是互斥的，所以如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞。

#### 事件触发线程

归属于浏览器而不是 JS 引擎，用来控制事件循环（可以理解，JS 引擎自己都忙不过来，需要浏览器另开线程协助）

当 JS 引擎执行代码块如 setTimeOut 时（也可来自浏览器内核的其他线程,如鼠标点击、AJAX 异步请求等），会将对应任务添加到事件线程中

当对应的事件符合触发条件被触发时，该线程会把事件添加到待处理队列的队尾，等待 JS 引擎的处理

注意，由于 JS 的单线程关系，所以这些待处理队列中的事件都得排队等待 JS 引擎处理（当 JS 引擎空闲时才会去执行）

#### 定时触发器线程

传说中的 setInterval 与 setTimeout 所在线程

浏览器定时计数器并不是由 JavaScript 引擎计数的,（因为 JavaScript 引擎是单线程的, 如果处于阻塞线程状态就会影响记计时的准确）

因此通过单独线程来计时并触发定时（计时完毕后，添加到事件队列中，等待 JS 引擎空闲后执行）

注意，W3C 在 HTML 标准中规定，规定要求 setTimeout 中低于 4ms 的时间间隔算为 4ms。

#### 异步 http 请求线程

在 XMLHttpRequest 在连接后是通过浏览器新开一个线程请求

将检测到状态变更时，如果设置有回调函数，异步线程就产生状态变更事件，将这个回调再放入事件队列中。再由 JavaScript 引擎执行。

![](https://ws4.sinaimg.cn/large/006tNbRwgy1fx5dl9dvdej307z0g1mxo.jpg)

### Event Loop

1. 所有同步任务都在主线程上执行，形成一个`执行栈（execution context stack）`
2. 主线程之外，事件触发线程管理一个`任务队列（task queue）`。
3. 当`执行栈`中所有的同步任务执行完成，系统就会读取`任务队列`，将可运行的异步任务添加到`执行栈`中，开始执行

![](https://ws1.sinaimg.cn/large/006tNbRwgy1fx5cqbhme7j30gy0hpdgl.jpg)

- 主线程运行时会产生执行栈，栈中的代码调用某些 api 时，它们会在事件队列中添加各种事件
- 而栈中的代码执行完毕，就会读取事件队列中的事件，去执行那些回调
- 如此循环

这个循环的过程称为“Event Loop”
** 注意，总是要等待执行栈中的代码执行完毕后才会去读取事件队列中的事件 **

![](https://ws3.sinaimg.cn/large/006tNbRwgy1fx6an3z4kzj30ho0ee0tl.jpg)

### 浏览器渲染流程

#### 参考资料

[阮一峰-网页性能管理详解](http://www.ruanyifeng.com/blog/2015/09/web-page-performance-in-depth.html)
[从输入 URL 到页面加载的过程？如何由一道题完善自己的前端知识体系！](https://segmentfault.com/a/1190000013662126#articleHeader34)

#### 页面的生成过程

1. 解析 HTML，构建 DOM 树
2. 解析 CSS，生成 CSS 规则树
3. 结合 DOM 树 和 CSS 规则 生成渲染树（Render Tree）
4. 布局 Render Tree（layout/reflow），负责各元素尺寸、位置的计算
5. 绘制 Render Tree（paint），绘制页面像素信息
6. 浏览器会将各层的信息发送给 GPU，GPU 会将各层合成（composite），显示在屏幕上

![](https://ws1.sinaimg.cn/large/006tNbRwgy1fx69iodg1sj30p009smxu.jpg)

** 第一步：解析 HTML，构建 DOM 树 **
过程：`Bytes → characters → tokens → nodes → DOM`
![](https://ws1.sinaimg.cn/large/006tNbRwgy1fx6g5efm4zj30m80cb762.jpg)

** 第二步：解析 CSS，生成 CSS 规则树 **
过程：`Bytes → characters → tokens → nodes → CSSOM`
![](https://ws3.sinaimg.cn/large/006tNbRwgy1fx6g7aw301j30g608bt9m.jpg)

** 第三步：生成渲染树 **
有一些不可见的 DOM 元素不会插入到渲染树中，如 head 这种不可见的标签或者 display: none 等。
![](https://ws1.sinaimg.cn/large/006tNbRwgy1fx6g87s37xj30m80adabj.jpg)

** 第四部：渲染 **
图中的线与箭头代表通过 js 动态修改了 DOM 或 CSS，导致了重新布局（Layout）或渲染（Repaint）。
![](https://ws4.sinaimg.cn/large/006tNbRwgy1fx6g9oa4z6j30m80640tv.jpg)

#### DOMContentLoaded 和 load

DOMContentLoaded 在 DOM 加载完之后触发
load 事件在 DOM、CSS、JS、图片都加载完之后才触发

DOMContentLoaded 先于 load 触发

#### 重排和重绘

重排/回流（reflow）：重新生成布局
重绘（repaint）：重新绘制
“重绘”不一定需要“重排”，“重排”必然导致“重绘”。

触发 reflow 的属性：

- 盒模型相关的属性: width，height，margin，display，border
- 定位属性及浮动相关的属性: top，position，float
- 改变节点内部文字结构也会触发回流: text-align, overflow, font-size, line-height, vertical-align

此外以下情况也会触发 reflow：

- 调整窗口大小
- 样式表变动
- 元素内容变化，尤其是输入控件
- dom 操作
- css 伪类激活
- 计算元素的 offsetWidth、offsetHeight、clientWidth、clientHeight、width、height、scrollTop、scrollHeight

触发 repaint 情况：

- 更新样式风格相关的属性，如 background，color，cursor，visibility

CSS 样式引起重绘和重排对照表：[https://csstriggers.com](https://csstriggers.com)

#### 复合层

[一篇文章说清浏览器解析和 CSS（GPU）动画优化](https://segmentfault.com/a/1190000008015671)

#### 提高性能的九个技巧

1. DOM 的多个读操作（或多个写操作），应该放在一起。不要两个读操作之间，加入一个写操作。
2. 如果某个样式是通过重排得到的，那么最好缓存结果。避免下一次用到的时候，浏览器又要重排。
3. 不要一条条地改变样式，而要通过改变 class，或者 csstext 属性，一次性地改变样式。
4. 尽量使用离线 DOM，而不是真实的网面 DOM，来改变元素样式。比如，操作 Document Fragment 对象，完成后再把这个对象加入 DOM。再比如，使用 cloneNode() 方法，在克隆的节点上进行操作，然后再用克隆的节点替换原始节点。
5. 先将元素设为 `display: none`（需要 1 次重排和重绘），然后对这个节点进行 100 次操作，最后再恢复显示（需要 1 次重排和重绘）。这样一来，你就用两次重新渲染，取代了可能高达 100 次的重新渲染。
6. position 属性为`absolute`或`fixed`的元素，重排的开销会比较小，因为不用考虑它对其他元素的影响。
7. 只在必要的时候，才将元素的 display 属性为可见，因为不可见的元素不影响重排和重绘。另外，`visibility : hidden`的元素只对重绘有影响，不影响重排。
8. 使用虚拟 DOM 的脚本库，比如 React 等。
9. 使用 window.requestAnimationFrame()、window.requestIdleCallback() 这两个方法调节重新渲染。

#### `window.requestAnimationFrame()`

将某些代码放到下一次重新渲染时执行，提高网页性能。

```javascript
// 让读操作和写操作分离，把所有的写操作放到下一次重新渲染
function doubleHeight(element) {
  var currentHeight = element.clientHeight
  window.requestAnimationFrame(function() {
    element.style.height = currentHeight * 2 + 'px'
  })
}
elements.forEach(doubleHeight)
```
