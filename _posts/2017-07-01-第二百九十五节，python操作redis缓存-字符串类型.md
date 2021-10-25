---
layout: post
title: " 第二百九十五节，python操作redis缓存-字符串类型 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**python操作redis缓存-字符串类型**

**首先要安装redis-py模块**



**python连接 **redis方式，有两种连接方式，一种是直接连接，一张是通过连接池连接****

****注意：以后我们都用的连接池方式连接，直接连接不推荐****

****1、 ** **直接连接方式：【不推荐】********

**Redis()配置连接信息**  
 **set()写入数据**  
 **get()读取数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis        #导入操作redis模块
    
    r = redis.Redis(host='127.0.0.1', port=6379)    #配置连接信息
    r.set('foo', 'asdvc344')                        #写入数据
    hc = r.get('foo')                               #读取数据
    print(hc)
[/code]

**2、连接池连接方式【推荐】**

**redis-py使用connection pool来管理对一个redis
server的所有连接，避免每次建立、释放连接的开销。默认，每个Redis实例都会维护一个自己的连接池。可以直接建立一个连接池，然后作为参数Redis，这样就可以实现多个Redis实例共享一个连接池。**

**ConnectionPool()配置连接池连接信息**  
 **Redis()连接连接池**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('foo', 'Bar1111111111')                               #写入数据
    r.get('foo')                                                #获取数据
[/code]





**字符串数据类型操作**

**String字符串类型操作，redis中的String在在内存中按照一个name对应一个value来存储。如图：**

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170701214418821-422753432.png)

**set(name, value, ex=None, px=None, nx=False, xx=False) 写入数据参数**

[code]

    在Redis中设置值，默认，不存在则创建，存在则修改
    参数：
         ex，过期时间（秒）
         px，过期时间（毫秒）
         nx，如果设置为True，则只有name不存在时，当前set操作才执行，用于创建
         xx，如果设置为True，则只有name存在时，当前set操作才执行，用于修改
[/code]

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('foo', 'Bar',ex=20)                                   #写入数据
    hc = r.get('foo')                                           #获取数据
    print(hc)
[/code]



**setnx(name, value) 只有name不存在时，执行设置操作（添加）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.setnx('foo', 'Bar22')                                   #写入数据setnx(name, value)只有name不存在时，执行设置操作（添加）
    hc = r.get('foo')                                           #获取数据
    print(hc)
[/code]



**setex(name, value, time) 设置值，参数：time，过期时间（数字秒 或 timedelta对象）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.setex('foo', 'Bar22',5)                                     #setex(name, value, time)设置值，参数：time，过期时间（数字秒 或 timedelta对象）
    hc = r.get('foo')                                           #获取数据
    print(hc)
[/code]



**psetex(name, time_ms, value) 设置值，参数：time_ms，过期时间（数字毫秒 或 timedelta对象）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.psetex('foo',5, 'Bar22')                                   #psetex(name, time_ms, value)设置值，参数：time_ms，过期时间（数字毫秒 或 timedelta对象）
    hc = r.get('foo')                                           #获取数据
    print(hc)
[/code]



**mset(*args, **kwargs) 批量设置**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.mset(k1='v1', k2='v2')                                    #mset(*args, **kwargs)批量设置
    #或者
    r.mset({'k3': 'v1', 'k4': 'v2'})
[/code]



**mget(keys, *args) 批量获取**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.mset(k1='v1', k2='v2')                                    #mset(*args, **kwargs)批量设置
    #或者
    r.mset({'k3': 'v3', 'k4': 'v4'})
    
    #mget(keys, *args)批量获取
    a = r.mget('k1', 'k2')
    #或者
    b = r.mget(['k3', 'k4'])
    print(a,b)
    #返回：[b'v1', b'v2'] [b'v3', b'v4']
[/code]



**getset(name, value) 设置新值并获取原来的值**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','v1')                                            #添加
    a = r.get('k1')                                             #获取
    print(a)
    
    #getset(name, value)设置新值并获取原来的值
    b = r.getset('k1','v222')
    print(b)
[/code]



**getrange(name, start, end) 获取指定名称的字符串里指定范围的字符**  
 **name,要获取的名称**  
 **start,要获取的字符串起始位置(字节)**  
 **end要获取的字符串结束位置(字节)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','afadfnanr')                                     #添加
    a = r.getrange('k1',2,5)                                        #getrange(name, start, end)获取指定名称的字符串里指定范围的字符
    print(a)
    #返回：adfn
