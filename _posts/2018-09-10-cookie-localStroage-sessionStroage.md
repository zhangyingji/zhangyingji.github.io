---
layout:     post
title:      "cookie、localStroage与sessionStroage"
subtitle:   ""
date:       2018-09-10 15:45:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## cookie

#### 应用场景

1. 判断用户是否登陆过网站, 以便下次登录时能够实现自动登录（或者记住密码）
2. 保持上次登录的时间等信息
3. 保存上次登录查看的页面
4. 浏览计数

#### 缺点

1. 最大4k
2. 会随请求发送，浪费带宽
3. 用户可以禁用cookie, 使功能受限
4. 安全性较低

## localStroage

#### API
```
// 增加数据项
localStorage.setItem(`myCat`, `Tom`);
// 读取
localStorage.getItem(`myCat`);
// 移除
localStorage.removeItem(`myCat`);
// 移除所有
localStorage.clear();
```

#### 应用场景

1. 长期登录+判断用户是否登录
2. 长期存储在本地的数据

#### 优点

1. 存储空间大
2. 安全性较高

#### 缺点

1. 在浏览器的隐私模式下不能读取；
2. 本质是在读写文件，写入数据量大的话会卡；
3. 不能被爬虫读取
4. IE8+

## sessionStroage

API、优点同localStroage

#### 应用场景

1. 敏感的一次性登录
2. 自动保存一个文本输入框的内容，如果浏览器因偶然因素被刷新了，文本输入框里面的内容会被恢复，因此写入的内容不会丢失。

#### 特点

同源策略限制

## 三者区别

1. 仅cookie在请求中携带;
2. 存储大小;
3. 有效期：cookie在设置的有效期内有效，不管窗口或者浏览器是否关闭；localStroage始终有效；sessionStroage仅在当前浏览器窗口关闭前有效；
4. 作用域；