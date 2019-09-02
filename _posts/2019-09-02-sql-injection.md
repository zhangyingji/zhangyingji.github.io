---
layout:     post
title:      "SQL注入漏洞"
subtitle:   ""
date:       2019-09-02 19:53:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 安全
    - 数据库
---

# 简介

SQL注入按数据类型可以分为

- 数字型
- 字符型
- 搜索型

按提交方式可分为

- GET型
- POST型
- Cookie型
- HTTP请求头注入

按执行效果可分为

- 报错注入
- 联合查询注入
- 盲注
- 堆查询注入

# 解决方案

第一种方法是使用预编译的方式执行SQL语句，用`java.sql.PreparedStatement`,执行进行变量绑定

```java
Connection conn
PreparedStatement ps = conn.prepareStatement(sql)

```

其他方法还有：

- 对带入SQL语句中的外部参数进行转义或者过滤
- 对于整数，判断是否为[0-9]的值；其他限定值，也可以做合法性校验
- 对于字符串，对特殊字符进行转义，如吧单引号转为两个单引号，把双引号转为两个单引号