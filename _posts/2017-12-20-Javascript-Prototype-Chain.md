---
layout: post
title: Javascript Prototype Chain
categories: Javascript
description: Javascript原型相关知识以及深入与理解。
tags: Javascript
---

我们知道在Javascript中，万物皆对象，但对象也是有区别的。
对象分为普通对象和函数对象，Object 、Function 是 JS 自带的函数对象。

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

```js
var A = Person.prototype
```

在上面我们给 A 添加了 四个属性：name、age、job、sayName。其实它还有一个默认的属性：**constructor**

> 在默认情况下，所有的原型对象都会自动获得一个 constructor（构造函数）属性，这个属性（是一个指针）指向 prototype 属性所在的函数（Person）

上面这句话有点拗口，我们「翻译」一下：A 有一个默认的 constructor 属性，这个属性是一个指针，指向 Person。即：

```js
Person.prototype.constructor == Person
```

在上面第二小节《构造函数》里，我们知道**实例的构造函数属性（constructor）指向构造函数** ：

```js
person1.constructor == Person
```

这两个「公式」好像有点联系:

```js
person1.constructor == Person
Person.prototype.constructor == Person
```

person1 为什么有 constructor 属性？那是因为 person1 是 Person 的实例。
那 Person.prototype 为什么有 constructor 属性？？同理， Person.prototype （你把它想象成 A） 也是Person 的实例。
也就是在 Person 创建的时候，创建了一个它的实例对象并赋值给它的 prototype，基本过程如下：

```js
var A = new Person();
Person.prototype = A;
```

所以我们得出一个结论：
> 原型对象（Person.prototype）是 构造函数（Person）的一个实例。

原型对象其实就是普通对象（但 Function.prototype 除外，它是函数对象，但它很特殊，他没有prototype属性（前面说道函数对象都有prototype属性））。看下面的例子：

```js
function Person(){};
 console.log(Person.prototype) //Person{}
 console.log(typeof Person.prototype) //Object
 console.log(typeof Function.prototype) // Function，这个特殊
 console.log(typeof Object.prototype) // Object
 console.log(typeof Function.prototype.prototype) //undefined
```

Function.prototype 为什么是函数对象呢？

```js
var A = new Function ();
Function.prototype = A;
```

上文提到凡是通过 new Function( ) 产生的对象都是函数对象。因为 A 是函数对象，所以Function.prototype 是函数对象。

那原型对象是用来做什么的呢？主要作用是用于继承。举个例子：

```js
var Person = function(name){
    this.name = name; // tip: 当函数执行时这个 this 指的是谁？
};
Person.prototype.getName = function(){
    return this.name;  // tip: 当函数执行时这个 this 指的是谁？
}
var person1 = new person('Mick');
person1.getName(); //Mick
```

小问题，上面两个 this 都指向谁？

```js
var person1 = new person('Mick');
person1.name = 'Mick'; // 此时 person1 已经有 name 这个属性了
person1.getName(); //Mick
```

故两次 this 在函数执行时都指向 person1。

## __proto__

JS 在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做__proto__ 的内置属性，用于指向创建它的构造函数的原型对象。
对象 person1 有一个 __proto__属性，创建它的构造函数是 Person，构造函数的原型对象是 Person.prototype ，所以：
person1.__proto__ == Person.prototype

请看下图：
![](/images/blog/proto.jpg)

根据上面这个连接图，我们能得到：

```js
Person.prototype.constructor == Person;
person1.__proto__ == Person.prototype;
person1.constructor == Person;
```

**不过，要明确的真正重要的一点就是，这个连接存在于实例（person1）与构造函数（Person）的原型对象（Person.prototype）之间，而不是存在于实例（person1）与构造函数（Person）之间。**

## 构造器

熟悉 Javascript 的童鞋都知道，我们可以这样创建一个对象：

```js
var obj = {};
```

它等同于下面这样：
```js
var obj = new Object();
```

obj 是构造函数（Object）的一个实例。所以：

```js
obj.constructor === Object
obj.__proto__ === Object.prototype
```

新对象 obj 是使用 new 操作符后跟一个构造函数来创建的。构造函数（Object）本身就是一个函数（就是上面说的函数对象），它和上面的构造函数 Person 差不多。只不过该函数是出于创建新对象的目的而定义的。所以不要被 Object 吓倒。

同理，可以创建对象的构造器不仅仅有 Object，也可以是 Array，Date，Function等。
所以我们也可以构造函数来创建 Array、 Date、Function

```js
var b = new Array();
b.constructor === Array;
b.__proto__ === Array.prototype;

var c = new Date();
c.constructor === Date;
c.__proto__ === Date.prototype;

var d = new Function();
d.constructor === Function;
d.__proto__ === Function.prototype;
```

这些构造器都是函数对象：
![](/images/blog/constructor.jpg)

## 原型链

小测试来检验一下你理解的怎么样：

1. person1.__proto__ 是什么？
2. Person.__proto__ 是什么？
3. Person.prototype.__proto__ 是什么？
4. Object.__proto__ 是什么？
5. Object.prototype__proto__ 是什么？

```js
第一题：
因为 person1.__proto__ === person1 的构造函数.prototype
因为 person1的构造函数 === Person
所以 person1.__proto__ === Person.prototype

第二题：
因为 Person.__proto__ === Person的构造函数.prototype
因为 Person的构造函数 === Function
所以 Person.__proto__ === Function.prototype

第三题：
Person.prototype 是一个普通对象，我们无需关注它有哪些属性，只要记住它是一个普通对象。
因为一个普通对象的构造函数 === Object
所以 Person.prototype.__proto__ === Object.prototype

第四题，参照第二题，因为 Person 和 Object 一样都是构造函数

第五题：
Object.prototype 对象也有proto属性，但它比较特殊，为 null 。因为 null 处于原型链的顶端，这个只能记住。
Object.prototype.__proto__ === null
```
