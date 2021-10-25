---
layout: post
title: " 第三百一十三节，Django框架，Session "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百一十三节，Django框架，Session**



**Django中默认支持Session，其内部提供了5种类型的Session供开发者使用：**

**1、数据库（默认）**  
 **2、缓存**  
 **3、文件**  
 **4、缓存+数据库**  
 **5、加密cookie**



**1、数据库Session，保存在数据库**

**Django默认支持Session，并且默认是将Session数据存储在数据库中，即：django_session 表中。**

**全局配置Session**

[code]

     Django默认支持Session，并且默认是将Session数据存储在数据库中，即：django_session 表中。
     
    a. 配置 settings.py
     
        SESSION_ENGINE = 'django.contrib.sessions.backends.db'   # 引擎（默认）数据库保存session引擎
         
        SESSION_COOKIE_NAME ＝ "sessionid"                       # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串（默认）
        SESSION_COOKIE_PATH ＝ "/"                               # Session的cookie保存的路径（默认）
        SESSION_COOKIE_DOMAIN = None                             # Session的cookie保存的域名（默认）
        SESSION_COOKIE_SECURE = False                            # 是否Https传输cookie（默认）
        SESSION_COOKIE_HTTPONLY = True                           # 是否Session的cookie只支持http传输（默认）
        SESSION_COOKIE_AGE = 1209600                             # Session的cookie失效日期（2周）（默认）
        SESSION_EXPIRE_AT_BROWSER_CLOSE = False                  # 是否关闭浏览器使得Session过期（默认）
        SESSION_SAVE_EVERY_REQUEST = False                       # 是否每次请求都保存Session，默认修改之后才保存（默认），默认就好
[/code]

**使用Session**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
        print(request.session['k1'])     #获取session
        return render(request, 'app1/index.html')
[/code]



**获取、设置、删除Session中指定数据**  
 **request.session['k1'] 获取Session中数据，不存在报错**  
 **request.session.get('k1',None) 获取Session中数据，不存在返回None**  
 **request.session['k1'] = 123 设置Session中数据，存在覆盖**  
 **request.session.setdefault('k1',123) 设置Session中数据，存在不设置**  
 **del request.session['k1'] 删除Session中指定数据**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
        print(request.session['k1'])     #获取session
        del request.session['k1']
        return render(request, 'app1/index.html')
[/code]



**获取Session中所有 键、值、键值对**  
 **request.session.keys() 获取Session中所有的键**  
 **request.session.values() 获取Session中所有的值**  
 **request.session.items() 获取Session中所有的键值对**  
 **request.session.iterkeys()**  
 **request.session.itervalues()**  
 **request.session.iteritems()**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
        request.session['k2'] = 456      # 设置session
        request.session['k3'] = 789      # 设置session
        # print(request.session['k1'])     #获取session
    
        #
        print(request.session.keys())
        print(request.session.values())
        print(request.session.items())
    
        return render(request, 'app1/index.html')
[/code]



**获取用户session的随机字符串，也就是session名称**  
 **request.session.session_key 获取用户session的随机字符串，也就是session名称**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
        request.session['k2'] = 456      # 设置session
        request.session['k3'] = 789      # 设置session
        # print(request.session['k1'])     #获取session
    
    
        print(request.session.session_key)
    
        return render(request, 'app1/index.html')
[/code]



**将所有Session失效日期小于当前日期的数据在数据库删除， 也就是在数据库删除过期的Session数据**  
 **request.session.clear_expired()**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        # request.session['k1'] = 123      #设置session
        # request.session['k2'] = 456      # 设置session
        # request.session['k3'] = 789      # 设置session
        # print(request.session['k1'])     #获取session
    
    
        request.session.clear_expired()
    
        return render(request, 'app1/index.html')
[/code]



**request.session.exists("获取当前随机字符串") 检查 用户session的随机字符串 在数据库中是否** **  
**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
    
    
        a = request.session.session_key
        print(request.session.exists(a))
    
        return render(request, 'app1/index.html')
[/code]

**request.session.delete("获取当前用户随机字符串") 删除当前用户的所有Session数据**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        request.session['k1'] = 123      #设置session
    
    
        a = request.session.session_key
        request.session.delete(a)
    
        return render(request, 'app1/index.html')
[/code]



**request.session.set_expiry(value) 设置session失效时间**  
 *** 如果value是个整数，session会在value秒数后失效。**  
 *** 如果value是个datatime或timedelta，session就会在这个时间后失效。**  
 *** 如果value是0,用户关闭浏览器session就会失效。**  
 *** 如果value是None,session会依赖全局session失效策略。**



* * *





**2、缓存Session，保存在服务器内存**

[code]

     a. 配置 settings.py
     
        SESSION_ENGINE = 'django.contrib.sessions.backends.cache'  # 引擎，表示保存在内存
        SESSION_CACHE_ALIAS = 'default'                            # 使用的缓存别名（default默认内存缓存，也可以是memcache,如果是memcache这里设置memcache缓存配置名称），此处别名依赖缓存的设置，见缓存章节
     
     
        SESSION_COOKIE_NAME ＝ "sessionid"                        # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串
        SESSION_COOKIE_PATH ＝ "/"                                # Session的cookie保存的路径
        SESSION_COOKIE_DOMAIN = None                              # Session的cookie保存的域名
        SESSION_COOKIE_SECURE = False                             # 是否Https传输cookie
        SESSION_COOKIE_HTTPONLY = True                            # 是否Session的cookie只支持http传输
        SESSION_COOKIE_AGE = 1209600                              # Session的cookie失效日期（2周）
        SESSION_EXPIRE_AT_BROWSER_CLOSE = False                   # 是否关闭浏览器使得Session过期
        SESSION_SAVE_EVERY_REQUEST = False                        # 是否每次请求都保存Session，默认修改之后才保存
