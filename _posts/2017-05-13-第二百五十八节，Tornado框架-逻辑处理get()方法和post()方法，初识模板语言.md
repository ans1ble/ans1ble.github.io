
---
layout: post
title: " 第二百五十八节，Tornado框架-逻辑处理get()方法和post()方法，初识模板语言 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Tornado框架-逻辑处理get()方法和post()方法，初识模板语言**





****Tornado框架，逻辑处理里的get()方法，和post()方法****

**get()方法，处理get方式的请求**  
 **post()方法，处理post方式的请求**

**self.get_argument()接收 **get方式或post方式** 请求传值，参数是要接收值的名称，如表单传值**

****接收表单数据****

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    
    #逻辑处理
    class MainHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                              #get()方法，接收get方式请求
            self.render("cshi.html")                #显示cshi.html文件
    
        def post(self, *args, **kwargs):            #post()方法，接收post方式请求
            name = self.get_argument('xxx')         #self.get_argument()方法，接收post方式提交name名称为xxx的值
            print(name)
            self.render("cshi.html")                #显示cshi.html文件
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"template",                 #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                     #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", MainHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <!--注意js和css文件路径配置后必须在引入路径里加上配置文件夹名称-->
        <link rel="stylesheet" href="static/s1.css">
    </head>
    <body>
        <h1>表单提交</h1>
        <form method="post" action="/index">
            <input type="text" name="xxx"/>
            <input type="submit" value="提交"/>
        </form>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170514165547535-1457072736.png)







**表单提交值，接收表单值并传入html模板语言渲染到页面**

**self.render()方法，参数1向用户请求打开指定html文件，参数2向html文件传入值到模板语言渲染**

**模板语言**

**{{...}}html模板语言,接收self.render()方法传值的变量或一个值**  
 **{%...%}{%end%}在html渲染代码块**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    
    BAODZHI = []                                    #设置一个全局变量列表。来接收表单的值
    
    #逻辑处理
    class MainHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                              #get()方法，接收get方式请求
            self.render("cshi.html",zhi = BAODZHI)  #显示cshi.html文件,将BAODZHI全局传到html模板语言进行渲染
    
        def post(self, *args, **kwargs):            #post()方法，接收post方式请求
            name = self.get_argument('xxx')         #self.get_argument()方法，接收post方式提交name名称为xxx的值
            BAODZHI.append(name)                    #将每次接收到的表单值，放入全局变量列表
            print(name)
            self.render("cshi.html",zhi = BAODZHI)  #显示cshi.html文件，将BAODZHI全局传到html模板语言进行渲染
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"template",                 #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                     #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", MainHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <!--注意js和css文件路径配置后必须在引入路径里加上配置文件夹名称-->
        <link rel="stylesheet" href="static/s1.css">
    </head>
    <body>
        <h1>表单提交</h1>
        <form method="post" action="/index">
            <input type="text" name="xxx"/>
            <input type="submit" value="提交"/>
        </form>
        <h1>展示内容</h1>
        <ul>
            {% for i in zhi %}
            <li>{{i}}</li>
            {% end %}
        </ul>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170514195312879-1883700843.gif)

**原理图**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170514200742238-1182160298.png)**



