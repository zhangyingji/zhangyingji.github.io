---
layout:     post
title:      "CSS3 媒体查询(Media Query)"
subtitle:   ""
date:       2018-09-15 17:22:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - CSS
---

# CSS3 媒体查询(Media Query)

CSS3的媒体查询可用来创建响应式布局，为特性的设备配置有选择性的加载CSS样式

## 语法

```
@media mediatype and|,|not|only (media feature) {
    CSS-Code;
}
```

### 常用媒体类型

1. all（所有），适用于所有设备。
2. handheld（手持），用于手持设备。
3. print（印刷），用于分页材料以及打印预览模式下在屏幕上的文档视图。
4. projection（投影），用于投影演示文稿，例如投影仪。
5.screen（屏幕），主要用于计算机屏幕。

### 逻辑查询

用and、,、not创建精确的媒体查询

### 查询特性

#### 长宽比 aspect-radio

限制水平像素与垂直像素的比值

```
/* 检测更宽一些的设备，当我们在播放视频时很有用 */
@media screen and (min-aspect-ratio: 16/9) {
    …
}
```

#### 取向 orientation

检测设备是横屏还是竖屏模式

```
@media all and (orientation: landscape) {
    …
}

@media all and (orientation: portrait) {
    …
}
```

#### 颜色 color

```
/* 检测设备是否至少支持8位颜色（256色） */
@media all and (min-color: 8) {
    …
}
```

#### 单色 monochrome

```
/* 检测设备的灰度 */
@media all and (min-monochrome: 8) {
    …
}
```

#### 分辨率 resolution

```
@media all and (min-resolution: 120dpi) {
    …
}
```

## 实例

为小屏幕设备的用户把元素（aside）隐藏起来

```
@media screen and (min-width: 680px) {
    aside {
        width: 33%;
    }
}

@media screen and (max-width: 680px) {
    aside {
        display: none;
    }
}
```

不同尺寸屏幕

```
/*在768 和991 像素之间的屏幕里，小屏幕，主要是PAD*/
@media (min-width: 768px) and (max-width: 991px) {
 * {font-size: 20px;}
}

/*在480 和767 像素之间的屏幕里，超小屏幕，主要是手机*/
@media (min-width: 480px) and (max-width: 767px) {
  * {font-size: 18px;}
}

/*在小于480 像素的屏幕，微小屏幕，更低分辨率的手机*/
@media (max-width: 479px) {
  * {font-size: 16px;}
}
```
