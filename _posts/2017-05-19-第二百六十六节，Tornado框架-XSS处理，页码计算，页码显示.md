
---
layout: post
title: " 第二百六十六节，Tornado框架-XSS处理，页码计算，页码显示 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Tornado框架-XSS处理，页码计算，页码显示**



**Tornado框架-XSS攻击过滤**

**注意： **Tornado框架的模板语言，读取数据已经自动处理了 **XSS攻击，过滤转换了危险字符******

******如果要使危险字符可以远行，就需要在模板语言接收数据的地方 {% raw 接收数据变量 %}******

******raw写在模板语言里，用{% raw 接收变量%}，让接收到的数据如果有html标签等进行原始显示，也就是可以运行，分页会用到******

******框架引擎******

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
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index/(?P<page>\d*)", index.indexHandler),    #正则匹配访问路径，访问录index/后面可以是可以是0个或多个数字
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
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
    SHUJU = [
        {"user":"lgx","emia":"729088188@qq.com"}
    ]
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
            #接收路由映射正则名称page，也就是用户访问的后缀，也就是访问的页码
            #假如每页显示5条信息，page就是当前页
            #第一页就应该获取SHUJU全局变量里的0-5条
            #第二页就应该获取SHUJU全局变量里的5-10条
    
            #换算页码获取数据范围的公式
            #当前页码减去1乘以显示条数=当前页获取数据的起始条数，也就是从第几条开始获取
            #当前页码乘以显示条数=当前页获取数据的结束条数，也就是从第几条结束获取
    
            try:                                        #尝试执行
                page = int(page)                        #将页码转换成数字类型
            except:                                     #如果出错
                page = 1                                #将页码等于1
            if page < 1:                                #判断页面如果小于1
                page = 1                                #页码等于1
    
            kaishi = (page - 1) * 5                     #当前页码获取数据起始位置
            jieshu = page * 5                           #当前页码获取数据结束位置
            xianshi = SHUJU[kaishi:jieshu]              #通过起始和结束位置以下标方式获取指定范围的列表数据
    
            self.render("index.html",shuju = xianshi,yema = page)   #显示index.html文件，通过起始和结束位置以下标方式获取指定范围的数据传入模板，传值页码
    
        def post(self,page):
            user = self.get_argument("user")            #接收用户提交的用户名
            emia = self.get_argument("emia")            #接收用户提交的邮箱
            temp = {"user":user,"emia":emia}            #将邮箱和用户名组合成字典，
            SHUJU.append(temp)                          #将字典追加到SHUJU全局变量
            self.redirect("/index/" + page)             #跳转到当前页面
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" href='{{static_url("s1.css")}}'>
    </head>
    <body>
    <h1>提交数据</h1>
    <form method="post" action="/index/{{yema}}">
        用户名：<input name="user" type="text"/>
        邮箱：<input name="emia" type="text"/>
        <input type="submit" value="提交"/>
    </form>
    <h1>显示数据</h1>
    <table border="1">
        <thead>
            <tr>
                <th>用户名</th>
                <th>邮箱</th>
            </tr>
        </thead>
        <tbody>
            <!--循环接收到的shuju显示到表格-->
            {% for i in shuju %}
                <tr>
                    <td>{{i["user"]}}</td>
                    <td>{% **raw** i["emia"] %} </td>
                </tr>
            {% end %}
        </tbody>
    </table>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170519201353432-30752661.png)

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170519201429572-484461957.png)**





**计算页码**  
 **第一步、数据总量除以显示条数，取余，两个变量接收，第一个变量得到相除后的整数，后一个变量得到相除后的余数(小数)**  
 **1、判断余数如果大于0，页面数等于整数加1，等于分页总量**  
 **第二步、定义一个列表接收分页数据**  
 **1、根据分页总量循环次数**  
 **2、判断循环到的页码等于当前页面，格式化当前页码设置样式**  
 **3、否则格式化当前页码，将格式化的页码数据追加到列表**  
 **4、将列表连接长一串字符串**  
 **5、将字符串传递到html模板**  
 **第三步、在html模板接收传递过来的字符串**

