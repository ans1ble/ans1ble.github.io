
---
layout: post
title: " 第三百零四节，Django框架，urls.py模块，views.py模块，路由映射与路由分发以及逻辑处理——url控制器 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Django框架，urls.py模块，views.py模块，路由映射与路由分发以及逻辑处理——url控制器**

**这一节主讲url控制器**

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709153234228-1960514504.png)



**一、urls.py模块**

**这个模块是配置路由映射的模块，当用户访问一个url地址时，通过这个路由映射模块，映射给对应的逻辑处理函数**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709075414884-993912328.png)**





**urlpatterns 等于的一个列表，列表里的一个元素就是一条路由映射**

**urlpatterns 路由映射配置方式**

**参数说明：**

**一个正则表达式字符串**  
 **一个可调用对象，通常为一个视图函数或一个指定视图函数路径的字符串**  
 **可选的要传递给视图函数的默认参数（字典形式）**  
 **一个可选的name参数**

[code]

    urlpatterns = [
        url(正则表达式, 映射函数，参数[可选]，别名[可选]),
    ]  
    
    urlpatterns  = [
        url(r'^admin/', admin.site.urls,{'a':'123'},'ADMIN'),
    ]
[/code]

**如：**

[code]

     """Xiangmu URL Configuration
    
    The `urlpatterns` list routes URLs to views. For more information please see:
        https://docs.djangoproject.com/en/1.10/topics/http/urls/
    Examples:
    Function views
        1. Add an import:  from my_app import views
        2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
    Class-based views
        1. Add an import:  from other_app.views import Home
        2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
    Including another URLconf
        1. Import the include() function: from django.conf.urls import url, include
        2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
    """
    from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),   #系统生成的映射
    　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　#注意里面的任意一条映射匹配成功，后面的则不在匹配
        url(r'^articles/2003/$', views.special_case_2003),                           #表示articles/2003/这个路径映射views模块的special_case_2003函数
        # url(r'^articles/([0-9]{4})/$', views.year_archive),                        #表示2003可以是0-9的任意4个数字
        # url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),            #表示匹配二级目录
        # url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),  #表示匹配三级目录
    ]
[/code]



**二、views.py模块，路由映射的函数模块，逻辑处理路由映射的需求**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709090027587-1889982022.png)**





**注意：自定义映射函数时，有两个重点**

****HttpResponse(字符串) 方法向用户返回字符串****

**1，定义的函数必须，定义一个形式参数，这个形式参数接收的url请求信息对象，可以通过这个形式参数的各种方法获取到各种请求信息**

**2，向用户返回信息，必须在函数结尾return，如果是要给用户返回一串字符串，那就必须返回** **HttpResponse
方法，参数是要返回的字符串，需要先导入这个方法**

[code]

    from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special_case_2003(request):
        print(request.method)       #获取用户请求的路径
        return HttpResponse('你好')
[/code]



**最后测试一下**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709091957556-377110033.png)**



**浏览器输入：http://127.0.0.1:8000/articles/2003/**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709092130650-565749167.png)**





**逻辑处理时获取用户访问路径**

**逻辑处理自定义函数的第二个参数，就是接收用户请求路径的，所以需要自定义形式参数来接收**

[code]

     from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special_case_2003(request,name):
        print(request.method)       #获取用户请求的路径
        print(name)　　　　　　　　   #打印路径
        return HttpResponse(name)　 #将路径返回到页面
[/code]

**注意：要获取路径时，需要在路由映射哪里用正则的分组()号，将要获取的路径分组，也就是括起来，
如果路由映射里有多个分组，逻辑函数就需要多个形式参数接收**

[code]

    """Xiangmu URL Configuration
    
    The `urlpatterns` list routes URLs to views. For more information please see:
        https://docs.djangoproject.com/en/1.10/topics/http/urls/
    Examples:
    Function views
        1. Add an import:  from my_app import views
        2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
    Class-based views
        1. Add an import:  from other_app.views import Home
        2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
    Including another URLconf
        1. Import the include() function: from django.conf.urls import url, include
        2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
    """
    from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),   #系统生成的映射
    
        url(r'^(articles/2003)/$', views.special_case_2003),                         #表示articles/2003/这个路径映射views模块的special_case_2003函数
        # url(r'^articles/([0-9]{4})/$', views.year_archive),                        #表示2003可以是0-9的任意4个数字
        # url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),            #表示匹配二级目录
        # url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),  #表示匹配三级目录
    ]
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709100858790-1230188269.png)

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709100921400-2131964771.png)**

**  上面我们讲到的是自定义形式参数接收访问路径，下面我们讲设置固定形式参数**

**逻辑处理函数，接收用户访问路径时设置固定形式参数，**

**需要在路由映射里设置，逻辑函数接收的参数名称?P <year>**

**路由映射**

