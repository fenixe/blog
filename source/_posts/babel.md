---
title: babel
date: 2022-01-20 22:15:09
categories:
- Tool
tags:
- babel
---

# base
babel是一个转译器

## 编译器和转译器
编译的定义就是从一种编程语言转成另一种编程语言。主要指的是高级语言到低级语言。


## @babel/polyfill和@babel/runtime的区别
经过下面这么多例子，总结一下@babel/polyfill和@babel/runtime的区别：前者改造目标浏览器，让你的浏览器拥有本来不支持的特性；后者改造你的代码，让你的代码能在所有目标浏览器上运行，但不改造浏览器。
　　一个显而易见的区别就是打开IE11浏览器，如果引入了@babel/polyfill，在控制台我们可以执行Object.assign({}, {})；而如果引入了@babel/runtime，会提示你报错，因为Object上没有assign函数。

链接：https://juejin.cn/post/6901649054225465352




