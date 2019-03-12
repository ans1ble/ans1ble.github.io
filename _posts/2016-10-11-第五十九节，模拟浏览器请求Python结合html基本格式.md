
---
layout: post
title: " 第五十九节，模拟浏览器请求Python结合html基本格式 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**模拟浏览器请求Python结合html基本格式**

**用Python模拟一个客户端，结合打开一个HTML页面**

**创建客户端**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import socket #导入单线程通讯模块
    def handle_request(client):
        buf = client.recv(1024)
        client.sendall(bytes("HTTP/1.1 201 OK\r\n\r\n","utf8")) #向客户端发送内容，以字节形式发送
        f = open("1.html", "r", encoding="utf-8")   #打开HTML文件
        f2 = f.read()   #读出HTML文件内容
        f.close()   #关闭打开的文件
    
        client.sendall(bytes(f2,"utf8")) #将读出HTML文件内容向客户端发送内容，以字节形式发送
    
    def main():
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)     #创建服务端通讯对象
        sock.bind(('localhost',8082))   #在服务端设置服务端ip和端口8
        sock.listen(5)      #监听IP和端口，设置一个参数，表示最多连接排队数量
    
        while True:
            connection, address = sock.accept()     #等待接收客户端的请求，一旦有客户端请求连接，就会返回两个值，一个是连接对象，一个是客户端的地址信息，所以需要两个变量来接收
            handle_request(connection)  #执行handle_request函数，将客户端请求连接传入handle_request函数
            connection.close()  #关闭连接
    
    if __name__ == '__main__':  #wds系统下if __name__ == "__main__"才能创建进程，我们调试没关系，以后在Linux系统没这个问题
    
        main() #执行main函数
[/code]

**HTML页面**

**将HTML页面放入客服端相同的目录里**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <h1>你好</h1>
    </body>
    </html>
[/code]

启动客户端后在浏览器输入http://127.0.0.1:8082/  可以看到以下结果

# 你好



**下面我们开始讲HTML知识**



**HTML基本格式**

[code]

     <!DOCTYPE html>                     //文档类型声明
    <html lang="zh-cn">                 //表示HTML文档开始，属性lang,属性值=zh-cn（声明中文网页的意思）
    <head>                              //包含文档元素开始
        <meta charset="UTF-8">          //声明字符编码
        <title>标题</title>             //设置文档标题
    </head>                             //包含文档元素结束
    <body>                              //表示HTML内容开始
    
    </body>                             //表示HTML内容结束
    </html>                             //表示HTML文档结束
[/code]



**<!DOCTYPE html > **  
**它主要告诉浏览器所查看的文件类型，表示为HTML文档类型**



**< html lang="zh-cn"></html> **  
**HTML元素是文档开始和结尾的元素，它是一个双标签，包含内容，这个元素有一个属性和属性值，lang="zh-
cn"，表示文档语言为：简体中文，如果是英文网页为lang="en"**



**< head> </head>**  
**用来包含元数据内容，元数据内容包括：
<link>、<meta>、<noscript>、<scripy>、<style>、<title>,这些内容用来向浏览器提供信息，比如link提供css信息，这些类型都是页面不可见的**



**< meta>**  
 **这个元素可以用来设置字符编码，告诉浏览器页面采用什么编码，除了设置编码还有别的**



**< title></title> **  
**这个元素是设置页面的标题的，标题会显示到浏览器上部，也会被搜索引擎识别**



**< body> </body>**  
 **用来包含文档内容的元素，也就是浏览器可见部分，所有的可见部分都应该写在这里**



