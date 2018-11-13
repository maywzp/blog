---
title: ES6 各种设计模式的实现
date: 2018-10-29 18:09:47
updated: 2018-11-12 11:16:30
tags: '知识点'
---

## 创造型模式

### 单例模式（Singleton）

保证一个类仅有一个实例，并提供一个访问它的全局访问点。

```javascript
class Singleton {
  constructor(data) {
    if (Singleton.prototype.Instance === undefined) {
      this.data = data
      Singleton.prototype.Instance = this
    }
    return Singleton.prototype.Instance
  }
}

const ob1 = new Singleton('one')
const ob2 = new Singleton('two')

ob1.data // 'one'
ob2.data // 'one'

ob1.flag = 'Object Flag'
ob1.flag // 'Object Flag'
ob2.flag // 'Object Flag'

ob1 === ob2 // true
```

### 工厂模式（Factory）

定义一个用于创建对象的接口，这个接口由子类决定实例化哪一个类。

```javascript
class ProductManager {
  constructor(productName) {
    this.name = productName
  }

  _createProductA() {}

  _createProductB() {}

  factory() {
    switch (this.name) {
      case 'productA':
        this._createProductA()
        break
      case 'productB':
        this._createProductB()
        break
    }
  }
}

const pm = new ProductManager()
const productA = pm.factory('productA')
```

### 抽象工厂模式（AbstractFactory）

抽象类是一种声明但不能使用的类，如果子类没有重写父类的抽象方法，将会报错。

```javascript
// 抽象工厂类
class AbstractFactory {
  constructor() {
    if (new.target === AbstractFactory) {
      throw new Error('不能直接使用抽象类')
    }
  }
  createProductA(product) {
    console.log('AbstractFactory createProductA')
  }
  createProductB(product) {
    console.log('AbstractFactory createProductB')
  }
}

// 子类重写父类方法
class ConcreteFactory1 extends AbstractFactory {
  constructor() {
    super()
  }

  createProductA(product) {
    console.log('ConcreteFactory1 createProductA')
  }

  createProductB(product) {
    console.log('ConcreteFactory1 createProductB')
  }
}

// 子类重写父类方法
class ConcreteFactory2 extends AbstractFactory {
  constructor() {
    super()
  }

  createProductA(product) {
    console.log('ConcreteFactory2 createProductA')
  }

  createProductB(product) {
    console.log('ConcreteFactory2 createProductB')
  }
}
```

### 建造者模式（Builder）

将一个对象复杂的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。
四要素：

1. Product（产品类）：一个较为复杂的对象
2. Builder （抽象建造者类）：将建造的具体过程交与它的子类实现
3. ConcreteBuilder （建造者类）：组建产品，返回组建好的产品
4. Director （指导类）：调用适当的建造者来组建产品

```javascript
class Product {
  constructor() {
    this.name = ''
  }

  setName(productName) {
    this.name = productName
  }
}

class Builder {
  constructor() {}

  buildPart(productName) {}
}

class ConcreteBuilder extends Builder {
  constructor() {
    super()
    this.product = new Product()
  }

  buildPart(productName) {
    this.product.setName(productName)
  }

  getResult() {
    console.log(this.product)
    return this.product
  }
}

class Director {
  constructor() {
    this.structure = ['Prod1', 'Prod2', 'Prod3']
  }

  construct() {
    this.structure.forEach(s => {
      const builder = new ConcreteBuilder()
      builder.buildPart(s)
      builder.getResult()
    })
  }
}

const director = new Director()
director.construct()
```

## 结构型模式

### 适配者模式（Adapter）

使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。
