---
layout: post
title: " 第五十五节，IO多路复用select模块加socket模块，伪多线并发 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**IO多路复用select模块加socket模块，伪多线并发，并不是真正的多线程并发，实际通过循环等待还是一个一个处理的**

**IO多路复用，lo就是文件或数据的输入输出， **IO多路复用就是可以多用户操作****

******IO多路复用，** 可以监听多个文件描述符（socke对象）（文件句柄），一旦文件句柄出现变化，即可感知到，感知到后作出相应操作****



****比如原生 ** **socke模块只能监听一个端口和只能一个用户连接，要想实现监听多个端口和支持多用户，就会使用
**IO多路复用**********



**IO多路复用select模块**

**********select()自动监听socket对象的客户端，连接地址和、客户端通讯地址，四个参数**********

select()自动监听列表里的socket对象（文件描述符），一旦监听的对象，谁发生了变化（有用户请求），  
就将发生变化对象的客户端连接地址赋值给第一个变量a，第一个变量接收的列表，列表里的每一个元素，就是一个端口的用户连接地址  
如果是多个端口在同时连接客户端，那么列表元素就是多个元素

最多监听端口1024个

**********使用方法：a, b, c = select.select(列表类型的 ** **socke对象变化**** ,
[可选：传参直接赋值给第二个变量], [可选： ** ** ** ** ** ** ** ** ** **列表类型的 **
**socke对象监听错误************************ ], 多少秒检测一次)**********

********** 需要四个参数 **********

**********参数一： ** ** ** ** **列表类型的 ** **socke对象，监听变化************************

**********参数二： ** ** ** ** **传参直接赋值给第二个变量********************

**********参数三： ** ** ** ** ** ** ** ** ** ** ** ** ** ** **列表类型的 **
**socke对象，监听错误********************************************

**********参数四： ** ** ** ** **多少秒检测一次********************

******************** 需要三个变量来接收返回值********************

******************** 第一个变量接收的：列表类型客户端连接地址，如果无客户端连接则为空列表********************

****************************************第二个变量接收的：第二个参数的值****************************************

****************************************第三个变量接收的：第三个参数监听 ** ** ** ** ** ** **
** ** ** ** ** ** ** ** ** ** ** ** ** **
**socke对象的错误信息,返回列表，无错误则为空列表********************************************  
****************************************

**********格式：a, b, c = select.select(lib, [], [], 1)**********

********************格式2：a, b, c = select.select(lib, k1, ** ** ** ** ** ** **
** ** **lib******************** , 1)********************

************IO多路复用** 多端口监听客户端连接地址、服务端代码**********

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """服务端"""
    import socket #导入模块
    """设置多个对象，绑定不同端口"""
    k1 = socket.socket() #创建对象
    k1.bind(('127.0.0.1', 9991)) #绑定服务端IP和端口
    k1.listen() #监听IP和端口
    
    k2 = socket.socket() #创建对象
    k2.bind(('127.0.0.1', 9992)) #绑定服务端IP和端口
    k2.listen() #监听IP和端口
    
    k3 = socket.socket() #创建对象
    k3.bind(('127.0.0.1', 9993)) #绑定服务端IP和端口
    k3.listen() #监听IP和端口
    """将多个对象组合成列表"""
    lib = [k1, k2, k3]
    
    """使用自动监听模块"""
    import select #导入自动监听多个端口模块
    while True:
        #select()自动监听列表里的socket对象（文件描述符），一旦监听的对象，谁发生了变化（有用户请求），
        # 就将发生变化对象的客户端连接地址赋值给第一个变量a，第一个变量接收的列表，列表里的每一个元素，就是一个端口的用户连接地址
        #如果是多个端口在同时连接客户端，那么列表元素就是多个元素
        a, b, c = select.select(lib, [], [], 1)
        for k in a: #循环出select()获取到的列表类型客户端连接地址
            d, e = k.accept() #将循环到的每一个客户端连接地址等待通讯，阻塞
            d.sendall(bytes("欢迎访问", encoding="utf-8")) #向连接的客户端发送一条消息
[/code]

**客户端代码1**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9991,))#连接服务端，在客户端绑定服务端IP和端口
    
    f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
    f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
    print(f2) #打印出服务端发来的信息
[/code]

**客户端代码2**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9992,))#连接服务端，在客户端绑定服务端IP和端口
    
    f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
    f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
    print(f2) #打印出服务端发来的信息
[/code]

**IO多路复用 ** ** ** ** **多端口监听、客户端连接地址原理图************

************![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160928190658813-1825178017.png)************



**IO多路复用监听客户端多通讯地址**

**通过select()监听到客户端变化信息对象，拿到变化信息对象，判断是连接信息对象，还是通讯信息对象？如果是连接信息对象，通过变化信息对象获取到此连接的通讯对象，将通讯对象添加到
**select()里监听，如果是通讯对象，通过通讯对象进行信息交互****

