---
layout:     post
title:      "前端代码规范"
subtitle:   ""
date:       2018-07-18 19:49:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---


#### 问题

项目需要在第一个请求执行成功取得一些参数后，立即执行第二个请求，而用默认参数直接嵌套没有达到想要的的效果

#### 解决

ajax中有一个**async**参数（异步属性），默认为true。故将其设置为false即可

对异步、同步的不了解的请自行查阅资料