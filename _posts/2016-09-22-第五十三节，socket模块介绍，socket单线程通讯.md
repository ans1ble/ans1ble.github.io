第五十三节，socket模块介绍，socket单线程通讯

**socket单线程通讯，只能 **单线程通讯，不能并发****



**socket是基于（TCP、UDP、IP）的通讯、也叫做套接字**

**通讯过程由服务端的 **socket处理信息发送，由客户端的 **socket处理信息接收。******

socket通常也称作"套接字"，用于描述IP地址和端口，是一个通信链的句柄，应用程序通常通过"套接字"向网络发出请求或者应答网络请求。

socket起源于Unix，而Unix/Linux基本哲学之一就是"一切皆文件"，对于文件用【打开】【读写】【关闭】模式来操作。socket就是该模式的一个实现，socket即是一种特殊的文件，一些socket函数就是对其进行的操作（读/写IO、打开、关闭）

socket和file的区别：

file模块是针对某个指定文件进行【打开】【读写】【关闭】

socket模块是针对 服务器端 和 客户端Socket 进行【打开】【读写】【关闭】

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160923164547746-1000989930.png)



******socket**** 通讯过程由服务端的 **socket处理信息发送，由客户端的 **socket处理信息接收。******

******举例：******

******模拟一个服务端的 ** ** **socket  WEB服务应用************

    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import socket
    
    def handle_request(client):
        buf = client.recv(1024)
        client.sendall(bytes("HTTP/1.1 200 OK\r\n\r\n", encoding='utf-8'))
        client.sendall(bytes("Hello, World", encoding='utf-8'))
    
    def main():
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.bind(('localhost',8080))
        sock.listen(5)
    
        while True:
            connection, address = sock.accept()
            handle_request(connection)
            connection.close()
    
    if __name__ == '__main__':
      main()

**启动服务端的socket后，我们利用浏览器的 **客户** 端socket来访问这个 WEB服务应用 （当然客户端的 **socket也可以自己写的**
）**

************打开浏览器输入  http://127.0.0.1:8080/ 就可以接收到服务端 **socket输出的  Hello,
World**************



****************socket通讯有基于TCP和UDP两个通讯的， ** ** ** ** ** ** **
**TCP是需要客户端和服务端相互连接后进行通讯， ** ** ** ** ** ** ** **UDP是不需要相互连接直接由单方面发起的，使用最多的还是
** ** ** ** ** ** **
**TCP****************************************************************





**socket通讯过程**  
 **socket通讯由服务端和客户端双方完成通讯，服务端启动着等待客户端来连接，客户端从服务端的IP和指定端口进行连接通讯**



****创建** 服务端**

**socket.socket()创建socket对象，有三个可选参数**

****socket.socket(socket.AF_INET,socket.SOCK_STREAM,0)****

参数一：地址簇

socket.AF_INET IPv4（默认）  
socket.AF_INET6 IPv6

socket.AF_UNIX 只能够用于单一的Unix系统进程间通信

参数二：类型

socket.SOCK_STREAM 流式socket , for TCP （默认）  
socket.SOCK_DGRAM 数据报式socket , for UDP

socket.SOCK_RAW
原始套接字，普通的套接字无法处理ICMP、IGMP等网络报文，而SOCK_RAW可以；其次，SOCK_RAW也可以处理特殊的IPv4报文；此外，利用原始套接字，可以通过IP_HDRINCL套接字选项由用户构造IP头。  
socket.SOCK_RDM
是一种可靠的UDP形式，即保证交付数据报但不保证顺序。SOCK_RAM用来提供对原始协议的低级访问，在需要执行某些特殊操作时使用，如发送ICMP报文。SOCK_RAM通常仅限于高级用户或管理员运行的程序使用。  
socket.SOCK_SEQPACKET 可靠的连续数据包服务

参数三：协议

0 （默认）与特定的地址家族相关的协议,如果是 0 ，则系统就会根据地址格式和套接类别,自动选择一个合适的协议

**使用方法：对象变量 =   **socket.socket()****

**格式：a = socket.socket()**



**bind()在服务端设置服务端ip和端口**

**使用方法：对象变量. **bind(元祖类型的服务端IP和端口)****

**格式：a.bind(('127.0.0.1',9999))**



**listen()监听IP和端口，设置一个参数，表示最多连接排队数量**

