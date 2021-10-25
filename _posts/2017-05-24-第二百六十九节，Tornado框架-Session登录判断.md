---
layout: post
title: " 第二百六十九节，Tornado框架-Session登录判断 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Tornado框架-Session登录判断**



****Session需要结合cookie来实现****

********Session的理解********

********1、用户登录系统时，服务器端获取系统当前时间，进行nd5加密，得到加密后的密串********

********2、将密串作为一个字典的键，值为一个字典，也就是嵌套字典，键为密串的字典里保存用户信息********

********3、将这个密串当做 ** **cookie值写入浏览器************

************4、当用户访问时，判断值为密串的 ** **cookie是否存在，如果存在，获取 **
**cookie的值也就是密串，将这个密串在服务端的字典里查找是否存在，如果存在就可以拿到用户保存的各种信息，判断用户是否是登录状态********************

********************![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170524102500122-621710224.png)********************





**框架引擎**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    
    
    container = {}                                  #用户登录信息字典,保存着用户的登录信息，{'328eb994f73b89c5f1de57742be1ee82': {'is_login': True, 'mim': 'admin', 'yhm': 'admin'}}
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                                              #get()方法，接收get方式请求
            hq_cookie = self.get_cookie('xr_cookie')                #获取浏览器cookie
            session = container.get(hq_cookie,None)                 #将获取到的cookie值作为下标，在数据字典里找到对应的用户信息字典
            if not session:                                         #判断用户信息不存在
                self.redirect("/dlu")  # 显示登录html文件            #跳转到登录页面
            else:
                if session.get('is_login',None) == True:            #否则判断用户信息字典里的下标is_login是否等于True
                    self.render("index.html")  # 显示index.html文件  #显示查看页面
                else:
                    self.redirect("/dlu")                           #跳转登录页面
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            hq_cookie = self.get_cookie('xr_cookie')                #获取浏览器cookie
            session = container.get(hq_cookie,None)                 #将获取到的cookie值作为下标，在数据字典里找到对应的用户信息字典
            if not session:                                         #判断用户信息不存在
                self.render("dlu.html")  # 显示登录html文件          #打开到登录页面
            else:
                if session.get('is_login',None) == True:            #否则判断用户信息字典里的下标is_login是否等于True
                    self.redirect("/index")  # 显示index.html文件    #跳转查看页面
                else:
                    self.redirect("/dlu")                           #跳转登录页面
    
        def post(self):
            yhm = self.get_argument('yhm')                          #接收用户输入的登录账号
            mim = self.get_argument('mim')                          #接收用户输入的登录密码
            if yhm == 'admin' and mim == 'admin':                   #判断用户的密码和账号
                import hashlib                                      #导入md5加密模块
                import time                                         #导入时间模块
                obj = hashlib.md5()                                 #创建md5加密对象
                obj.update(bytes(str(time.time()),encoding = "utf-8"))  #获取系统当前时间，传入到md5加密对象里加密
                suijishu = obj.hexdigest()                              #获取加密后的密串
                container[suijishu] = {}                                #将密串作为下标到container字典里，创建一个新空字典
                container[suijishu]['yhm'] = yhm                        #字典里的键为yhm，值为用户名
                container[suijishu]['mim'] = mim                        #字典里的键为mim，值为用户密码
                container[suijishu]['is_login'] = True                  #字典里的键为is_login，值为True
                self.set_cookie('xr_cookie',suijishu,expires_days=1)    #将密串作为cookie值写入浏览器
                self.redirect("/index")                                 #跳转到查看页面
            else:
                self.redirect("/dlu")
    
    settings = {                                        #html文件归类配置，设置一个字典
        "template_path":"views",                     #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                         #键为static_path固定的，值为要存放js和css的文件夹名称
        "cookie_secret":"61oETzKXQAGaYdkL5gEmGeJJY",
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", indexHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", dluHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]





********Session模块封装以及使用********

**Session(self,1)
创建session对象，参数1接收接收tornado.web.RequestHandler的self对象，也就是继承RequestHandler对象，参数2cookie过期时间**  
 **session['yhm']=yhm 自定义用户保存数据，保存在字典里['键']=值**  
 **session['yhm'] 获取自定义保存的数据，['键']**

