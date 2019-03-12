
---
layout: post
title: " 第三百八十五节，Django+Xadmin打造上线标准的在线教育平台—登录功能实现，回填数据以及错误提示html "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十五节，Django+Xadmin打造上线标准的在线教育平台—登录功能实现**



**1，配置登录路由**

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





**2，编写表单验证**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    # 表单验证
    
    from django import forms                 # 导入Django的表单验证模块
    from captcha.fields import CaptchaField
    
    class deng_lu_forms(forms.Form):         # 自定义验证表单类，继承Django的表单验证类
        username = forms.CharField(
            required=True,
            max_length=20,
            min_length=2,
            error_messages={
                'required': '用户名不能为空',
                'max_length': '用户名长度不得超过20个字符',
                'min_length': '用户名长度不得少于2个字符',
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
[/code]





**3，在逻辑处理里，进行表单验证，如果验证失败提示错误回填数据，如果验证成功，获取验证后的表单数据，将获取到的用户名拿到数据库查找用户是否存在，如果不存在提示用户不存在回填数据，如果存在获取到用户密码，用django的密码验证函数check_password(用户输入密码,
数据库加密密码)，返回布尔值，如果一致返回真，如果密码正确创建session，向session里写入一个表示登录的键值，如果密码不正确提示密码错误回填数据**

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
    
    class deng_lu(View):
        def get(self, request):
            return render(request, 'login.html', {})
    
        def post(self, request):
            f = deng_lu_forms(request.POST)                 # 实列化表单认证类，将用户post提交的数据传入进行认证
            if f.is_valid():                                # 判断认证是否成功
                tong_guo = f.cleaned_data                   # 认证成功，接收用户数据
                username = tong_guo['username']
                password = tong_guo['password']
                user = Users.objects.filter(username=username)
                if user:
                    for i in user:
                        mima = i.password
                        pdmima = check_password(password, mima)
                        if not pdmima:
                            tishi = '密码不正确'
                            return render(request, 'login.html', {'tishi': tishi})
                        else:
                            request.session["zhuang_tai"] = True                      # 创建session
                            request.session["username"] = username
                            # request.session["password"] = password
                            return redirect('/index.html')
                else:
                    tishi = '用户不存在'
                    return render(request, 'login.html', {'tishi': tishi})
            else:                                                                   # 认证不成功，接收错误信息
                cuo_wu = f.errors                                                   # 接收错误信息
                return render(request, 'login.html', {'cuo_wu': cuo_wu})            # 将错误信息传到登录页面
    
    
    class logout(View):
        def get(self, request):
            try:
                request.session.flush()
            except KeyError:
                pass
    
            return redirect('/index.html')
    
        def post(self, request):
            pass
[/code]





**4，settings.py配置session**

[code]

     # session配置
    SESSION_COOKIE_NAME = "_sessionid_"             # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串（默认）
    SESSION_COOKIE_PATH = "/"                       # Session的cookie保存的路径（默认）
    SESSION_COOKIE_DOMAIN = None                    # Session的cookie保存的域名（默认）
    SESSION_COOKIE_SECURE = False                   # 是否Https传输cookie（默认）
    SESSION_COOKIE_HTTPONLY = True                  # 是否Session的cookie只支持http传输（默认）
    SESSION_COOKIE_AGE = 1209600                    # Session的cookie失效日期（2周）（默认）
    SESSION_EXPIRE_AT_BROWSER_CLOSE = False         # 是否关闭浏览器使得Session过期（默认）
    SESSION_SAVE_EVERY_REQUEST = False              # 是否每次请求都保存Session，默认修改之后才保存（默认），默认就好
[/code]





**5，编写一个中间件来专门用于用户登录账号状态检测，在中间件里获取设置的session状态,通过request.META将登录状态向所有页面注入，在页面接收这个登录状态，判断如果登录显示会员区块，如果状态是没登录显示，注册和登录区块**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from django.utils.deprecation import MiddlewareMixin
    from django.shortcuts import render
    
    
    class zhongjianjian(MiddlewareMixin):
    
        def process_request(self, request):
            print('有请求时执行')
            # print(request.META) #请求对象内容
            #在这里可以做ip访问拦截器
    
        def process_view(self, request, callback, callback_args, callback_kwargs):
            print('逻辑处理之前执行')
            zhuang_tai = request.session.get("zhuang_tai")
            request.META['zhuang_tai'] = zhuang_tai
    
            username = request.session.get("username")
            request.META['username'] = username
    
        def process_exception(self, request, exception):
            print('出错时执行')
            # return render(request, 'app1/cuowu.html')
            print(exception)
            #做程序出错时处理
    
        def process_response(self, request, response):
            print('响应后执行，无论是否出错')
    
            return response
[/code]



**html页面接收中间件注入的登录状态**

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
    <body>
    <section class="headerwrap ">
        <header>
            <div  class=" header">
                 <div class="top">
                    <div class="wp">
                        <div class="fl"><p>服务电话：<b>33333333</b></p></div>
                        <!--登录后跳转-->
                        {{ request.META.zhuang_tai }}
                        {% if request.META.zhuang_tai == True %}
                            <div class="personal">
                                <dl class="user fr">
                                    <dd>{{ request.META.username }}<img class="down fr" src="/static/images/top_down.png"/></dd>
                                    <dt><img width="20" height="20"
                                             src="/static/media/image/2016/12/default_big_14.png"/></dt>
                                </dl>
                                <div class="userdetail">
                                    <dl>
                                        <dt><img width="80" height="80"
                                                 src="/static/media/image/2016/12/default_big_14.png"/></dt>
                                        <dd>
    
                                            <h2>{{ request.META.username }}</h2>
                                            <p>{{ request.META.username }}</p>
                                        </dd>
                                    </dl>
                                    <div class="btn">
                                        <a class="personcenter fl" href="usercenter-info.html">进入个人中心</a>
                                        <a class="fr" href="/logout/">退出</a>
                                    </div>
                                </div>
                            </div>
                        {% elif request.META.zhuang_tai != True %}
                            <a style="color:white" class="fr registerbtn" href="{% url 'register' %}">注册</a>
                            <a style="color:white" class="fr loginbtn" href="/login.html">登录</a>
                        {% endif %}
    
                    </div>
                </div>
    
    
[/code]



![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170916132737078-365697745.png)



**回填数据以及错误提示html**

**回填数据 yanzh.email.value   表单对象.表单字段. **value****

[code]

     <div class="tab-form">
                        <form id="email_register_form" method="post" action="{% url 'register'%}" autocomplete="off">
                            <input type='hidden' name='csrfmiddlewaretoken' value='gTZljXgnpvxn0fKZ1XkWrM1PrCGSjiCZ' />
                            <div class="form-group marb20 {% if cuo_wu.email %}errorput{% endif %} ">
                                <label>邮&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;箱</label>
                                <input  type="text" id="id_email" name="email" value="{{ yanzh.email.value }}" placeholder="请输入您的邮箱地址" />
                            </div>
                            <div class="form-group marb8 {% if cuo_wu.password %}errorput{% endif %}">
                                <label>密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码</label>
                                <input type="password" id="id_password" name="password"  value="{{ yanzh.password.value }}" placeholder="请输入6-20位非中文字符密码" />
                            </div>
                            <div class="form-group marb8 captcha1 {% if cuo_wu.captcha %}errorput{% endif %}">
                                <label>验&nbsp;证&nbsp;码</label>
                                {{ yanzhm.captcha }}
                            </div>
                            <div class="error btns" id="jsEmailTips">
                                {% for key,error in cuo_wu.items %}{{ error }}{% endfor %}    #错误提示
                                {% if tishi %}{{ tishi }}{% endif %}
                            </div>
                            <div class="auto-box marb8">
                            </div>
                            <input class="btn btn-green" id="jsEmailRegBtn" type="submit" value="注册并登录" />
                        <input type='hidden' name='csrfmiddlewaretoken' value='5I2SlleZJOMUX9QbwYLUIAOshdrdpRcy' />
                        {% csrf_token %}
                        </form>
                    </div>
[/code]



