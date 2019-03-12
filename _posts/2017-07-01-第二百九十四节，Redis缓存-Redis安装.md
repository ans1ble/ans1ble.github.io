---
layout: post
title: " 第二百九十四节，Redis缓存-Redis安装 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

****redis简介****

**redis是一个key-
value存储系统。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list(链表)、set(集合)、zset(sorted
set
--有序集合)和hash（哈希类型）。这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-
slave(主从)同步。**



**Redis缓存-Redis安装**

**************Linux版安装**************

[code]

    wget http: //download.redis.io/releases/redis-3.0.6.tar.gz
    tar xzf redis-3.0.6.tar.gz
    cd redis-3.0.6
    make
[/code]



**Window版安装**

****下载 ** **Window版本 ** ** **Redis软件，下一步，下一步，安装即可**************

**安装好Redis软件后，管理员身份运行cmd目录，首先cd 进入到 ** ** ** ** ** **
**Redis软件的安装目录****************

****************启动 ** ** ** ** ** ** **Redis软件******************************

[code]

    redis-server
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170701102816727-87671163.png)

****************配置远程连接信息****************

[code]

    redis-cli -h  127.0.0.1 -p 6379 -a 123456
    #说明：redis-cli -h ip -p 端口 -a 密码  
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170701103234602-741064419.png)

****************关闭服务****************

[code]

    redis-cli -h  127.0.0.1 -p 6379 shutdown
[/code]



**Redis管理平台软件  
**

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170701204708571-805561021.png)



