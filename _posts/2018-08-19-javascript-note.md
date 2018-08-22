---
layout:     post
title:      "JavaScript高级程序设计学习笔记"
subtitle:   "第3版"
date:       2018-08-19 16:42:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## 1 组成

- ECMAScript
- 文档对象模型(DOM,Document Object Model)
- 浏览器对象模型(BOM,Browser Object Model)



## 2 使用JS

- <noscript> 脚本不能执行时显示此部分
 
- 延迟脚本

```
// 页面解析完后运行，只适用外部脚本，且不一定按顺序执行
<script> defer=“defer”></script>
```

- 异步脚本

```
// 需要确保脚本不存在依赖关系
<stript async></sctipt>
```

## 3 基本概念

- 标识符 驼峰表示法
- 注释 //  /**/
- 严格模式

```
“use strict”;
```

- 变量

```
var message = "hi";
```

##### 基本数据类型

- Undefined

声明而未初始化时

- Null
- Boolean
- Number

```
// 检测“不是数值”
isNaN(); 

// 数值转换
parseInt();
parseFloat();
Number(); // 复杂
```

- String

```
// 转换为字符串
var ageAsString = age.toString();
// 字符串拼接
var lang = "Java" + "Script";
```

- Object

检测类型： typeof

##### 操作符
- ++ --
- ~ NOT
- & AND
- | OR
- ^ XOR
- << 左移
- \>> 有符号右移; >>> 无符号右移
- && || ! 与或非
- \* % + -
- < > <= >= 
- == != === !===
- ?: = ,

##### 语句

- if
- do-while
- while
- for
- for-in

迭代对象为null或undefinded时会抛出错误

- label && break && continue
- with

严格模式下不允许使用，大量使用会导致性能下降

- switch

```
switch(expression) {
    case value: statement
        break;
    default;
}
```

##### 函数

- function

```
// 不能重载，但是可通过arguments对象访问参数数组，判断arguments.length达到伪重载
function functionName(arg0,...,argN) {
    statements
}

```

## 4 变量、作用域和内存
##### 基本类型和引用类型的值

复制引用类型的值→引用的是同一个对象

- 传递函数

参数都是按值传递的

- 检测类型

基本数据类型用 typeof

```
// 对象或者null则返回object
```


对象类型用 instanceof

```
// 引用类型、Object构造函数为true,基本类型则返回false
alert(person instanceof Object)
```

##### 执行环境及作用域

- 延长作用域链

catch块、with语句

- 没有块级作用域

if、for语句声明的变量会存在于外部执行环境中

- 声明变量

使用var声明的变量会被添加到最接近的环境中，如函数内最接近的环境为该函数的局部环境；若不使用var，则添加至全局环境

- 查询标识符

```
// 向上逐级查询，匹配即停止
var color = "blue";

function getColor(){
    var color = "red";
    return color;
}

alert(getColor()); // "red"
```

##### 垃圾收集

- 机制

找出不再使用的变量，释放其占用的内存

一般函数执行结束，则可以释放局部变量占的内存

- 标记清除（主流）：标识进入环境、离开环境
- 引用计数（存在循环引用的问题）
- 性能问题？
- 管理内存

优化内存占用：只保存必要的数据。一旦数据不再有用，解除引用（置null），这样垃圾收集器下次运行时则会将其回收

## 5 引用类型
##### Object类型

- 创建

```
// 1 new
var person = new Object();
person.name = "Zhang Yingji";
// 2 对象字面量，可读性好
var person = {
    name : "Zhang Yingji";
}
```

- 对象字面量是向函数传递大量可选参数的首选方式
- 访问对象属性使用点表示法

##### Array类型

- 创建

```
// 1 new
// new可省略
var colors = new Array();
var colors = new Array(20);
var colors = new Array("red","blue","green");
// 2 数组字面量
var colors = ["red","blue","green"];
var names = [];
```

- length属性
- 检测数组

```
// 一个网页/全局作用域/框架
if (value instanceof Array) {
    // do something
}
// 通用情况,IE9+
if {Array.isArray(value) {
    // do something
}
```

- 转换方法

toLocaleString();tostring();valueOf()

- 栈方法 push();pop()
- 队列方法 push();shift()
- 重排序方法 reverse();sort()

```
// sort()会转化为字符串后再比较
// 故接受一个比较函数来正确排序
function compare(value1,value2) {
    if(value1 < value2) {
        return -1;
    } else if (value > value2) {
        return 1;
    } else {
        return 0;
    }
}

values.sort(compare);
```

- 操作方法

```
// concat() 创建新的数组，末尾追加
var colors2 = colors.concat("yellow");

// slice(start,[end]) 创建新的数组，返回索引start到end的项，不包括end
var colors3 = colors.slice(2);

// splice()
// 删除，指定起始位置、要删除的项数
splice(0,2)
// 插入，指定起始位置、要删除的项数、要插入的项
splice(2,0,"zhang","yingji");
// 替换，指定起始位置，要删除的项数，要插入的项
splice(2,1,"zhang");
```

- 位置方法

接收的参数：要查找项和表示查找起点的索引（可选）

```
// 从开头向后查找
indexOf()
// 从结尾向前查找
lastIndexOf()
```

- 迭代方法

...

- 归并方法
 
...

##### Date 类型

```
// 创建,获得当前日期和时间
var now = new Date();

// 基于GTM创建指定日期 
// 1 Date.parse(),可以后台调用
var someDate = new Date("May 25,2004");
// 2 Date.UTC()
// GMT 2005.5.5 5:55:55,一月是0
var allFives = new Date(Date.UTC(2005,4,5,17,5,5)

// 基于系统设置本地时区，参数一致
var allFives = new Date(2005,4,5,17,5,5)

// 返回调用方法时的毫秒数
var start = Date.now();
```

- 继承的方法/格式化方法
- 日期/时间组件方法 P102

##### RegExp类型

- 创建

```
// 使用字面量形式
var expression = / pattern / falgs

// 使用构造函数
var pattern = new RegExp("pattern","flags")
```

flgs可有一或多个：
1. g 被应用于所有字符串
2. i 不区分大小写
3. m 到达一行末尾时还会继续查找下一行

- 正则表达式元字符需要转义：
([{\^$|)>*+.]}

- RegExp实例属性、方法

```
// exec()
// test()，验证是否匹配时常用
if(pattern.test(text)) {
    alert("matched")
}
```

- RegExp构造函数属性、模式局限性

...

##### Function类型

- 声明

```
// 函数声明，提前
function sum(num1,num2){}

// 函数表达式,另外构造函数法不推荐
var sum = function(num1,num2){}
```

- 没有重载
- 作为值的函数
- 函数内部属性：arguments,this

```
// arguments.callee解除代码与函数名的耦合
function factorial(num) {
    if(num <= 1) {
        return 1;
    } else {
        return num * arguments.callee(num-1);
    }
}

//
```


##### 基本包装类型

##### 单体内置对象


## 6 面向对象
