---
layout: post
title: " 第二百九十三，Memcached缓存 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Memcached
是一个高性能的分布式内存对象缓存系统，用于动态Web应用以减轻数据库负载。它通过在内存中缓存数据和对象来减少读取数据库的次数，从而提高动态、数据库驱动网站的速度。Memcached基于一个存储键/值对的hashmap。其守护进程（daemon
）是用C写的，但是客户端可以用任何语言来编写，并通过memcached协议与守护进程通信。**

  **Memcached只能接受键值对方式的字符串**

**Memcached安装和基本使用**

**Window下memcached安装与测试步骤**

**下载好软件包memcached-1.4.20版本**

**安装步骤**  
 **1、解压到指定目录，如：E:\memcached**  
 **2、用cmd打开命令窗口，转到解压的目录，输入 “ memcached -d install”如下图：**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170629202523914-445613740.png)**



**查看是否安装成功，输入 memcached –h，出现下图窗口说明已经安装成功。**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170629202644508-224311336.png)

**默认命令说明**  
 **-p 监听的端口**  
 **-l 连接的IP地址, 默认是本机**  
 **-d start 启动memcached服务**  
 **-d restart 重起memcached服务**  
 **-d stop|shutdown 关闭正在运行的memcached服务**  
 **-d install 安装memcached服务**  
 **-d uninstall 卸载memcached服**  
 **-u 以的身份运行 (仅在以root运行的时候有效**  
 **-m 最大内存使用，单位MB。默认64M**  
 **-M 内存耗尽时返回错误，而不是删除**  
 **-c 最大同时连接数，默认是102**  
 **-f 块大小增长因子，默认是1.2**  
 **-n 最小分配空间，key+value+flags默认是4**  
 **-h 显示帮助**



**linux安装 **memcached****

[code]

    wget http: //memcached.org/latest
    tar -zxvf memcached-1.x.x.tar.gz
    cd memcached-1.x.x
    ./configure && make && make test && sudo make install
     
    PS：依赖libevent
           yum install libevent-devel
           apt-get install libevent-dev
[/code]

**Memcached命令**

[code]

    存储命令:  set/add/replace/append/prepend/cas
    获取命令: get/gets
    其他命令: delete/stats..
[/code]



**Python操作Memcached**

**安装API模块python-memcached**

****python-memcached属于第三方模块需要安装****

**安装好后，在命令终端启动 **memcached并且配置 **python-memcached连接参数ip端口连接数内存大小等信息******

[code]

    **memcached -d -m 10    -u root -l 127.0.0.1 -p 12000 -c 256 -P /tmp/** **memcached.pid**     #配置连接
    memcached  -d -m 10    -u root -l 服务器ip -p 端口 -c 256 -P /tmp/memcached.pid     　　#配置连接说明
     
    参数说明:
        -d 是启动一个守护进程
        -m 是分配给Memcache使用的内存数量，单位是MB
        -u 是运行Memcache的用户
        -l 是监听的服务器IP地址
        -p 是设置Memcache监听的端口,最好是1024以上的端口
        -c 选项是最大运行的并发连接数，默认是1024，按照你服务器的负载量来设定
        -P 是设置保存Memcache的pid文件
[/code]



**第一次操作**

**Client([ip:端口]) 创建memcache对象，配置连接memcache信息**

**set() 通过memcache向内存写入键值对，字符串，可以设置超时时间**  
 **使用方式： memcache对象.set("键","值")**

**get() 通过memcache在内存里读取写入的键值对**  
 **使用方式： memcache对象.get('键')**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import memcache             #导入操作memcached软件控制模块
    
    mc = memcache.Client(['127.0.0.1:12000'], debug=True)  #debug = True 表示运行出现错误时，显示错误信息，上线后移除该参数。
    mc.set("foo", "bar3333",5)      #第三个参数可以设置超时时间，单位为秒，也就是5秒后内存会自动删除
    ret = mc.get('foo')
    print(ret)
    #输出：bar3333
[/code]



**天生支持集群**

**python-memcached模块原生支持集群操作，其原理是在内存维护一个主机列表，且集群中主机的权重值和主机在列表中重复出现的次数成正比**

**集群**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import memcache             #导入操作memcached软件控制模块
    #假如连接4台服务器集群
    mc = memcache.Client(['127.0.0.1:12000',
                          '127.0.0.1:12001',
                          '127.0.0.1:12002',
                          '127.0.0.1:12004'], debug=True)
    mc.set("foo", "bar3333",5)      #向服务器内存写入键值对数据，集群会通过算法确定写入那台服务器，如下说明
    #memcache模块会通过里面的cmemcache_hash方法将要写入内存的数据foo键二进制转换成数字
    #然后将转换的数字除以集群服务器列表数，得到的余数如果是2就将数据写入集群第二台服务器中，以此类推
    ret = mc.get('foo')  #当获取数据时同样通过算法到对应的服务器读取数据
[/code]

**集群权重**

****集群权重就是在集群的服务器，将一台或者多台服务器提高权重，使其被算法多次匹配，就可以多放数据****

****简单理解就是，提高指定服务器在配置列表的次数，出现次数越多算法匹配就越多，这样数据也就放的越多****

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import memcache             #导入操作memcached软件控制模块
    #假如连接4台服务器集群
    mc = memcache.Client([('127.0.0.1:12000',3),   #表示此服务器在列表出现3次，提高权重运算匹配几率
                          ('127.0.0.1:12001',2),   #表示此服务器在列表出现2次，提高权重运算匹配几率
                          ('127.0.0.1:12002'),
                          ('127.0.0.1:12004')], debug=True)
    mc.set("foo", "bar3333",5)      #向服务器内存写入键值对数据，集群会通过算法确定写入那台服务器，如下说明
    #memcache模块会通过里面的cmemcache_hash方法将要写入内存的数据foo键二进制转换成数字
    #然后将转换的数字除以集群服务器列表数，得到的余数如果是2就将数据写入集群第二台服务器中，以此类推
    ret = mc.get('foo')  #当获取数据时同样通过算法到对应的服务器读取数据
[/code]

** **

**add()添加一条键值对，如果已经存在的 key，重复执行add操作异常**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
    mc.add('k1', 'v1')
    # mc.add('k1', 'v2') # 报错，对已经存在的key重复添加，失败！！！
[/code]



**replace()修改某个key的值，如果key不存在，则异常**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
    # 如果memcache中存在kkkk，则替换成功，否则一场
    mc.replace('kkkk','999')
[/code]



**set() 和 set_multi()**  
 **set()设置一个键值对，如果key不存在，则创建，如果key存在，则修改**  
 **set_multi()设置多个键值对，如果key不存在，则创建，如果key存在，则修改**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
     
    mc.set('key0', 'wupeiqi')
     
    mc.set_multi({'key1': 'val1', 'key2': 'val2'})
[/code]



**delete 和 delete_multi**  
 **delete()在Memcached中删除指定的一个键值对**  
 **delete_multi()在Memcached中删除指定的多个键值对**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
     
    mc.delete('key0')
    mc.delete_multi(['key1', 'key2'])
[/code]



**get 和 get_multi**  
 **get()获取一个键值对**  
 **get_multi()获取多一个键值对**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
     
    val = mc.get('key0')
    item_dict = mc.get_multi(["key1", "key2", "key3"])
[/code]



**append 和 prepend**  
 **append()修改指定key的值，在该值 后面 追加内容**  
 **prepend()修改指定key的值，在该值 前面 插入内容**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
    # k1 = "v1"
     
    mc.append('k1', 'after')
    # k1 = "v1after"
     
    mc.prepend('k1', 'before')
    # k1 = "beforev1after"
[/code]



**decr 和 incr**  
 **incr()自增，将Memcached中的某一个值增加 N （ N默认为1 ）**  
 **decr()自减，将Memcached中的某一个值减少 N （ N默认为1 ）**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import memcache
     
    mc = memcache.Client(['10.211.55.4:12000'], debug=True)
    mc.set('k1', '777')
     
    mc.incr('k1')
    # k1 = 778
     
    mc.incr('k1', 10)
    # k1 = 788
     
    mc.decr('k1')
    # k1 = 787
     
    mc.decr('k1', 10)
    # k1 = 777
[/code]



**gets()获取数据 和 cas()设置数据**  
 **如商城商品剩余个数，假设改值保存在memcache中，product_count = 900**  
 **A用户刷新页面从memcache中读取到product_count = 900**  
 **B用户刷新页面从memcache中读取到product_count = 900**

**如果A、B用户均购买商品**

**A用户修改商品剩余个数 product_count＝899**  
 **B用户修改商品剩余个数 product_count＝899**

**如此一来缓存内的数据便不在正确，两个用户购买商品后，商品剩余还是 899**  
 **如果使用python的set和get来操作以上过程，那么程序就会如上述所示情况！**

**如果想要避免此情况的发生，只要使用 gets 和 cas 即可，如：**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import memcache             #导入操作memcached软件控制模块
    
    mc = memcache.Client(['127.0.0.1:12000'], debug=True,cache_cas=True)  #debug = True 表示运行出现错误时，显示错误信息，上线后移除该参数。
    mc.set('product_count',100)         #设置基础数据
    v = mc.gets('product_count')        #用gets获取数据100
    
    # 如果有人在gets之后和cas之前修改了product_count，那么，下面的设置将会执行失败，剖出异常，从而避免非正常数据的产生
    # 重点：也就是说如果多个用户获取到相同数修改时，只有最先修改那个用户可以修改，后面的用户不可以修改，因为原始值已经被最先
    # 修改的用户改变了，其他用户只能重新获取修改后的数据再次修改，这样避免相同的数据被多个用户修改，保证数据的安全
    
    
    mc.cas('product_count', "899")      #cas修改数据，如果这次修改相同的值已经被其他用户修改了，那么将无法修改
    
    #注意：只有用gets()获取数据，和用cas()修改数据，两者同时用才具备此功能
    #要实现此功能在Client()的参数里，还必须加上cache_cas=True
[/code]

Ps：本质上每次执行gets时，会从memcache中获取一个自增的数字，通过cas去修改gets的值时，会携带之前获取的自增值和memcache中的自增值进行比较，如果相等，则可以提交，如果不想等，那表示在gets和cas执行之间，又有其他人执行了gets（获取了缓冲的指定值），
如此一来有可能出现非正常数据，则不允许修改。



**Memcached用途session，或者页面缓存**

