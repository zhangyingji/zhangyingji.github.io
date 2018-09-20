---
layout:     post
title:      "了解CORS和CSRF攻击、XSS攻击"
subtitle:   ""
date:       2018-09-20 17:12:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 前端
---

# CORS

CORS(Cross Origin Resourse-Sharing)定义了在必须访问跨域资源时，浏览器与服务器应该如何沟通。基本思想就是使用自定义的HTTP头让浏览器与服务器进行沟通,从而决定请求或响应是否成功。

## 技术原理

分为简单跨域请求和非简单跨域请求

### 非简单请求

预检查的机制会发送一个OPTIONS请求到服务器。如果服务器没有返回带有特殊头部的数据，简单请求GET或者POST请求仍然会发送，服务器的数据也会返回，但是浏览器会阻止Javascript获取这次请求。

下面详细分析一下实现安全跨域请求的控制方式:

浏览器先发送一个options方法的请求,带有如下字段：

```
Origin: 普通的HTTP请求也会带有，在CORS中专门作为Origin信息供后端比对,表明来源域。
Access-Control-Request-Method: 接下来请求的方法，例如PUT, DELETE等等
Access-Control-Request-Headers: 自定义的头部，所有用setRequestHeader方法设置的头部都将会以逗号隔开的形式包含在这个头中
```

如果服务器配置了cors，会返回对应对的字段:

```
Access-Control-Allow-Origin: 
Access-Control-Allow-Methods:
Access-Control-Allow-Headers:
```

然后浏览器再根据服务器的返回值判断是否发送非简单请求。**简单请求直接发送，加一个origin字段表明跨域请求的来源**。服务器处理完请求之后，会再返回结果中加上如下控制字段：

```
Access-Control-Allow-Origin: 允许跨域访问的域，可以是一个域的列表，也可以是通配符"*"。这里要注意Origin规则只对域名有效，并不会对子目录有效。即http://foo.example/subdir/ 是无效的。但是不同子域名需要分开设置，这里的规则可以参照同源策略。如果需要实现带cookie的跨域请求，需要明确的配置允许来源的域，使用任意域的配置是不合法的
Access-Control-Allow-Credentials: 是否允许请求带有验证信息
Access-Control-Expose-Headers: 允许脚本访问的返回头，请求成功后，脚本可以在XMLHttpRequest中访问这些头的信息(貌似webkit没有实现这个)
Access-Control-Max-Age: 缓存此次请求的秒数。在这个时间范围内，所有同类型的请求都将不再发送预检请求而是直接使用此次返回的头作为判断依据，非常有用，大幅优化请求次数
Access-Control-Allow-Methods: 允许使用的请求方法，以逗号隔开
Access-Control-Allow-Headers: 允许自定义的头部，以逗号隔开，大小写不敏感
```

最后，浏览器通过返回结果的这些控制字段来决定是将结果开放给客户端脚本读取还是屏蔽掉。**如果服务器没有配置CORS，则返回结果没有控制字段**，浏览器会屏蔽脚本对返回信息的读取

## 安全隐患

服务器接收到跨域请求的时候，并没有先验证，而是先处理了请求。

如果程序猿偷懒将Access-Control-Allow-Origin设置为允许来自所有域的跨域请求。那么cors的安全机制几乎就无效了。

从思路上讲，存在两种类型的攻击方式。

一种是在攻击者自己控制的网页上嵌入跨域请求，用户访问链接，执行了跨域请求，从而攻击目标，比如访问了内网敏感资源。

还有一种是正常的网页被嵌入了到攻击者控制页面的跨域请求，从而劫持用户的会话。

# CSRF攻击

CSRF：跨站请求伪造（Cross-site request forgery）

推荐[CSRF攻击与防御（写得非常好）](https://blog.csdn.net/stpeace/article/details/53512283)
 
# XSS攻击

XSS：跨站脚本（Cross-site scripting）XSS 

它一定是由用户的输入引起的，无论是提交表单、还是点击链接（参数）的方式，只要是对用户的输入不做任何转义就写到数据库，或者写到 html，js 中，就很有可能出错

分类：
1. 反射型：经过后端，不经过数据库， 即浏览器 -> 后端 -> 浏览器
2. 存储型：经过后端，经过数据库
3. DOM：不经过后端,DOM—based XSS漏洞是基于文档对象模型Document Objeet Model,DOM)的一种漏洞,dom - xss是通过url传入参数去控制触发的。

## 前端防范措施

1、转义用户的输入，把用户的输入解读为数据而不是代码

2、校验，对用户的输入及请求都进行过滤检查，如对特殊字符进行过滤，设置输入域的匹配规则等。

# 参考文章
1. 跨域资源共享(CORS)安全性浅析 http://www.freebuf.com/articles/web/18493.html
2. 揭密HTML5带来的攻击手法 http://www.freebuf.com/articles/web/11779.html
3. HTML5安全风险之CORS攻击详解 https://www.jb51.net/hack/383329.html
