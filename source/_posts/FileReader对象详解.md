---
title: FileReader对象详解
date: 2017-2-5 13:47:15
updated: 2017-2-5 13:47:15
tags: ['javascript']
description: 用来把文件读入内存，并且读取文件中的数据。FileReader接口提供了一个异步API，使用该API可以在浏览器主线程中异步访问文件系统，读取文件中的数据。到目前文职，只有FF3.6+和Chrome6.0+实现了FileReader接口。
photos: http://oizt3fjv8.bkt.clouddn.com/filereader_no1.png
---

## 方法
方法名               |参数           |描述
--------------------|----------------|---------
readAsBinaryString  |flie            |将文件读取为二进制编码
readAsText          |flie,[encoding] |将文件读取为文本
readAsDataURL       |flie            |将文件读取为DataURL
abort               |(none)          |终端读取操作

## 事件
事件                |描述
--------------------|---------
onabort             |中断
onerror             |出错
onloadstart         |开始
onprogress          |正在读取
onload              |成功读取
onloadend           |读取完成，无论成功失败

## 使用
```html
<div>  
    <label>请选择一个文件：</label>  
    <input type="file" id="file" />  
    <input type="button" value="读取图像" onclick="readAsDataURL()" />  
    <input type="button" value="读取二进制数据" onclick="readAsBinaryString()" />  
    <input type="button" value="读取文本文件" onclick="readAsText()" />  
</div>  
<div id="result" name="result"></div>  
```
```javascript
var result=document.getElementById("result");  
var file=document.getElementById("file");  

//判断浏览器是否支持FileReader接口  
if(typeof FileReader == 'undefined'){  
    result.InnerHTML="<p>你的浏览器不支持FileReader接口！</p>";  
    //使选择控件不可操作  
    file.setAttribute("disabled","disabled");  
}  

function readAsDataURL(){  
    //检验是否为图像文件  
    var file = document.getElementById("file").files[0];  
    if(!/image\/\w+/.test(file.type)){  
        alert("看清楚，这个需要图片！");  
        return false;  
    }  
    var reader = new FileReader();  
    //将文件以Data URL形式读入页面  
    reader.readAsDataURL(file);  
    reader.onload=function(e){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML='<img src="' + this.result +'" alt="" />';  
    }  
}  

function readAsBinaryString(){  
    var file = document.getElementById("file").files[0];  
    var reader = new FileReader();  
    //将文件以二进制形式读入页面  
    reader.readAsBinaryString(file);  
    reader.onload=function(f){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML=this.result;  
    }  
}  

function readAsText(){  
    var file = document.getElementById("file").files[0];  
    var reader = new FileReader();  
    //将文件以文本形式读入页面  
    reader.readAsText(file);  
    reader.onload=function(f){  
        var result=document.getElementById("result");  
        //显示文件  
        result.innerHTML=this.result;  
    }  
}  
```
