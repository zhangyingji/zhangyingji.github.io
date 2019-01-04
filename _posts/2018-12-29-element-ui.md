---
layout:     post
title:      "element-ui问题整理"
subtitle:   "笔记"
date:       2018-12-29 23:25:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 框架
---

1. 重置表单this.refs[′addServiceForm′].resetFields()不起作用

`el-from`接受一个`model`,`el-from-item`绑定`prop`属性

2. 表单验证提示消息没有正常消失

`prop`属性值要与`v-model`绑定的值一样

3. 如何获取tabel已勾选的row

在`table`中添加`@selection-change="handleSelectionChange"
```
handelSelectionChange (selection) {
    this.selection = selection
}
```
