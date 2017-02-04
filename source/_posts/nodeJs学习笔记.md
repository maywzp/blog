---
title: nodeJS学习笔记
date: 2016-12-18 16:44:28
tags: ['node']
description: Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。
photos: http://oizt3fjv8.bkt.clouddn.com/nodeno1.jpg
---

## 程序构成-四大模块
1.入口模块（index.js）:创建http服务器，加载router文件模块，分发请求资源。
2.路由处理模块（router.js）:处理所有请求资源，分发到不同处理模块。
3.DNS解析模块（parse_dns.js）: 根据获取的域名进行解析，返回相应的处理结果到页面。
4.首页展示模块（main_index.js）：使用fs模块读取index.html页面字符数据，然后返回到客户端。

## 全局变量
```
_filename：输出当前文件的绝对路径，包含文件名
e:\WebWork\uuuuu\bin\test-stream.js

_dirname: 输出当前文件所在目录，不包含文件名
e:\WebWork\uuuuu\bin
```

## 事件模块（events）
```javascript
var events = require('events');  //引用events模块
var eventEmitter =new events.EventEmitter();     //创建eventEmitter对象

eventEmitter.on('one', function(name, age){         //     事件绑定
  console.log("连接成功");
  console.log(name);
  console.log(age);
});
eventEmitter.emit('one', 'cangjie', 22);     //事件触发
eventEmitter.emit('error');     //自带error事件
```

### eventEmitter方法
```javascript
addListener(event, listener)    添加一个监听器到监听数组末尾，与on功能相同;
on(event, listener)             注册一个监听器；
once(event, listener)           注册单次监听器；
removeListener(event, listener) 删除指定监听器；
removeAllListener([event])      删除全部监听器，若有参数删除指定监听器；
setMaxListeners(n)              设置最大数量监听器；
listeners(event)                返回事件的监听执行函数；
emit()                          触发监听器；
```

## url处理
require('url')
require('querystring')
```javascript
(例url:http://localhost:3000//test?name=cangjie&book=nodeJs)
req.url: test?name=cangjie&book=nodeJs
获取pathname:   url.parse(req.url).pathname //test
```
### get
```
获取参数:   var paramStr = url.parse(req.url).query   //name=cangjie&book=nodeJs
参数解析：   var param = querystring.parse(paramStr )      //{name: 'cangjie', book: 'nodeJs'}   JSON类型
获取name：   var name = querystring.parse(url.parse(req.url).query).name   //cangjie
```

### post
```javascript
req.addListener("data",function(postDataChunk){
    postData += postDataChunk;
})
req.addListener("end",function(){
    var param = querystring.parse(postData);
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('success');
})
```

## http
### http属性
```javascript
res.writeHead:            添加响应头部
res.setEncoding("utf-8"): 设置返回客户端数据格式
res.end:                  执行响应返回web客户端
```

### http方法
```javascript
createServer:                         创建一个http服务器
req.addListener("data",function(){}): 数据传输到服务器时触发的事件，读取客户端传递来的数据
req.addListener("end",function(){}):  数据接收完成触发的事件
```

## 文件模块
```javascript
fs.rename(path1, path2, [callback]) ——重命名
fs.chmod(path, mode, [callback]) ——修改权限
fs.stat(path, [callback]) ——获取文件元信息
fs.realfile(path, [callback]) ——读取文件数据
fs.exists(path, [callback]) ——验证文件存在
fs.unlink(path, [callback]) ——删除文件
fs.write(fd, buffer, offset, length, position, [callback]) ——文件写读

callback：
function(err){
    if(err){
        throw err;
     }
}
```

## module.exports和exports的区别
module.exports包含exports,exports只能返回一个json对象，而module.exports可以返回多种数据格式。

## 文件流模块（stream）
### 读取文件
```javascript
var readerStream = fs.createReadStream('./index.js');
  readerStream.on('data',function(chunk){  //内容读取过程
  data += chunk;
});
readerStream.on('end',function(){          //内容读取完成
  console.log(data);
});
readerStream.on('err',function(err){       //异常处理
  console.log(err.stack);
});
```
### 写入流：（文件会被新内容覆盖）
```
var writeStream = fs.createWriteStream('./http.js');
writeStream.write(data,'utf-8');     //写入数据
writeStream.end();     //标记文件末尾
writeStream.on('finish',function(){
  console.log('写入完成');
});
```
### 管道流：
```javascript
readerStream.pipe(writeStream);  //将读取的文件写入另一个文件中
```

## 继承
```javascript
util.inherits(a,b)     //a继承b
```

<!-- jade模板:
格式：
extends layout

block centent
    h1 = title
    p Welcome to #{title}
语句：
if条件语句：
if ${name} == 'admin'
    p     this is an admin
  else
    p     this is not an admin

each循环语句：
var items = ["one", "two", "three"]
each i in items
    li = item

for循环语句：
for user in users
    for role in user.roles
          li = role -->
