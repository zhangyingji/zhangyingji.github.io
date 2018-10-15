---
layout:     post
title:      "IDEA热加载自动更新（Update classes and resources）"
subtitle:   ""
date:       2018-04-15 13:58:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 工具
---

### 问题描述

初次使用IDEA，修改JSP页面后，渲染内容需要重启Tomcat后才更新

### 任务

实现热加载自动更新

### 解决

1. IDEA 菜单 > Run > Edit Edit Configurations... 
2. 在Deployment页面卡下，将Artifact类型改为exploded
3. 回到Server页面卡，将
On 'Update' action、On frame deactivation的选项改为 **Update classes and resources**

### 效果

修改JSP、刷新页面后即可看到更改后的页面效果
    


