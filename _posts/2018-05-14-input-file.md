---
layout:     post
title:      "解决button无法触发input类型为file的方法"
subtitle:   ""
date:       2018-05-14 23:56:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 前端
---

## 问题描述

默认input[type=file]样式太丑，做了个美化的button，对其添加click事件后发现只能选择文件，而当点击提交按钮无法真正上传文件

## 思路

进行伪装，当点击button时实际上点在input[type=file]上

## 操作

通过CSS，使input[type=file]
- 位于按钮上层
- 大小与button相同
- opacity设为0，使其透明

## HTML5拓展

增加multiple属性后，一次可上传多个文件

```
<form action="" method="">
  <input type="file" name="" multiple="multiple" />
  <input type="submit" />
</form>
```

webkitdirectory可上传文件夹，但仅Chrome有效

```
<input type="file" id="file_input" webkitdirectory />
```