******IO多路复用监听客户端多通讯地址服务端代码******

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """服务端"""
    import socket #导入模块
    k1 = socket.socket() #创建对象
    k1.bind(('127.0.0.1', 9991)) #绑定服务端IP和端口
    k1.listen() #监听IP和端口
    lib = [k1]
    
    """使用自动监听模块"""
    import select #导入自动监听多个端口模块
    while True:
        #select()自动监听列表里的socket对象（文件描述符），一旦监听的对象，谁发生了变化（有用户请求），
        # 就将发生变化对象的客户端连接地址赋值给第一个变量a，第一个变量接收的列表，列表里的每一个元素，就是一个端口的用户连接地址
        #如果是多个端口在同时连接客户端，那么列表元素就是多个元素
        a, b, c = select.select(lib, [], [], 1)
        print("正在监听的socket对象 %d" % len(lib)) #监听的对象有多少个
        print(a) #监听发生变化的有哪些
        for k in a: #循环出select()获取到的列表类型客户端连接地址
            if k == k1: #判断循环到的连接地址等于socket对象，说明有新用户连接
                d, e = k.accept() #等待请求，获取客户端通讯地址
                lib.append(d) #将客户端通讯地址追加到列表，传入select()监听通讯变化
                d.sendall(bytes("你好", encoding="utf-8"))
            else: #如果不是连接信息，说明是通讯信息
                try: #监控代码是否出现异常，如果客户端关闭了就会出现异常，没出现异常执行里面的代码
                    fd = k.recv(1024)
                    f = str(fd, encoding="utf-8")
                    g = f + "好"
                    k.sendall(bytes(g, encoding="utf-8"))
                except Exception as ex: #出现异常将当前通讯对象移除列表，select不在监听
                    lib.remove(k)
[/code]

**客户端代码**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9991,))#连接服务端，在客户端绑定服务端IP和端口
    while True:
        f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
        f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
        print(f2) #打印出服务端发来的信息
        a = input("输入要发送的信息")
        z.sendall(bytes(a, encoding="utf-8"))
[/code]

  **IO多路复用监听客户端多通讯原理图**

**![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160929110227610-1523795347.png)**



**IO多路复用,有三种方式(select)、(poll)、(epoll) select和poll其实都是调用计算机底层来实现的监听处理，
**epoll** 是异步处理的是文件描述符发生变化后主动告诉 **epoll** 的，这里我们需要知道一下**

**注意：wds系统只支持 **select模块，****





**利用select()的第二个参数，实现IO多路复用，服务端读写分离**  
 **也就是读和写分开，在不同的代码块**



**服务端读写分离代码**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """服务端实现读写分离"""
    import socket #导入模块
    k1 = socket.socket() #创建对象
    k1.bind(('127.0.0.1', 9991)) #绑定服务端IP和端口
    k1.listen() #监听IP和端口
    
    lib = [k1] #监听的客户连接地址或，客户通讯地址,传给select第一个参数
    lib2 = [] #接收客户端通讯地址，传给select第二个参数
    jilu = {} #接收字典，里面是客户端发通讯内容的用户通讯地址(键)和通讯内容(值)
    
    """使用自动监听模块"""
    import select #导入自动监听多个端口模块
    while True:
        #select()自动监听列表里的socket对象（文件描述符），一旦监听的对象，谁发生了变化（有用户请求），
        # 就将发生变化对象的客户端连接地址赋值给第一个变量a，第一个变量接收的列表，列表里的每一个元素，就是一个端口的用户连接地址
        #如果是多个端口在同时连接客户端，那么列表元素就是多个元素
        a, b, c = select.select(lib, lib2, lib, 1)
        print("正在监听的socket对象 %d" % len(lib)) #监听的对象有多少个
        print(a) #监听发生变化的有哪些
        """循环判断链接地址或通讯地址，获取客户端通讯信息以及内容"""
        for k in a: #循环出select()获取到的列表类型客户端连接地址
            if k == k1: #判断循环到的连接地址等于socket对象，说明有新用户连接
                d, e = k.accept() #等待请求，获取客户端通讯地址
                lib.append(d) #将客户端通讯地址追加到列表，传入select()监听通讯变化
                jilu[d] = [] #将连接用户通讯地址添加到字典为键，值为空列表
            else: #如果不是连接信息，说明是通讯信息
                try: #监控代码是否异常
                    fd = k.recv(1024) #获取客户端发的信息
                except Exception as e: #如果异常将此通讯地址移除列表，停止监听
                    lib.remove(k) #通讯地址移除列表
                else:
                    fd2 = str(fd, encoding="utf-8") #接收客户端发的信息转换成字符串
                    jilu[k].append(fd2) # 将客户端转换的字符串追加到，字典里当前客户键的，列表里为值
                    lib2.append(k) #将当前客户通讯地址，添加到select第二个参数列表里
        """向客户端发信息"""
        for km in b: #循环select第二个参数列表里的通讯用户
            jkd = jilu[km][0] #通过通讯用户拿到字典里对应的通讯内容
            del jilu[km][0] #拿到通讯内容后删除通讯内容
            km.sendall(bytes(jkd+"好", encoding="utf-8")) #将通讯内容加个好字，在发给客户端
            lib2.remove(km ) #在通讯列表移除当前通讯地址
    
        for fh in c: #如果监听连接出现异常
            lib.remove(fh) #移除当前连接
[/code]

**客户端代码**



[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9991,))#连接服务端，在客户端绑定服务端IP和端口
    while True:
        a = input("输入要发送的信息")
        z.sendall(bytes(a, encoding="utf-8"))
        f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
        f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
        print(f2) #打印出服务端发来的信息
[/code]

  **IO多路复用，服务端读写分离原理图**

**![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160930164848625-2047340885.png)**

