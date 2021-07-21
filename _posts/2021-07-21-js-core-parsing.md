---
layout:     post
title:      "《JavaScript核心原理解析》 --周爱民"
subtitle:   "笔记"
date:       2021-07-21 23:50:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

# 从零开始：JavaScript语言是如何构建起来的

## detele 0

- delete 运算符尝试删除值数据时，会返回 true，用于表示没有错误（Error）
- delete 0 的本质是删除一个表达式的值（Result）
- delete x 与上述的区别只在于 Result 是一个引用（Reference）
- delete 其实只能删除一种引用，即对象的成员（Property）。

附：

1. [MDN：delete操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)
2. [深入detele](https://time.geekbang.org/column/article/164312)