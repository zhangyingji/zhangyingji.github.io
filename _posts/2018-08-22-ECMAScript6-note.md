---
layout:     post
title:      "ECMAScript 6"
subtitle:   " 学习笔记"
date:       2018-08-22 17:16:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---


## 1 Babel
##### 根目录下配置文件.babelrc

- 基本格式

```
{
  "presets": [],
  "plugins": []
}
```

- presets 转码规则

```
# 安装转码规则
$ npm install --save-dev babel-preset-latest

$ npm install --save-dev babel-preset-react
```

- plugins 插件

```
# 安装插件
npm install babel-preset-es2015 --save-dev
```

##### 命令行转码babel-cli

```
# 安装在项目之中
$ npm install --save-dev babel-cli

# 然后改写package.json
# src:源目录；lib:目标目录
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}

# 转码
$ npm run build
```

##### babel-node

...

##### babel-register
##### babel-core
##### babel-polyfill
##### 浏览器环境
##### 在线转换、直接插入网页、Traceur转码器

## 2 let和const命令
##### 基本用法

- let所声明的变量，只在let命令所在的代码块内有效(eg:for)

```
// 循环变量部分是一个父作用域，循环体内部是一个单独的子作用域
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}

// 输出结果
// abc
// abc
// abc
```

- 不存在变量提升

```
// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

- 暂时性死区

总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）

- 不允许重复声明

##### 块级作用域

按道理ES6支持在块级作用域中声明函数，但为了减轻因此产生的不兼容问题，ES6 在附录 B里面规定，浏览器的实现可以不遵守上面的规定，有自己的行为方式。因为环境导致的行为差异太大，==应该避免在块级作用域内声明函数==

##### const

- const声明一个只读的常量
- 本质

实际上保证的，并不是变量的值不得改动，而是变量指向的那个*内存地址*不得改动

##### 顶层对象的属性

顶层对象，在浏览器环境指的是*window对象*，在 Node 指的是*global对象*。

var命令和function命令声明的全局变量依旧是顶层对象的属性。let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性

##### global对象

...

## 14 Promise对象

...

## 16 Generator函数的语法

...

## 19 class的基本语法

```
// 定义类
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```