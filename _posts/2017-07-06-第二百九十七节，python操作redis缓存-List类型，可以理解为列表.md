---
layout: post
title: " 第二百九十七节，python操作redis缓存-List类型，可以理解为列表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**python操作redis缓存-List类型，可以理解为列表， 是可以有重复元素的列表**



**List操作，redis中的List在在内存中按照一个name对应一个List来存储。如图：**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170706113531706-1955793302.png)**







**lpush(name,values) 在name对应的list中添加元素，每个新的元素都添加到列表的最左边**  
 **如：**  
 **lpush('adc8868', 11,22,33)**  
 **保存顺序为:[ 33,22,11]**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.lpush('adc8868',11,22,33)                                     #lpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最左边
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'33', b'22', b'11']
[/code]



**rpush(name,values) 在name对应的list中添加元素，每个新的元素都添加到列表的最右边**  
 **如：**  
 **rpush('adc8868', 11,22,33)**  
 **保存顺序为:[ 11,22,33]**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'11', b'22', b'33']
[/code]



**lpushx(name,value) 在name对应的list中添加元素，只有name已经存在时，值添加到列表的最左边**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    r.lpushx('adc8868',44)                                          #lpushx(name,value)在name对应的list中添加元素，只有name已经存在时，值添加到列表的最左边
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'44', b'11', b'22', b'33']
[/code]



**rpushx(name, value) 在name对应的list中添加元素，只有name已经存在时，值添加到列表的最右边**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    r.rpushx('adc8868',44)                                          #rpushx(name, value)在name对应的list中添加元素，只有name已经存在时，值添加到列表的最右边
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    #[b'11', b'22', b'33', b'44']
[/code]



**llen(name) name对应的list元素的个数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.llen('adc8868'))                                        #llen(name)name对应的list元素的个数
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # 3
    # [b'11', b'22', b'33']
[/code]



**linsert(name, where, refvalue, value)) 在name对应的列表的某一个值前或后插入一个新值**  
 **参数：**  
 **name，redis的name**  
 **where，BEFORE或AFTER，BEFORE(前)或AFTER(后)**  
 **refvalue，标杆值，即：在那个元素值前后插入数据**  
 **value，要插入的数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                            #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    r.linsert('adc8868','BEFORE',22,44)                              #linsert(name, where, refvalue, value))在name对应的列表的某一个值前或后插入一个新值
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'11', b'44', b'22', b'33']
[/code]



**lset(name, index, value) 对name对应的list中的某一个索引位置重新赋值**  
 **参数：**  
 **name，redis的name**  
 **index，list的索引位置**  
 **value，要设置的值**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    r.lset('adc8868',1,55)                                          #lset(name, index, value)对name对应的list中的某一个索引位置重新赋值
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    #[b'11', b'55', b'33']
[/code]



**lrem(name, value, num) 在name对应的list中删除指定的值**  
 **参数：**  
 **name，redis的name**  
 **value，要删除的值**  
 **num， num=0，删除列表中所有的指定值；**  
 **     num=2,从前到后，删除2个；**  
 **     num=-2,从后向前，删除2个**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    r.lrem('adc8868',22,num=0)                                      #lrem(name, value, num)在name对应的list中删除指定的值
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    #[b'11', b'33']
[/code]



**lpop(name) 在name对应的列表的左侧获取第一个元素并在列表中移除，返回值则是第一个元素**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.lpop('adc8868'))                                        #lpop(name)在name对应的列表的左侧获取第一个元素并在列表中移除，返回值则是第一个元素
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # b'11'
    # [b'22', b'33']
[/code]



**rpop(name) 在name对应的列表的右侧获取第一个元素并在列表中移除，返回值则是第一个元素**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.rpop('adc8868'))                                        #rpop(name)在name对应的列表的右侧获取第一个元素并在列表中移除，返回值则是第一个元素
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # b'33'
    # [b'11', b'22']
[/code]



**lindex(name, index) 在name对应的列表中根据索引获取列表元素**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.lindex('adc8868',2))                                    #lindex(name, index)在name对应的列表中根据索引获取列表元素
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # b'33'
    # [b'11', b'22', b'33']
[/code]



**lrange(name, start, end) 在name对应的列表分片获取数据**  
 **参数：**  
 **name，redis的name**  
 **start，索引的起始位置**  
 **end，索引结束位置**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.lrange('adc8868',0,1))                                  #lrange(name, start, end)在name对应的列表分片获取数据
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'11', b'22']
    # [b'11', b'22', b'33']
[/code]



**ltrim(name, start, end) 在name对应的列表中移除没有在start-end索引之间的值**  
 **参数：**  
 **name，redis的name**  
 **start，索引的起始位置**  
 **end，索引结束位置**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.ltrim('adc8868',0,1))                                   #ltrim(name, start, end)在name对应的列表中移除没有在start-end索引之间的值
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # True
    # [b'11', b'22']
[/code]



**rpoplpush(src, dst) 从一个列表取出最右边的元素，同时将其添加至另一个列表的最左边**  
 **参数：**  
 **src，要取数据的列表的name**  
 **dst，要添加数据的列表的name**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8868',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    print(r.rpoplpush('adc8868','adc'))                             #rpoplpush(src, dst)从一个列表取出最右边的元素，同时将其添加至另一个列表的最左边
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8868'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # b'33'
    # [b'11', b'22']
[/code]



**自定义增量迭代**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                           #连接连接池
    r.rpush('adc8861',11,22,33)                                     #rpush(name,values)在name对应的list中添加元素，每个新的元素都添加到列表的最右边
    
    
    
    #由于redis类库中没有提供对列表元素的增量迭代，如果想要循环name对应的列表的所有元素，那么就需要自定义迭代器：
    liebiao = []
    def list_iter(name):
        """
        自定义redis列表增量迭代
        :param name: redis中的name，即：迭代name对应的列表
        :return: yield 返回 列表元素
        """
        list_count = r.llen(name)
        for index in range(list_count):
            yield r.lindex(name, index)
    # 使用
    for item in list_iter('adc8861'):
        liebiao.append(item)
    print(liebiao)
    
    #返回
    # [b'11', b'22', b'33']
[/code]