**模板引擎**

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
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index/(?P<page>\d*)", index.indexHandler),    #正则匹配访问路径，访问录index/后面可以是可以是0个或多个数字
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
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
    SHUJU = [
        {"user":"lgx","emia":"729088188@qq.com"}
    ]
    for f in range(300):
        SHUJU.append({"user": "lgx", "emia": "729088188@qq.com"})   #填充数据到300条
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
            #接收路由映射正则名称page，也就是用户访问的后缀，也就是访问的页码
            #假如每页显示5条信息，page就是当前页
            #第一页就应该获取SHUJU全局变量里的0-5条
            #第二页就应该获取SHUJU全局变量里的5-10条
    
            #换算页码获取数据范围的公式
            #当前页码减去1乘以显示条数=当前页获取数据的起始条数，也就是从第几条开始获取
            #当前页码乘以显示条数=当前页获取数据的结束条数，也就是从第几条结束获取
    
            try:                                        #尝试执行
                page = int(page)                        #将页码转换成数字类型
            except:                                     #如果出错
                page = 1                                #将页码等于1
            if page < 1:                                #判断页面如果小于1
                page = 1                                #页码等于1
    
            kaishi = (page - 1) * 5                     #当前页码获取数据起始位置
            jieshu = page * 5                           #当前页码获取数据结束位置
            xianshi = SHUJU[kaishi:jieshu]              #通过起始和结束位置以下标方式获取指定范围的列表数据
    
    
            #计算页码显示
            zyema,c = divmod(len(SHUJU),5)              #数据总量除以显示条数，取余，两个变量接收，第一个变量得到相除后的整数，后一个变量得到相除后的余数(小数)
            if c > 0:                                   #判断余数如果大于0，
                zyema += 1                              #页面数等于整数加1，等于分页总量
    
            yema = []                                   #定义一个列表接收分页数据
            for i in range(zyema):                      #根据分页总量循环次数
                if i+1 == page:                         #判断循环到的页码等于当前页面
                    temp = '<li class="yem"><a href="/index/%s">%s</a></li>' % (i+1,i+1)    #格式化当前页码设置样式
                else:
                    temp = '<li><a href="/index/%s">%s</a></li>' % (i + 1, i + 1)           #格式化当前页码
                yema.append(temp)                                                           #将格式化的页码数据追加到列表
                zfpage = "".join(yema)                                                      #将列表连接长一串字符串
    
            self.render("index.html",shuju = xianshi,yema = page,zfpage = zfpage)   #显示index.html文件，传递当前页码，传递分页显示页码
    
        def post(self,page):
            user = self.get_argument("user")            #接收用户提交的用户名
            emia = self.get_argument("emia")            #接收用户提交的邮箱
            temp = {"user":user,"emia":emia}            #将邮箱和用户名组合成字典，
            SHUJU.append(temp)                          #将字典追加到SHUJU全局变量
            self.redirect("/index/" + page)             #跳转到当前页面
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" href='{{static_url("s1.css")}}'>
    </head>
    <body>
    <h1>提交数据</h1>
    <form method="post" action="/index/{{yema}}">
        用户名：<input name="user" type="text"/>
        邮箱：<input name="emia" type="text"/>
        <input type="submit" value="提交"/>
    </form>
    <h1>显示数据</h1>
    <table border="1">
        <thead>
            <tr>
                <th>用户名</th>
                <th>邮箱</th>
            </tr>
        </thead>
        <tbody>
            <!--循环接收到的shuju显示到表格-->
            {% for i in shuju %}
                <tr>
                    <td>{{i["user"]}}</td>
                    <td>{% raw i["emia"] %}</td>
                </tr>
            {% end %}
        </tbody>
    </table>
    <ul class="fy">
        {% raw zfpage %}
    </ul>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170520071335307-155538133.png)





**页码显示**