**********Session封装模块**********

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    container = {}
    # container = {
    #     # "第一个人的随机字符串":{}，
    #     # "第一个人的随机字符串":{'k1': 111, 'parents': '你'}，
    # }
    
    class Session:
        def __init__(self, handler,gqshijian):
            """
            创建Session()对象时接收两个参数
            参数1、接收RequestHandler的self对象，也就是继承RequestHandler对象
            参数2、接收cookie过期时间天数
            """
            self.handler = handler                                  #handler接收tornado.web.RequestHandler的self对象，也就是继承RequestHandler对象
            self.random_str = None                                  #初始化随机密串
            self.gqshijian = gqshijian                              #获取设置cookie过期时间
    
        def __genarate_random_str(self):                            #生成随机密串
            import hashlib                                          #导入md5加密模块
            import time                                             #导入时间模块
            obj = hashlib.md5()                                     #创建md5加密对象
            obj.update(bytes(str(time.time()), encoding='utf-8'))   #获取系统当前时间，进行md5加密
            random_str = obj.hexdigest()                            #获取加密后的md5密串
            return random_str                                       #返回加密后的md5密串
    
        def __setitem__(self, key,value):                                   #当创建Session对象，后面跟着[xxx]=xxx的时候自动执行并且接收[xxx]=xxx的值
            """
            使用方法：Session对象[xxx]=xxx
            功能：随机生成密串写入cookie，接收自定义用户数据，添加到cookie密串对应的字典里
            """
            # 在container中加入随机字符串
            # 定义专属于自己的数据
            # 在客户端中写入随机字符串
            # 判断，请求的用户是否已有随机字符串
            if not self.random_str:                                         #判断初始化密串不存在
                random_str = self.handler.get_cookie('xr_cookie')          #获取客服端浏览器get_cookie里的密串
                if not random_str:                                          #判断客服端浏览器get_cookie里如果没有密串
                    random_str = self.__genarate_random_str()               #执行密串生成方法，生成密串
                    container[random_str] = {}                              #在container字典里添加一个，密串作为键，值为空字典的元素
                else:                                                       #如果客服端浏览器get_cookie里有密串
                    # 客户端有随机字符串
                    if random_str in container.keys():                      #判断密串在container字典的键里是否存在
                        pass                                                #如果存在什么都不做
                    else:                                                   #如果不存在
                        random_str = self.__genarate_random_str()           #重新生成密串
                        container[random_str] = {}                          #在container字典里添加一个，密串作为键，值为空字典的元素
                self.random_str = random_str                                #将密串赋值给，初始化密串
            # 如果用户密串初始化就存在，说明登录过并且cookie和container字典里都存在
            container[self.random_str][key] = value                                                     #找到container字典里键为密串的元素值是一个字典，将接收到的key作为键，value作为值添加到元素字典里
            self.handler.set_cookie("xr_cookie", self.random_str,expires_days = self.gqshijian)        #将密串作为cookie值，向浏览器写入cookie
    
        def __getitem__(self,key):                                          #当创建Session对象，后面跟着[xxx]自动执行，并接收[xxx]的值
            """
            使用方法：Session对象[xxx]
            功能：获取cookie对应字典里，键为接收到参数的值，存在返回值，不存在返回None
            """
            # 获取客户端的随机字符串
            # 从container中获取专属于我的数据
            #  专属信息【key】
            random_str =  self.handler.get_cookie("xr_cookie")             #获取cookie里的密串
            if not random_str:                                              #判断cookie里的密串如果不存在
                return None                                                 #返回None
            # 客户端有随机字符串
            user_info_dict = container.get(random_str,None)                 #在container字典里找到密串对应的元素
            if not user_info_dict:                                          #如果container字典里没有密串对应的元素
                return None                                                 #返回None
            #如果cookie里的密串存在，并且container字典里也存在密串对应的元素
            value = user_info_dict.get(key, None)                           #接收用户传来的值，将值作为键找到字典里对应的值
            return value                                                    #返回值
[/code]

**框架引擎**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import session_lei                              #导入session模块
    
    
    
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self):                               #get()方法，接收get方式请求
            session = session_lei.Session(self,1)    #创建session对象，cookie保留1天
            if session['zhuangtai'] == True:         #判断session里的zhuangtai等于True
                self.render("index.html")            #显示查看页面
            else:
                self.redirect("/dlu")                #跳转到登录页面
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            session = session_lei.Session(self,1)    #创建session对象，cookie保留1天
            if session['zhuangtai'] == True:         #判断session里的zhuangtai等于True
                self.redirect("/index")              #跳转到查看页面
            else:
                self.render("dlu.html",tishi = '请登录')  #打开登录页面
        def post(self):
            yhm = self.get_argument('yhm')               #接收用户提交的用户名
            mim = self.get_argument('mim')               #接收用户提交的密码
            if yhm == 'admin' and mim == 'admin':        #判断用户名和密码
                session = session_lei.Session(self,1)    #创建session对象，cookie保留1天
                session['yhm'] = yhm                     #将用户名保存到session
                session['mim'] = mim                     #将密码保存到session
                session['zhuangtai'] = True              #在session写入登录状态
                self.redirect("/index")                  #跳转查看页面
            else:
                self.render("dlu.html",tishi = '用户名或密码错误') #打开登录页面
    
    settings = {                                        #html文件归类配置，设置一个字典
        "template_path":"views",                     #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                         #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index", indexHandler),                   #判断用户请求路径后缀是否匹配字符串index,如果匹配执行MainHandler方法
        (r"/dlu", dluHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**登录页面**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <h1>请登录</h1>
        <form method="post" action="/dlu">
            用户名<input type="text" name="yhm"/>
            密码<input type="text" name="mim"/>
            <input type="submit" value="提交"/><p style="color: #ff201e">{{tishi}}</p>
        </form>
    </body>
    </html>
[/code]

**登录后查看页面**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>测试网站</title>
        <link rel="stylesheet" href='{{static_url("muban.css")}}'>     <!--接收被继承页面的css连接-->
    </head>
    <body>
    登录后才能查看的信息
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170524231923341-2059470155.gif)



