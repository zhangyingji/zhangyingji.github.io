---
layout:     post
title:      "web前端响应式设计"
subtitle:   ""
date:       2021-09-02 23:03:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 前端
---

# 概述

响应式是指根据不同设备浏览器分辨率或尺寸来展示不同页面结构、行为、表现的设计方式。

响应式网站，目前比较主流的做法是通过前端通过判断`userAgent`

1. 依赖设备本身浏览器或设备特点
2. 需要分配多个站点页面跳转适配浏览器 .xx.com，m.xx.com，来分别存放PC端和移动端的页面
3. 多了一次跳转，跳转之前的逻辑不能少，用户体验变差

完整的响应式网站的实现其实需要考虑到以下这些问题：

- 响应式布局
- 响应式HTML和CSS
- 响应式媒体
- 响应式JavaScript

## 一 响应式布局

首先推荐以移动端为主、PC端为扩展的方式，这样可以避免移动端加载多余的PC端内容。响应式布局主要可以结合几种实现方式：

- 移动端布局控制：HTML5 视区(viewport)
- 栅格布局
- 不同设备元素容器布局

### A 移动端布局控制：HTML5 视区(viewport)**

在HTML添加以下代码

```HTML
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
<!-- 兼容IE8，激活Chrome Frame -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
```

content参数说明：

- width 可视区域的宽度
- initial-scale=1.0 以页面的实际尺寸显示，无任何缩放
- mininum-scale 允许用户的最小缩放值
- maximum-scale
- user-scalable 0为禁用缩放

### B 栅格布局

栅格系统由以下几个部分组成

- container 整个栅格系统的容器
- row 行
- column 列
- gutters 列的间隙


`container`：为了给整个栅格系统设置宽度，我们需要一个容器。容器的宽度通常为100%，但你可能希望为更大的显示器设置最大宽度max-width。

```CSS
.grid-container {
    width : 100%;
    max-width : 1200px; 
```

`row`：行元素用于防止里面的列溢出到其他的行。通常会使用clearfix来清除浮动，因为我们是通过浮动来制作栅格系统的

```CSS
/*-- 清除浮动 -- */ 
.row:before, 
.row:after {
    content: "";
    display: table ;
    clear:both;
```

`column`：利用`float`实现，为了避免列都是空的，可以：

```CSS
[class*='col-'] {
    float: left;
    min-height: 1px; 
}
```

容器为100%，要六列，则每列宽 100/6=16.66%

```CSS
[class*='col-'] {
        float: left;
        min-height: 1px; 
        width: 16.66%; 
}
```

还可以定义多种宽度

```CSS
.col-1{
        width: 16.66%; 
    }
.col-2{
    width: 33.33%; 
}
.col-3{
    width: 50%; 
}
.col-4{
    width: 66.664%;
}
.col-5{
    width: 83.33%;
}
.col-6{
    width: 100%;
}
```

`gutter`：由于列的宽度单位是响应式的 % ，我们给列元素的间距是固定单位的padding（px），为了避免复杂的计算，我们规定所有的盒子模型为`border-box`类型

```CSS
.grid-container *{
    box-sizing: border-box; 
}

[class*='col-'] {
    float: left;
    min-height: 1px; 
    width: 16.66%; 
    /*-- 设置间隙 --*/
    padding: 12px;
}
```

### 不同设备元素容器布局

```CSS
.container{
    width: 25%;
}
.mobile .container{
    width: 50%;
}
```

## 二 响应式HTML和CSS

对于要在移动端要隐藏的元素通过`display: none`来控制html是否显示；

对于展示样式不同的，需要在PC端额外引入css覆盖移动端的原有样式。

## 三 响应式媒体

### 字体：使用rem

1. 确定基数，一般10px
2. html { font-size: 百分数 } 百分数 = 基数/16
3. `px`换算`rem`: 62.5% = 14px => 1.4rem;

```CSS
/* 重置根元素字体大小 */
html {
    font-size: 62.5%;
}

/* 定义不同设备下的字体大小 */
@media (min-width:640px) { body { font-size: 1rem; }}
@media (min-width:960px) { body { font-size: 1.2rem; }}
@media (min-width:1200px) { body { font-size: 1.5rem; }}

/* 使用JS控制 */
var docEl = document.documentElement
var clientWidth = docEl.clientWidth
// 750为设计图的宽度,100px即为1rem
docEl.style.fontSize = 100 *(clientWidth/750) + 'px'
```

### 图片

// TODO

## 四 响应式JavaScript

```JS
if(isMobile) {
    require.async(['zepto', './mobileMain'], function($, main){
        main.init();
    });
} else {
    require.async(['jquery', './main'], function($, main){
        main.init();
    });
}
```

## 一般响应式网站的架构

简单网站的响应式结构

使用`Media Query`指定屏幕适应属性实现网页自适应，不同设备下的CSS写在一个文件内，CSS按模块管理。模块分开，易于管理和编码实现，也便于维护，是中小型网站实现响应式的不二选择

分流响应式站点

根据`userAgent`特性来加载不同域下的CSS，可以尽可能避免使用`Media Query`，不同浏览器环境下的样式分离管理，实现了平台样式分离，易于cdn管理

缺点：

- 需要维护多套样式表，即使公共部分抽离，一旦修改，影响多个平台环境
- 需要判断`UA`
- 架构实现稍微复杂

后台页面直出

和`adaptive-images`实现方法类似，首先是建立在不同环境下样式分离管理的基础上，后台根据静态文件请求所带的cookie信息直出静态页面，拉取相对应的cs。

缺点：

- 需要依赖cookie机制，服务器需要进行处理。(不过这层直出可以使用node中间服务获取，由这层服务请求后台，再返回给前端)

## 参考资料

1. [web前端响应式设计总结](https://blog.csdn.net/pupilxiaoming/article/details/77703805)
2. [跟着写一个CSS栅格布局](https://blog.csdn.net/qq_37204849/article/details/73542782)
