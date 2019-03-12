
---
layout: post
title: " 第三百零一节，python操作redis缓存-管道、发布订阅 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**python操作redis缓存-管道、发布订阅**



**一、管道**

**redis-
py默认在执行每次请求都会创建（连接池申请连接）和断开（归还连接池）一次连接操作，如果想要在一次请求中指定多个命令，则可以使用pipline实现一次请求指定多个命令，并且默认情况下一次
pipline 是原子性操作。**

**pipeline(transaction=True)
transaction=True将多个操作组合成原子性操作，也就是一个整体，有一个操作失败，意味着全部失败，数据回滚**

**pipe.execute() 执行原子性操作**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    
    
    pipe = r.pipeline(transaction=True)  #将多个操作组合成原子性操作，也就是一个整体，有一个操作失败，意味着全部失败，数据回滚
    
    pipe.set('name', 'alex')
    pipe.set('role', 'sb')
    
    pipe.execute()                       #执行原子性操作
[/code]





**二、发布订阅**  

**也就是，多个订阅端循环监听着Redis里的一个name名称通道，当这个通道里有内容时立即获取到，发布端向这个
**name名称通道里写入类容提供订阅者获取****

**订阅端**  
 **pubsub() 创建订阅对象**  
 **subscribe('fm104') 创建订阅通道，也就是redis里的一个name名称**  
 **parse_response() 循环监听通道里的类容**  
 **发布端**  
 **publish('fm104','12') 发布内容**

****订阅端****

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    """
    订阅者
    """
    import redis     #导入缓存模块
    
    r = redis.Redis(host='127.0.0.1', port=6379)     #配置连接池连接信息
    pub = r.pubsub()                                 #创建订阅对象
    pub.subscribe('fm104')                           #创建订阅通道，也就是redis里的一个name名称
    while True:
        msg = pub.parse_response()                   #循环监听通道里的类容
        print(msg)                                   #通道里有内容就打印
[/code]

**发布端**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    """
    发布者
    """
    import redis     #导入缓存模块
    
    r = redis.Redis(host='127.0.0.1', port=6379)     #配置连接池连接信息
    r.publish('fm104','12')
[/code]



**以后可以封装成一个模块，如：**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis
    
    
    class RedisHelper:
    
        def __init__(self):
            self.__conn = redis.Redis(host='10.211.55.4')
            self.chan_sub = 'fm104.5'
            self.chan_pub = 'fm104.5'
    
        def public(self, msg):　　　　　　　　#发布方法
            self.__conn.publish(self.chan_pub, msg)
            return True
    
        def subscribe(self):　　　　　　　　  #订阅方法
            pub = self.__conn.pubsub()
            pub.subscribe(self.chan_sub)
            pub.parse_response()
            return pub
[/code]



