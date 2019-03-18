---
layout:     post
title:      "前端笔试"
subtitle:   ""
date:       2019-03-08 14:12:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 工作
---

# HTML

- HTML5了解哪些？

# CSS

- CSS3了解哪些？
- 常用布局
- [水平垂直居中](https://blog.zhangyingji.cn/2018/07/23/center/)
- [flex布局](https://blog.zhangyingji.cn/2018/05/18/flex/)
- [响应式设计](https://blog.zhangyingji.cn/2018/09/15/web-responsive-design/)
- CSS3动画、阴影

# JS

- ES6了解哪些？
- 常用方法

```
字符串：split(),replace(),match(),concat(),charAt(),indexOf(),substring()
数组：slice(),splice(),join(),concat(),push(),pop(),unshift(),shift(),reverse()
object：assign(),create(),defineProperties(),entries(),values(),hasOwnProperty(),freeze(),isFrozen()
```

- 闭包：能够读取其他函数内部变量的函数

```javascript
function f1(){
  n=999;
  function f2(){
    alert(n);
  }
  return f2;
}

var result=f1();
result();
```

- 原型链与继承
- 事件流
- 面向对象的特性：封装、继承、多态
- 函数声明定义的方法、异同、使用场景

---

- [深拷贝](http://blog.zhangyingji.cn/2018/10/23/deep-clone/)
- 数组去重

```javascript
Array.from(new set(arr));
```

- this的指向问题
- ajax和fetch
- 异步的方案

## 框架

- [react、angular、vue的对比](https://cn.vuejs.org/v2/guide/comparison.html)
- vue组件通信

```
父=>子：props属性
子=>父：$emit(）
非父子：建立空的实例（还有更好的办法）
兄弟：子=>父=>子
大型应用：引入vuex插件*
```

## 综合

- [输入url到加载出页面中间的流程](https://blog.zhangyingji.cn/2018/07/26/loading-web/)
- [HTTP状态码](https://blog.zhangyingji.cn/2018/07/26/http-status/)
- [本地存储](https://blog.zhangyingji.cn/2018/09/10/cookie-localStroage-sessionStroage/)
- [跨域的原理、解决方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)
- [浏览器渲染页面的过程](https://segmentfault.com/a/1190000010298038)
- 防抖和节流
- 作用域、怎么预防作用域污染：定义全局变量命名空间、匿名函数