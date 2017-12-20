---
layout: blog
title: Talk About Javascript 
---
Javascript中有几个非常重要的语言特性——对象、原型继承、闭包。
其中闭包对于那些使用传统静态语言的程序员来说是一个新的语言特性。
闭包是Javascript语言的一个难点，也是它的特色，很多高级应用都要依靠闭包实现。

## 闭包的定义

> A closure is the combination of a function and the lexical environment within which that function was declared.

> Closures(闭包)是使用被作用域封闭的变量，函数，闭包等执行的一个函数的作用域。通常我们用和其相应的函数来指代这些作用域。(可以访问独立数据的函数)

> 闭包是一个函数和声明该函数的词法环境的组合。从理论角度来说，所有函数都是闭包。

这是[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)官方给出的闭包的定义。比较晦涩难懂。我个人理解为闭包有以下几个特点：
* 闭包就是能够读取其他函数内部变量的函数。
* 闭包就是函数的局部变量集合，只是这些局部变量在函数返回后会继续存在。
* 闭包就是就是函数的“堆栈”在函数返回后并不释放，我们也可以理解为这些函数堆栈并不在栈上分配而是在堆上分配
* 当在一个函数内定义另外一个函数就会产生闭包

由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。

所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

如果要全面学习学好Javascript高级技巧以及熟练运用框架和理解框架，那么一定要学好闭包。说到闭包，那就不得不说另外一个很让人感兴趣的话题，就是**变量的作用域**。

## 变量的作用域

我们可以回忆一下，我们现在在用的语言，拿C#来举例。你在一个方法中定义了一个变量，那么你只能在这个方法的范围内访问这个变量。在这个方法之外是无法访问到这个变量的。这就是变量的作用域。在Javascript中也是一样，我们考虑以下的Javascript代码片段：
```js
var a = 999;
function foo(){
    alert(a);
}
foo(); // 999
```

```js
function foo(){
    var a = 999;
}
alert(a); // error
```
Javascript函数内部可以访问全局变量，而函数外部则无法访问函数内部的变量。
那么我们有这样的场景，我需要从函数外部访问函数内部定义好的变量，应该怎么办？
这时候，闭包就派上用场了。

### 作用域是什么

