
---
layout: post
title: " 第三百节，python操作redis缓存-其他常用操作，用于操作redis里的数据name，不论什么数据类型 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**python操作redis缓存-其他常用操作，用于操作redis里的数据name，不论什么数据类型**



**delete(*names) 根据删除redis中的任意数据类型**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.delete('rdi1')                                                 #delete(*names)根据删除redis中的任意数据类型
    
    
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # []
[/code]



**exists(name) 检测redis的name是否存在**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    print(r.exists('rdi1') )                                                #exists(name)检测redis的name是否存在
    
    
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # True
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**keys(pattern='*') 根据模型获取redis的name**  
 **更多：**  
 **KEYS * 匹配数据库中所有 key 。**  
 **KEYS h? llo 匹配 hello ， hallo 和 hxllo 等。？匹配一个任意字符**  
 **KEYS h *llo 匹配 hllo 和 heeeeello 等。*匹配多个任意字符**  
 **KEYS h [ae]llo 匹配 hello 和 hallo ，但不匹配 hillo，[]或者，匹配括号里的任意一个字符**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    a = r.keys(pattern='*')                                      #keys(pattern='*')根据模型获取redis的name,
    print(a)        #获取所有
    b = r.keys(pattern='r?i1')     #匹配一个任意字符
    print(b)
    
    
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # [b'rdi1']
    # [b'rdi1']
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**expire(name ,time) 为某个redis的某个name设置超时时间（秒）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.expire('rdi1',60)                                         #expire(name ,time)为某个redis的某个name设置超时时间
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
[/code]



**rename(src, dst) 对redis的name重命名为**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.rename('rdi1','adc')                                         #rename(src, dst)对redis的name重命名为
    
    n = r.zrange('adc',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**move(name, db)) 将redis的某个值移动到指定的db下**



**randomkey() 随机获取一个redis的name（不删除）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    print(r.randomkey())                                         #randomkey()随机获取一个redis的name（不删除）
    
    n = r.zrange('adc',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # b'rdi1'
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**type(name) 获取name对应值的类型**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    print(r.type('rdi1'))                                         #type(name)获取name对应值的类型
    
    n = r.zrange('adc',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # b'zset'
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**scan(cursor=0, match=None, count=None) 增量式迭代获取，redis里匹配的的name【推荐使用下面的方法】**  
 **cursor，游标（基于游标分批取获取数据）**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    a, b = r.scan(cursor=0, match='r*', count=None)                 #scan(cursor=0, match=None, count=None)增量式迭代获取，redis里匹配的的name
    print(a, b)
    #如果数据多
    a2, b2 = r.scan(cursor=a, match='r*', count=None)
    print(a2, b2)
    
    n = r.zrange('adc',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 0 [b'rdi1']
    # 0 [b'rdi1']
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



**scan_iter(match=None, count=None) 增量式迭代获取，redis里匹配的的name【推荐】**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)          #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    b = r.scan_iter(match='r*', count=None)                 #scan_iter(match=None, count=None)增量式迭代获取，redis里匹配的的name
    for i in b:
        print(i)
    
    
    n = r.zrange('adc',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # b'rdi1'
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'51'")]
[/code]



