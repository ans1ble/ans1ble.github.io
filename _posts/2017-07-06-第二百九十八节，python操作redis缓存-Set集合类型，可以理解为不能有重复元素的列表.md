---
layout: post
title: " 第二百九十八节，python操作redis缓存-Set集合类型，可以理解为不能有重复元素的列表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**python操作redis缓存-Set集合类型，可以理解为 不能有重复元素的列表**



**sadd(name,values) name对应的集合中添加元素**



[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('adc8868','123')                                         #sadd(name,values)name对应的集合中添加元素
    
    f = r.smembers('adc8868')                                       #获取name对应的集合的所有成员
    print(f)
    #返回
    #{b'123'}
[/code]





**scard(name) 获取name对应的集合中元素个数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('adc8868','123')                                         #sadd(name,values)name对应的集合中添加元素
    
    f = r.scard('adc8868')                                          #scard(name)获取name对应的集合中元素个数
    print(f)
    #返回
    #1
[/code]



**sdiff(keys, *args) 在第一个name对应的集合中且不在其他name对应的集合的元素集合**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('adc8861','123','456')                                   #sadd(name,values)name对应的集合中添加元素
    r.sadd('adc8862','123','456','789')
    
    f = r.sdiff('adc8862','adc8861')                                #sdiff(keys, *args)在第一个name对应的集合中且不在其他name对应的集合的元素集合
    print(f)
    #返回
    #{b'789'}
[/code]



**sdiffstore(dest, keys, *args)
获取第一个name对应的集合中且不在其他name对应的集合，再将其新加入到dest对应的集合中**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('adc8861','123','456')                                   #sadd(name,values)name对应的集合中添加元素
    r.sadd('adc8862','123','456','789')
    
    f = r.sdiffstore('adc','adc8862','adc8861')                    #sdiffstore(dest, keys, *args)获取第一个name对应的集合中且不在其他name对应的集合，再将其新加入到dest对应的集合中
    print(f)
    
    n = r.smembers('adc')                                          #获取name对应的集合的所有成员
    print(n)
    #返回
    # 1
    # {b'789'}
[/code]



**sinter(keys, *args) 获取多个集合与第一个集合里交集的数据，也就是相同的数据**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.sinter("rdi1","rdi2")                                     #sinter(keys, *args)获取多个集合与第一个集合里交集的数据，也就是相同的数据
    print(n)
    
    #返回
    #{b'123', b'456'}
[/code]



**sinterstore(dest, keys, *args)
获取多个集合与第一个集合里交集的数据，也就是相同的数据，在将其加入到dest对应的集合中**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.sinterstore('adc',"rdi1","rdi2")                           #sinterstore(dest, keys, *args)获取多个集合与第一个集合里交集的数据，也就是相同的数据，在将其加入到dest对应的集合中
    print(n)
    
    n = r.smembers('adc')                                          #获取name对应的集合的所有成员
    print(n)
    #返回
    # 2
    # {b'123', b'456'}
[/code]



**sismember(name, value) 检查value是否是name对应的集合的成员**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.sismember("rdi1",'851')                           #sismember(name, value)检查value是否是name对应的集合的成员
    print(n)
    
    #返回
    #True
[/code]



**smembers(name) 获取name对应的集合的所有成员**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.smembers("rdi1")                           #smembers(name) 获取name对应的集合的所有成员
    print(n)
    
    #返回
    #{b'123', b'851', b'456'}
[/code]



**smove(src, dst, value) 将某个成员从一个集合中移动到另外一个集合**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.smove("rdi1",'rdi2','851')                           #smove(src, dst, value)将某个成员从一个集合中移动到另外一个集合
    print(n)
    
    #返回
    #True
[/code]



**spop(name) 从集合的右侧（尾部）移除一个成员，并将其返回**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.spop("rdi1")                           #spop(name)从集合的右侧（尾部）移除一个成员，并将其返回
    print(n)
    
    #返回
    #b'851'
[/code]



**srandmember(name, numbers) 从name对应的集合中随机获取 numbers 个元素**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.srandmember("rdi1",number=2)                           #srandmember(name, numbers)从name对应的集合中随机获取 numbers 个元素
    print(n)
    
    #返回
    #[b'851', b'123']
[/code]



**srem(name, values) 在name对应的集合中删除某些值**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.srem("rdi1",'456')                           #srem(name, values)在name对应的集合中删除某些值
    print(n)
    
    #返回
    #1
[/code]



**sunion(keys, *args) 获取多个name对应的集合的并集，并集后相同的数据只显示一个**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    n = r.sunion("rdi1",'rdi2')                           #sunion(keys, *args)获取多个name对应的集合的并集，并集后相同的数据只显示一个
    print(n)
    
    #返回
    #{b'456', b'123', b'789', b'851'}
[/code]



**sunionstore(dest,keys, *args)
获取多个name对应的集合的并集，并集后相同的数据只取一个，并将结果保存到dest对应的集合中**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    r.sunionstore('adc',"rdi1",'rdi2')               #sunionstore(dest,keys, *args)获取多个name对应的集合的并集，并集后相同的数据只取一个，并将结果保存到dest对应的集合中
    n = r.smembers("adc")                           #smembers(name) 获取name对应的集合的所有成员
    print(n)
    
    #返回
    #{b'456', b'851', b'123', b'789'}
[/code]



**sscan(name, cursor=0, match=None, count=None)
同字符串的操作，用于增量迭代分批获取元素，避免内存消耗太大【推荐使用下面那个方法】**  
 **name，redis的name**  
 **cursor，游标（基于游标分批取获取数据）**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**  
 **如：**  
 **第一次：cursor1, data1 = r.sscan('name', cursor=0, match=None, count=None)**  
 **第二次：cursor2, data2 = r.sscan('name', cursor=cursor1, match=None,
count=None)**  
 **...**  
 **直到返回值cursor的值为0时，表示数据已经通过分片获取完毕**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    #sscan(name, cursor=0, match=None, count=None)用于增量迭代分批获取元素，避免内存消耗太大
    cursor1, data1 = r.sscan('rdi1',cursor=0,match='*1',count=None)       #获取name对应的元素，匹配以1结尾的元素
    print(cursor1, data1)                                                 #返回两个值，第一个是获取的游标位置，第二个是获取到的数据
    
    cursor2, data2 = r.sscan('rdi1',cursor=cursor1,match='*2',count=None)    #第二次获取，游标使用第一次返回的游标位置，使其向后继续
    print(cursor2, data2)
    
    
    #返回
    #0 [b'851']
    #0 []
[/code]



**sscan_iter(name, match=None, count=None) 用于增量迭代分批获取元素，避免内存消耗太大【推荐】**  
 **name，redis的name**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.sadd('rdi1','123','456','851')                                #sadd(name,values)name对应的集合中添加元素
    r.sadd('rdi2','123','456','789')
    
    #sscan_iter(name, match=None, count=None)用于增量迭代分批获取元素，避免内存消耗太大
    n = r.sscan_iter('rdi1',match='*1',count=None)       #获取name对应的元素，匹配以1结尾的元素
    print(n)                                             #返回获取到的数据对象，需要循环
    
    for i in n:
        print(i)                                         #循环出获取到的数据
    
    
    #返回
    # <generator object StrictRedis.sscan_iter at 0x0000023F18C94570>
    # b'851'
[/code]



