---
layout:     post
title:      "bootstrap中的模态框和UEditor层次冲突"
subtitle:   ""
date:       2018-05-25 16:43:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---


## 问题描述

1. 在bootstrap模态框中嵌入了UEditor
2. 点击UEditor的工具栏，发现工具界面在遮罩层之下


## 解决方法

定位模态框和UEditord工具界面的z-index

在UEditor.config.js文件中，编辑器层级的基数,默认是900（默认被注释）

将其z-index的参数设置大于模态框的z-index即可