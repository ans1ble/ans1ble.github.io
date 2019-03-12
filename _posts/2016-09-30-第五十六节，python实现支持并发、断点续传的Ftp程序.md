
---
layout: post
title: " 第五十六节，python实现支持并发、断点续传的Ftp程序 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


# 一、要求

1、用户md5认证

2、支持多用户同时登陆（并发）

3、进入用户的命令行模式，支持cd切换目录，ls查看目录子文件

4、执行命令（ipconfig）

5、传输文件：

a、支持断点续传

b、传输中显示进度条

# 二、思路



## 1.客户端用户登录和注册：

a、客户端仅提供用户名和密码，选择登录或注册，  
b、服务器端进行注册并将加密后的密码写入文件，最后返回给客户端是否登录或注册成功

## 2.ls和cd命令

a、客户端输入命令，服务器端处理并返回给客户端

## 3.执行命令：

a、客户端发送需要执行的命令  
b、服务器端执行命令，并返回客户端需要接收该命令的次数s=r[0]+1,其中r=divmod（结果总长度，1024）  
c、客户端收到次数，告诉服务端已经收到  
d、服务端发送执行结果，客户端进行for循环接收该结果

## 4.发送文件：

a、客户端输入文件路径（测试版路径为：f.png），发送文件名和文件大小  
b、服务器端检测指定目录是否含有该文件，如果没有，返回给客户端字符串s，即从头开始发送start，has_recv=0  
如果有，即需要断点续传，返回给客户端已经上传了多少has_recv  
c、客户端接收返回值，并seek到has_recv的位置，进行循环收发，打印当前进度，直到传输完毕。

注：本程序可循环接收用户选择传输文件和执行命令

# 三、代码



## 配置文件：

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import os
    BASE_DIR = os.path.dirname(os.path.dirname(__file__))  #配置文件的上层目录
    NEW_FILENAME=os.path.join(BASE_DIR,'view')             #新文件目录
    NAME_PWD=os.path.join(BASE_DIR,'db','name_pwd')        #用户名和密码目录
    USER_FILE=os.path.join(BASE_DIR,'db')
[/code]

