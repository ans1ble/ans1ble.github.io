
---
layout: post
title: " 第三百一十五节，Django框架，CSRF跨站请求伪造 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


  
**第三百一十五节，Django框架，CSRF跨站请求伪造**

**  全局CSRF**

**如果要启用防止 **CSRF跨站请求伪造，就需要在中间件开启 **CSRF******

[code]

     #中间件
    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        # 'django.middleware.csrf.CsrfViewMiddleware',   #开启csrf
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]
[/code]

**注意：一旦开启了csrf提交表单时会出现403错误，必须结合两个步骤来使用**

**第一、页面响应返回必须由** **render()方法**

**第二、必须在html页面的 <form>标签里用上模板语言** **{% csrf_token %}**

**< form>**  
 **{% csrf_token %}**  
 **...**  
 **< /form>**



**逻辑处理**

[code]

     from django.shortcuts import render,redirect
    
    from app1.chajian.fen_ye import fen_ye_lei  #导入分页模块
    from app1.models import *   #导入数据库模块
    #逻辑处理模块
    def special(request):
    
        return render(request, 'app1/index.html',locals())
[/code]

**html**

[code]

    <!DOCTYPE html>
    <html lang= "en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" type="text/css" href="/static/css/tou.css">
    </head>
    <body>
    <form action='/bugarticles/' method="post">
        {% csrf_token %}
        <input type="text" name="nad"/>
        <input type="submit" value="搜索"/>
    </form>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170719173241396-317464911.png)





**局部CSRF**

**局部 **CSRF，可以用装饰器在逻辑处理函数上做装饰****

****需要导入模块： from django.views.decorators.csrf import
csrf_exempt,csrf_protect****

**@csrf_protect ，为当前函数强制设置防跨站请求伪造功能，即便settings中没有设置全局中间件。使用了同样遵守上面两个步骤**  
 **@csrf_exempt ，取消当前函数防跨站请求伪造功能，即便settings中设置了全局中间件。**

**  逻辑处理**

[code]

    from django.shortcuts import render,redirect
    from django.views.decorators.csrf import csrf_exempt,csrf_protect
    from app1.chajian.fen_ye import fen_ye_lei  #导入分页模块
    from app1.models import *   #导入数据库模块
    
    #逻辑处理模块
    @csrf_protect
    def special(request):
    
        return render(request, 'app1/index.html',locals())
[/code]

**html**

[code]

    <!DOCTYPE html>
    <html lang= "en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" type="text/css" href="/static/css/tou.css">
    </head>
    <body>
    <form action='/bugarticles/' method="post">
        {% csrf_token %}
        <input type="text" name="nad"/>
        <input type="submit" value="搜索"/>
    </form>
    </body>
    </html>
[/code]



**Ajax提交**

[code]

    <!DOCTYPE html>
    <html>
    <head lang= "en">
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        {% csrf_token %}
      
        <input type="button" onclick="Do();"  value="Do it"/>
      
        <script src="/static/plugin/jquery/jquery-1.8.0.js"></script>
        <script src="/static/plugin/jquery/jquery.cookie.js"></script>
        <script type="text/javascript">
            var csrftoken = $.cookie('csrftoken');   #从cookie获取到csrf密串
      
            function csrfSafeMethod(method) {
                // these HTTP methods do not require CSRF protection
                return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
            }
            $.ajaxSetup({     #设置ajax全局方法，设置后所有的ajax请求前都会先执行这个方法
                beforeSend: function(xhr, settings) {
                    if (!csrfSafeMethod(settings.type) && !this.crossDomain) {
                        xhr.setRequestHeader("X-CSRFToken", csrftoken);         #将获取到的csrf密串，添加到请求头传输到逻辑处理
                    }
                }
            });
            function Do(){
      
                $.ajax({
                    url:"/app01/test/",
                    data:{id:1},
                    type:'POST',
                    success:function(data){
                        console.log(data);
                    }
                });
      
            }
        </script>
    </body>
    </html>
[/code]







****

