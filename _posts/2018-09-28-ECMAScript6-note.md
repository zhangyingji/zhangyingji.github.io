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

Promise 新建后立即执行，然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行

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

`Promise.resolve()` 将现有对象转为 Promise 对象

```
const jsPromise = Promise.resolve($.ajax('/whatever.json'));
```

## 应用

加载图片

```
const preloadImage = function (path) {
  return new Promise(function (resolve, reject) {
    const image = new Image();
    image.onload  = resolve;
    image.onerror = reject;
    image.src = path;
  });
};
```

**缺点**

首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择

