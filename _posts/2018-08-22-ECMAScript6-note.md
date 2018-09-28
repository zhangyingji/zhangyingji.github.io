---
layout:     post
title:      "ECMAScript 6"
subtitle:   "学习笔记"
date:       2018-09-28 14:28:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

# 前言

记录一些es6的实用用法，es6学习推荐[阮一峰《ECMAScript 6 入门》](http://es6.ruanyifeng.com/)

# 14 Promise

`Promise.all()`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例

```
// jquery自带promise
Promise.all([
    // 多个ajax请求
  $.ajax({}),$.ajax({})
]).then(result => {
    // 正确
}, err => {
    // 错误
});
```

`Promise.race()` 竞速

```
// 只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数
const p = Promise.race([p1, p2, p3]);
```

