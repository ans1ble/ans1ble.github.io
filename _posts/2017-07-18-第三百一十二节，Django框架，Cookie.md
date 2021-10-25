---
layout: post
title: " 第三百一十二节，Django框架，Cookie "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百一十二节，Django框架，Cookie**

**注意：获取 **Cookie是在请求对象里处理，设置 **Cookie是在响应对象里处理******

**普通Cookie**  
 **set_cookie() 设置普通cookie**

**参数：**  
 **key, 键**  
 **value='', 值**  
 **max_age=None, 超时时间， **秒，也支持时间戳****  
 **expires=None, 超时时间(IE requires expires, so set it if hasn't been
already.)**  
 **path='/', Cookie生效的路径，/ 表示根路径，特殊的：跟路径的cookie可以被任何url的页面访问**  
 **domain=None, Cookie生效的域名**  
 **secure=False, https传输**  
 **httponly=False 只能http协议传输，无法被JavaScript获取（不是绝对，底层抓包可以获取到也可以被覆盖）**

**COOKIES 获取普通cookie**  
 **COOKIES['k1'] 获取指定普通cookie，存在获取，不存在报错**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        print(request.COOKIES)                      #获取所有cookie
        print(request.COOKIES['k1'])                #获取指定cookie
    
        rep = render(request, 'app1/index.html')
        rep.set_cookie('k1',123)                    #设置cookie
        return rep
[/code]



**加密Cookie**

**set_signed_cookie() 设置加密cookie**

**参数：**  
 **key, 键cookie名称**  
 **value='', 值**  
 **salt='' 加严**  
 **max_age=None, 超时时间，秒，也支持时间戳**  
 **expires=None, 超时时间(IE requires expires, so set it if hasn't been
already.)**  
 **path='/', Cookie生效的路径，/ 表示根路径，特殊的：跟路径的cookie可以被任何url的页面访问**  
 **domain=None, Cookie生效的域名**  
 **secure=False, https传输**  
 **httponly=False 只能http协议传输，无法被JavaScript获取（不是绝对，底层抓包可以获取到也可以被覆盖）**

**get_signed_cookie() 获取加密cookie**  
 **参数：**  
 **key 键cookie名称**  
 **salt='' 加严**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        a = request.get_signed_cookie('k2',salt='adc')  #获取加密cookie
        print(a)
    
        rep = render(request, 'app1/index.html')
        rep.set_signed_cookie('k2','v2',salt='adc')     #设置加密cookie
        return rep
[/code]



**由于cookie保存在客户端的电脑上，所以，JavaScript和jquery也可以操作cookie。**

