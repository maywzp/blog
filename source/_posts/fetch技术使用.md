---
title: fetch技术使用
date: 2017-1-5 14:47:15
updated: 2017-1-5 14:47:15
tags: ['javascript']
description: 与XMLHttpRequest(XHR)类似，fetch()方法允许你发出AJAX请求。区别在于Fetch API使用Promise，因此是一种简洁明了的API，比XMLHttpRequest更加简单易用。
---

## 使用

```javascript
function status(response) {
  if (response.status >= 200 && response.status < 300) {
    return Promise.resolve(response)
  } else {
    return Promise.reject(new Error(response.statusText))
  }
}

const fetchWrap = url => ops => fetch(url, {
  method: 'post',
  headers: {
    'Content-type': 'application:/x-www-form-urlencoded:charset=UTF-8'
  },
  body: 'name=may&age=40',
  ...ops
})
  .then(status)
  .then(json)
  .then(function(data) {
    console.log('请求成功，JSON解析后的响应数据为:', data)
  })
  .catch(function(err) {
    console.log('Fetch错误:' + err)
  })
```
