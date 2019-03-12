
---
layout: post
title: " 第三百八十二节，Django+Xadmin打造上线标准的在线教育平台—xadmin管理员详情页面布局，导航图标设置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十二节，Django+Xadmin打造上线标准的在线教育平台—xadmin进阶**



**1、后台管理员详情页面布局**

****后台管理员详情页面，区块是可以拖动的，而且分为了很多个区块****

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911210256547-1707755522.png)**



**这个页面的布局在xadmin/plugins/auth.py里的UserAdmin类，修改这个类里的get_form_layout函数，就可以修改布局**

[code]

     def get_form_layout(self):
        if self.org_obj:
            self.form_layout = (
            #Fieldset表示一个区块
                Main(
                    Fieldset('',
                             'username', 'password',                    # 显示字段
                             css_class='unsort no_title'                # css_class='unsort no_title'表示定位区块不能拖动
                             ),
                    Fieldset(_('Personal info'),                        #Fieldset第一个参数表示区块名称
                             Row('first_name', 'last_name'),            # Row 表示将里面的字段作为一行显示
                             'email',
                             ),
                    Fieldset(_('Permissions'),
                             'groups', 'user_permissions',
                             ),
                    Fieldset(_('Important dates'),
                             'last_login', 'date_joined',
                             ),
                ),
                #Side表示状态区块
                Side(
                    Fieldset(_('Status'),
                             'is_active', 'is_staff', 'is_superuser',
                             ),
                )
            )
        return super(UserAdmin, self).get_form_layout()
[/code]

**如下修改将所有区块定位，不能拖动**

[code]

         def get_form_layout(self):
            if self.org_obj:
                self.form_layout = (
                    Main(
                        Fieldset('',
                                 'username', 'password',
                                 css_class='unsort no_title'
                                 ),
                        Fieldset(_('Personal info'),
                                 Row('first_name', 'last_name'),
                                 'email',
                                 css_class='unsort no_title'
                                 ),
                        Fieldset(_('Permissions'),
                                 'groups', 'user_permissions',
                                 css_class='unsort no_title'
                                 ),
                        Fieldset(_('Important dates'),
                                 'last_login', 'date_joined',
                                 css_class='unsort no_title'
                                 ),
                    ),
                    Side(
                        Fieldset(_('Status'),
                                 'is_active', 'is_staff', 'is_superuser',
                                 ),
                    )
                )
            return super(UserAdmin, self).get_form_layout()
[/code]





**2、导航图标设置**

**导航图标采用 **font-awesome图标****

****如果想用最新版本的 ** **font-awesome图标，到 **
**中文网站<http://fontawesome.dashgame.com/>
下载解压后将解压的css和fonts两个文件夹，替换xadmin/static/xadmin/vendor/font-
awesome/下的相同文件************

************导航子目录图标设置，也就是数据表的图标************

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170912110613438-2001389184.png)**

**在当前app目录下的 adminx.py数据库表注册的管理器里设置**  
 **model_icon = 'fa fa-图标名称'**  
 **如：model_icon = 'fa fa-user-plus'**

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
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]





**************导航主目录图标设置，也就是自定义的app名称的图标**************

**这个我没找到可以设置的地方只有改源码了**

**修改源码**

**修改xadmin/templates/xadmin/includes/ sitemenu_accordion.html文件**

[code]

    {% extends 'xadmin/includes/sitemenu_default.html' %}
    {% load i18n xadmin_tags %}
    
    
    {% block navbar_md %}
    <div class="panel-group hide-sm nav-sitemenu col-md-2" id="nav-accordion">
      {% for item in nav_menu %}
      <div class="panel panel-{% if item.selected %}info{%else%}default{% endif %}">
        <div class="panel-heading">
          <h6 class="panel-title">
            <span class="badge badge-info">{{ item.menus|length }}</span>
            <a class="accordion-toggle" data-toggle="collapse" data-parent="#nav-accordion" href="#nav-panel-{{forloop.counter}}">
              {% if item.url %}<a href="{{ item.url }}" class="section">{% endif %}
              {% if item.icon %}<i class="fa-fw {{item.icon}}"></i>
              {% elif item.first_icon %}  {#<i class="fa-fw {{item.first_icon}}"></i>#} {#这个标签注释后，当子导航设置了图标时app名称不显示图标#}
              {%else%}<i class="fa-fw fa fa-circle-o"></i>{% endif %}
              {% autoescape off %} {% trans item.title %} {% endautoescape %}   {#这里显示的自定义app名称，加上{% autoescape off %}{% endautoescape %}后在自定义名称时可以通过class自定义图标#}
              {% if item.url %}</a>{% endif %}
            </a>
          </h6>
        </div>
        <div id="nav-panel-{{forloop.counter}}" class="list-group panel-collapse collapse{% if item.selected %} in{% endif %}">
          {% for sitem in item.menus %}
          <a href="{{ sitem.url|default_if_none:'#' }}" class="list-group-item{% if sitem.selected %} active{% endif %}">
            {% if sitem.icon %}<i class="fa-fw {{sitem.icon}}"></i>{%else%}<i class="fa-fw fa fa-circle-o"></i>{% endif %}
            {{ sitem.title }}</span>
          </a>
          {% endfor %}
        </div>
      </div>
      {% endfor %}
    </div>
    {% endblock navbar_md %}
[/code]

**sitemenu_accordion.html 文件修改后**

**在当前app目录的 apps.py文件里设置后台app名称时用class自定义图标**

[code]

    from django.apps import AppConfig
    
    
    class AppUsersConfig(AppConfig):
        name = 'app_users'                  # app目录名称
        verbose_name = '<i class="fa fa-user-secret"></i>用户管理'  # 要设置的中文名称
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170912112851938-207163576.png)





** **

