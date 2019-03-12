
---
layout: post
title: " 第二百七十节，Tornado框架-生成验证码图片，以及验证码结合Session验证 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Tornado框架-生成验证码图片，以及验证码结合Session验证**



**第一、生成验证码图片**

**  生成验证码图片需要两个必须模块**

**1、python自带的 random(随机模块)**

**2、** **Pillow()图像处理模块 里的PIL(图像库)，为第三方模块，需要安装**



**封装验证码图片生成插件py**

**在封装文件里先导入 **random(随机模块) ，和 **Pillow()图像处理模块里的所需py文件******

********封装验证码图片生成插件功能，调用后返回 验证码图片，和字符串类型验证码，两个返回值********

********注意：验证码需要一个字体文件，这个字体文件必须和封装创建放在一起********

********验证码图片生成插件py********

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import random
    from PIL import Image, ImageDraw, ImageFont, ImageFilter
    
    _letter_cases = "abcdefghjkmnpqrstuvwxy"  # 小写字母，去除可能干扰的i，l，o，z
    _upper_cases = _letter_cases.upper()  # 大写字母
    _numbers = ''.join(map(str, range(3, 10)))  # 数字
    init_chars = ''.join((_letter_cases, _upper_cases, _numbers))
    
    def create_validate_code(size=(120, 30),
                             chars=init_chars,
                             img_type="GIF",
                             mode="RGB",
                             bg_color=(255, 255, 255),
                             fg_color=(0, 0, 255),
                             font_size=18,
                             font_type="Monaco.ttf",
                             length=4,
                             draw_lines=True,
                             n_line=(1, 2),
                             draw_points=True,
                             point_chance = 2):
        '''
        @todo: 生成验证码图片
        @param size: 图片的大小，格式（宽，高），默认为(120, 30)
        @param chars: 允许的字符集合，格式字符串
        @param img_type: 图片保存的格式，默认为GIF，可选的为GIF，JPEG，TIFF，PNG
        @param mode: 图片模式，默认为RGB
        @param bg_color: 背景颜色，默认为白色
        @param fg_color: 前景色，验证码字符颜色，默认为蓝色#0000FF
        @param font_size: 验证码字体大小
        @param font_type: 验证码字体，默认为 ae_AlArabiya.ttf
        @param length: 验证码字符个数
        @param draw_lines: 是否划干扰线
        @param n_lines: 干扰线的条数范围，格式元组，默认为(1, 2)，只有draw_lines为True时有效
        @param draw_points: 是否画干扰点
        @param point_chance: 干扰点出现的概率，大小范围[0, 100]
        @return: [0]: PIL Image实例
        @return: [1]: 验证码图片中的字符串
        '''
    
        width, height = size # 宽， 高
        img = Image.new(mode, size, bg_color) # 创建图形
        draw = ImageDraw.Draw(img) # 创建画笔
    
        def get_chars():
            '''生成给定长度的字符串，返回列表格式'''
            return random.sample(chars, length)
    
        def create_lines():
            '''绘制干扰线'''
            line_num = random.randint(*n_line) # 干扰线条数
    
            for i in range(line_num):
                # 起始点
                begin = (random.randint(0, size[0]), random.randint(0, size[1]))
                #结束点
                end = (random.randint(0, size[0]), random.randint(0, size[1]))
                draw.line([begin, end], fill=(0, 0, 0))
    
        def create_points():
            '''绘制干扰点'''
            chance = min(100, max(0, int(point_chance))) # 大小限制在[0, 100]
    
            for w in range(width):
                for h in range(height):
                    tmp = random.randint(0, 100)
                    if tmp > 100 - chance:
                        draw.point((w, h), fill=(0, 0, 0))
    
        def create_strs():
            '''绘制验证码字符'''
            c_chars = get_chars()
            strs = ' %s ' % ' '.join(c_chars) # 每个字符前后以空格隔开
    
            font = ImageFont.truetype(font_type, font_size)
            font_width, font_height = font.getsize(strs)
    
            draw.text(((width - font_width) / 3, (height - font_height) / 3),
                        strs, font=font, fill=fg_color)
    
            return ''.join(c_chars)
    
        if draw_lines:
            create_lines()
        if draw_points:
            create_points()
        strs = create_strs()
    
        # 图形扭曲参数
        params = [1 - float(random.randint(1, 2)) / 100,
                  0,
                  0,
                  0,
                  1 - float(random.randint(1, 10)) / 100,
                  float(random.randint(1, 2)) / 500,
                  0.001,
                  float(random.randint(1, 2)) / 500
                  ]
        img = img.transform(size, Image.PERSPECTIVE, params) # 创建扭曲
    
        img = img.filter(ImageFilter.EDGE_ENHANCE_MORE) # 滤镜，边界加强（阈值更大）
    
        return img, strs  #返回验证码图片，和字符串类型验证码
[/code]

********验证码图片生成插件py使用方法********

********在验证码HTML的，img标签的src图片地址，路由映射的逻辑处理函数里使用********

********首先在要显示验证码图片的html， **img标签的src="/yanzhma"，一个路由映射路径**********

********html********

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
            用户名<input type="text" name="yhm"/><br/><br/>
            密码<input type="text" name="mim"/><br/><br/>
            验证码<input type="text" name="yanzhma"/><br/><br/>
            <img **src ="/yanzhma"**><br/><br/>
            <input type="submit" value="提交"/>
        </form>
    </body>
    </html>
