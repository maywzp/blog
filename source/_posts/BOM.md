---
title: BOM 操作
date: 2018-10-23 19:31:39
updated: 2018-10-23 19:31:39
tags: 'javascript操作手册'
description: Javascript BOM操作总结
---

### 全局对象
```bash
window     当前窗口，如果文档包含框架（frame 或 iframe 标签），浏览器会为 HTML 文档创建一个 window 对象，并为每个框架创建一个额外的 window 对象。
top        最顶层浏览器窗口
parent     当前窗口的父窗口
self       当前窗口,等价于window
```

### 窗口位置
```
screen.width   浏览器屏幕宽度
screen.height  浏览器屏幕高度

pageXOffset    滚动条距离左边的位置
pageYOffset    滚动条距离顶部的位置

scrollTo(w, h) 滚动到那个位置
```


注：以下对象都为全局对象，即 `window.history === history`

### history

#### forward（前进）

等价于 `history.go(1)`

```javascript
history.forward()
```

#### back（后退）

等价于 `history.go(-1)`

```javascript
history.back()
```

#### go（跳转至指定历史页面）

指定值大于当前历史长度时无效

```javascript
history.go(2)
```

#### pushState（无刷新的插入一条历史记录）

并不会刷新页面 参数：stateObject 状态对象、title 标题、url 历史记录地址 适用于单页应用，在完成一次Ajax请求的同时，为浏览器创造一个历史状态。

```javascript
// 假如当前URL为：http://example.com/getFinaData.php
history.pushState({year: 2018}, '页面标题', 'getFinaData.php?year=2018')
// 此时URL变为：http://example.com/getFinaData.php?year=2018
```

#### replaceState（替换当前历史状态）

并不会刷新页面 参数：stateObject 状态对象、title 标题、url 历史记录地址

```javascript
history.replaceState({year: 2018}, '页面标题', 'getFinaData.php?year=2018')
```

### location

下面的接口不止用于获取当前URL信息，同样可用于设置URL信息。

#### protocol（协议）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.protocol // 'https'
```

#### host（主机域名加端口号）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.host // 'www.google.com'
```

#### hostname（主机域名）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’location.hostname
location.hostname // 'www.google.com'
```

#### port（端口号）

默认端口号是 80

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.port //  ''
```

#### pathname（路径名）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.pathname // 'search'
```

#### search（查询参数）

`?` 号之后的部分，不包含 hash

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.search // '?q=may&oq=may'
```

#### hash（锚点）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash’
location.hash // '#hash'
```

#### href（完整路径）

```javascript
// url ：'https://www.google.com/search?q=may&oq=may#hash'
location.href // 'https://www.google.com/search?q=may&oq=may#hash'
```

#### assign（加载新页面）

会增加一个历史状态，不会替换掉当前历史

```javascript
location.assign('https://www.baidu.com')
```

#### replace（替换页面）

直接替换当前历史状态

```javascript
location.replace('https://www.baidu.com')
```

#### reload（刷新页面）

参数：forced 是否强制从服务器加载资源，如果为false则从浏览器缓存中读取网页资源。默认：false。

```javascript
location.reload()
location.reload(true)
```

### naviagtor

#### platform（当前浏览器所在的操作系统）

```javascript
navigator.platform // 'MacIntel'
```

#### userAgent（当前浏览器版本信息）

```javascript
navigator.userAgent // 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36'
```

#### 获取客户端操作系统

```javascript
// 返回值：Windows、Unix、Linux、Mac、Iphone、Android、Unknown
function getOS() {
  const ua = navigator.userAgent.toLowerCase()
  let osName = 'Unknown'

  if (ua.includes('win')) osName = 'Windows'
  else if (ua.includes('iphone')) osName = 'Iphone'
  else if (ua.includes('mac')) osName = 'Mac'
  else if (ua.includes('linux') && ua.includes('android')) osName = 'Android'
  else if (ua.includes('linux') && !ua.includes('android')) osName = 'Linux'
  else if (
    ua.includes('x11') ||
    ua.includes('unix') ||
    ua.includes('sunname') ||
    ua.includes('bsd')
  )
    osName = 'Unix'
  else osName = 'Unknown'

  return osName
}
```

#### 获取客户端浏览器信息

```javascript
function getBrowser() {
  const ua = navigator.userAgent.toLowerCase()
  let browserName = 'Unknown'

  if (ua.includes('firefox')) browserName = 'Firefox'
  else if (ua.includes('trident')) browserName = 'IE'
  else if (ua.includes('qqbrowser') || ua.includes('tencenttraveler'))
    browserName = 'QQ'
  else if (ua.includes('ubrowser')) browserName = 'UC'
  else if (ua.includes('bidubrowser')) browserName = '百度'
  else if (ua.includes('metasr')) browserName = '搜狗'
  else if (
    Object.values(navigator.mimeTypes).some(
      v => v.type === 'application/vnd.chromium.remoting-viewer'
    )
  )
    browserName = '360'
  else if (ua.includes('chrome') && window.chrome) browserName = 'Chrome'
  else if (ua.includes('safari')) browserName = 'Safari'
  else browserName = 'Unknown'

  return browserName
}
```

