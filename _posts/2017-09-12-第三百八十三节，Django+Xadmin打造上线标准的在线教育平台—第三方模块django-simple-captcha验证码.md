
---
layout: post
title: " 第三百八十三节，Django+Xadmin打造上线标准的在线教育平台—第三方模块django-simple-captcha验证码 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十三节，Django+Xadmin打造上线标准的在线教育平台—第三方模块django-simple-captcha验证码**



**下载地址：https://github.com/mbi/django-simple-captcha**

**文档说明：http://django-simple-captcha.readthedocs.io/en/latest/usage.html**



**安装模块**

**下载后 python  ** **setup.py  install安装模块******



******在配置文件settings.py，里注册app名称 captcha，因为这个验证码插件，自动生成自己的一张数据库表******

[code]

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
        'xadmin',                           # 注册xadmin的app
        'crispy_forms',                     # 注册xadmin的依赖app
        'captcha',                          # 注册验证码app
    ]
[/code]



**配置图面验证码url路由映射**

[code]

     from django.conf.urls import url, include                   # 导入django自在的include逻辑
    from django.contrib import admin
    from django.views.generic import TemplateView               # 导入django自带的TemplateView逻辑
    
    import xadmin                                               # 导入xadmin
    
    from app_users.views import deng_lu, zhu_ce, yanzhmaHandler                         # 导入登录逻辑处理类
    
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        url(r'^register.html', TemplateView.as_view(template_name='register.html'), name='register'),
        url(r'^zhu_ce', zhu_ce.as_view(), name='zhu_ce'),
        url(r'^yanzhm', yanzhmaHandler.as_view(), name='yanzhm'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
    
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
    
    ]
[/code]



**生成验证码数据表**

**执行migrate命令 **生成验证码数据表****

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170914105346860-707776633.png)**



**编写当前app下的forms.py表单验证**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    # 表单验证
    
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
    **captcha** **= CaptchaField(　　　　　　　　　　　　 # captcha名称是固定的
            required=True,
            error_messages={
                'required': '验证码不能为空',
                'invalid': '验证码不正确'
            }
        )**
[/code]



**验证码使用**

**在需要使用验证码表单的逻辑处理函数里使用**

**1在get请求时实例化表单验证类，将实例化的类传输到html页面**

**2在HTML页面接收表单类下面的captcha,会自动生成验证码包括输入框，数据库里也会生成验证码，这样包括验证等都会自动完成**

**逻辑处理**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import io  # 导入io模块
    
    from django.shortcuts import render, HttpResponse                                           # 导入django向浏览器返回方法
    from django.views.generic.base import View
    from django.db.models import F,Q                                                            # 导入F和Q
    from django.contrib.auth.hashers import make_password, check_password                       # 导入django密码加密，和密码验证
    from django.contrib.auth.models import User
    
    from app_users.forms import deng_lu_forms, zhu_ce_forms                                    # 导入登录页面表单认证
    from app_users.models import Users                                                          # 导入数据库操作
    
    
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
[/code]

**html**

[code]

                             <div class="form-group marb8 captcha1 {% if cuo_wu.captcha %}errorput{% endif %}">
                                <label>验&nbsp;证&nbsp;码</label>
                                {{ yanzhm.captcha }}
                            </div>
[/code]



**验证码的各种设置在settings.py里配置**

[code]

     # Application definition
    
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
        'xadmin',                           # 注册xadmin的app
        'crispy_forms',                     # 注册xadmin的依赖app
        'captcha',                          # 注册验证码app
    ]
    # 格式
    CAPTCHA_OUTPUT_FORMAT = u'%(text_field)s %(hidden_field)s %(image)s'
    # 噪点样式
    CAPTCHA_NOISE_FUNCTIONS = (
        'captcha.helpers.noise_null',       # 没有样式
        # 'captcha.helpers.noise_arcs',     # 线
        'captcha.helpers.noise_dots',       # 点
    )
    # 图片大小
    CAPTCHA_IMAGE_SIZE = (100, 30)
    # 字符个数
    CAPTCHA_LENGTH = 4
    # 超时(minutes)
    CAPTCHA_TIMEOUT = 1
    # 文字倾斜
    CAPTCHA_LETTER_ROTATION = (-10,10)
    # 背景颜色
    CAPTCHA_BACKGROUND_COLOR = '#FFFFFF'
    # 文字颜色
    CAPTCHA_FOREGROUND_COLOR = '#0A12E5'
    # 验证码类型
    # 图片中的文字为随机英文字母，如 mdsh
    CAPTCHA_CHALLENGE_FUNCT = 'captcha.helpers.random_char_challenge'
    # 图片中的文字为数字表达式，如1+2=
    # CAPTCHA_CHALLENGE_FUNCT = 'captcha.helpers.math_challenge'
[/code]



