
---
layout: post
title: " 第三百九十三节，Django+Xadmin打造上线标准的在线教育平台—Xadmin后台进阶开发配置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十三节，Django+Xadmin打造上线标准的在线教育平台—Xadmin后台进阶开发配置**



**设置后台某个字段的排序规则**

**在当前APP里的adminx.py文件里的数据表管理器里设置**

**ordering = ['-要排序的字段名称']-为倒序排序**

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
        model_icon = 'fa fa-user-plus'
        ordering = ['-id']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]





**设置后台某个字段为只读，不能修改**

****在当前APP里的adminx.py文件里的数据表管理器里设置****

****readonly_fields = ['要设置只读的字段名称']****

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
        model_icon = 'fa fa-user-plus'
        ordering = ['-id']
        readonly_fields = ['password']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]





**设置后台某个字段不显示**

**在当前APP里的adminx.py文件里的数据表管理器里设置**

**exclude = ['要隐藏的字段']**

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
        model_icon = 'fa fa-user-plus'
        ordering = ['-id']
        readonly_fields = ['password']
        exclude = ['first_name','last_name']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]





**设置后台某个外键字段，点击后不完全将数据加载出来，如果数据太大就很有用了，设置后会根据用户搜索词来显示外键，也就是自动ajax请求数据**

**注意：这个要设置在外键连接的表里，不是设置在外键表里【重点】**

**在当前APP里的adminx.py文件里的数据表管理器里设置**

[code]

     class CityDictAdmin(object):
        list_display = ['name', 'desc', 'add_time']
        search_fields = ['name', 'desc']
        list_filter = ['name', 'desc', 'add_time']
        model_icon = 'fa fa-flag-o'
        relfield_style = 'fk-ajax'
    xadmin.site.register(CityDict, CityDictAdmin)
[/code]

**数据库文件**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    
    from system.storage import ImageStorage
    
    
    class CityDict(models.Model):
        name = models.CharField(max_length=20, verbose_name='城市')
        desc = models.CharField(max_length=200, verbose_name='描述')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '城市表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name
    
    
    class CourseOrg(models.Model):
        name = models.CharField(max_length=50, verbose_name='机构名称')
        desc = models.TextField(verbose_name='机构描述')
        category = models.CharField(max_length=20, verbose_name='机构类别', default='pxjg', choices=(('pxjg', '培训机构'), ('gx', '高校'), ('gr', '个人')))
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        image = models.ImageField(upload_to='org/%Y/%m', storage=ImageStorage(), verbose_name='封面图', max_length=100)
        address = models.CharField(max_length=150, verbose_name='机构地址')
        city = models.ForeignKey(CityDict, verbose_name='外键城市表')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程机构表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name
[/code]





**当添加或者编辑被外键表数据时，将外键表自动组装到被外键表**

****在当前APP里的adminx.py文件里的数据表管理器里设置****

**  注意：只能将外键表组装到被外键表**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import xadmin
    
    from .models import CityDict, CourseOrg, Teacher
    
    
    class Lessonline(object):                           # 自定义类来组装，当添加或者编辑被外键表数据时，将外键表自动组装到被外键表
        model =CourseOrg                                # 设置外键表类名称
        extra = 0
    
    
    class CityDictAdmin(object):                        # 城市表被机构表外键
        list_display = ['name', 'desc', 'add_time']
        search_fields = ['name', 'desc']
        list_filter = ['name', 'desc', 'add_time']
        model_icon = 'fa fa-flag-o'
        relfield_style = 'fk-ajax'
        inlines = [Lessonline]                          # 在被外键表写入inlines = 组装来
    xadmin.site.register(CityDict, CityDictAdmin)
    
    
    class CourseOrgAdmin(object):                       # 机构表外键了城市表
        list_display = ['name', 'desc', 'click', 'fav_nums', 'image', 'address', 'city', 'add_time']
        search_fields = ['name', 'desc', 'fav_nums', 'address']
        list_filter = ['name', 'desc', 'click', 'fav_nums', 'image', 'address', 'city', 'add_time']
        model_icon = 'fa fa-graduation-cap '
    xadmin.site.register(CourseOrg, CourseOrgAdmin)
[/code]





**后台显示两张表名称，管理的同一张表**

**实现原理，在models重新定义一个数据表类，继承原来的表，不写任何字段设置表名称，设置不生成表，然后将新定义的表类注册到后台即可，注册和显示字段等配置给原理的注册同理**

****models****

****注意： ** **models里一定要设置  ****proxy = True 否则会生成新的表****

[code]

    class CourseOrg(models.Model):
        name = models.CharField(max_length=50, verbose_name='机构名称')
        desc = models.TextField(verbose_name='机构描述')
        category = models.CharField(max_length=20, verbose_name='机构类别', default='pxjg', choices=(('pxjg', '培训机构'), ('gx', '高校'), ('gr', '个人')))
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        image = models.ImageField(upload_to='org/%Y/%m', storage=ImageStorage(), verbose_name='封面图', max_length=100)
        address = models.CharField(max_length=150, verbose_name='机构地址')
        city = models.ForeignKey(CityDict, verbose_name='外键城市表')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程机构表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name
    
    
    class CourseOrg2(CourseOrg):                    # 继承机构表
        class Meta:
            verbose_name = '课程机构表2'
            verbose_name_plural = verbose_name
            proxy = True                            # 表示不生成表
[/code]

****在当前APP里的adminx.py文件里的数据表管理器里设置****

[code]

     class CourseOrg2Admin(object):
        # 设置xadmin后台显示字段
        list_display = ['name']
    xadmin.site.register(CourseOrg2, CourseOrg2Admin)
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170922173506212-879197076.png)



