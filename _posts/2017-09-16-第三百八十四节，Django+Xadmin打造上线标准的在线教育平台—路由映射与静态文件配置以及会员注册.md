
---
layout: post
title: " 第三百八十四节，Django+Xadmin打造上线标准的在线教育平台—路由映射与静态文件配置以及会员注册 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十四节，Django+Xadmin打造上线标准的在线教育平台—路由映射与静态文件配置以及会员注册**



****基于类的路由映射****

[code]

     from django.conf.urls import url, include                   # 导入django自在的include逻辑
    from django.contrib import admin
    from django.views.generic import TemplateView               # 导入django自带的TemplateView逻辑
    
    import xadmin                                               # 导入xadmin
    
    from app_users.views import deng_lu, zhu_ce, active_code, logout                 # 导入登录逻辑处理类
    
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        url(r'^register.html', zhu_ce.as_view(), name='register'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
        url(r'^active/(?P<active_de>.*)/$', active_code.as_view(), name="user_active"),
    
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
        url(r'^logout', logout.as_view(), name='deng_lu'),
    ]
[/code]



**静态文件配置**

**settings.py**

[code]

    STATIC_URL =  '/static/'    # 设置静态文件前缀名称
    #配置静态文件目录
    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static'),   # 设置静态文件路径
    ]
[/code]



**html静态文件引用**

