
---
layout: post
title: " 第二百六十八节，Tornado框架-路由映射之二级域名支持，html模板继承以及导入 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Tornado框架-路由映射之二级域名支持，html模板继承以及导入**



**二级域名路由映射**  
 **add_handlers()设置二级域名路由映射**

**注意：二级域名需要结合服务器ip绑定域名**

**框架引擎**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    from controllers import index
    
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"views",                    #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                    #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    
    #路由映射
    #一级路由映射如localhost.com
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index/(?P<page>\d*)", index.indexHandler),    #正则匹配访问路径，访问录index/后面可以是可以是0个或多个数字
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    #二级域名路由映射如buy.localhost.com
    application.add_handlers('buy.localhost.com$',[
        (r"/index/(?P<page>\d*)", index.buy),      #二级域名访问函数
    ])
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**逻辑处理**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    from pymkuai import fenye
    
    
    SHUJU = [
        {"user":"lgx","emia":"729088188@qq.com"}
    ]
    for f in range(300):
        SHUJU.append({"user": "lgx", "emia": "729088188@qq.com"})   #填充数据到300条
    
    
    #逻辑处理
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
    
            fen_ye = fenye.fen_ye_lei(page,SHUJU,10,11,5,'/index/')       #执行分页对象
    
            if fen_ye.dang_qian_ye > fen_ye.zong_ye_ma:             #判断分页对象里的当前页码如果大于总页码
                zfchdqy = str(fen_ye.zong_ye_ma)                    #将总页码转换成字符串
                self.redirect("/index/" + zfchdqy)                  #跳转到总页码
            else:
                self.render("index.html",dqy=fen_ye.dang_qian_ye,shuju=fen_ye.shu_ju_fan_wei(),yem=fen_ye.xian_shi_ye_ma())  # 显示index.html文件，传递当前页码，传递数据，传递分页
    
    
        def post(self,page):
            user = self.get_argument("user")            #接收用户提交的用户名
            emia = self.get_argument("emia")            #接收用户提交的邮箱
            temp = {"user":user,"emia":emia}            #将邮箱和用户名组合成字典，
            SHUJU.append(temp)                          #将字典追加到SHUJU全局变量
            self.redirect("/index/" + page)             #跳转到当前页面
    
    class buy(tornado.web.RequestHandler):
        def get(self):
            self.render("buy.html")
[/code]







**母板继承**

****母板继承就是访问的页面继承一个母板，将访问页面的内容引入到母板里指定的地方，组合成一个新页面返回给浏览器****

****一般母板里都是写的一个网页里不变的地方，也就是通用的地方，被继承页（访问页）都是每个页面不同的地方，也就是将页面不同的地方引入到母板组合成一个新页面返回浏览器****

****母板里一般都是网页的、头部、底部、头部底部css、头部底部js****

****被继承页 ** **（访问页）里一般都是新内容，新内容的css和js********



**{% extends '母板路径名称'%}访问页面继承母板**  
 **{% block 代码块名称 %} <html代码块>{% end %}在访问页设置一个可引入到母板的html代码块**  
 **{% block 代码块名称 %}{% end %}在母板，引入访问页对应的html代码块**



**框架引擎**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    from controllers import index
    
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"views",                    #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                    #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    
    #路由映射
    #一级路由映射如localhost.com
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index/(?P<page>\d*)", index.indexHandler),    #正则匹配访问路径，访问录index/后面可以是可以是0个或多个数字
        (r"/nevm/(?P<page>\d*)", index.nevmHandler)
    ],**settings)                                         #将html文件归类配置字典，写在路由映射的第二个参数里
    
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**逻辑处理**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    from pymkuai import fenye
    
    
    
    #逻辑处理
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
            self.render("index.html")                # 显示html文件，
    
    class nevmHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
            self.render("nevm.html")                # 显示html文件，
[/code]

**muban.html 母板html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>测试网站</title>
        <link rel="stylesheet" href='{{static_url("muban.css")}}'>
        {% block css %}{% end %}                                        <!--接收被继承页面的css连接-->
    </head>
    <body>
    <div id="tou">头部</div>
    
    {% block neir %}{% end %}                                           <!--接收被继承页面的内容区块-->
    
    <div id="dibu">底部</div>
    </body>
    </html>
[/code]

**index.html 访问页(被继承页)**

[code]

     {% extends 'muban.html'%}                                       <!--继承母板muban.html-->
    
    {% block css %}                                                 <!--导入css到继承页面指定地方-->
    <link rel="stylesheet" href='{{static_url("index.css")}}'>
    {% end %}
    
    {% block neir %}                                                <!--导入内容区块到继承页面指定地方-->
    <div id="neir">首页内容</div>
    {% end %}
[/code]

**nevm.html  访问页(被继承页)**

[code]

    {% extends 'muban.html'%}                                       <!--继承母板muban.html-->
    
    {% block css %}                                                 <!--导入css到继承页面指定地方-->
    <link rel="stylesheet" href='{{static_url("nevm.css")}}'>
    {% end %}
    
    {% block neir %}                                                <!--导入内容区块到继承页面指定地方-->
    <div id="neir">内页内容</div>
    {% end %}
[/code]

**index.html 返回浏览器**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170522064939335-448791555.png)**

**nevm.html 返回浏览器**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170522065002773-749661978.png)**





**html导入**

**将一个写有html代码块的文件，导入到另一个html文件中显示**

**一般用于导入小区块**

**被导入文件也支持模板语言**

**{% include '被导入区块html文件路径名称' %}写在需要导入区块的html文件里，将一个html文件导入到当前文件显示，**

**当前html**

[code]

    {% extends 'muban.html'%}                                        <!--继承母板muban.html-->
    
    {% block css %}                                                 <!--导入css到继承页面指定地方-->
    <link rel="stylesheet" href='{{static_url("index.css")}}'>
    <link rel="stylesheet" href='{{static_url("qukuai.css")}}'>
    {% end %}
    
    {% block neir %}                                                <!--导入内容区块到继承页面指定地方-->
    <div id="neir">
        首页内容
        {% include 'qukuai.html' %}
    </div>
    {% end %}
[/code]

**被导入html**

[code]

     <div id="qukuai">
        区块内容
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170522080000679-361749928.png)