**使用方法：对象变量. **listen(排队数)****

**格式：a.listen(5)**



**accept()等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接对象，一个是客户端的地址信息，所以需要两个变量来接收**

**注意：
**accept()是阻塞的，意思就是程序执行带这里就是等待状态，在没有客户端请求连接的情况下，下面的代码将不会执行，只有客户端请求连接时下面的代码才会被执行****

****accept()被客户端连接一次后就会被中断，可以写个while循环让它永远等待客户端连接****

**使用方法：定义连接变量,定义客户端地址信息变量 = 对象变量. **accept()****

**格式：b, c = a.accept()**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    while True: #accept()被客户端连接一次后就会被中断，写个while循环让它永远等待客户端连接
        b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收
        print(b, c) #打印出客户端连接的，连接，和客服端地址信息

**  根据以上就创建了一个等待客户端连接的socket服务端**



**创建客户端**

****connect** ()连接服务端，在客户端绑定服务端IP和端口**

**使用方法：对象变量. **socket( ** **元祖类型的服务端IP和端口**** )****

**格式：z.connect(('127.0.0.1', 9999,))**



**close()在客户端关闭连接**

**使用方法：对象变量. **close()****

**格式：z.close()**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    z.close() #在客户端关闭连接



**客户端每次连接服务端后，服务端的accept()就能获取到来自客户端的一个连接对象，和客户端地址信息，两个元素**

 客户端执行代码

    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    z.close() #在客户端关闭连接

等待接收客户端连接的服务端代码

    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    while True: #accept()被客户端连接一次后就会被中断，写个while循环让它永远等待客户端连接
        b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收
        print(b, c) #打印出客户端连接的，连接，和客服端地址信息
    
    #显示客户端的连接信息
    # <socket.socket fd=264, family=AddressFamily.AF_INET, type=SocketKind.SOCK_STREAM, proto=0, laddr=('127.0.0.1', 9999), raddr=('127.0.0.1', 58272)> ('127.0.0.1', 58272)

 客户端访问服务端流程图

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160923193007793-610704345.png)



**sendall()【推荐】服务端向客户端发信息，或者客户端向服务端发信息**

**服务端：通过 ** **accept（）接收到的客户端对象信息变量，客户端对象信息变量. **sendall( ** **
**字节方式要发送的字符串****** )********

**客户端：通过客户端的 **socket对象. **sendall( ** ** ** ** ** **
**字节方式要发送的字符串************** )******

**格式：b.sendall(bytes("欢迎你",encoding='utf-8'))**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    while True: #accept()被客户端连接一次后就会被中断，写个while循环让它永远等待客户端连接
        b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收
        b.sendall(bytes("你好欢迎你",encoding='utf-8')) #根据accept()接收到客户端连接对象信息，向客户端发送信息



**recv()【推荐】服务端接收客户端发来的信息，或者客户端接收服务端发来的信息**

**注意： **recv()也是阻塞的，也就是说 ** **等待接收信息，如果 ** ** **
**recv()没接收到信息，下面的代码就不会执行，只有接收到信息后下面的代码才会被执行****************

**服务端： **通过 ** **accept（）接收到的客户端对象信息变量，客户端对象信息变量. **recv()******** **  
****

********客户端： **通过客户端的 **socket对象. ** **recv()****************

**格式：f = z.recv(1024)**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
    f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
    print(f2) #打印出服务端发来的信息
    z.close() #在客户端关闭连接
    # 输出
    # 你好欢迎你

 客户端连接服务端，服务端向客户端发送一条信息原理图

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160923221551309-1957257147.png)





**客户端与服务端进行交互信息**

**服务端代码**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    while True: #accept()被客户端连接一次后就会被中断，写个while循环让它永远等待客户端连接
        b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收
        b.sendall(bytes("你好欢迎你",encoding='utf-8')) #根据accept()接收到客户端连接对象信息，向客户端发送信息
        while True: #当客户端连接成功后，进入循环，保持与客户端的通讯
            j = b.recv(1024)#接收客户端发来的信息
            j2 = str(j, encoding='utf-8') #将接收到的客户端信息转换成字符串
            print(j2)
            if j2 == "q": #判断客户端输入q，表示不再与服务端通讯，跳出循环，不在保持客户端的通讯
                break
            b.sendall(bytes(j2+"好",encoding='utf-8')) #将接收到客户端的信息加上一个好字，在发送给客户端

