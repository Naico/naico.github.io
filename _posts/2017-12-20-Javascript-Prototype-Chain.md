---
layout: blog
title: Javascript Prototype Chain 
---

# 万物皆是对象

## 普通对象和函数对象

我们知道在Javascript中，万物皆对象，但对象也是有区别的。
对象分为普通对象和函数对象，Object 、Function 是 JS 自带的函数对象。下面举例说明：

```js
var o1 = {};
var o2 =new Object();
var o3 = new f1();

function f1(){};
var f2 = function(){};
var f3 = new Function('str','console.log(str)');

console.log(typeof Object); //function
console.log(typeof Function); //function

console.log(typeof f1); //function
console.log(typeof f2); //function
console.log(typeof f3); //function

console.log(typeof o1); //object
console.log(typeof o2); //object
console.log(typeof o3); //object
```

在上面的例子中 o1 o2 o3 为普通对象，f1 f2 f3 为函数对象。
怎么区分，其实很简单，**凡是通过 new Function() 创建的对象都是函数对象，其他的都是普通对象。**
f1,f2,归根结底都是通过 new Function()的方式进行创建的。Function Object 也都是通过 New Function()创建的。

## 构造函数

来看一个例子：

```js
function Person(name, age, job) {
 this.name = name;
 this.age = age;
 this.job = job;
 this.sayName = function() { alert(this.name) }
}
var person1 = new Person('Zaxlct', 28, 'Software Engineer');
var person2 = new Person('Mick', 23, 'Doctor');
```

上面的例子中 person1 和 person2 都是 Person 的实例。这两个实例都有一个**constructor（构造函数）**属性，该属性（是一个指针）指向 Person。 即：

```js
console.log(person1.constructor == Person); //true
console.log(person2.constructor == Person); //true
```

我们要记住两个概念（构造函数，实例）：
**person1 和 person2 都是 构造函数 Person 的实例**
一个公式：
**实例的构造函数属性（constructor）指向构造函数。**

## 原型对象

在 JavaScript 中，每当定义一个对象（函数也是对象）时候，对象中都会包含一些预定义的属性。其中每个函数对象都有一个prototype 属性，这个属性指向函数的原型对象。（先用不管什么是 __proto__ 后面我会详细的剖析）

```js
function Person() {}
Person.prototype.name = 'Zaxlct';
Person.prototype.age  = 28;
Person.prototype.job  = 'Software Engineer';
Person.prototype.sayName = function() {
  alert(this.name);
}

var person1 = new Person();
person1.sayName(); // 'Zaxlct'

var person2 = new Person();
person2.sayName(); // 'Zaxlct'

console.log(person1.sayname == person2.sayname); //true
```

于是我们得到了第一个[定律]()：

> 每个对象都有 __proto__ 属性，但只有函数对象才有 prototype 属性

那什么是原型对象呢？
我们把上面的例子改一改你就会明白了：

```js
Person.prototype = {
   name:  'Zaxlct',
   age: 28,
   job: 'Software Engineer',
   sayName: function() {
     alert(this.name);
   }
}
```

原型对象，顾名思义，它就是一个普通对象。从现在开始你要牢牢记住原型对象就是 Person.prototype ，如果你还是害怕它，那就把它想想成一个字母 A：

> var A = Person.prototype

在上面我们给 A 添加了 四个属性：name、age、job、sayName。其实它还有一个默认的属性：**constructor**

> 在默认情况下，所有的原型对象都会自动获得一个 constructor（构造函数）属性，这个属性（是一个指针）指向 prototype 属性所在的函数（Person）

上面这句话有点拗口，我们「翻译」一下：A 有一个默认的 constructor 属性，这个属性是一个指针，指向 Person。即：
> Person.prototype.constructor == Person

在上面第二小节《构造函数》里，我们知道**实例的构造函数属性（constructor）指向构造函数** ：
> person1.constructor == Person