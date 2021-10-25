---
layout: post
title: " 第二百九十九节，python操作redis缓存-SortSet有序集合类型，可以理解为有序列表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**python操作redis缓存-SortSet有序集合类型，可以理解为有序列表**

**有序集合，在集合的基础上，为每元素排序；元素的排序需要根据另外一个值来进行比较，所以，对于有序集合，每一个元素有两个值，即：值和分数，分数专门用来做排序。**



**zadd(name, *args, **kwargs) 在name对应的有序集合中添加元素**  
 **如：**  
 **zadd('zz', 'n1(值)', 1(分), 'n2(值)', 2(分)) 值表示是元素值，分可以理解为是元素序号**

**zadd('zz', 'n1', 1, 'n2', 2)**  
 **或**  
 **zadd('zz', n1=11, n2=22)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1', 1, 'n2', 2)                                 #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.zadd('zz', n1=11, n2=22)
    
    
    n = r.zrange('rdi1',0, 1, desc=False, withscores=True, score_cast_func=str)  #获取有序列表
    print(n)
    
    
    #返回
    # [(b'n1', "b'1'"), (b'n2', "b'2'")]
[/code]



**zcard(name) 获取name对应的有序集合元素的数量**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1', 1, 'n2', 2)                                 #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    
    n = r.zrange('rdi1',0, 1, desc=False, withscores=True, score_cast_func=str)  #获取有序列表
    print(n)
    
    f = r.zcard('rdi1')                                                          #zcard(name)获取name对应的有序集合元素的数量
    print(f)
    #返回
    # [(b'n1', "b'1'"), (b'n2', "b'2'")]
    # 2
[/code]



**zcount(name, min, max) 获取name对应的有序集合中分数 在 [min,max] 之间的个数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1',1, 'n2',2, 'n3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    
    n = r.zrange('rdi1',0, 1, desc=False, withscores=True, score_cast_func=str)  #获取有序列表
    print(n)
    
    f = r.zcount('rdi1',1,4)                                             #zcount(name, min, max)获取name对应的有序集合中分数 在 [min,max] 之间的个数
    print(f)
    #返回
    # [(b'n1', "b'1'"), (b'n2', "b'2'")]
    # 2
[/code]



**zincrby(name, value, amount) 自增name对应的有序集合的 值 对应的分数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1',1, 'n2',2, 'n3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zincrby('rdi1','n2',amount=2)                    #zincrby(name, value, amount)自增name对应的有序集合的 值 对应的分数
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #获取有序列表
    print(n)
    #返回
    # 4.0
    # [(b'n1', "b'1'"), (b'n3', "b'3'"), (b'n2', "b'4'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zrange( name, start, end, desc=False, withscores=False,
score_cast_func=float) 按照索引范围获取name对应的有序集合的元素**

**参数：**  
 **name，redis的name**  
 **start，有序集合索引起始位置（非分数）**  
 **end，有序集合索引结束位置（非分数）**  
 **desc，排序规则，默认按照分数从小到大排序**  
 **withscores，是否获取元素的分数，默认只获取元素的值**  
 **score_cast_func，对分数进行 数据转换的函数**  
 **更多：**  
 ** 从大到小排序**  
 **zrevrange(name, start, end, withscores=False, score_cast_func=float)**  
 **按照分数范围获取name对应的有序集合的元素**  
 **zrangebyscore(name, min, max, start=None, num=None, withscores=False,
score_cast_func=float)**  
 ** 从大到小排序**  
 **zrevrangebyscore(name, max, min, start=None, num=None, withscores=False,
score_cast_func=float)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1',1, 'n2',2, 'n3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zincrby('rdi1','n2',amount=2)                    #zincrby(name, value, amount)自增name对应的有序集合的 值 对应的分数
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #zrange( name, start, end, desc=False, withscores=False, score_cast_func=float)按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 4.0
    # [(b'n1', "b'1'"), (b'n3', "b'3'"), (b'n2', "b'4'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zrank(name, value) 获取某个值在 name对应的有序集合中的排行（从 0 开始）**

**zrevrank(name, value) **获取某个值在 name对应的有序集合中的排行** ，从大到小排序**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','n1',1, 'n2',2, 'n3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zrank('rdi1','n5')                    #zrank(name, value)获取某个值在 name对应的有序集合中的排行（从 0 开始）
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #zrange( name, start, end, desc=False, withscores=False, score_cast_func=float)按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 4
    # [(b'n1', "b'1'"), (b'n2', "b'2'"), (b'n3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zrangebylex(name, min, max, start=None, num=None)**  
 **当有序集合的所有成员都具有相同的分值时，有序集合的元素会根据成员的 值 （lexicographical
ordering）来进行排序，而这个命令则可以返回给定的有序集合键 key 中， 元素的值介于 min 和 max 之间的成员**  
 **对集合中的每个成员进行逐个字节的对比（byte-by-byte compare）， 并按照从低到高的顺序， 返回排序后的集合成员。
如果两个字符串有一部分内容是相同的话， 那么命令会认为较长的字符串比较短的字符串要大**  
  