[code]

     <!DOCTYPE html>
    <html>
    {% load staticfiles %}      {# 启用静态文件引用 #}
    <head>
        <meta charset="UTF-8">
        <meta name="renderer" content="webkit">
        <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1" >
        <title>课程机构列表 - 慕学在线网</title>
        <link rel="stylesheet" type="text/css" href="{% static 'css/reset.css' %}">     {# 启用静态文件引用后才可以 #}
        <link rel="stylesheet" type="text/css" href="{% static 'css/animate.css' %}">
        <link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}">
        
        <script src="{% static 'js/jquery.min.js' %}" type="text/javascript"></script>
        <script src="{% static 'js/jquery-migrate-1.2.1.min.js' %}" type="text/javascript"></script>
    
    </head>
[/code]





**会员注册**

**1，首先路由映射好逻辑处理类**

[code]

     from django.conf.urls import url, include                   # 导入django自在的include逻辑
    from django.contrib import admin
    from django.views.generic import TemplateView               # 导入django自带的TemplateView逻辑
    
    import xadmin                                               # 导入xadmin
    
    from app_users.views import deng_lu, zhu_ce, active_code, logout                 # 导入登录逻辑处理类
    
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        url(r'^register.html', zhu_ce.as_view(), name='register'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
        url(r'^active/(?P<active_de>.*)/$', active_code.as_view(), name="user_active"),
    
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
        url(r'^logout', logout.as_view(), name='deng_lu'),
    ]
[/code]



  
**2，编写表单验证forms文件**

[code]

     from django import forms                 # 导入Django的表单验证模块
    from captcha.fields import CaptchaField
    
    
    class zhu_ce_forms(forms.Form):
        email = forms.EmailField(
            required=True,
            max_length=40,
            min_length=2,
            error_messages={
                'required': '邮箱名不能为空',
                'max_length': '邮箱名长度不得超过40个字符',
                'min_length': '邮箱名长度不得少于2个字符',
            }
        )
        password = forms.CharField(
            required=True,
            max_length=20,
            min_length=2,
            error_messages={
                'required': '密码不能为空',
                'max_length': '密码长度不得超过20个字符',
                'min_length': '密码长度不得少于2个字符',
            }
        )
        captcha = CaptchaField(
            required=True,
            error_messages={
                'required': '验证码不能为空',
                'invalid': '验证码不正确'
            }
        )
[/code]

  
  

  
**3，在逻辑处理类里将request.POST也就是用户提交的表单，放到表单类里验证，验证不通过返回提示信息，回填数据，验证通过获取验证通过的表单数据
（包括验证码验证，前后将）**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import io  # 导入io模块
    
    from django.shortcuts import render, HttpResponse, redirect                                 # 导入django向浏览器返回方法
    from django.views.generic.base import View
    from django.db.models import F,Q                                                            # 导入F和Q
    from django.contrib.auth.hashers import make_password, check_password                       # 导入django密码加密，和密码验证
    from django.contrib.auth import login                                                       # 调用django的登录函数
    
    from app_users.forms import deng_lu_forms, zhu_ce_forms                                    # 导入登录页面表单认证
    from app_users.models import Users, Email                                                   # 导入数据库操作
    from utils.email_send import send_register_email                                            # 导入邮件发送
    
    
    class zhu_ce(View):
        def get(self, request):
            yanzhm = zhu_ce_forms()
            return render(request, 'register.html', {'yanzhm': yanzhm})
    
      def post(self, request):
            f = zhu_ce_forms(request.POST)
            if f.is_valid():                                # 判断认证是否成功
                tong_guo = f.cleaned_data                   # 认证成功，接收用户数据
                email = tong_guo['email']
                password = tong_guo['password']else:                                           # 认证不成功，接收错误信息
                cuo_wu = f.errors                           # 接收错误信息
                print(cuo_wu)
                return render(request, 'register.html', {'cuo_wu': cuo_wu, 'yanzh': f})        # 将错误信息传到登录页面
[/code]





**4，将用户名拿到数据库，查找用户是否存在，用户存在提示信息回填数据，用户不存在说明可以注册，注意用户密码需要加密，可以用django密码加密函数make_password(要加密的密码)，然后将用户信息写入数据库**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import io  # 导入io模块
    
    from django.shortcuts import render, HttpResponse, redirect                                 # 导入django向浏览器返回方法
    from django.views.generic.base import View
    from django.db.models import F,Q                                                            # 导入F和Q
    from django.contrib.auth.hashers import make_password, check_password                       # 导入django密码加密，和密码验证
    from django.contrib.auth import login                                                       # 调用django的登录函数
    
    from app_users.forms import deng_lu_forms, zhu_ce_forms                                    # 导入登录页面表单认证
    from app_users.models import Users, Email                                                   # 导入数据库操作
    from utils.email_send import send_register_email                                            # 导入邮件发送
    
    
    class zhu_ce(View):
        def get(self, request):
            yanzhm = zhu_ce_forms()
            return render(request, 'register.html', {'yanzhm': yanzhm})
    
        def post(self, request):
            f = zhu_ce_forms(request.POST)
            if f.is_valid():                                # 判断认证是否成功
                tong_guo = f.cleaned_data                   # 认证成功，接收用户数据
                email = tong_guo['email']
                password = tong_guo['password']
                user = Users.objects.filter(username=email).values()
                if len(user) >= 1:
                    tishi = '用户已经存在'
                    return render(request, 'register.html', {'tishi': tishi, 'yanzh': f})
                else:
                    a = {'username': email,                                         # 将要写入的数据组合成字典，键为字段值为数据
                         'password': make_password(password),
                         'is_active': 0
                         }
                    Users.objects.create(**a)                                       # 添加到数据库，注意字典变量名称一定要加**
                    send_register_email(email)                                      # 执行验证邮件发送
                    return render(request, 'login.html')
            else:                                           # 认证不成功，接收错误信息
                cuo_wu = f.errors                           # 接收错误信息
                print(cuo_wu)
                return render(request, 'register.html', {'cuo_wu': cuo_wu, 'yanzh': f})        # 将错误信息传到登录页面
[/code]





**5，激活用户，自定义一个用户邮件激活函数，**  
 **在数据库专门用一张表来记录激活用户所需要的随机字符和邮箱等信息**  
 **当用户数据写入数据库后，随机生成一个字符**  
 **向用户激活表里写入当前的随机字符，和用户验证邮箱**  
 **然后向用户的邮箱发送一条激活连接，激活连接由域名加随机字符组成，然后提示用户到邮箱激活**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    from random import Random                       # 导入随机函数
    from django.core.mail import send_mail          # 导入django邮件函数
    
    from app_users.models import Email              # 导入激活操作数据库表
    from MxOnline.settings import DEFAULT_FROM_EMAIL
    
    
    def random_str(randomlength=8):
        """
        循环获取随机字符串，默认8位
        """
        str = ''
        chars = 'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz0123456789'
        length = len(chars) - 1
        random = Random()
        for i in range(randomlength):
            str+=chars[random.randint(0, length)]
        return str
    
    
    def send_register_email(email, send_type="register"):
        """
        发送邮件
        :接收两个参数：
        :第一个验证邮箱，第二个验证类型
        """
        """写入数据库验证信息"""
        email_record = Email()                              # 实例化数据库表
        if send_type == "update_email":
            code = random_str(4)                            # 生成4位随机数
        else:
            code = random_str(16)                           # 生成16位随机数
        email_record.code = code                            # 数据库写入验证随机数
        email_record.email = email                          # 数据库写入验证邮箱
        email_record.send_type = send_type                  # 数据库写入验证类型
        email_record.save()
    
        """发送验证邮件"""
        email_title = ""                                    # 记录邮件标题
        email_body = ""                                     # 记录邮件内容
    
        if send_type == "register":
            email_title = "慕学在线网注册激活链接"
            email_body = "请点击下面的链接激活你的账号: http://127.0.0.1:8000/active/{0}".format(code)
    
            send_status = send_mail(email_title, email_body, DEFAULT_FROM_EMAIL, [email])
            if send_status:
                pass
        elif send_type == "forget":
            email_title = "慕学在线网注册密码重置链接"
            email_body = "请点击下面的链接重置密码: http://127.0.0.1:8000/reset/{0}".format(code)
    
            send_status = send_mail(email_title, email_body, DEFAULT_FROM_EMAIL, [email])
            if send_status:
                pass
        elif send_type == "update_email":
            email_title = "慕学在线邮箱修改验证码"
            email_body = "你的邮箱验证码为: {0}".format(code)
    
            send_status = send_mail(email_title, email_body, DEFAULT_FROM_EMAIL, [email])
            if send_status:
                pass
[/code]



**6.设置激活连接逻辑**  
 **当用户点击激活连接时，获取到激活连接的随机字符，**  
**将随机字符拿到激活表里去查询是否有这条随机字符，如果有，将当前随机字符的所有信息获取到，通过获取到的信息，将对应用户表里用户状态改为激活状态，返回登录页面，提示以激活请登录**

[code]

     from django.conf.urls import url, include                   # 导入django自在的include逻辑
    from django.contrib import admin
    from django.views.generic import TemplateView               # 导入django自带的TemplateView逻辑
    
    import xadmin                                               # 导入xadmin
    
    from app_users.views import deng_lu, zhu_ce, active_code, logout                 # 导入登录逻辑处理类
    
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        url(r'^register.html', zhu_ce.as_view(), name='register'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
        url(r'^active/(?P<active_de>.*)/$', active_code.as_view(), name="user_active"),
    
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
        url(r'^logout', logout.as_view(), name='deng_lu'),
    ]
[/code]

**激活逻辑处理**

[code]

     class active_code(View):
        def get(self, request, active_de):
            yanzh_email = Email.objects.filter(code=active_de)
            if yanzh_email:
                for record in yanzh_email:
                    email = record.email
                    Users.objects.filter(username=email).update(is_active=True)
                    Email.objects.filter(code=active_de).delete()
            return render(request, 'login.html')
[/code]



**找回密码等更能也是这个原理**