[code]

     """Xiangmu URL Configuration
    
    The `urlpatterns` list routes URLs to views. For more information please see:
        https://docs.djangoproject.com/en/1.10/topics/http/urls/
    Examples:
    Function views
        1. Add an import:  from my_app import views
        2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
    Class-based views
        1. Add an import:  from other_app.views import Home
        2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
    Including another URLconf
        1. Import the include() function: from django.conf.urls import url, include
        2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
    """
    from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),   #系统生成的映射
    
        url(r'^( **?P <year>**articles/2003)/$', views.special_case_2003),                         #表示articles/2003/这个路径映射views模块的special_case_2003函数
        # url(r'^articles/([0-9]{4})/$', views.year_archive),                        #表示2003可以是0-9的任意4个数字
        # url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),            #表示匹配二级目录
        # url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),  #表示匹配三级目录
    ]
[/code]

**逻辑处理**

[code]

     from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special_case_2003(request,year):
        print(year)
        return render(request,'index.html')
[/code]





**逻辑处理返回html文件**

**将HTML文件放到 templates文件夹，逻辑处理的时候会自动到这个文件夹搜索相应文件**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709110016212-416757330.png)**

**需要先导入render方法**

**render(用户请求对象，html文件路径名称) 方法,向用户返回html文件内容**

[code]

    from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special_case_2003(request,name):
        return render(request,'index.html')
[/code]



**整个流程**

**路由映射**

[code]

     """Xiangmu URL Configuration
    
    The `urlpatterns` list routes URLs to views. For more information please see:
        https://docs.djangoproject.com/en/1.10/topics/http/urls/
    Examples:
    Function views
        1. Add an import:  from my_app import views
        2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
    Class-based views
        1. Add an import:  from other_app.views import Home
        2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
    Including another URLconf
        1. Import the include() function: from django.conf.urls import url, include
        2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
    """
    from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),   #系统生成的映射
    
        url(r'^(articles/2003)/$', views.special_case_2003),                         #表示articles/2003/这个路径映射views模块的special_case_2003函数
        # url(r'^articles/([0-9]{4})/$', views.year_archive),                        #表示2003可以是0-9的任意4个数字
        # url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),            #表示匹配二级目录
        # url(r'^articles/([0-9]{4})/([0-9]{2})/([0-9]+)/$', views.article_detail),  #表示匹配三级目录
    ]
[/code]

**逻辑处理**

[code]

     from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special_case_2003(request,name):
        return render(request,'index.html')
[/code]



****整个流程图****

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709110926837-1138776157.png)**



**上面讲的，都是通过全局里的urls.py模块路由映射的，如果网站很大有很多个app应用，那么就需要路由分发，每一个app应用负责一个业务**

****路由分发****

****过个全局里的 **urls.py模块，配置路由分发，将制定的路径分发到指定的app应用里的 ** **
**urls.py模块里路由映射************

************全局 ** ** **urls.py模块路由分发******************

******************首先要在全局 ** ** ** ** ** ** ** **
**urls.py模块引入************************************

************************************from django.conf.urls import include,
url************************************

************************************include('app1.urls')
函数，设置要分发的路由映射路径名称************************************



**************全局 ** ** **urls.py模块路由分发********************

[code]

     from django.conf.urls import include, url
    urlpatterns = [
        url(r'^bug', include('app1.urls')),   #将访问路径以bug开头的路径分发到app1下的urls.py模块里进行路由映射
    
    ]
[/code]

**app1.py路由映射**

[code]

     from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'articles/', views.special),  #表示接收全局的路由分发，做路由映射，映射到views下的special函数处理
    ]
[/code]

**views.py逻辑处理**

[code]

     from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special(request):
        return render(request,'index.html')   #向用户显示一个html页面
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709143352384-941891911.png)





**路由映射第三个参数，额外传参，字典方式，逻辑处理函数以参数方式接收字典键**

**路由映射**

[code]

     from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'articles/', views.special,{'anme':1234})     #路由映射第三个参数，额外传参，字典方式，逻辑处理函数以参数方式接收字典键
    ]
[/code]

**逻辑处理**

[code]

     from django.shortcuts import render,HttpResponse
    
    # Create your views here.
    
    def special(request,anme):
        print(anme)                           #接收路由映射的额外传参字典的键
        return render(request,'index.html')   #向用户显示一个html页面
[/code]

**注意：如果额外参数，如果写在全局的路由分发里，那么这个路由分发下的所有路由映射函数都可以获取到**





****路由映射第四个参数，给路由映射的路径取一个别名，这个别名代指的就是路由映射路径，****

[code]

     from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'articles/', views.special,{'anme':1234},name='luj')     #路由映射第三个参数，额外传参，字典方式，逻辑处理函数以参数方式接收字典键
    ]
[/code]



**最终url控制器流程图**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709153344634-65438795.png)**