## 服务器端：

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
     
    import sys,os
    import time
    import socket
    import hashlib
    import pickle
    import subprocess
    import socketserver
    sys.path.append(os.path.dirname(os.path.dirname(__file__)))
    from config import settings
     
     
    new=settings.NEW_FILENAME
    class Myserver(socketserver.BaseRequestHandler):
     
        def recv_file(self):
            '''
            文件传输
            :return:
            '''
            conn=self.request
            a=str(conn.recv(1024),encoding='utf-8')
            file_size,file_name=a.split(',')
            new_file_name=os.path.join(new,file_name)
            if file_name in new:            #检测文件是否已存在，涉及断点续传
                has_recv=os.stat(new).st_size #计算临时文件大小
                conn.sendall(bytes(has_recv,encoding='utf-8'))
                with open(new_file_name,'ab') as f:  #追加模式
                    while has_recv<=int(file_size):
                        data=conn.recv(1024)
                        f.write(data)
                        has_recv+=len(data)
            else:
                has_recv=0
                conn.sendall(bytes('s',encoding='utf-8')) # 客户端收到字符串s，从0开始发送
                with open(new_file_name,'wb') as f:
                    while has_recv<=int(file_size):
                        data=conn.recv(1024)
                        f.write(data)
                        has_recv+=len(data)
     
        def command(self):
            '''
            执行命令
            :return:
            '''
            conn=self.request
            a=conn.recv(1024)
            ret=str(a,encoding='utf-8')
            ret2 = subprocess.check_output(ret, shell=True)
            r=divmod(len(ret2),1024)
            s=r[0]+1         #客户端需要接收的次数
            conn.sendall(bytes(str(s),encoding='utf-8'))
            conn.recv(1024)  #确认客户端收到需要接收的次数
     
            conn.sendall(ret2)
     
        def md5(self,pwd):
            '''
            对密码进行加密
            :param pwd: 密码
            :return:
            '''
            hash=hashlib.md5(bytes('xx7',encoding='utf-8'))
            hash.update(bytes(pwd,encoding='utf-8'))
            return hash.hexdigest()
     
     
        def login(self,usrname,pwd):
            '''
            登陆
            :param usrname: 用户名
            :param pwd: 密码
            :return:是否登陆成功
            '''
            conn=self.request
            s=pickle.load(open(settings.NAME_PWD,'rb'))
            if usrname in s:
                 if s[usrname]==self.md5(pwd):        #和加密后的密码进行比较
                    return True
                 else:
                    return False
            else:
                return False
     
     
        def regist(self,usrname,pwd):
            '''
            注册
            :param usrname: 用户名
            :param pwd: 密码
            :return:是否注册成功
            '''
     
            conn=self.request
            s=pickle.load(open(settings.NAME_PWD,'rb'))
            if usrname in s:
                 return False
            else:
                s[usrname]=self.md5(pwd)
                mulu=os.path.join(settings.USER_FILE,usrname)
                os.makedirs(mulu,'a')
                pickle.dump(s,open(settings.NAME_PWD,'wb'))
                return True
     
        def before(self,usrname,pwd,ret):
            '''
            判断注册和登陆，并展示用户的详细目录信息，支持cd和ls命令
            :return:
            '''
            conn=self.request
            if ret=='1':
                r=self.login(usrname,pwd)
                if r:
                    conn.sendall(bytes('y',encoding='utf-8'))
                else:
                    conn.sendall(bytes('n',encoding='utf-8'))
            elif ret=='2':
                # print(usrname,pwd)
                r=self.regist(usrname,pwd)
                if r:
                    conn.sendall(bytes('y',encoding='utf-8'))
                else:
                    conn.sendall(bytes('n',encoding='utf-8'))
        def usr_file(self,usrname):
            '''
            展示用户的详细目录信息，支持cd和ls命令
            :param usrname: 用户名
            :return:
            '''
            conn=self.request
            conn.recv(1024)
            mulu=os.path.join(settings.USER_FILE,usrname)
            conn.sendall(bytes(mulu,encoding='utf-8'))
            while True:
                b=conn.recv(1024)
                ret=str(b,encoding='utf-8')
                try:
                    a,b=ret.split(' ',1)
                except Exception as e:
                    a=ret
                if a=='cd':
                    if b=='..':
                        mulu=os.path.dirname(mulu)
                    else:
                        mulu=os.path.join(mulu,b)
                    conn.sendall(bytes(mulu,encoding='utf-8'))
                elif a=='ls':
                    ls=os.listdir(mulu)
                    print(ls)
                    a=','.join(ls)
                    conn.sendall(bytes(a,encoding='utf-8'))
                elif a=='q':
                    break
     
     
        def handle(self):
            conn=self.request
            conn.sendall(bytes('welcome',encoding='utf-8'))
            b=conn.recv(1024)
            ret=str(b,encoding='utf-8')
            print(ret)
            conn.sendall(bytes('b ok',encoding='utf-8'))
            c=conn.recv(1024)
            r=str(c,encoding='utf-8')
            usrname,pwd=r.split(',')
            self.before(usrname,pwd,ret) #登陆或注册验证
            self.usr_file(usrname)  #展示用户的详细目录信息，支持cd和ls命令
            while True:
                a=conn.recv(1024)
                conn.sendall(bytes('收到a',encoding='utf-8'))
                ret=str(a,encoding='utf-8')
                if ret=='1':
                    self.recv_file()
                    # conn.sendall(bytes('file ok',encoding='utf-8'))
                elif ret=='2':
                    self.command()
                elif ret=='q':
                    break
                else:
                    pass
     
    if __name__=='__main__':
        sever=socketserver.ThreadingTCPServer(('127.0.0.1',9999),Myserver)
        sever.serve_forever()
[/code]

