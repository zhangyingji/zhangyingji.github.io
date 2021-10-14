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

### 04 | export default function() {}：你无法导出一个匿名函数表达式

解析export

```js

// 导出“（声明的）名字”
export <let/const/var> x ...;
export function x() ...
export class x ...
export {x, y, z, ...};


// 导出“（重命名的）名字”
export { x as y, ...};
export { x as default, ... };


// 导出“（其它模块的）名字”
export ... from ...;


// 导出“值”
export default <expression
```

### 05 | for (let x of [1,2,3]) ...：for循环并不比使用函数递归节省开销

循环语句（对于支持“let/const”的 for 语句来说）“通常情况下”只支持一个块级作用域

## 从表达式到执行引擎：JavaScript是如何运行的 (7讲)

### 06 | x: break x; 搞懂如何在循环外使用break，方知语句执行真解

### 07 | `${1}`：详解JavaScript中特殊的可执行结构

### 08 | x => x：函数式语言的核心抽象：函数与表达式的同一性

1. 传入参数的过程执行于函数之外，例如f(a=100)；
2. 绑定参数的过程执行于函数（的闭包）之内，例如function foo(x=100) ..。x=>x在函数界面的两端都是值操作，也就是说 input/output 的都是数据的值，而不是引用。
3. 参数有两种初始化方法，它们根本的区别在于绑定初值的方式不同。
4. 闭包是函数在运行期的一个实例。

### 09 | (...x)：不是表达式、语句、函数，但它却能执行

标题中的示例是不能执行的，因为其中的括号并不是表达式中分组运算符，也不是语句中的函数调用，也不是声明中的形式参数表。声明中的...x被定义为“展开语法”，是逻辑的映射（它返回的是处理逻辑），而不是“值”或“引用”。它在不同的位置被 JavaScript 解释成不同的语义，包括对象展开和数组展开，并通过一组特定的代码来实现上述的语义。


在...x被理解为数组展开时，本质上是将x视为一个可迭代对象，并通过一个迭代变量（例如 tor）来管理它的迭代过程。在 JavaScript 中的迭代对象 x 的生存周期是交由使用它的表达式、语句或语法来管理的，包括在必要的时候通过 tor 来向内通知 return/throw 事件。

### 10 | x = yield x：迭代过程的“函数式化”


### 11 | throw 1;：它在“最简单语法榜”上排名第三


### 加餐 | 让JavaScript运行起来


## 从原型到类：JavaScript是如何一步步走向应用编程语言的


### 12 | 1 in 1..constructor：这行代码的结果，既可能是true，也可能是false

JavaScript 中面向对象系统的独特设计，它的对象属性存取结果总是不确定的。

- 如果属性不是自有的，那么它的值就是原型决定的；
- 当属性是存取方法的，那么它的值就是求值决定的。