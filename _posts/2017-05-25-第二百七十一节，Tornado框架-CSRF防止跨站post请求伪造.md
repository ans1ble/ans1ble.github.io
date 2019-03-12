
---
layout: post
title: " 第二百七十一节，Tornado框架-CSRF防止跨站post请求伪造 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Tornado框架- CSRF防止跨站post请求伪造**

****CSRF **是什么******

********CSRF是用来在post请求时做请求验证的，防止 **跨站post请求伪造**********

**********当用户访问一个表单页面时，会自动在表单添加一个隐藏的input标签，name="_xsrf"，value="等于一个密串"**********

**********当用户post请求提交数据时，会将 ** ** ** **
**_xsrf的密串提交到后台，后台会判断这个密串存在就允许提交数据，否则不允许提交********************

********************进行 **CSRF验证只需要两步**********************



**********************1、在框架配置字典里开启 **CSRF验证，开启后会自动接收post传来的 ** ** ** ** ** **
** ** ** **_xsrf密串判断是否合法********************************************

************************"xsrf_cookies":True   ** ** ** ** ** ** ** ** ** **
**开启 **CSRF验证，开启后会自动接收post传来的 ** ** ** ** ** ** ** ** **
**_xsrf密串判断是否合法********************************************************************

********************************************************************2、在HTML页面，用模板语言接收添加
** ** ** ** ** ** ** ** ** ** **
**CSRF密串********************************************************************************************

********************************************************************************************{%
raw xsrf_form_html()%} ** ** ** **
**当用户访问一个表单页面时，会自动在表单添加一个隐藏的input标签，name="_xsrf"，value="等于一个密串"******************************************************************************************************

******************************************************************************************************框架引擎******************************************************************************************************

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import session_lei                                              #导入session模块
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("dlu.html")
        def post(self):
            pass
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
        "xsrf_cookies":True
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/dlu", dluHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**html**

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
            {% raw xsrf_form_html()%}
            用户名<input type="text" name="yhm"/><br/><br/>
            密码<input type="text" name="mim"/><br/><br/>
            验证码<input type="text" name="yanzhma"/><br/><br/>
            <input type="submit" value="提交"/>
        </form>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170525232548154-1755444283.png)







**ajax的post请求CSRF验证**

**当html页面 ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** **{% raw
xsrf_form_html()%}生成密串时，会自动将密串写入浏览器的一个cookie**********************************************************************************************

**********************************************************************************************用jquery.cookie插件获取CSRF验证的cookie**********************************************************************************************

**********************************************************************************************在用jquery的ajax请求将
** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**cookie传输到路由映射，就会自动通过验证********************************************************************************************************************************************************************************************

********************************************************************************************************************************************************************************************框架引擎********************************************************************************************************************************************************************************************

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import session_lei                                              #导入session模块
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("dlu.html")
        def post(self):
            self.write("Hello, world")
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
        "xsrf_cookies":True
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/dlu", dluHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <script type="text/javascript" src='{{static_url("jquery.min.js")}}' charset="UTF-8"></script>
        <script type="text/javascript" src='{{static_url("jquery.cookie.js")}}' charset="UTF-8"></script>
    </head>
    <body>
    <h1>请登录</h1>
        <form method="post" action="/dlu">
            {% raw xsrf_form_html()%}
            用户名<input type="text" name="yhm"/><br/><br/>
            密码<input type="text" name="mim"/><br/><br/>
            验证码<input type="text" name="yanzhma"/><br/><br/>
            <input type="button" value="提交" onclick="csrf();"/>
        </form>
        <script type="text/javascript">
            function csrf() {
                var hacsrf = $.cookie('_xsrf');       //jquery.cookie插件获取CSRF验证的cookie
                $.ajax({                              //jquery的ajax请求
                    type: 'POST',
                    url: '/dlu',
                    data: {'_xsrf':hacsrf},           //将CSRF验证的cookie值提交到路由映射，就会自动通过验证
                    success: function (response, status, xhr) {
                        //请求完成后自动执行
                    }
                });
            }
        </script>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170526095451982-1651480513.png)



