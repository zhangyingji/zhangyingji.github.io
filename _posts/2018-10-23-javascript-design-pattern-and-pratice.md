---
layout:     post
title:      "JavaScript设计模式与开发实践"
subtitle:   "笔记"
date:       2018-11-06 23:44:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

> 《JavaScript设计模式与开发实践》 曾探

## ch1 面向对象

`多态`背后的思想是将“做什么”和“谁去做以及怎样去做”分离开来

## ch2 this、call、apply

`this`的指向大致分为
- 作为对象的方法调用
- 作为普通函数调用
- 构造器调用
- call、apply调用

**特别注意**，在作为普通函数调用时，内部的`this`指向`window`,故可以提前使用一个变量保存当前`this`的引用

**`call`和`apply`的区别**
- 传参形式

当第一个参数为`null`时，函数体内的`this`指向默认的宿主对象。特别地，严格模式下仍为`null`

**`call`和`apply`的用途**
- 改变this的指向
- 借用其他对象的方法

## ch3 闭包和高阶函数

**闭包的作用**
- 封装变量
- 延续局部变量的寿命

**闭包与内存泄漏**

COM对象的垃圾回收机制采用的是引用技术策略，只要把循环引用中的变量置null即可解决内存泄漏

**函数作为参数传递**
- 回调函数
- Array.prototype.sort

**函数作为返回值输出**
- 判断数据的类型
- getSingle


## ch18 单一职责原则

一个对象(方法)只做一件事

## ch21 接口和面向接口编程

## ch22 代码重构