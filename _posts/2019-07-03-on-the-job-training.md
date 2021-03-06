---
layout:     post
title:      "入职培训日记"
subtitle:   ""
date:       2019-07-03 21:10:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 分享
---
# 7月19日

git(李金华)

测试(严泳键)

将需求分解成任务和测试

# 7月18日

RTP实战（陈冠星、钟晓欣、黄少聪)

# 7月17日

RTP前端(陈冠星)

- 框架概述
- 功能模块

# 7月16日

RTP后端（钟晓欣、黄少聪）

# 7月15日

代码简洁之道(马雪阳)

- 好的代码：正确、高效、可维护
- 案例分析：抽象、命名、消除冗余、注释、单一原则、卫语句、嵌套层次、简化表达式、避免强制跳转、设计模式
- 规范总结
- 经验之谈：统一代码风格、以人为本、想清楚再写

开发规范(区伟洪)

- 学习习惯：系统化学习、知其然知其所以然
- java开发规范：格式化和命名规范、注释、日志、资源释放、翻页、线程池、数据库连接、避免死锁、高并发避免等号判断
- web应用安全技术规范：任意文件上传/下载漏洞、SQL注入、XSS攻击、越权访问、接口访问、短信炸弹、信息脱敏、上下文验证、业务层漏洞

# 7月12日

数据库（韦翼基）

- 概述
- 表的创建、更新、查询
- 索引
- 事务机制和锁机制
- 数据导出导入

# 7月11日

## linux基础（邓皓文）

以下是PPT中留下的思考题：

1. linux操作系统中，/boot目录放置的是什么东西？--内核文件。
2. 用户登录之后，首先被加载的是哪里的文件以及哪个文件？

```
/etc/profile中的
- ~/.bash_profile
- ~/.bash_login
- ~/.profile
```

3. 根据内核的此版本号判断，稳定版本的版本号是奇数还是偶数？--偶数。
4. xargs命令的本质是什么？--是给命令传递参数的一个过滤器。
5. 一般情况下，如何解除压缩一个tar文件？

```
# 压缩
tar -zvf <压缩包的名> <压缩的文件或目录>
# 解压
tar –xvf <压缩包名> -C <解压路径>
```

6. 通过使用vi编辑器，如何完成编辑文件的操作？-- 输入a或者i或者o进入相应的编辑模式，修改完按ESC进入命令行模式，再输入`:wq`保存并退出。
7. 输入命令cat abc.txt | awk '{print $NF}'的效果是什么？--显示abc.txt的字段数。
8. 如何把当前用户切换成mysql用户？

```
su - mysql
```

9. 需要以root用户在linux中远程登录到192.168.0.2服务器，应该输入什么命令？

```
ssh root@192.168.0.2
```

10. 输入命令route -n会显示什么？--路由信息。
11. 如何在命令模式下测试是否能访问www.baidu.com?

```
ping -c3 www.baidu.com
```

12. linux采用什么方法来区分和定义文件或文件夹的权限？

首先文件和文件夹d（目录、-（二进制文件）和l（软链接），其次权限分为r（可读）、w（可写）、x（可执行），最后是权限归属，分为文件文件夹所有者、所属用户组以及其他，这三者分别可定义其读、写和执行的权限。

13. 如何理解linux权限规划中所属者、所属用户组的含义？--方便权限的分配。
14. 输入命令charrt +a abc.txt有什么效果？--abc.txt文件只允许追加数据，不允许覆盖或者截断。
15. 如果需要成果实现setfacl操作内容，首要条件必须保证完成什么内容？--使用时指出针对的用户或者用户组。

## Nginx基础（欧阳康轲）

ES6 promise（詹嘉乔）

# 7月10日

部门简介、半年总结与迎新会

# 7月9日

## vue前端框架（陈冠星）

- vue基本概念：vue.set
- 常用命令：计算属性（缓存和监听）、不能用箭头函数的地方
- 组件封装：全局注册、局部注册、组件通信（传参，事件，插槽）
- 风格指南

## javascript基础精讲与编程实践（詹嘉乔）

- 类与继承：ES6中引入了`class`、`extend`和`super`
- 观察者模式
- MVC模式

# 7月8日

## 新起点新作为（李怀根）

- 养成良好习惯
- 守时
- 从认知到执行
- 关注细节，手比头高：细节决定成败、知其然知其所以然、勤思考、多动手，多动笔、学会问问题
- 主动积极
- 志存高远
- 自觉遵守规范：规矩与方圆、企业规范＋企业文化、研发中心首要的是技术规范、团队协作、架构的合理性和软件生产成本
- 勇于承担的责任心
- 自我管理、自我约束

## JavaEE入门（崔健锋）

- web项目结构：web.xml
- 常用组件：servlet
- MVC模式

# 7月5号

Java入门（陈洪宝）

- 基础知识：注释规范、命名规范、数据类型、变量类型、异常控制
- 面向对象
- 常用API
- 开发与测试

# 7月4号

银行IT系统架构（曾以蓁）

- 跨行转账的流程
- 风险监控的方法
- 用户交互：客户识别、客户接待
- 渠道整合：推荐产品、综合服务
- 业务服务: 产品制作、产品创新
- 基础资源: 账务管理、客户管理
- 管理决策: 人员招聘、营销决策、财务管理
- 数据智能层: 数据整合、智能分析

课题需求分析会（前端小组）

# 7月3日

学习智能网点（彭理）和信用卡基础知识（侯静）

发现精彩app（王海宁）

- 用户体验
- 极致
- 应对秒杀：限流、缓存、降级

用户体验专题（涂雪丹）:要以用户为中心

- 一致性
- 简洁性
- 遵从用户习惯
- 使用用户语言
- 内嵌帮助
- 适当提供反馈
- 突出主题
- 美观与协调
- 合理分组
- 有效引导

# 7月2日

学习企业文化（荣福丽）、人力资源管理制度（王淑君）、行政办公制度与员工行为规范（杜丹瑕）、银行业务基础（赵磊）、银行账户体系业务知识（谭红军）

书籍推荐
1. 《用户体验要素》
2. 《吃掉那只青蛙》

# 7月1日

入职典礼，其中师兄的分享的核心是：
1. 代码追求极致
2. 多做总结

