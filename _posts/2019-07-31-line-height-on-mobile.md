---
layout:     post
title:      "安卓端使用line-height垂直居中产生偏移的解决方案"
subtitle:   ""
date:       2019-07-31 21:17:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - CSS
---

# 情景

1. 安卓（IOS未测试）
2. 使用line-height做垂直居中
3. 浏览器显示正常，安卓端文字向上偏移

产生原因：待考究

# 解决方案1：transform 

首先将原来的参数设置至原来的两倍

```
// height: .2rem;
height: .4rem;
```

然后将盒子缩小至原来的一半

```
height: .4rem;

-webkit-transform: scale(0.5, 0.5);
transform: scale(0.5, 0.5);
```

1. 注意数值的计算以达到设计图的效果
2. 以height为例，缩放后盒子占据的高度仍然是.4rem。对比原先，我们的盒子会被撑开，此时需要设置外层盒子的高度以达到设计图的效果