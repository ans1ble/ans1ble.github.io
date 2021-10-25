---
layout: post
title: " 第三百零五节，Django框架，Views（视图函数），也就是逻辑处理函数里的各种方法与属性 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Django框架，Views（视图函数），也就是逻辑处理函数里的各种方法与属性**



**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709164402384-1389711402.png)**





**Views（视图函数）逻辑处理，最终是围绕着两个对象实现的**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709165938790-737655812.png)**

**http请求中产生两个核心对象：**

**http请求：HttpRequest对象**

**http响应：HttpResponse对象**

**所在位置：django.http**

**之前我们用到的参数request就是HttpRequest    **



**HttpRequest对象**

**逻辑处理函数的第一个形式参数，接收到的就是 **HttpRequest对象，这个对象里封装着用户的各种请求信息，通过 **
**HttpRequest对象的方法或者属性，可以获取到响应的请求信息********



**********HttpRequest请求对象里的方法和属性如下：**********

**path属性 ，获取请求页面的全路径，不包括域名**

[code]

    from django.shortcuts import render,HttpResponse
    
    def special(request):
        print(request.path)
        return render(request,'index.html')   #向用户显示一个html页面
    
    #返回：
    #/bug/articles/5555
[/code]



**method属性 ，获取请求中使用的HTTP方式的字符串表示。全大写表示**

[code]

    from django.shortcuts import render,HttpResponse
    
    def special(request):
        print(request.method)
        return render(request,'index.html')   #向用户显示一个html页面
    
    #返回：
    #GET
[/code]



**GET属性 ，获取HTTP GET方式请求传参，的参数（字典类型）**  
 **如：http://127.0.0.1:8000/bug/articles/?mch=123 & mim=456**

[code]

    from django.shortcuts import render,HttpResponse
    
    def special(request):
        print(request.GET)
        return render(request,'index.html')   #向用户显示一个html页面
    
    #返回：
    #<QueryDict: {' mim': ['456'], 'mch': ['123 ']}>
[/code]



**更多**

[code]

     # POST：       包含所有HTTP POST参数的类字典对象
    #
    #              服务器收到空的POST请求的情况也是可能发生的，也就是说，表单form通过
    #              HTTP POST方法提交请求，但是表单中可能没有数据，因此不能使用
    #              if req.POST来判断是否使用了HTTP POST 方法；应该使用  if req.method=="POST"
    #
    #
    #
    # COOKIES:     包含所有cookies的标准Python字典对象；keys和values都是字符串。
    #
    # FILES：      包含所有上传文件的类字典对象；FILES中的每一个Key都是<input type="file" name="" />标签中name属性的值，FILES中的每一个value同时也是一个标准的python字典对象，包含下面三个Keys：
    #
    #             filename：      上传文件名，用字符串表示
    #             content_type:   上传文件的Content Type
    #             content：       上传文件的原始内容
    #
    #
    # user：       是一个django.contrib.auth.models.User对象，代表当前登陆的用户。如果访问用户当前
    #              没有登陆，user将被初始化为django.contrib.auth.models.AnonymousUser的实例。你
    #              可以通过user的is_authenticated()方法来辨别用户是否登陆：
    #              if req.user.is_authenticated();只有激活Django中的AuthenticationMiddleware
    #              时该属性才可用
    #
    # session：    唯一可读写的属性，代表当前会话的字典对象；自己有激活Django中的session支持时该属性才可用。
[/code]



**get_full_path()方法 ，获取HTTP GET方式请求传参，的URL地址**  
 **比如：http://127.0.0.1:8000/index33/?name=123**  
 **get_full_path()得到的结果就是/index33/?name=123**





**HttpResponse响应对象方法和属性如下：**

**对于HttpRequest请求对象来说，是由django自动创建的，但是，HttpResponse响应对象就必须我们自己创建。每个view请求处理方法必须返回一个HttpResponse响应对象。**

**HttpResponse类在django.http.HttpResponse**

**在HttpResponse对象上扩展的常用方法：**

**render(请求对象，'html文件和路径') 方法，将指定 **页面渲染后返回给浏览器，****

[code]

     from django.shortcuts import render
    
    def special(request):
        return render(request,'index.html')   #向用户显示一个html页面
[/code]



**render_to_response('html文件和路径') **方法，将指定 **页面渲染后返回给浏览器，******

[code]

     from django.shortcuts import render,render_to_response
    def special(request):
        return render_to_response('index.html')   #向用户显示一个html页面
[/code]



**redirect('跳转路径和名称') 方法， **页面跳转****

[code]

     from django.shortcuts import render,render_to_response,redirect
    def special(request):
        return redirect('http://www.jxiou.com/')   #跳转页面
[/code]



**locals(变量名称) 可以直接将逻辑处理函数中的所有变量传给模板    **

[code]

    from django.shortcuts import render
    def special(request):
    
        a1 = 123
        a2 = 456
        a3 = 789
        return render(request,'index.html',locals())   #跳转页面
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
    <h1>主页</h1>
    <p>{{ a1 }}</p>
    <p>{{ a2 }}</p>
    <p>{{ a3 }}</p>
    </body>
    </html>
[/code]



