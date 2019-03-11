第五十四节，socketserver通讯模块实现并发操作，真多线程并发

**socketserver通讯模块实现并发操作，基于select、epoll、socket、多线程，实现的正真多线程多并发**

****socketserver通讯模块底层调用的** socket模块，只是它作了处理基于lo多路复用加多线程，能实现 **并发操作，1****

SocketServer内部使用 IO多路复用 以及 "多线程" 和 "多进程"
，从而实现并发处理多个客户端请求的Socket服务端。即：每个客户端请求连接到服务器时，Socket服务端都会在服务器是创建一个"线程"或者"进程"
专门负责处理当前客户端的所有请求。



**通讯模块实现并发操作服务端，2**

**1，import socketserver #导入模块,3**

**2，必须创建一个类来，继承两个类socketserver和BaseRequestHandler，注意必须创建一个类来继承这两个模块内部指定的类4**

****socketserver，创建类模块指定继承类名称5****

****BaseRequestHandler ** **，创建类模块指定继承类名称6********

**
注意：这个类对象里自动封装了3个普通字段分别为，self.request（客户端连接对象）,self.client_address（客户端IP和端口）,self.server（服务端对象）7**

****self.request（客户端连接对象）8****

****self.client_address（客户端IP和端口）9****

****self.server（服务端对象）10****

**3，创建的类里必须创建一个handle()方法，当客户端连接后就会执行这个
**handle()方法，所以各种发送数据和接收数据都是写在这个方法里11****

**** 在这个方法里通过对象普通字段的 **self.request（客户端连接对象）来做通讯操作12******

********handle()客户端连接后自动执行方法13********

********4，ocketserver.ThreadingTCPServer(元祖类型IP端口,
创建的类名称)设置服务端的IP和端口，并且把创建的类传进去给模块14********

******** 使用方法：定义变量 =  ** ** ** **ocketserver.ThreadingTCPServer(元祖类型IP端口,
创建的类名称)15****************

******** 如：shezhi = socketserver.ThreadingTCPServer(('127.0.0.1', 9999,),
bf)16********

********5，serve_forever()
执行模块，循环等待客户端连接，能处理并发操作，一旦有客户端连接就会执行创建类里的handle方法17********

****************使用方法： ** ** ** **设置服务端的IP和端口******** 变量. ** ** **
**serve_forever()  18************************

********如：shezhi.serve_forever()19********



**********并发操作服务端代码20**********



    
    
    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    """创建并发服务端"""
    import socketserver #导入模块
    
    """创建类"""
    class bf(socketserver.BaseRequestHandler): #创建一个类，继承两个类socketserver和BaseRequestHandler，注意必须创建一个类来继承这两个模块内部指定的类
         """定义方法"""
         def handle(self):
             #对象自动封装了（客户端连接对象）,（客户端IP和端口）,（服务端对象）
             # print self.request（客户端连接对象）,self.client_address（客户端IP和端口）,self.server（服务端对象）
             b = self.request #客户端连接对象
             b.sendall(bytes("你好欢迎你",encoding='utf-8')) #根据accept()接收到客户端连接对象信息，向客户端发送信息
    
             while True: #当客户端连接成功后，进入循环，保持与客户端的通讯
                j = b.recv(1024)#接收客户端发来的信息
                j2 = str(j, encoding='utf-8') #将接收到的客户端信息转换成字符串
                if j2 == "q": #判断客户端输入q，表示不再与服务端通讯，跳出循环，不在保持客户端的通讯
                    break
                b.sendall(bytes(j2+"好",encoding='utf-8')) #将接收到客户端的信息加上一个好字，在发送给客户端
    
    """设置服务端IP端口，并且把创建类传入socketserver模块"""
    shezhi = socketserver.ThreadingTCPServer(('127.0.0.1', 9999,), bf) #设置服务端的IP和端口，并且把创建的类传进去
    
    """执行socketserver模块"""
    shezhi.serve_forever() #执行模块，循环等待客户端连接，能处理并发操作，一旦有客户端连接就会执行创建类里的handle方法

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160928073639438-2048589746.png)

**********并发操作服务端流程图21**********

![](https://images2015.cnblogs.com/blog/955761/201609/955761-20160928072050703-409204703.png)



**重点：注意传输数据时的粘包问题22**

**粘包就是一端发了两次信息或数据，第一次发的有可能计算机缓冲区还没发出去，第二次的信息就发到了缓冲区，这样两次的信息粘在一起发出去了，为了避免粘包问题，在第一次发送后接收一下另外一端是否接收到第一次发的信息，如果接收到才发第二次，如果没接收到就不发用，recv()阻塞，**

** **

