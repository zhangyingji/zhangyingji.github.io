---
layout:     post
title:      "MongoDB集群（分片+副本集）"
subtitle:   ""
date:       2018-05-12 23:31:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 数据库
---

    

## 简述
##### 相关概念

1. config(配置服务器）

数据和片的对应关系以及相应的配置信息

2. mongos(路由服务器)

负责把对应的数据请求请求转发到对应的shard服务器上

3. mongod(分片服务器)

##### 环境准备

- windows10 + mongodb3.4 + matlab
- 3台可以互相ping通的主机(单机下也可以建立不同的文件进行伪分布)
- 开发过程中尽量保持相同的版本号、开发工具，避免不必要的问题

##### 端口分配

- mongos: 20000
- config: 20010
- shard1: 20001
- shard2: 20002
- shard3: 20003

## 任务

1. 一个分片下建副本集
2. 建立多分片

## 集群搭建
##### 1 准备

在每台服务器新建mongos、config、shard1、shard2、shard3目录

各目录下再分别建data、log目录

##### 2 副本集

以分片一为例，启动服务器

```
#集群名字为shard1
mongod --shardsvr --replSet shard1 --port 20001 --dbpath shard1_1/data --logpath shard1_1/log/shard.log --nojournal --oplogSize 10;
mongod --shardsvr --replSet shard1 --port 20002 --dbpath shard1_2/data --logpath shard1_2/log/shard.log --nojournal --oplogSize 10;
mongod --shardsvr --replSet shard1 --port 20003 --dbpath shard1_3/data --logpath shard1_3/log/shard.log --nojournal --oplogSize 10;
```

登录其中一个配置服务器，为分片配置副本集

```
# IP为配置服务器相应IP、Port
mongo IP:port

config = {
    _id : "cfgSet",
    members: [
        {_id : 0,host : "副本IP:port"},
        {_id : 0,host : "副本IP:port"},
        {_id : 0,host : "副本IP:port"}
    ]
} 
```

初始化

```
# 初始化 
rs.initiate(config) 
# 查看配置
rs.conf()  
# 查看状态
rs.status() 
# 查看是否是主节点
rs.isMaster() 
```

其他分片的副本集依此类推

##### 3 分片

以分片一为例，启动配置服务器

mongodb3.4以后要求配置服务器也创建副本集

```
mongod --configsvt --replSet cfgSet --dbpath config\data --port 20010 --logpath config\log\config.log
```

启动mongod服务器(上一步已启动)

启动mongos服务器
> 在生产环境通常有多mongos作为请求的入口，防止其中一个挂掉所有的mongodb请求都没有办法操作

```
mongos --configdb cfgSet/IP:port --port 20000 -logpath mongos/log/mongos.log
```

启用分片

```
# 登录其中一mongos
mongo IP:port
# 切换admin
use admin
#串联路由服务器与分配副本集
sh.addShard("shard1/副本IP:port,副本IP:port,副本IP:port")

```

指定数据库、集合的分片生效

```
db.runCommand({enablesharding:"testdb"})

db.runCommand({shardcollection:"testdb.table1",key:{id:1}})
```

测试分片配置效果

```
use testdb
# 插入测试数据
for (var i = 1; i <= 10000; i++)
db.table1.save({id:i,"test1":"testval1"});
# 查看
db.table1.stats();
```

## Result
##### 启动顺序

先启动配置服务器，再启动分片，最后启动mongos，而本教程配置过程中是先搭建副本集再作分片，因为[2]中提到：*这样就既可以快速读取数据，又可以防止数据丢失*（未验证）

##### 待解决

1. 安装3.6.4版本时提示ended prematurely because of an error.Your system has not been modified.


## 参考资料

1. https://www.cnblogs.com/ityouknow/p/7344005.html

2. https://blog.csdn.net/bfdnmy/article/details/51842217

3. https://www.cnblogs.com/wangshouchang/p/6130857.html


