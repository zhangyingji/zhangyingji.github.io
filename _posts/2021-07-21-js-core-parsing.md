---
layout:     post
title:      "《JavaScript核心原理解析》 - 周爱民"
subtitle:   "笔记"
date:       2021-07-21 23:50:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

# 《JavaScript核心原理解析》 - 周爱民

## 从零开始：JavaScript语言是如何构建起来的

### 01 | delete 0：JavaScript中到底有什么是可以销毁的

- delete 运算符尝试删除值数据时，会返回 true，用于表示没有错误（Error）
- delete 0 的本质是删除一个表达式的值（Result）
- delete x 与上述的区别只在于 Result 是一个引用（Reference）
- delete 其实只能删除一种引用，即对象的成员（Property）。

附：

1. [MDN：delete操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)
2. [深入detele](https://time.geekbang.org/column/article/164312)

### 02 | var x = y = 100：声明语句与语法改变了JavaScript语言核心性质

- var 等声明语句总是在变量作用域（变量表）或词法作用域中静态地声明一个或多个标识符
- 全局变量的管理方式决定了“向一个不存在的变量赋值”所导致的变量泄漏是不可避免的
- 动态添加的“var 声明”是可以删除的，这是唯一能操作 varNames 列表的方式（不过它并不存在多少实用意义）
- 变量声明在引擎的处理上被分成两个部分：一部分是静态的、基于标识符的词法分析和管理，它总是在相应上下文的环境构建时作为名字创建的；另一部分是表达式执行过程，是对上述名字的赋值，这个过程也称为绑定
- 标题里的这行代码中，x 和 y 是两个不同的东西，前者是声明的名字，后者是一个赋值过程可能创建的变量名

### 03 | a.x = a = {n:2}：一道被无数人无数次地解释过的经典面试题

```js
// 结合指针很好理解，此时a和ref只指向同一块内存地址
var a = {n:1}, ref = a; 
// a指向新的内存地址 {n:2}
// 原来的内存地址（ref)增加了新的属性x
a.x = a = {n:2};
console.log(a.x); // --> undefined
console.log(ref.x); // {n:2}
```
