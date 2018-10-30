---
layout:     post
title:      "输入URL到页面加载完发生的那些事儿"
subtitle:   ""
date:       2018-07-26 13:30:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 网络
---

**1 浏览器解析URL解析出主机名**

URL示例

http://www.zhangyingji.cn/index.html

对应如下：

协议 + // + Web服务器名 + / + 文件路径名

**2 浏览器将主机名转换成服务器ip地址**

浏览器先查看浏览器缓存-系统缓存-路由器缓存
- 有
- 没有：进行*DNS解析*，获取IP

**3 浏览器向服务器发起TCP连接**

TCP连接：三次握手
- 客户端发送SYN为1的TCP包①给服务器
- 服务器收到SYN包，返回SYN为1的TCP包，同时还包含表示收到①包的ACK
- 客户端收到SYN＋ACK包，返回一个包含表示确认的ACK的TCP包。连接建立。

ps:

TCP断开：四次挥手
- 客户端发送FIN：1
- 服务器返回ACK
- 服务器发送FIN：1
- 客户端返回ACK

**4 浏览器向服务器发送http请求，请求数据包**

**5 服务器处理收到的请求，将数据返回至浏览器**

**6 浏览器收到http响应**

**7 关闭连接 浏览器解析文档**

**8 如果文档中有资源,重复567动作,直至资源全部加载完毕**

---

页面渲染过程参考[浏览器渲染页面过程与页面优化](https://segmentfault.com/a/1190000010298038)

HTML解析(DOM Tree) → CSS解析(CSSOM Tree) → 脚本解析 → 呈现树(Render Tree)包含样式计算等 → 布局(Layout) → 绘制(Painting)