**客户端代码**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    f = z.recv(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
    f2 = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
    print(f2) #打印出服务端发来的信息
    while True: #当连接服务端成功后进入循环，保持与服务端的通讯
        a = input("请输入信息")
        z.sendall(bytes(a,encoding='utf-8')) #向服务端发送信息
        if a == "q": #判断客户端输入 q表示，不再以服务端通讯跳出循环
            break
        js = z.recv(1024) #接收服务端发来的信息
        js2 = str(js, encoding='utf-8') #将服务端发来的信息转换成字符串
        print(js2)
    z.close() #在客户端关闭连接

  **客户端与服务端进行交互信息原理图**

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160924201217246-1099496592.png)



**UDP通讯方式**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """UDP通讯"""
    #服务端
    import socket
    ip_port = ('127.0.0.1',9999)
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    sk.bind(ip_port)
    while True:
        data = sk.recv(1024)
        print(data)
    #客户端
    import socket
    ip_port = ('127.0.0.1',9999)
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    while True:
        inp = input('数据：').strip()
        if inp == 'exit':
            break
        sk.sendto(inp,ip_port)
    sk.close()



**setblocking()设置accept()和recv()是否阻塞，参数为1表示阻塞【默认】，参数为0表示不阻塞，那么accept和recv时一旦无数据，则报错**

**使用方法：对象变量. **setblocking(0)****

**格式：a.setblocking(0)**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    a.setblocking(0) #设置为不阻塞
    b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收



**connect_ex()客户端连接服务端，与connect()相同，只不过会有返回值，连接成功时返回 0 ，连接失败时候返回编码，例如：10061**

**使用方法：对象变量. **connect_ex(元祖类型IP和端口)****