[/code]

**在框架引擎，配置这个验证码图片src路由映射路径，和逻辑处理函数**

**********src路由映射路径的逻辑处理函数里使用验证码图片生成插件**********

**********需要导入 io模块，和，生成验证码图片插件py**********

**********框架引擎**********

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                              #导入tornado模块下的web文件
    import session_lei                              #导入session模块
    
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            self.render("dlu.html")  #打开登录页面
        def post(self):
            yhm = self.get_argument('yhm')               #接收用户提交的用户名
            mim = self.get_argument('mim')               #接收用户提交的密码
    
    class yanzhmaHandler(tornado.web.RequestHandler):
        def get(self):
            #生成图片并且返回
            import io                                       #导入io模块
            import check_code                               #导入验证码图片生成插件
            mstream = io.BytesIO()                          #创建一个BytesIO临时保存生成图片数据
            img,code = check_code.create_validate_code()    #执行图片生成插进里的check_code.create_validate_code类，返回验证码图片生成数据，和字符串验证码
            img.save(mstream,"PNG")                         #将返回的验证码图片数据，添加到BytesIO临时保存
            self.write(mstream.getvalue())                  #从BytesIO临时保存，获取图片返回给img的 src= 进行显示
    
    settings = {                                        #html文件归类配置，设置一个字典
        "template_path":"views",                     #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                         #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([         #创建一个变量等于tornado.web下的Application方法
        (r"/dlu", dluHandler),
        (r"/yanzhma", yanzhmaHandler),
    ],**settings)                                   #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                    #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170525121912279-283877150.png)

**利用js实现，点击图片刷新验证码，也就是点击一下发送一次验证码请求**

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
            用户名<input type="text" name="yhm"/><br/><br/>
            密码<input type="text" name="mim"/><br/><br/>
            验证码<input type="text" name="yanzhma"/><br/><br/>
            <img src="/yanzhma" onclick='ChangeCode();' id='imgCode'><br/><br/>
            <input type="submit" value="提交"/>
        </form>
        <script type="text/javascript">
    
            function ChangeCode() {
                var code = document.getElementById('imgCode');
                code.src += '?';
            }
        </script>
    
    </body>
    </html>
[/code]







**第二、验证码结合Session验证**

**也就是在导入Session模块，将字符串验证码写入用户的 **Session里，然后判断用户输入的验证码和 **
**Session里的验证码是否一致********



[code]

    #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import session_lei                                              #导入session模块
    
    class indexHandler(tornado.web.RequestHandler):
        def get(self):
            session = session_lei.Session(self, 1)                  #创建session对象，cookie保留1天
            zhuangti = session['zhuangtai']                         #获取用户cookie对应字典里的zhuangtai
            if zhuangti == True:                                    #判断zhuangtai是否等于True
                self.render("index.html")                           #说明登陆了显示查看页
            else:
                self.redirect('/dlu')                               #跳转登录页
    
    class dluHandler(tornado.web.RequestHandler):
        def get(self):
            session = session_lei.Session(self, 1)                  #创建session对象，cookie保留1天
            zhuangti = session['zhuangtai']                         #获取用户cookie对应字典里的zhuangtai
            if zhuangti == True:                                    #判断zhuangtai是否等于True
                self.redirect("/index")                             #说明登陆了跳转查看页
            else:
                self.render("dlu.html",tishi = '')                      #打开登录页面
        def post(self):
            yhm = self.get_argument('yhm')                          #接收用户提交的用户名
            mim = self.get_argument('mim')                          #接收用户提交的密码
            if yhm == "admin" and mim == "admin":                   #判断用户名和密码
                session = session_lei.Session(self, 1)              # 创建session对象，cookie保留1天
                session['yhm'] = yhm                                # 将用户名保存到session
                session['mim'] = mim                                # 将密码保存到session
                session['zhuangtai'] = True                         # 在session写入登录状态
                shur_yzhm = self.get_argument('yanzhma').upper()    #获取用户输入验证码，转换成大写
                session_yzhm = session['yanzhma'].upper()           #获取session里的验证码，转换成大写
                if shur_yzhm == session_yzhm:                       #判断用户输入的验证码，和session里的验证码是否一致
                    self.redirect("/index")                         #跳转查看页
                else:
                    self.render("dlu.html", tishi="验证码不正确")
            else:
                self.render("dlu.html",tishi = "用户名或密码不正确")
    
    class yanzhmaHandler(tornado.web.RequestHandler):
        def get(self):
            #生成图片并且返回
            import io                                       #导入io模块
            import check_code                               #导入验证码图片生成插件
            mstream = io.BytesIO()                          #创建一个BytesIO临时保存生成图片数据
            img,code = check_code.create_validate_code()    #执行图片生成插进里的check_code.create_validate_code类，返回验证码图片生成数据，和字符串验证码
            img.save(mstream,"PNG")                         #将返回的验证码图片数据，添加到BytesIO临时保存
            self.write(mstream.getvalue())                  #从BytesIO临时保存，获取图片返回给img的 src= 进行显示
            session = session_lei.Session(self, 1)          # 创建session对象，cookie保留1天
            session['yanzhma'] = code                       #将字符串验证码添加到session里
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/dlu", dluHandler),
        (r"/yanzhma", yanzhmaHandler),
        (r"/index", indexHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8888)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]