## 客户端：

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
     
    import sys
    import time
    import os
    import socket
    sys.path.append(os.path.dirname(os.path.dirname(__file__)))
    from config import settings
     
     
     
    def send_file(file_path):
        '''
        发送文件
        :param file_name:文件名
        :return:
        '''
        size=os.stat(file_path).st_size
        file_name=os.path.basename(file_path)
        obj.sendall(bytes(str(size)+','+file_name,encoding='utf-8')) #发送文件大小和文件名
        ret=obj.recv(1024)   #接收已经传了多少
        r=str(ret,encoding='utf-8')
        if r=='s': #文件不存在，从头开始传
            has_send=0
        else:   #文件存在
            has_send=int(r)
     
        with open(file_path,'rb') as f:
            f.seek(has_send) #定位到已经传到的位置
            while has_send<size:
                data=f.read(1024)
                obj.sendall(data)
                has_send+=len(data)
                sys.stdout.write('\r')  #清空文件内容
                time.sleep(0.2)
                sys.stdout.write('已发送%s%%|%s' %(int(has_send/size*100),(round(has_send/size*40)*'★')))
                sys.stdout.flush()   #强制刷出内存
            print("上传成功\n")
     
    def command(command_name):
        '''
        执行命令
        :param command_name:
        :return:
        '''
        obj.sendall(bytes(command_name,encoding='utf-8'))
        ret=obj.recv(1024)  #接收命令需要接收的次数
        obj.sendall(bytes('收到次数',encoding='utf-8'))
        r=str(ret,encoding='utf-8')
        for i in range(int(r)): #共需要接收int(r)次
            ret=obj.recv(1024)  #等待客户端发送
            r=str(ret,encoding='GBK')
            print(r)
     
    def login(usrname,pwd):
        '''
        登陆
        :param usrname:用户名
        :param pwd:密码
        :return:是否登陆成功
        '''
        obj.sendall(bytes(usrname+','+pwd,encoding='utf-8'))
        ret=obj.recv(1024)
        r=str(ret,encoding='utf-8')
        if r=='y':
            return 1
        else:
            return 0
     
    def regist(usrname,pwd):
        '''
        注册
        :param usrname:用户名
        :param pwd:密码
        :return:是否注册成功
        '''
        obj.sendall(bytes(usrname+','+pwd,encoding='utf-8'))
        ret=obj.recv(1024)
        r=str(ret,encoding='utf-8')
        if r=='y':
            return 1
        else:
            return 0
    def before(usrname,pwd):
        '''
        选择登陆或注册，展示用户的详细目录信息，支持cd和ls命令
        :return:
        '''
        a=input('请选择1.登陆 2.注册')
        obj.sendall(bytes(a,encoding='utf-8'))
        obj.recv(1024)
        if a=='1':
            ret=login(usrname,pwd)
            if ret:
                print('登陆成功')
                return 1
            else:
                print('用户名或密码错误')
                return 0
        elif a=='2':
            ret=regist(usrname,pwd)
            if ret:
                print('注册成功')
                return 1
            else:
                print('用户名已存在')
                return 0
    def usr_file(usrname):
        obj.sendall(bytes('打印用户文件路径',encoding='utf-8'))
        ret=obj.recv(1024)  #等待客户端发送
        r=str(ret,encoding='utf-8')
        print(r)
        while True:
            a=input('输入cd切换目录，ls查看目录详细信息，q退出>:')
     
            obj.sendall(bytes(a,encoding='utf-8'))
            if a=='q':
                break
            else:
                ret=obj.recv(1024)  #等待客户端发送
                r=str(ret,encoding='utf-8')
                if len(r)==1:#判断是cd结果还是ls的结果（ls只有一个子目录也可以直接打印）
                    print(r)
                else:
                    li=r.split(',')
                    for i in li:
                        print(i)  #打印每一个子目录
     
    def main(usrname,pwd):
        ret=obj.recv(1024)  #等待客户端发送
        r=str(ret,encoding='utf-8')
        print(r)
        result=before(usrname,pwd)#登陆或注册
        if result:
            usr_file(usrname)
            while True:
                a=input('请选择1.传文件 2.执行命令 q退出:')
                obj.sendall(bytes(str(a),encoding='utf-8'))
                ret=obj.recv(1024) #确认是否收到a
                r=str(ret,encoding='utf-8')
                print(r)
                if a=='1':
                    b=input('请输入文件路径（测试版路径为：f.png）:')
                    # b='f.png'
                    if os.path.exists(b):
                        send_file(b)
                        obj.sendall(bytes('hhe',encoding='utf-8'))
                        # obj.recv(1024)
                elif a=='2':
                    b=input('请输入command:')
                    command(b)
                elif a=='q':
                    break
                else:
                    print('输入错误')
     
        obj.close()
     
    if __name__ == '__main__':
        obj=socket.socket() #创建客户端socket对象
        obj.connect(('127.0.0.1',9999))
        usrname=input('请输入用户名')
        pwd=input('请输入密码')
        main(usrname,pwd)
    　　
[/code]