[/code]



**setrange(name, offset, value) 从指定字符串索引开始向后替换（新值太长时，则向后添加）**  
 **offset，字符串的索引，字节（一个汉字三个字节）**  
 **value，要设置的值**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','afadfnanr')                                     #添加
    r.setrange('k1',2,'111')                                    #setrange(name, offset, value)从指定字符串索引开始向后替换（新值太长时，则向后添加）
    a = r.get('k1')
    print(a)
    #返回：af111nanr
[/code]



**setbit('name', 7, 1) ，将指定名称里的内容转换成0和1表示的二进制，在从二进制指定的位置替换成指定的值，要替换的值只能是0或者1
**

**字符串转换成二进制**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','foo')                                     #添加
    a = r.get('k1')                                       #获取内容
    print(a)                                              #得到字节类型
    
    c = str(a,encoding='utf-8')                           #将字节转换成字符串
    print(c)                                              #得到字符串类型
    
    for i in c:                                           #循环字符串
        num = ord(i)                                      #将循环到的字符串，转换成十进制
        print(bin(num).replace('b', ''))                  #将十进制转换成二进制，返回的二进制里有个b，表示二进制的意思，将b替换成空
    
    #那么字符串，foo，的二进制表示就是01100110 01101111 01101111
    
    r.setbit('k1',7,1)                                    #setbit('name', 7, 1)，将指定名称里的内容转换成0和1表示的二进制，在从二进制指定的位置替换成指定的值，要替换的值只能是0或者1
    e = r.get('k1')
    print(e)
    
    f = str(e,encoding='utf-8')
    print(f)
    for i in f:
        num = ord(i)
        print(bin(num).replace('b', ''))
    
    
    #转换过程
    # b'foo'
    # foo
    # 01100110
    # 01101111
    # 01101111
    # b'goo'
    # goo
    # 01100111
    # 01101111
    # 01101111
    
    #原始数据：foo 二进制表示：01100110 01101111 01101111
    #通过setbit('k1',7,1)：用1替换了二进制表示的第7个位置
    #替换后变成：goo 二进制表示：01100111 01101111 01101111
[/code]



**getbit(name, offset) 将指定名称的内容，转换成0和1表示的二进制，获取二进制里指定位置的二进制表示**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','foo')                                           #添加
    a = r.getbit('k1',7)                                        #将指定名称的内容，转换成0和1表示的二进制，获取二进制里指定位置的二进制表示
    print(a) 
[/code]



**bitcount(name, start, end) 将指定名称的内容，转换成二进制位表示，然后计算出1表示的个数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','foo')                                           #添加
    a = r.bitcount('k1',0,7)                                    #将指定名称的内容，转换成0和1表示的二进制，获取二进制里指定位置的二进制表示
    print(a)                                                    #bitcount(name, start, end)将指定名称的内容，转换成二进制位表示，然后计算出1表示的个数
    #返回：16
    
    #二进制表示
    # 01100110
    # 01101111
    # 01101111
[/code]



**bitop(operation, dest, *keys)
获取Redis中n1,n2,n3对应的值，然后将所有的值做二进制位运算（求并集），然后将结果保存 new_name 对应的值中**  
 **operation,AND（并） 、 OR（或） 、 NOT（非） 、 XOR（异或）**  
 **dest, 新的Redis的name**  
 ***keys,要查找的Redis的name**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','234')                                           #添加
    r.set('k2','567')                                           #添加
    r.set('k3','89')                                            #添加
    
    
    r.bitop("AND", 'new_name', 'k1', 'k2', 'k3')                #bitop(operation, dest, *keys)获取Redis中n1,n2,n3对应的值，然后将所有的值做二进制位运算（求并集），然后将结果保存 new_name 对应的值中
    
    d = r.get('new_name')
    print(d)
[/code]



**strlen(name) 返回name对应值的字节长度（一个汉字3个字节）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                       #连接连接池
    r.set('k1','林贵秀')                                        #添加
    
    d = r.strlen('k1')                                              #strlen(name)返回name对应值的字节长度（一个汉字3个字节）
    
    print(d)
    #返回9
[/code]



