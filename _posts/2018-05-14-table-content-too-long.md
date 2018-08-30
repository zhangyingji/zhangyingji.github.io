---
layout:     post
title:      "CSS实现表格内容过长时用省略号表示"
subtitle:   ""
date:       2018-05-14 22:33:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - CSS
---

    
    ```
    table {
        /* 列宽由表格宽度和列宽度设定 */
    　　table-layout: fixed;
    }
    
    td {
        /* 不换行 */
    　　white-space: nowrap;
    　　/* 超出单元格的部分隐藏 */
    　　overflow: hidden;
    　　/* 用省略号代替被隐藏的部分 */
    　　text-overflow: ellipsis;
    }
    ```