要完全说清楚作用域，可能就要从Javascript引擎说起了。这里面包含了编译原理，以及引擎和作用域的交互。是个很复杂很大的话题。今天暂且不讨论这些。有兴趣的同学可以参见ECMAScript的[ECMA-262标准](https://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf)以及[Chrome V8 Engine](http://www.v8project.org)的具体实现。
下面我们通过一个简单的赋值语句来大体介绍一下引擎和作用域是如何协同工作的。

```js
var a = 2;
```

下面我们将这一句话分解开来看。其实这句话用我们熟悉的伪代码来表述就是：“为一个变量分配一份内存，并命名为a，然后将2这个值保存到a这个变量中”。那我们来看编译器是如何处理的：

1. 遇到 var a，编译器会询问作用域，是否已经有一个该名称的变量存在于同一个作用域的集合中。如果是，编译器会忽略该声明，继续进行编译。否则，它会要求作用域在当前的作用域集合中声明一个新的变量，并命名为 a。
2. 然后编译器会为引擎生成运行时所需要的代码，这些代码会处理a = 2这个操作。引擎运行时会首先询问作用域，在当前的作用域集合中是否存在一个叫做a的变量。如果是，引擎就会使用这个变量，如果不是，那么引擎会继续查找该变量。

明白了这个道理，我们再看上面两个例子，就明白为什么函数外部访问不了函数内部定义的变量了。

> 这里有个引申的学习点，在这里我只是大体的介绍了什么是作用域，如果想深入学习，可以了解一些有关词法作用域/函数作用域/块作用域。

## 闭包来袭

我们通过代码来展示闭包究竟是怎么形成的。考虑如下的Javascript代码段：

```js
function greeting(name) {
    var text = 'Hello ' + name; // local variable
    // 每次调用时，产生闭包，并返回内部函数对象给调用者
    return function() { alert(text); }
}
var sayHello = greeting("Closure");
sayHello();  // 通过闭包访问到了局部变量text
```

上述代码的执行结果是：Hello Closure，因为sayHello()函数在greeting函数执行完毕后，仍然可以访问到了定义在其之内的局部变量text。
这个就是传说中闭包的效果，闭包在Javascript中有多种应用场景和模式，比如Singleton模式就离不开对闭包的使用。

### ECMAScript闭包模型

ECMAScript到底是如何实现闭包的呢？想深入了解的亲们可以获取ECMAScript规范进行研究，我这里也只做一个简单的讲解，内容主要是来自于网络。

在ECMAscript的脚本的函数运行时，每个函数关联都有一个执行上下文场景(Execution Context) ，这个执行上下文场景中包含三个部分

1. 文法环境（The LexicalEnvironment）
2. 变量环境（The VariableEnvironment）
3. this绑定

其中第三点this绑定与闭包无关，不在本文中讨论。
文法环境中用于解析函数执行过程使用到的变量标识符。我们可以将文法环境想象成一个对象，该对象包含了两个重要组件，环境记录(Enviroment Recode)，和外部引用(指针)。环境记录包含包含了函数内部声明的局部变量和参数变量，外部引用指向了外部函数对象的上下文执行场景。全局的上下文场景中此引用值为NULL。这样的数据结构就构成了一个单向的链表，每个引用都指向外层的上下文场景。

例如上面我们例子的闭包模型应该是这样，sayHello函数在最下层，上层是函数greeting，最外层是全局场景。如下图：
![](/assets/images/closure.png)

因此当sayHello被调用的时候，sayHello会通过上下文场景找到局部变量text的值，因此在屏幕的对话框中显示出”Hello Closure”
变量环境(The VariableEnvironment)和文法环境的作用基本相似，具体的区别请参看ECMAScript的规范文档。

## 闭包的样列

前面的我大致了解了Javascript闭包是什么，闭包在Javascript是怎么实现的。下面我们通过针对一些例子来帮助大家更加深入的理解闭包，下面共有5个样例，例子来自于JavaScript Closures For Dummies(镜像)。

### 例子1:闭包中局部变量是引用而非拷贝

```js
function say667() {
    // Local variable that ends up within closure
    var num = 666;
    var sayAlert = function() { alert(num); }
    num++;
    return sayAlert;
}
 
var sayAlert = say667();
sayAlert();
```

因此执行结果应该弹出的667而非666。

### 例子2：多个函数绑定同一个闭包，因为他们定义在同一个函数内。

```js
function setupSomeGlobals() {
    // Local variable that ends up within closure
    var num = 666;
    // Store some references to functions as global variables
    gAlertNumber = function() { alert(num); }
    gIncreaseNumber = function() { num++; }
    gSetNumber = function(x) { num = x; }
}
setupSomeGlobals(); // 为三个全局变量赋值
gAlertNumber(); //666
gIncreaseNumber();
gAlertNumber(); // 667
gSetNumber(12);//
gAlertNumber();//12
```

### 例子3：当在一个循环中赋值函数时，这些函数将绑定同样的闭包

```js
function buildList(list) {
    var result = [];
    for (var i = 0; i < list.length; i++) {
        var item = 'item' + list[i];
        result.push( function() {alert(item + ' ' + list[i])} );
    }
    return result;
}
 
function testList() {
    var fnlist = buildList([1,2,3]);
    // using j only to help prevent confusion - could use i
    for (var j = 0; j < fnlist.length; j++) {
        fnlist[j]();
    }
}
```

testList的执行结果是弹出item3 undefined窗口三次，因为这三个函数绑定了同一个闭包，而且item的值为最后计算的结果，但是当i跳出循环时i值为4，所以list[4]的结果为undefined.

### 例子4：外部函数所有局部变量都在闭包内，即使这个变量声明在内部函数定义之后。

```js
function sayAlice() {
    var sayAlert = function() { alert(alice); }
    // Local variable that ends up within closure
    var alice = 'Hello Alice';
    return sayAlert;
}
var helloAlice=sayAlice();
helloAlice();
```

执行结果是弹出"Hello Alice"的窗口。即使局部变量声明在函数sayAlert之后，局部变量仍然可以被访问到。

### 例子5：每次函数调用的时候创建一个新的闭包

```js
function newClosure(someNum, someRef) {
    // Local variables that end up within closure
    var num = someNum;
    var anArray = [1,2,3];
    var ref = someRef;
    return function(x) {
        num += x;
        anArray.push(num);
        alert('num: ' + num +
        '\nanArray ' + anArray.toString() +
        '\nref.someVar ' + ref.someVar);
    }
}
closure1 = newClosure(40,{someVar:'closure 1'});
closure2 = newClosure(1000,{someVar:'closure 2'});
closure1(5); // num:45 anArray[1,2,3,45] ref:'someVar closure1'
closure2(-10);// num:990 anArray[1,2,3,990] ref:'someVar closure2'
```

### 闭包的应用 - Singleton 单例模式：

```js
var singleton = function () {
    var privateVariable;
    function privateFunction(x) {
        ...privateVariable...
    }
 
    return {
        firstMethod: function (a, b) {
            ...privateVariable...
        },
        secondMethod: function (c) {
            ...privateFunction()...
        }
    };
}();
```

这个单例模式通过闭包来实现。通过闭包完成了私有的成员和方法的封装。匿名主函数返回一个对象。
对象包含了两个方法，方法1可以方法私有变量，方法2访问内部私有函数。
需要注意的地方是匿名主函数结束的地方的'()’，如果没有这个'()’就不能产生单例。因为匿名函数只能返回了唯一的对象，而且不能被其他地方调用。这个就是利用闭包产生单例的方法。