**incr(self, name, amount=1) 必须整数自增，自增
name对应的值，当name不存在时，则创建name＝amount，否则，则自增。**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                      #连接连接池
    r.set('k1','1')                                             #添加
    
    d = r.incr('k1',amount=1)                                  #incr(self, name, amount=1)整数自增，自增 name对应的值，当name不存在时，则创建name＝amount，否则，则自增。
    
    print(d)
[/code]



**incrbyfloat(self, name, amount=1.0) 浮点数自增，整数自增负数自减
name对应的值，当name不存在时，则创建name＝amount，否则，则自增。**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                      #连接连接池
    r.set('k1','2')                                          #添加
    
    d = r.incrbyfloat('k1',amount=1.5)                       #incrbyfloat(self, name, amount=1.0)浮点数自增，整数自增负数自减 name对应的值，当name不存在时，则创建name＝amount，否则，则自增。
    
    print(d)
    #返回：3.5
[/code]



**decr(self, name, amount=1) 整数自减 name对应的值，当name不存在时，则创建name＝amount，否则，则自减。**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                      #连接连接池
    r.set('k1','2')                                          #添加
    
    d = r.decr('k1',amount=1)                                #decr(self, name, amount=1)整数自减 name对应的值，当name不存在时，则创建name＝amount，否则，则自减。
    
    print(d)
    #返回：1
[/code]



**append(name, value) 在redis name对应的值后面追加内容**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import redis                #导入操作redis模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                      #连接连接池
    r.set('k1','2')                                          #添加
    
    r.append('k1','22')                                      #append(name, value)在redis name对应的值后面追加内容
    
    d = r.get('k1')
    print(d)
    #返回：222
[/code]



**利用字符串方式缓存网页应用**

****Tornado框架****

**write()方法：web.py文件里的write()方法，接收字符串显示给用户**

**使用的Tornado框架，但是
**Tornado框架在将html转换成字符串显示给用户后，就删除了，所以我们需要修改一下源码，添加一个字段保存一下html字符串接，
在web.py文件里的write()方法里修改源码，添加一个字段self._response_html = chunk
保存html文件转换的字符串，这样我们方便得到html转换的字符串****

********在web.py文件里的write()方法里修改源码********

********![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170703115705331-709820641.png)********



********封装一个缓存处理模块********

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import redis                #导入操作redis缓存模块
    
    pool = redis.ConnectionPool(host='127.0.0.1', port=6379)  #配置连接池连接信息
    
    r = redis.Redis(connection_pool=pool)                      #连接连接池
    
    
    class huancuen:
        """
        处理缓存对象
        """
        def __init__(self,_self,name):
            """
            self._self  接收创建对象时传进来的对象
            self.name   接收创建对象时传进来的缓存名称
            self.shi_jian   设置缓存有效时间，（秒）
            """
            self._self = _self
            self.name = name
            self.shi_jian = 10
    
    
        def hc_get(self):
            """
            hc_get()方法：无参，返回缓存内容
            根据创建对象时传进来的缓存名称，到缓存里获取到对应名称的缓存
            判断此缓存如果存在，就读取缓存显示给用户
            """
            html = r.get(self.name)
            if html:
                self._self.write(html)
            return html
    
    
        def hc_set(self):
            """
            r.set()方法：无参，无返回
            获取到用户请求的html字符串，将htnl字符串作为值，创建对象时传入的缓存名称作为名称，写入缓存
            缓存有效时间，是对象里的self.shi_jian字段值
            """
            r.set(self.name,self._self._response_html,ex=self.shi_jian)
[/code]

**逻辑处理调用**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import time
    import huanc
    
    
    #逻辑处理
    class MainHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                  #get()方法，接收get方式请求
            shjan = time.time()
    
            hc = huanc.huancuen(self,'index')           #创建缓存对象
            if hc.hc_get():                             #获取缓存展现给用户，会返回一个htnl字符串，判断字符串存在说明缓存存在
                return                                  #返回不执行下面代码
            self.render("index.html",shjan = shjan)     #显示cshi.html文件,将shjan变量传到模板语言里渲染
            hc.hc_set()                                 #将html字符串写入缓存
            self.write()
    
    
    
    class DluHandler(tornado.web.RequestHandler):
        def get(self, *args, **kwargs):
            shjan = time.time()
    
            hc = huanc.huancuen(self,'dlu')
            if hc.hc_get():
                return
            self.render("dlu.html", shjan=shjan)
            hc.hc_set()
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"views",                 #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                     #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", MainHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", DluHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]



