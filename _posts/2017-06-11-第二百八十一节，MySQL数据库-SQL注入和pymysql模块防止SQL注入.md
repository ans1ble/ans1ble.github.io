
---
layout: post
title: " 第二百八十一节，MySQL数据库-SQL注入和pymysql模块防止SQL注入 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**MySQL数据库-SQL注入和pymysql模块防止SQL注入**

****SQL注入就是通过 **SQL语句绕开程序判断，获取到数据库的内容******

******下面以一个简单的程序登录 ** ** **SQL注入举例：************

************正常登录************

************1、数据库有一张会员表************

************![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611164151637-393515660.png)************



**2、用户输入账号和密码，到数据库查找此用户是否存在，存在登录成功，不存在登录失败**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611164508403-882566367.png)**



[code]

    #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import pymysql                                                  #导入数据库模块
    
    class khdHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("khd.html")
        def post(self):
            yhm = self.get_argument('yhm')  #接收用户名
            mim = self.get_argument('mim')  #接收密码
    
            #连接数据库
            conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
            # 创建游标
            cursor = conn.cursor()
    
            temp = "select yhm from yhxx where yhm='%s' and mim='%s'"%(yhm,mim) #字符串拼接SQL查询语句
            print(temp)
    
            # 执行SQL，并返回收影响行数
            effect_row = cursor.execute(temp)
    
            shuju = cursor.fetchall()  # 获取游标里的数据
            print(shuju)
            # 提交，不然无法保存新建或者修改的数据
            # conn.commit()
    
            # 关闭游标
            cursor.close()
            # 关闭连接
            conn.close()
            
            
            if shuju:                       #判断数据库存在用户
                self.write('登录成功')       #登录成功
            else:                           #数据库不存在用户
                self.write('登录失败')       #登录失败
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/khd", khdHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8002)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]



**3、正常登录**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611165419106-739911360.png)

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import pymysql                                                  #导入数据库模块
    
    class khdHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("khd.html")
        def post(self):
            yhm = self.get_argument('yhm')  #接收用户名
            mim = self.get_argument('mim')  #接收密码
    
            #连接数据库
            conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
            # 创建游标
            cursor = conn.cursor()
    
            temp = "select yhm from yhxx where yhm='%s' and mim='%s'"%(yhm,mim) #字符串拼接SQL查询语句
            print(temp)
    
            # 执行SQL，并返回收影响行数
            effect_row = cursor.execute(temp)
    
            shuju = cursor.fetchall()  # 获取游标里的数据
            print(shuju)
            # 提交，不然无法保存新建或者修改的数据
            # conn.commit()
    
            # 关闭游标
            cursor.close()
            # 关闭连接
            conn.close()
    
    
            if shuju:                       #判断数据库存在用户
                self.write('登录成功')       #登录成功
            else:                           #数据库不存在用户
                self.write('登录失败')       #登录失败
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/khd", khdHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8002)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**实际SQL查询语句**

[code]

     select yhm from yhxx where yhm='张三' and mim='123456'
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611165753075-1023439970.png)

**数据库返回**

**(('张三',),) 返回了元祖类型的数据库查到的数据**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611170018778-512300142.png)





**SQL注入绕开密码**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611170222418-277368922.png)**

****实际SQL查询语句****

[code]

     select yhm from yhxx where yhm='张三' -- j' and mim='789'
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611170915762-1270462474.png)**

**可以看到实际用户密码已经被注释了，也就不起作用了，只要用户名存在就可以登录，对于密码已经失效**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611170740622-1155524743.png)**



****SQL注入绕开用户名和密码****

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611171050903-984944148.png)**

****实际SQL查询语句****

[code]

     -- 查询yhxx表的yhm字典等于张飞，或者 1 = 1，即使yhm字段没有张飞，也能查询到所有数据
    select yhm from yhxx where yhm='张飞' or 1 = 1 -- d' and mim='789'
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611171537747-202898305.png)

**可以看到实际 **SQL查询语句，已经绕开了用户名和密码，直接获取了全部数据****

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611172035215-1263755824.png)**





**pymysql模块防止SQL注入**

****pymysql模块的execute()方法，的参数2 字符串占位符变量，在参数2格式化 **SQL语句字符串，会自动调用
**pymysql模块里的mogrify()方法，将第二个参数的字符串里含有'号转化成\号，这样就防止了 **SQL注入**********

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import pymysql                                                  #导入数据库模块
    
    class khdHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("khd.html")
        def post(self):
            **yhm** = self.get_argument('yhm')  #接收用户名
            **mim** = self.get_argument( 'mim')  #接收密码
    
            #连接数据库
            conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
            # 创建游标
            cursor = conn.cursor()
    
            #查看execute()方法调用的mogrify()方法，将接收到的数据，会把有'转换成\
            quer = cursor.mogrify("select yhm from yhxx where yhm=%s and mim=%s", **(yhm,mim))** print(quer)
    
    
            # 执行SQL，并返回收影响行数
            effect_row = cursor.execute("select yhm from yhxx where yhm=%s and mim=%s", **(yhm,mim))**
             shuju = cursor.fetchall()  # 获取游标里的数据
            print(shuju)
            # 提交，不然无法保存新建或者修改的数据
            # conn.commit()
    
            # 关闭游标
            cursor.close()
            # 关闭连接
            conn.close()
    
    
            if shuju:                       #判断数据库存在用户
                self.write('登录成功')       #登录成功
            else:                           #数据库不存在用户
                self.write('登录失败')       #登录失败
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/khd", khdHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8002)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170611184751809-276986729.png)

**被mogrify()方法，转换后的实际SQL语句**

[code]

     select yhm from yhxx where yhm='张飞\' or 1 = 1 -- d' and mim='123456'
[/code]

**可以看到用户输入的'已经被转换成了\了，这样就防止了SQL注入**



