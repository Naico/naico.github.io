---
layout: blog
title: Talk About Javascript 
---

闭包（closure）是Javascript语言的一个难点，也是它的特色，很多高级应用都要依靠闭包实现。

# 闭包的定义

> A closure is the combination of a function and the lexical environment within which that function was declared.

> Closures(闭包)是使用被作用域封闭的变量，函数，闭包等执行的一个函数的作用域。通常我们用和其相应的函数来指代这些作用域。(可以访问独立数据的函数)

> 闭包是一个函数和声明该函数的词法环境的组合。从理论角度来说，所有函数都是闭包。

这是[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)官方给出的闭包的定义。比较晦涩难懂。我个人理解为闭包就是能够读取其他函数内部变量的函数。

由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。

所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

如果要全面学习学好Javascript高级技巧以及熟练运用框架和理解框架，那么一定要学好闭包。说到闭包，那就不得不说另外一个很让人感兴趣的话题，就是**变量的作用域**。

# 变量的作用域

我们可以回忆一下，我们现在在用的语言，拿C#来举例。你在一个方法中定义了一个变量，那么你只能在这个方法的范围内访问这个变量。在这个方法之外是无法访问到这个变量的。这就是变量的作用域。在Javascript中也是一样，我们考虑以下的Javascript代码片段：
```js
var a = 999;
function foo(){
    alert(a);
}
foo(); // 999
```

