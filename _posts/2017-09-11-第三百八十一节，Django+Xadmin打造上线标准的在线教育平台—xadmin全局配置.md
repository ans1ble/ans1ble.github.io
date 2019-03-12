
---
layout: post
title: " 第三百八十一节，Django+Xadmin打造上线标准的在线教育平台—xadmin全局配置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十一节，Django+Xadmin打造上线标准的在线教育平台—xadmin全局配置**



**1、xadmin主题设置**

**要使用xadmin主题，需要在一个app下的adminx.py后台注册文件里，写一个主题管理器绑定xadmin的views.BaseAdminView注册**  
 **一般我们会在用户相关的app下的adminx.py后台注册文件里写**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import xadmin
    from xadmin import views                # 导入xadmin的views
    
    from .models import Users, Email, Banner
    
    
    class BasdSetting(object):              # 主题管理器
        enable_themes = True                # 使用主题
        use_bootswatch = True
    xadmin.site.register(views.BaseAdminView, BasdSetting)      # 将主题管理器绑定views.BaseAdminView注册
    
    
    class UsersAdmin(object):               # 自定义用户信息数据表管理器类
        # 设置xadmin后台显示字段
        list_display = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined']
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile']
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
    
    
    class EmailAdmin(object):
        list_display = ['code', 'email', 'send_type', 'send_time']
        search_fields = ['code', 'email', 'send_type']
        list_filter = ['code', 'email', 'send_type', 'send_time']
    xadmin.site.register(Email, EmailAdmin)
    
    
    class BannerAdmin(object):
        list_display = ['title', 'index', 'image', 'url', 'add_time']
        search_fields = ['title', 'index', 'image', 'url']
        list_filter = ['title', 'index', 'image', 'url', 'add_time']
    xadmin.site.register(Banner, BannerAdmin)
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911145357235-553443810.png)



  
**2、头部系统名称和底部版权以及导航折叠设置**  
**需要在一个app下的adminx.py后台注册文件里，写一个头部系统名称和底部版权管理器绑定xadmin的views.CommAdminView注册**  
 **一般我们会在用户相关的app下的adminx.py后台注册文件里写**

[code]

     import xadmin
    from xadmin import views                # 导入xadmin的views
    
    from .models import Users, Email, Banner
    
    
    class BasdSetting(object):              # 主题管理器
        enable_themes = True                # 使用主题
        use_bootswatch = True
    xadmin.site.register(views.BaseAdminView, BasdSetting)      # 将主题管理器绑定views.BaseAdminView注册
    
    
    class GlobalSettings(object):                               # 头部系统名称和底部版权管理器
        site_title = '玉秀管理系统'                              # 头部系统名称
        site_footer = '玉秀管理系统，玉秀公司版权所有'             # 底部版权
        menu_style = 'accordion'                                # 设置数据管理导航折叠，以每一个app为一个折叠框
    xadmin.site.register(views.CommAdminView, GlobalSettings)   # 头部系统名称和底部版权管理器绑定views.CommAdminView注册
    
    
    class UsersAdmin(object):               # 自定义用户信息数据表管理器类
        # 设置xadmin后台显示字段
        list_display = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined']
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile']
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
    
    
    class EmailAdmin(object):
        list_display = ['code', 'email', 'send_type', 'send_time']
        search_fields = ['code', 'email', 'send_type']
        list_filter = ['code', 'email', 'send_type', 'send_time']
    xadmin.site.register(Email, EmailAdmin)
    
    
    class BannerAdmin(object):
        list_display = ['title', 'index', 'image', 'url', 'add_time']
        search_fields = ['title', 'index', 'image', 'url']
        list_filter = ['title', 'index', 'image', 'url', 'add_time']
    xadmin.site.register(Banner, BannerAdmin)
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911171033078-1240766998.png)





**3、导航app名称设置成中文，需要以下两步**

**在当前app目录下的apps.py文件里配置后台要显示的中文名称**

****apps.py文件****

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from django.apps import AppConfig
    
    
    class AppCoursesConfig(AppConfig):
        name = 'app_courses'            # 当前app名称
        verbose_name = '课程管理'        # 要设置的中文名称
[/code]

**在当前app目录下的__init__.py文件里应用app中文名称设置类的路径**

**default_app_config = app中文名称设置类的路径，从app开始到类**

****__init__.py文件****

[code]

    default_app_config =  'app_courses.apps.AppCoursesConfig'
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911173415157-156209427.png)