[/code]

**使用同上**

** **

* * *



**3、文件Session，保存在文件里**

[code]

     a. 配置 settings.py
     
        SESSION_ENGINE = 'django.contrib.sessions.backends.file'    # 引擎，文件保存引擎
        SESSION_FILE_PATH = None                                    # 缓存文件路径，如果为None，则使用tempfile模块获取一个临时地址tempfile.gettempdir()                                                            # 如：/var/folders/d3/j9tj0gz93dg06bmwxmhh6_xm0000gn/T
     
     
        SESSION_COOKIE_NAME ＝ "sessionid"                          # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串
        SESSION_COOKIE_PATH ＝ "/"                                  # Session的cookie保存的路径
        SESSION_COOKIE_DOMAIN = None                                # Session的cookie保存的域名
        SESSION_COOKIE_SECURE = False                               # 是否Https传输cookie
        SESSION_COOKIE_HTTPONLY = True                              # 是否Session的cookie只支持http传输
        SESSION_COOKIE_AGE = 1209600                                # Session的cookie失效日期（2周）
        SESSION_EXPIRE_AT_BROWSER_CLOSE = False                     # 是否关闭浏览器使得Session过期
        SESSION_SAVE_EVERY_REQUEST = False                          # 是否每次请求都保存Session，默认修改之后才保存
[/code]

**使用同上**





* * *





**4、缓存+数据库Session，缓存和数据库都保存**

**用户首次将 **Session保存到数据库，并保存一份到缓存，第二次到缓存里拿，如果缓存里没有，在到数据库拿又保存到缓存****

[code]

     数据库用于做持久化，缓存用于提高效率
     
    a. 配置 settings.py
     
        SESSION_ENGINE = 'django.contrib.sessions.backends.cached_db'        # 引擎
[/code]

**使用同上**



* * *





****5、加密cookie Session， **Session以 **cookie方式加密后保存在客户端********

[code]

     a. 配置 settings.py
         
        SESSION_ENGINE = 'django.contrib.sessions.backends.signed_cookies'   # 引擎
[/code]



**登录认证小列子**

[code]

     def login(request):
        if request.method == "POST":
            username = request.POST.get("username")
            password = request.POST.get("password")
            if username == "zhangsan" and password == "123456":
                request.session["IS_LOGIN"] = True  #创建session
                return redirect("/app01/home/")
        return render(request,"app01/login.html")
    
    def home(request):
        islogin = request.session.get("IS_LOGIN",False)
        if islogin:#如果用户已登录
            return render(request,"app01/menus.html")
        else:
            return redirect("/app01/login/")
    
    def logout(request):#退出
        try:
            del request.session['IS_LOGIN']
        except KeyError:
            pass
        return redirect("/app01/login/")
[/code]





**Session，保存在** **Redis**

**首先安装 **Redis软件，然后安装第三方插件 django-redis模块****

****需要在全部配置里，将 缓存配置和 **Session配置 都要配置上******

[code]

    #缓存配置
    # 自定义缓存key
    def default_key_func(key, key_prefix, version):
        return '%s:%s:%s' % (key_prefix, version, key)
    # 配置：
    CACHES = {
        'default': {
            'BACKEND': "django_redis.cache.RedisCache",     #配置文件引擎
            'LOCATION': "redis://127.0.0.1:6379",           #配置文件缓存路径
    
            'TIMEOUT': 300,                                 # 缓存超时时间（默认300秒，None表示永不过期，0表示立即过期）如果使用中没设置，这里启用
            'OPTIONS': {
                "CLIENT_CLASS": "django_redis.client.DefaultClient",
                'MAX_ENTRIES': 300,                         # 最大缓存个数（默认300）
                'CULL_FREQUENCY': 3,                        # 缓存到达最大个数之后，剔除缓存个数的比例，即：1/CULL_FREQUENCY（默认3，删除百分之3）
            },
            'KEY_PREFIX': 'jxiou',                          # 缓存key的前缀（默认空）
            'VERSION': 1,                                   # 缓存key的版本（默认1），设置后缓存key会是，KEY_PREFIX前缀加VERSION版本
            # 'KEY_FUNCTION': default_key_func              # 生成key的函数（默认函数会生成为：【前缀:版本:key】）
        }
    }
      
    
    #配置Session
    SESSION_ENGINE = 'django.contrib.sessions.backends.cache'  # 引擎，表示保存在内存
    SESSION_CACHE_ALIAS = 'default'  　　　　　　　　# 使用的缓存别名（default默认内存缓存，也可以是memcache,如果是memcache这里设置memcache缓存配置名称），此处别名依赖缓存的设置，见缓存章节
    
    SESSION_COOKIE_NAME = "sessionid"  　　　　　　# Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串
    SESSION_COOKIE_PATH = "/" 　　　　　　　　　　　　 # Session的cookie保存的路径
    SESSION_COOKIE_DOMAIN = None 　　　　　　 　　# Session的cookie保存的域名
    SESSION_COOKIE_SECURE = False  　　　　　　# 是否Https传输cookie
    SESSION_COOKIE_HTTPONLY = True  　　　　　　# 是否Session的cookie只支持http传输
    SESSION_COOKIE_AGE = 1209600  　　　　　　　　# Session的cookie失效日期（2周）
    SESSION_EXPIRE_AT_BROWSER_CLOSE = False  　　# 是否关闭浏览器使得Session过期
    SESSION_SAVE_EVERY_REQUEST = False  　　　　# 是否每次请求都保存Session，默认修改之后才保存
[/code]

**应用同上**



