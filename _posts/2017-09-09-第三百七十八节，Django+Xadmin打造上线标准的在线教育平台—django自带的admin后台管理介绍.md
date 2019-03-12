
---
layout: post
title: " 第三百七十八节，Django+Xadmin打造上线标准的在线教育平台—django自带的admin后台管理介绍 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十八节，Django+Xadmin打造上线标准的在线教育平台—django自带的admin后台管理介绍**



**配置django的admin数据库管理后台**

**首先urls.py配置数据库后台路由映射,一般这个路由映射在生成项目的时候已经生成了**

![复制代码](https://common.cnblogs.com/images/copycode.gif)

[code]

    from django.conf.urls import url
     from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
        url(r'admin/', admin.site.urls),   #路由映射admin数据库管理
        url(r'articles/', views.special)     #路由映射第三个参数，额外传参，字典方式，逻辑处理函数以参数方式接收字典键
    ]
[/code]

![复制代码](https://common.cnblogs.com/images/copycode.gif)

**然后在PyCharm终端输入命令  Python manage.py createsuperuser**

**1、设置用户名**

**2、设置邮箱**

**3、设置密码，8位以上，不能纯数字**

**4、确认密码**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909194844272-498420013.png)**



**然后用刚才设置的用户名和密码登录**

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909195151538-1606551925.png)

**登录后可以看到后台是英文的，我们可以设置成中文，在 settings.py文件配置**

[code]

    # Internationalization
    # https://docs.djangoproject.com/en/1.10/topics/i18n/
    
    LANGUAGE_CODE = 'zh-hans'       # 设置自带后台admin为中文
    
    TIME_ZONE = 'Asia/Shanghai'     # 设置系统时间为上海时间
    
    USE_I18N = True
    
    USE_L10N = True
    
    USE_TZ = False                  # 设置数据库写入时间，不用国际时间
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909195627335-1369301354.png)

**将数据库的表注册到admin页面显示**

**默认，admin页面只注册了Django系统生成的用户表，所以我们只能看到这张表，我们自定义的数据库表，需要在对应的
app的admin.py文件里注册表到admin页面才能显示**



**admin.site.register(参数是数据库操作表的类) ，注册数据库表到admin页面显示，参数是models.py里操作数据库表的类**

****admin.py****

[code]

     from django.contrib import admin
    
    from app_courses.models import Course
    
    
    class CourseAdmin(admin.ModelAdmin):    # 自定义一个类继承admin.ModelAdmin类，设置一个表的管理器
        pass
    
    admin.site.register(Course)             # 注册数据库到admin后台显示，参数是models.py里操作数据库表的类
[/code]



