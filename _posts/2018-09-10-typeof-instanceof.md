---
layout:     post
title:      "typeof和instanceof"
subtitle:   ""
date:       2018-09-10 11:24:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## typeof

用于判断变量的数据类型

typeof返回的值有：object、undefined、boolean、string、number、function、symbol

无法具体识别数组和其他对象

#### 使用场景
```
// 判断一个变量是否存在,避免a不存在时报错
if(typeof a != "undefined") {
    alert("YES");
}
```

#### Examples
```
// object
typeof new Number(1)
typeof null
typeof {a:1}
// use Array.isArray
typeof [1,2,3]

// undefined
typeof undefined
typeof bafkbfkjwhkaskjfhjhkhfaksbfabsfbns

// boolean
typeof true
typeof Boolean(true)

// string
typeof ""

// number
typeof NaN
typeof Infinity

// function
typeof function(){}
typeof class C{}
typeof Math.sin

// symbols
typeof Symbol() === 'symbol'
typeof Symbol('foo') === 'symbol'
typeof Symbol.iterator === 'symbol'

```

## instanceof

用于判断变量是否为对象的实例

#### 使用场景
```
// 判断foo是否为Foo类的实例
function Foo(){} 
var foo = new Foo(); 
// true
console.log(foo instanceof Foo);

// 判断 foo 是否是 Foo 类的实例 , 并且是否是其父类型的实例
function Aoo(){} 
function Foo(){} 
// 原型继承
Foo.prototype = new Aoo();
 
var foo = new Foo(); 
// true 
console.log(foo instanceof Foo)
console.log(foo instanceof Aoo)
```

#### Example
```
// true
Object instanceof Object
Function instanceof Function
```