**参数：**  
 **name，redis的name**  
 **min，左区间（值）。 + 表示正无限； - 表示负无限； ( 表示开区间； [ 则表示闭区间**  
 **min，右区间（值）**  
 **start，对结果进行分片处理，索引位置**  
 **num，对结果进行分片处理，索引后面的num个元素**  
 **如：**  
 **ZADD myzset 0 aa 0 ba 0 ca 0 da 0 ea 0 fa 0 ga**  
 **r.zrangebylex('myzset', "-", "[ca") 结果为：['aa', 'ba', 'ca']**  
  
**更多：**  
 **从大到小排序**  
 **zrevrangebylex(name, max, min, start=None, num=None)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',1, 'c3',1, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zrangebylex('rdi1', "-", "[c")                    #获取元素分数相同，值小于c的值
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #zrange( name, start, end, desc=False, withscores=False, score_cast_func=float)按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # [b'a1', b'b2']
    # [(b'a1', "b'1'"), (b'b2', "b'1'"), (b'c3', "b'1'"), (b'n1', "b'1'"), (b'n2', "b'1'"), (b'n3', "b'1'")]
[/code]



**zrem(name, values) 删除name对应的有序集合中值是values的成员**

**如：zrem('zz', ['s1', 's2']) 删除多个值**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zrem('rdi1', 'b2')                    #zrem(name, values)删除name对应的有序集合中值是values的成员
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 1
    # [(b'a1', "b'1'"), (b'c3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zremrangebyrank(name, min, max) 根据排行范围删除**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zremrangebyrank('rdi1',0,3)                    #zremrangebyrank(name, min, max)根据排行范围删除
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 1
    # [(b'a1', "b'1'"), (b'c3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zremrangebyscore(name, min, max) 根据分数范围删除**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zremrangebyscore('rdi1',1,3)                    #zremrangebyscore(name, min, max)根据分数范围删除
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 3
    # [(b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zremrangebylex(name, min, max) 根据值返回删除**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zremrangebylex('rdi1',"-", "[c")                    #删除值小于c的元素
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 2
    # [(b'c3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]



**zscore(name, value) 获取name对应有序集合中 value 对应的分数**



[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    f = r.zscore('rdi1','c3')                    #zscore(name, value)获取name对应有序集合中 value 对应的分数
    print(f)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 3.0
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'")]
[/code]





**zinterstore(dest, keys, aggregate=None)
获取两个有序集合的交集，如果遇到相同值不同分数，则按照aggregate进行操作添加到新的有序集合**  
 **aggregate的值为: sum(相加和),min(最小),max(最大)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.zadd('rdi2','a1',8, 'b2',9, 'c10',10, 'n11',11, 'n12',12)
    
    f = r.zinterstore('rd',['rdi1','rdi2'],aggregate=None)                 #获取两个有序集合的交集，如果遇到相同值不同分数，则按照aggregate进行操作添加到新的有序集合
    print(f)
    
    n = r.zrange('rd',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 2
    # [(b'a1', "b'9'"), (b'b2', "b'11'")]
[/code]



**zunionstore(dest, keys, aggregate=None)
获取两个有序集合的并集，如果遇到相同值不同分数，则按照aggregate进行操作添加到新的有序集合**  
 **aggregate的值为: sum(相加和),min(最小),max(最大)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c3',3, 'n4',4, 'n5',5)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    r.zadd('rdi2','a1',8, 'b2',9, 'c10',10, 'n11',11, 'n12',12)
    
    f = r.zunionstore('rd',['rdi1','rdi2'],aggregate=None)                 #获取两个有序集合的并集，如果遇到相同值不同分数，则按照aggregate进行操作添加到新的有序集合
    print(f)
    
    n = r.zrange('rd',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 8
    # [(b'c3', "b'3'"), (b'n4', "b'4'"), (b'n5', "b'5'"), (b'a1', "b'9'"), (b'c10', "b'10'"), (b'b2', "b'11'")]
[/code]



**zscan(name, cursor=0, match=None, count=None, score_cast_func=float)
增量式迭代获取，对于数据大的数据非常有用，并非一次性将数据全部获取完，从而防止内存被撑爆【推荐使用下面的方法】**

**name，redis的name**  
 **cursor，游标（基于游标分批取获取数据）**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**  
 **score_cast_func，用来对分数进行数据转换操作的函数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    cursor1, data1 = r.zscan('rdi1',cursor=0,match='*1',count=None,score_cast_func=str)     #获取name对应的有序列表值，以1结尾的元素
    print(cursor1, data1)
    cursor2, data2 = r.zscan('rdi1',cursor=cursor1,match='*1',count=None,score_cast_func=str)
    print(cursor2, data2)
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # 0 [(b'a1', "b'1'"), (b'c1', "b'3'")]
    # 0 [(b'a1', "b'1'"), (b'c1', "b'3'")]
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'c3', "b'31'"), (b'n5', "b'51'")]
[/code]







**zscan_iter(name, match=None, count=None,score_cast_func=float)
增量式迭代获取，对于数据大的数据非常有用，并非一次性将数据全部获取完，从而防止内存被撑爆【推荐】**



**name，redis的name**  
 **match，匹配指定key，默认None 表示所有的key**  
 **count，每次分片最少获取个数，默认None表示采用Redis的默认分片个数**  
 **score_cast_func，用来对分数进行数据转换操作的函数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.zadd('rdi1','a1',1, 'b2',2, 'c1',3, 'n4',4, 'n5',51)           #zadd(name, *args, **kwargs)在name对应的有序集合中添加元素
    
    cur = r.zscan_iter('rdi1',match='*1',count=None,score_cast_func=str)     #获取name对应的有序列表值，以1结尾的元素
    for i in cur:
        print(i)
    
    
    n = r.zrange('rdi1',0, 5, desc=False, withscores=True, score_cast_func=str)  #按照索引范围获取name对应的有序集合的元素
    print(n)
    #返回
    # (b'a1', "b'1'")
    # (b'c1', "b'3'")
    # [(b'a1', "b'1'"), (b'b2', "b'2'"), (b'c1', "b'3'"), (b'n4', "b'4'"), (b'c3', "b'31'"), (b'n5', "b'51'")]
[/code]