**格式：b = z.connect_ex(('127.0.0.1', 9999,))**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect_ex(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    print(b)



**recvfrom()接收数据信息，与recv()类似，但返回值是（data,address）。其中data是包含接收数据的字符串，address是发送数据的套接字地址**

    
    
     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    f,s = z.recvfrom(1024) #客户端接收服务端sendall()发来的信息，1024表示最大接收1024字节
    f = str(f, encoding='utf-8') #将接收到的服务端字节信息转换成字符串
    print(f,s) #打印出服务端发来的信息



**send()发数据， **sendall底层也是调用的它，**
将string中的数据发送到连接的套接字。返回值是要发送的字节数量，该数量可能小于string的字节大小。即：可能未将指定内容全部发送。**



****sendto(string[,flag],address)
发送数据，将数据发送到套接字，address是形式为（ipaddr，port）的元组，指定远程地址。返回值是发送的字节数。该函数主要用于UDP协议。****

    
    
     # 服务端
    import socket
    ip_port = ('127.0.0.1',9999)
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    sk.bind(ip_port)
    
    while True:
        data,(host,port) = sk.recvfrom(1024)
        print(data,host,port)
        sk.sendto(bytes('ok', encoding='utf-8'), (host,port))
    
    
    #客户端
    import socket
    ip_port = ('127.0.0.1',9999)
    
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    while True:
        inp = input('数据：').strip()
        if inp == 'exit':
            break
        sk.sendto(bytes(inp, encoding='utf-8'),ip_port)
        data = sk.recvfrom(1024)
        print(data)
    
    sk.close()



**settimeout(timeout)设置连接超时时间，设置套接字操作的超时期，timeout是一个浮点数，单位是秒。值为None表示没有超时期。一般，超时期应该在刚创建套接字时设置，因为它们可能用于连接的操作（如
client 连接最多等待5s ）**



****getpeername()客户端获取服务端信息或者服务端获取客户端信息如IP，**
返回连接套接字的远程地址。返回值通常是元组（ipaddr,port）**



****getsockname() ** **客户端获取服务端信息或者服务端获取客户端信息如IP，******
返回套接字自己的地址。通常是一个元组(ipaddr,port)**



****fileno()通讯信号检测，** 套接字的文件描述符**



**UDP通讯举例**

    
    
     # 服务端
    import socket
    ip_port = ('127.0.0.1',9999)
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    sk.bind(ip_port)
    
    while True:
        data,(host,port) = sk.recvfrom(1024)
        print(data,host,port)
        sk.sendto(bytes('ok', encoding='utf-8'), (host,port))
    
    
    #客户端
    import socket
    ip_port = ('127.0.0.1',9999)
    
    sk = socket.socket(socket.AF_INET,socket.SOCK_DGRAM,0)
    while True:
        inp = input('数据：').strip()
        if inp == 'exit':
            break
        sk.sendto(bytes(inp, encoding='utf-8'),ip_port)
        data = sk.recvfrom(1024)
        print(data)
    
    sk.close()



**基于socket实现文件上传**

列如：客户端向服务端上传文件

1.客户端连接上服务端

2.客户端检测要传给服务端的文件大小，并且通讯告诉服务端，

3.服务端接收客户端发来的文件大小信息，接收文件大小信息后通讯客户端告诉客户端文件大小信息收到（解决粘包问题）

4.客户端接收服务端是否收到文件大小的信息，没收到服务端信息阻塞，收到继续下面执行

5.客户端已字节方式打开要传输的文件，for循环打开的文件，每循环一行向服务端传输一行的数据

6.服务端设置一个文件接收了多少的判断变量默认等于0

7.服务端打开文件等待写入接收到的客户端文件数据

8.服务端while
循环接收客户端发的文件数据并且写入文件，每循环写入一次检查一下服务端，当次接收到客户端多少字节文件数据，将当次接收到的文件大小字节累计加到，文件接收判断变量里

9.if判断，当文件接收判断变量等于文件总大小时，说明文件已经接收完成，跳出循环，关闭打开的文件

服务端代码

    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建服务端"""
    import socket #导入模块
    a = socket.socket() #创建socket对象
    a.bind(('127.0.0.1', 9999,)) #绑定服务端ip和端口
    a.listen(5) #监听IP和端口，设置一个参数，表示最多连接排队数量
    while True: #accept()被客户端连接一次后就会被中断，写个while循环让它永远等待客户端连接
        b, c = a.accept() #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接，一个是客户端的地址信息，所以需要两个变量来接收
        # 接收客户端发来的文件大小
    
        dx = b.recv(1024) #接受客户端发来的文件大小
        dx2 = str(dx, encoding="utf-8") #将文件大小转换成字符串
        dx3 = int(dx2) #将文件大小字符串转换成数字
    
        b.sendall(bytes("文件大小接收完成", encoding="utf-8")) #接收到文件大小后，告诉客户端
        #设置接收判断
    
        pd = 0 #设置一个接受了文件的判断大小
        #服务端打开文件接收
    
        f = open("456.png", "wb")
        while True: #循环写入接收到客户端发的文件内容
            if pd == dx3: #判断，判断大小等于总大小的时候跳出循环
                break
            j = b.recv(1024) #接收到的文件内容
            f.write(j) #将接收到的内容写入文件
            pd += len(j) #每循环写入一次就将写入的大小加给判断
        f.close()#关闭打开的文件

客户端代码

    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建客户端"""
    import os
    import socket #导入模块
    z = socket.socket() #创建socket对象
    b = z.connect(('127.0.0.1', 9999,))#连接服务端，在客户端绑定服务端IP和端口
    #检查发送文件大小
    
    dx = os.stat("32.png").st_size #检测要发送文件的大小
    z.sendall(bytes(str(dx), encoding="utf-8")) #将文件大小发送给服务端
    
    bao = z.recv(1024) #接收服务端文件大小，接收成功后的返回信息
    bao2 = str(bao, encoding="utf-8")
    print(bao2)
    #打开文件循环发送文件
    
    with open("32.png", "rb") as f:
        for i in f: #循环文件
            z.sendall(i) #将每次循环到文件内容发送给服务端
    z.close() #关闭通讯连接

**重点：注意传输数据时的粘包问题**

**粘包就是一端发了两次信息或数据，第一次发的有可能计算机缓冲区还没发出去，第二次的信息就发到了缓冲区，这样两次的信息粘在一起发出去了，为了避免粘包问题，在第一次发送后接收一下另外一端是否接收到第一次发的信息，如果接收到才发第二次，如果没接收到就不发用recv()阻塞，注意上面的列子**

**注意：socket模块不能处理并发，也就是不能实现多线路通讯，只能一条线路，第二个进来第一个占线着，要第一个退出后第二个才能进来**

