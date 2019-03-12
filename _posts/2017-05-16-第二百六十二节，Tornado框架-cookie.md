---
layout: post
title: " 第二百六十二节，Tornado框架-cookie "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Tornado框架-cookie**

**Cookie 是网站用来在客户端保存识别用户的一种小文件。一般来用库可以保存用户登 录信息、购物数据信息等一系列微小信息。**

**self.set_cookie()方法，创建cookie必写参数，cookie名称和cookie值，后面有可选参数**  
 **self.get_cookie()方法，获取指定cookie值，必写参数要获取的cookie名称**

**模板引擎**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import uimodule
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            if self.get_cookie("admin") == "admin":                 #判断cookie值等于admin
                self.render("index.html")                           #显示index.html文件
            else:
                self.redirect("/dlu")                               #否则跳转到登录
    
    
    class dluHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            self.render("dlu.html",shib="")                         #显示dlu.html文件
        def post(self, *args, **kwargs):                            #处理post请求
            yhm = self.get_argument('yhm')                          #接收用户名
            mim = self.get_argument('mim')                          #接收密码
            if yhm =="admin" and mim =="admin":                     #判断用户名和密码
                self.set_cookie(yhm,mim,expires_days=2)             #创建cookie
                self.redirect("/index")                             #跳转用户查看页面
            else:
                self.render("dlu.html", shib="用户名或密码不正确")    #如果用户名和密码不正确，打开登录页面
    
    class tuichuHandler(tornado.web.RequestHandler):
        def get(self):                                              #处理get方法请求
            self.set_cookie("admin","0",expires=0)                  #修改cookie值
            self.redirect("/index")                                 #跳转页面
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"template",                 #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                     #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", indexHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", dluHandler),
        (r"/tuichu", tuichuHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**内容html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" href='{{static_url("s1.css")}}'>
    </head>
    <body>
    <h1>登录成功后才能看到</h1><a href="/tuichu">退出</a>
    </body>
    </html>
[/code]

**登录html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <form method="post" action="/dlu">
        用户名：<input type="text" name="yhm"/>
        密码：<input type="text" name="mim"/>
        <input type="submit" value="提交"/>
        <span style="color: #ee1215">{{shib}}</span>
    </form>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170516203643760-360647891.gif)



**self.set_cookie()方法，创建cookie参数详情**  
 **1、cookie名称**  
 **2、cookie值**  
 **3、domain : 'www.jxiou.com', 设置域名，设置域名后，cookie在指定域名下有效**  
 **4、expires:过期时间的时间戳**  
 **5、expires_days:过期时间天**  
 **6、path:'/', 设置cookie有效路径，/表示全局目录有效**





**销毁 **cookie****

****将过期时间 **expires设置成系统当前时间戳减一，也就是过去了的时间，就会自动销毁 ** **cookie**********



[code]

    #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import uimodule
    import time
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            if self.get_cookie("admin") == "admin":                 #判断cookie值等于admin
                self.render("index.html")                           #显示index.html文件
            else:
                self.redirect("/dlu")                               #否则跳转到登录
    
    
    class dluHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            self.render("dlu.html",shib="")                         #显示dlu.html文件
        def post(self, *args, **kwargs):                            #处理post请求
            yhm = self.get_argument('yhm')                          #接收用户名
            mim = self.get_argument('mim')                          #接收密码
            if yhm =="admin" and mim =="admin":                     #判断用户名和密码
                self.set_cookie(yhm,mim,expires_days=2)             #创建cookie
                self.redirect("/index")                             #跳转用户查看页面
            else:
                self.render("dlu.html", shib="用户名或密码不正确")    #如果用户名和密码不正确，打开登录页面
    
    class tuichuHandler(tornado.web.RequestHandler):
        def get(self):                                              #处理get方法请求
            self.set_cookie("admin","0",expires=time.time()-1)                  #将过期时间设置成当前时间戳减1，成过去时间，销毁cookie
            self.redirect("/index")                                 #跳转页面
            print()
    
    
    settings = {                                    #html文件归类配置，设置一个字典
        "template_path":"template",                 #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                     #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", indexHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", dluHandler),
        (r"/tuichu", tuichuHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]





**self.set_secure_cookie()方法，创建加密cookie，参数为cookie名称和cookie值**  
 **self.get_secure_cookie()方法，读取加密cookie，参数为要读取加密cookie的名称**

**注意，self.get_secure_cookie()读取到的cookie值是字节类型需要decode()转换成字符串**  
 **注意，使用self.set_secure_cookie()加密cookie，必须在配置字典里写cookie_secret:密匙**  
 **cookie_secret:密匙，加密会根据这个密匙提高加密级别**

**注意：此加密采用base64加密**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import uimodule
    import time
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            if self.get_secure_cookie("admin"):
                ckk = self.get_secure_cookie("admin")
                cke = ckk.decode()
                if cke == "admin":                                      #判断cookie值等于admin
                    self.render("index.html")                           #显示index.html文件
                else:
                    self.redirect("/dlu")
            else:
                self.redirect("/dlu")                               #否则跳转到登录
    
    
    class dluHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            self.render("dlu.html",shib="")                         #显示dlu.html文件
        def post(self, *args, **kwargs):                            #处理post请求
            yhm = self.get_argument('yhm')                          #接收用户名
            mim = self.get_argument('mim')                          #接收密码
            if yhm =="admin" and mim =="admin":                     #判断用户名和密码
                self.set_secure_cookie(yhm,mim)
                self.redirect("/index")                             #跳转用户查看页面
            else:
                self.render("dlu.html", shib="用户名或密码不正确")    #如果用户名和密码不正确，打开登录页面
    
    class tuichuHandler(tornado.web.RequestHandler):
        def get(self):                                              #处理get方法请求
            self.set_secure_cookie("admin","0",expires=time.time()-1)                  #将过期时间设置成当前时间戳减1，成过去时间，销毁cookie
            self.redirect("/index")                                 #跳转页面
    
    
    settings = {                                        #html文件归类配置，设置一个字典
        "template_path":"template",                     #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"static",                         #键为static_path固定的，值为要存放js和css的文件夹名称
        "cookie_secret":"61oETzKXQAGaYdkL5gEmGeJJFuY",
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", indexHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", dluHandler),
        (r"/tuichu", tuichuHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]



