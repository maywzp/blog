---
title: JS常用代码片段
date: 2016-12-16T16:44:28.000Z
tags:
  - javascript
description: Javascript 片段积累
photos: 'http://oizt3fjv8.bkt.clouddn.com/javascriptno2.jpg'
---

# 保留两位小数

```javascript
number.toFixed(2)
```

# 解决数组引用问题

```javascript
arr.concat() //数组复制
```

# 解决对象引用问题

```javascript
Object.assign({}, obj) //对象复制
```

# 获取下拉框文字

```javascript
 $("#FinanceCostType").find("option:selected").text();
```

# 获取下拉框索引

```javascript
$("select[name='select1']").get(0).selectedIndex;
```

# 阻止默认事件

```javascript
 e.preventDefault();
```

# 阻止事件冒泡

```javascript
 e.stopPropagation();
```

# 动态引入JavaScript

```javascript
var script = document.createElement('script')
script.setAttribute('type', 'text/javascript')
script.setAttribute('src', '')
document.getElementsByTagName('head')[0].appendChild(script)
```

# uri编码:防止乱码
## 加码(必须套两层)。

```javascript
var login_name = encodeURI(encodeURI(login_name));
```

## 解码

```javascript
js:   loginName = decodeURI(decodeURI(loginName));
Java：loginName = java.net.URLDecoder.decode(loginName,"UTF-8");
```

# JSON操作

```javascript
eval("("+data+")")
$.param(data)
JSON.parse(str);
JSON.stringify(obj);
```

# 自动触发事件

```javascript
$('#loadBtn').trigger("click");
```

# 金钱格式化（加千分号，保留两位小数）

```javascript
var money = (money.toFixed(2) + '').replace(/\d{1,3}(?=(\d{3})+(\.\d*)?$)/g, '$&,');
```

# 前进

```javascript
window.history.go(-1)
history.go(-1)
```

# 后退

```javascript
window.history.back()
history.back()
```

# 刷新

```javascript
window.location.reload();
```

# 后退并刷新页面

```javascript
self.location=document.referrer; (返回导航到当前网页的超链接所在网页的URL)
```

# 复选框全选

```javascript
$("#checkAll").click(function() {
  $('input[name="subBox"]').attr("checked",this.checked);
});
var $subBox = $("input[name='subBox']");
$subBox.click(function(){
  $("#checkAll").attr("checked",$subBox.length == $("input[name='subBox']:checked").length ? true : false);
});
```

# form表单
## 表头

```javascript
headers : {'Content-Type': 'application/json;charset=utf-8'},
```

## 重置表单

```javascript
reset: function () {
    $("#StartTime").val($("#hidStartTime").val());
    $("#EndTime").val($("#hidEndTime").val());
    $("#BankName option[value='']").attr("selected", true);
    $("#formTable input[type='text']").val("");
    $("#formTable select").each(function () {
        $(this).find("option:first").attr("selected", "selected");
    });
},
```

## 图片上传

```html
<form enctype="multipart/form-data" action="http://192.168.1.155:8080/regulator/common/upload/image" method="post">
    <input type="file" name="file"/>
    <input type="submit"  value="上传" >
</form>
<input id="filePicker" type="file" accept="image/*;capture=camera" class="input">
```

## 表单提交

```javascript
var frm = $('form');
frm.submit(function (e) {
    $.ajax({
        type: frm.attr('method'),
        url: frm.attr('action'),
        data: frm.serialize(),
        success: function (data) {
            alert('ok');
        },
        error:function(err){
            alert(err);
        }
    });
    e.preventDefault();
});
```

## 反序列化

```javascript
serializeJson: function(obj) {
    var jsonObj = {};

    $.each(obj, function() {
        var value = $.trim($(this).val());

        if (value !== '') {
            var key = $(this).attr('name');
            key && (jsonObj[key] = value);
        }
    });
    return jsonObj;
}
var JsonObj = $.serializeJson($("#tableCondition").find("select,input[type='text']"));
```

## 获取 URL 中传递的参数

```javascript
$.urlParam = function(name){
    var results = new RegExp('[\\?&]' + name + '=([^&#]*)').exec(window.location.href);
    if (!results) { return 0; }
    return results[1] || 0;
}
```

# 添加收藏夹

```javascript
function addFavorite(url, title) {
    if (document.all) {
        window.external.addFavorite(url, title);
    } else if (window.sidebar) {
        window.sidebar.addPanel(title, url, "");
    }
}
```

# html字符串转义

```javascript
function htmlEscape(htmlString) {
    htmlString = htmlString.replace(/&/g, '&amp;');
    htmlString = htmlString.replace(/</g, '&lt;');
    htmlString = htmlString.replace(/>/g, '&gt;');
    htmlString = htmlString.replace(/'/g, '&acute;');
    htmlString = htmlString.replace(/"/g, '&quot;');
    htmlString = htmlString.replace(/\|/g, '&brvbar;');
    return htmlString;
}
```

# 设置Cookie

```javascript
function setCookie(name, value) {
    var expires = (arguments.length > 2) ? arguments[2] : null;
    document.cookie = name + "=" + encodeURIComponent(value) + ((expires == null) ? "" : ("; expires=" + expires.toGMTString())) + ";path=" + window.location.href;
}
```

# 获取Cookie

```javascript
function getCookie(name) {
    var value = document.cookie.match(new RegExp("(^| )" + name + "=([^;]*)(;|$)"));
    if (value != null) {
        return decodeURIComponent(value[2]);
    } else {
        return null;
    }
}
```

# 删除cookie

```javascript
function removeCookie(name) {
    var expires = new Date();
    expires.setTime(expires.getTime() - 1000 * 60);
    setCookie(name, "", expires);
}
```

