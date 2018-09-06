---
layout:     post
title:      "清除浮动、浏览器前缀"
subtitle:   ""
date:       2018-07-22 21:48:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - CSS
---

## 清除浮动

- 给父元素加高度
- CSS设置clear:both; 但会导致margin失效
- 隔墙法

```
<div class=”cl h10”></div> 

.cl {clear: both;} 
// 控制间距
.h10 { height:10px} 
```

- 给父元素增加overflow:hidden;IE6追加_zoom: 1;


## 浏览器前缀

- webkit  以webkit/Blink做内核的浏览器:chrome、傲游
- ms Trident: IE
- moz Gecko: Firefox 
- o opera


