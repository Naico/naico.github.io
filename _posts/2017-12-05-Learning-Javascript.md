---
layout: blog
title: Step Into Javascript Language 
---

# 从闭包开始

## 闭包的定义

> **A closure is the combination of a function and the lexical environment within which that function was declared.**

> **Closures(闭包)是使用被作用域封闭的变量，函数，闭包等执行的一个函数的作用域。通常我们用和其相应的函数来指代这些作用域。(可以访问独立数据的函数)**

> **闭包是一个函数和声明该函数的词法环境的组合。从理论角度来说，所有函数都是闭包。**

这是MDN官方给出的闭包的定义。比较晦涩难懂。我个人理解为闭包就是能够读取其他函数内部变量的函数。

由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。

所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。