# 返回顶部

```javascript
 // fade in .back-to-top
$(window).scroll(function () {
    if ($(this).scrollTop() > 500) {
        $('.back-to-top').fadeIn();
    } else {
        $('.back-to-top').fadeOut();
    }
});

// scroll body to 0px on click
$('.back-to-top').click(function () {
    $('html, body').animate({
        scrollTop: 0,
        easing: 'swing'
    }, 750);
    return false;
});
```

# 判断是否为pc浏览器

```javascript
function isPc() {
    var userAgentInfo = navigator.userAgent;
    var Agents = ["Android", "iPhone",
                "SymbianOS", "Windows Phone",
                "iPad", "iPod"];
    var flag = true;
    for (var v = 0; v < Agents.length; v++) {
        if (userAgentInfo.indexOf(Agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}
```

# 判断是否为手机浏览器或ipad浏览器

```javascript
function isMobile() {
    var sUserAgent = navigator.userAgent.toLowerCase();
    var bIsIpad = sUserAgent.match(/ipad/i) == "ipad";
    var bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os";
    var bIsMidp = sUserAgent.match(/midp/i) == "midp";
    var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4";
    var bIsUc = sUserAgent.match(/ucweb/i) == "ucweb";
    var bIsAndroid = sUserAgent.match(/android/i) == "android";
    var bIsCE = sUserAgent.match(/windows ce/i) == "windows ce";
    var bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile";
    var flag = true;
    if (!(bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) ){
        flag = false;
    }
    return flag;
}
```

# 判断是否为微信浏览器

```javascript
function isWeiXin(){
    var ua = navigator.userAgent.toLowerCase();
    if(ua.match(/MicroMessenger/i) == 'micromessenger'){
        return true;
    }else{
        return false;
    }
}
```

# 阻止页面滚动

```javascript
document.ontouchstart=function(){
  return false;
}
```

# 获取鼠标坐标：

```javascript
function getMousePos(event) {
    var e = event || window.event;
    var scrollX = document.documentElement.scrollLeft || document.body.scrollLeft;
    var scrollY = document.documentElement.scrollTop || document.body.scrollTop;
    var x = e.pageX || e.clientX + scrollX;
    var y = e.pageY || e.clientY + scrollY;
    return { 'x': x, 'y': y };
}
onmousemove="getMousePos(event)"
getMousePos(e).x
getMousePos(e).y
```

# localStorage

```javascript
localStorage.user = JSON.stringify(user)
localStorage.removeItem('name')
localStorage.clear()
```

# 日期格式化

```javascript
/**
 *   对Date的扩展，将 Date 转化为指定格式的String
 *   月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符，
 *   年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字)
 *   例子：
 *   fmtDate(new Date(), "yyyy-MM-dd hh:mm:ss.S") ==> 2006-07-02 08:09:04.423
 *   fmtDate(new Date(), "yyyy-M-d h:m:s.S")      ==> 2006-7-2 8:9:4.18
 */
const fmtDate = function(date, fmt) {
    var o = {
        "M+": date.getMonth() + 1, //月份
        "d+": date.getDate(), //日
        "h+": date.getHours(), //小时
        "m+": date.getMinutes(), //分
        "s+": date.getSeconds(), //秒
        "q+": Math.floor((date.getMonth() + 3) / 3), //季度
        "S": date.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt))
        fmt = fmt.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt))
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
}
```

# 日期转换

```javascript
/**
 *   对Date的扩展，将相差毫秒数转化为文字
 *   例子：
 *   MillisecondToDate(new Date() - new Date('2006-07-02')) ==> 10年前
 */
const MillisecondToDate = function(msd) {
    var time = parseFloat(msd) / 1000;
    var str ="";
    if (null != time && "" != time) {

        if (time > 60 && time < 3600) {
            str = parseInt(time / 60.0) + " 分钟前";
        }
        else if (time >= 3600 && time < 86400) {
            str = parseInt(time / 3600.0) + " 小时前" ;
        }
        else if (time >= 86400 && time < 86400*30) {
            str = parseInt(time / 86400.0) + " 天前" ;
        }
        else if (time >= 86400*30 && time < 86400*365) {
            str = parseInt(time / (86400.0*30)) + " 个月前" ;
        }
        else if(time >= 86400*365){
            str = parseInt(time / (86400.0*365)) + " 年前" ;
        }
        else {
            str = parseInt(time) + " 秒前";
        }
    }
    return str;
}
```

# 克隆

```javascript
function clone(data){
    return JSON.parse(JSON.stringify(data))
}
```

# RGB转16进制

```javascript
function rgbToHex (red, green, blue) {
  if (typeof red === 'string') {
    const res = red.match(/\b\d{1,3}\b/g).map(Number)
    red = res[0]
    green = res[1]
    blue = res[2]
  }

  if (
    typeof red !== 'number' ||
    typeof green !== 'number' ||
    typeof blue !== 'number' ||
    red > 255 ||
    green > 255 ||
    blue > 255
  ) {
    throw new TypeError('Expected three numbers below 256')
  }

  return ((blue | green << 8 | red << 16) | 1 << 24).toString(16).slice(1)
}
```

# 16进制转RGB

```javascript
function hexToRgb (hex) {
  if (typeof hex !== 'string') {
    throw new TypeError('Expected a string')
  }

  hex = hex.replace(/^#/, '')

  if (hex.length === 3) {
    hex = hex[0] + hex[0] + hex[1] + hex[1] + hex[2] + hex[2]
  }

  let num = parseInt(hex, 16)

  return [num >> 16, num >> 8 & 255, num & 255]
}
```
