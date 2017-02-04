---
title: 'JS深入学习'
date: 2017-01-18 09:41:29
tags: ["javascript"]
description: JavaScript博大精深此文用于积累自己平时对JS基础知识的学习
photos: http://oizt3fjv8.bkt.clouddn.com/javascriptsrxx.png
---

## 对象
js是按共享传递的方式传值:对象属性值会被修改，但本身不会被修改。
在调用函数时，传递的是对象的引用副本，与引用传递不同的是，共享传递中对形参的赋值并不会改变实参的值，但对形参的属性赋值却会改变实参的属性值。
例：
```javascript
var obj = {name:"job"};

function foo1(x){
    x.name = "wzp";
}
foo1(obj); //obj.name = "wzp";  属性值会被修改

function foo2(x){
    x = "a";
}
foo2(obj); //obj.name = "job";  实参本身不会被修改

```
SO所有基本属性值是不会变的，修改的值都是存放在一个新的变量中：
```javascript
var num = 1;
function foo3(x){
    x = 3;
}
foo3(num); //num = 1; //基本属性的值不会被修改
var numFB = foo3(num); //numFB = 3; //修改的值存放在副本中
```

## 继承
### 原型链继承
```javascript
function SuperType(){
  this.property = true;
}

SuperType.prototype.getSuperValue = function(){
  return this.property;
};
function SubType(){
  this.subproperty = false;
}
//继承了SuperType
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function (){
  return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue()); //true
```

总结：改变SubType的prototype，使其指向SuperType的实例，而不是SubType的构造函数。共享属性，不能传参。

### 借用构造函数
```javascript
function SuperType(){
  this.colors = ["red", "blue", "green"];
}
function SubType(){
  //继承了SuperType
  SuperType.call(this);
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
```
总结： 实例独立，无法复用。

### 组合继承
```JavaScript
function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
  alert(this.name);
};
function SubType(name, age){
  //继承属性
  SuperType.call(this, name);
  this.age = age;
}
//继承方法
SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
  alert(this.age);
};
var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
instance1.sayName(); //"Nicholas";
instance1.sayAge(); //29
var instance2 = new SubType("Greg", 27);
alert(instance2.colors); //"red,blue,green"
instance2.sayName(); //"Greg";
instance2.sayAge(); //27
```
总结：原型继承和构造函数继承的融合。
SuperType 构造函数定义了两个属性：name 和colors。SuperType 的原型定义
了一个方法sayName()。SubType 构造函数在调用SuperType 构造函数时传入了name 参数，紧接着
又定义了它自己的属性age。然后，将SuperType 的实例赋值给SubType 的原型，然后又在该新原型
上定义了方法sayAge()。这样一来，就可以让两个不同的SubType 实例既分别拥有自己属性——包
括colors 属性，又可以使用相同的方法了。
组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为JavaScript 中最常用的继
承模式。而且，instanceof 和isPrototypeOf()也能够用于识别基于组合继承创建的对象。


## 在函数内任何位置用var申明的变量都会置顶在函数头部
```
myname = "global"; // 全局变量
function func() {
  alert(myname); // "undefined" var myname被置顶
  var myname = "local";
  alert(myname); // "local"
}
func();
```

## for-in 循环注意过略原型链上的属性(用于对象循环)
```
var man = {
  hands: 2,
  legs: 2,
  heads: 1
};

for(var i in man){
    if(man.hasOwnProperty(i)){
        alert(i + ":" + man[i]);
    }
}
```

## 进制转换
10进制转2进制：var a = parseInt("100",10).toString(2);

## && 和 ||
&&运算如果返回true，则取后面的值，如果|| 返回true,则取前面的值

```javascript
var  a = “”  ||  null  || 3  ||  4  
//等价于
var a = fasel || false || true ||  true  //结果为true  则返回第一个true,即是3

var b = 4 && 5 && null && 0  
//等价于
var b = true && true && false && false   //结果是false   则返回第一个false   即是null
```

## attr 和 prop
什么时候使用attr()，什么时候使用prop()？
1.添加属性名称该属性就会生效应该使用prop();
2.是有true,false两个属性使用prop();
3.其他则使用attr();

## 获取字符串中x和o是否相等
```javascript
function XO(str) {
  let x = str.match(/x/gi);
  let o = str.match(/o/gi);
  return (x && x.length) === (o && o.length);
  //&& 返回true,则返回后者。返回false,则返回前者。
  //这里如果x为空，则返回false,返回x;如果x不为空，则返回true，返回x.length;
}
```

## 链式调用
```javascript
function Node(data){
    this.data = data;
    this.next = null;
}

function push(head, data){
    var node  = new Node(data);
    node.next = head;
    return node;
}

function printABC(){
    return  push(push(push(null, 3), 2),1);
}

调用：printABC();
结果：Node -> 1 -> 2 ->3 
```