**计算每页显示多少个页码**  
 **假设每页显示11个页码，当前页的前5个和后5个**  
 **所以需要动态调整循环里的值**

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
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/index/(?P<page>\d*)", index.indexHandler),    #正则匹配访问路径，访问录index/后面可以是可以是0个或多个数字
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
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
    SHUJU = [
        {"user":"lgx","emia":"729088188@qq.com"}
    ]
    for f in range(300):
        SHUJU.append({"user": "lgx", "emia": "729088188@qq.com"})   #填充数据到300条
    
    #逻辑处理
    
    class indexHandler(tornado.web.RequestHandler):  #定义一个类，继承tornado.web下的RequestHandler类
        def get(self,page):                                              #get()方法，接收get方式请求
            #接收路由映射正则名称page，也就是用户访问的后缀，也就是访问的页码
            #假如每页显示5条信息，page就是当前页
            #第一页就应该获取SHUJU全局变量里的0-5条
            #第二页就应该获取SHUJU全局变量里的5-10条
    
            #换算页码获取数据范围的公式
            #当前页码减去1乘以显示条数=当前页获取数据的起始条数，也就是从第几条开始获取
            #当前页码乘以显示条数=当前页获取数据的结束条数，也就是从第几条结束获取
    
            try:                                        #尝试执行
                page = int(page)                        #将页码转换成数字类型
            except:                                     #如果出错
                page = 1                                #将页码等于1
            if page < 1:                                #判断页面如果小于1
                page = 1                                #页码等于1
    
            kaishi = (page - 1) * 5                     #当前页码获取数据起始位置
            jieshu = page * 5                           #当前页码获取数据结束位置
            xianshi = SHUJU[kaishi:jieshu]              #通过起始和结束位置以下标方式获取指定范围的列表数据
    
    
            #计算页码显示
            zyema,c = divmod(len(SHUJU),5)              #数据总量除以显示条数，取余，两个变量接收，第一个变量得到相除后的整数，后一个变量得到相除后的余数(小数)
            if c > 0:                                   #判断余数如果大于0，
                zyema += 1                              #页面数等于整数加1，等于分页总量
    
            yema = []                                   #定义一个列表接收分页数据
    
            #计算每页显示多少个页码
            #假设每页显示11个页码，当前页的前5个和后5个
            #所以需要动态调整循环里的值
            if zyema < 11:                      #判断总页码小于11
                s = 1                           #起始页码为1
                t = zyema                       #结束页码为总页码
            else:
                if page <= 6:                   #判断当前页码小于等于6
                    s = 1                       #起始页码为1
                    t = 11                      #结束页码为11
                else:
                    if (page + 5) > zyema:      #判断当前页加5如果大于总页数
                        s = zyema - 10          #起始页为总页数减以10
                        t = zyema               #结束页为总页数
                    else:
                        s = page - 5            #起始页为当前页减以5
                        t = page + 5            #结束页为当前页加5
    
            for i in range(s,t+1):                      #根据分页总量循环次数
                if i == page:                         #判断循环到的页码等于当前页面
                    temp = '<li class="yem"><a href="/index/%s">%s</a></li>' % (i,i)    #格式化当前页码设置样式
                else:
                    temp = '<li><a href="/index/%s">%s</a></li>' % (i, i)           #格式化当前页码
                yema.append(temp)                                                           #将格式化的页码数据追加到列表
                zfpage = "".join(yema)                                                      #将列表连接长一串字符串
    
            self.render("index.html",shuju = xianshi,yema = page,zfpage = zfpage)   #显示index.html文件，传递当前页码，传递分页显示页码
    
        def post(self,page):
            user = self.get_argument("user")            #接收用户提交的用户名
            emia = self.get_argument("emia")            #接收用户提交的邮箱
            temp = {"user":user,"emia":emia}            #将邮箱和用户名组合成字典，
            SHUJU.append(temp)                          #将字典追加到SHUJU全局变量
            self.redirect("/index/" + page)             #跳转到当前页面
[/code]

**html**



[code]

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" href='{{static_url("s1.css")}}'>
    </head>
    <body>
    <h1>提交数据</h1>
    <form method="post" action="/index/{{yema}}">
        用户名：<input name="user" type="text"/>
        邮箱：<input name="emia" type="text"/>
        <input type="submit" value="提交"/>
    </form>
    <h1>显示数据</h1>
    <table border="1">
        <thead>
            <tr>
                <th>用户名</th>
                <th>邮箱</th>
            </tr>
        </thead>
        <tbody>
            <!--循环接收到的shuju显示到表格-->
            {% for i in shuju %}
                <tr>
                    <td>{{i["user"]}}</td>
                    <td>{% raw i["emia"] %}</td>
                </tr>
            {% end %}
        </tbody>
    </table>
    <ul class="fy">
        {% raw zfpage %}
    </ul>
    </body>
    </html>
[/code]





** **



