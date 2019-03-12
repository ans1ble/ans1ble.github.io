
---
layout: post
title: " 第三百八十七节，Django+Xadmin打造上线标准的在线教育平台—网站上传资源的配置与显示 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十七节，Django+Xadmin打造上线标准的在线教育平台—网站上传资源的配置与显示**



**首先了解一下static静态文件与上传资源的区别， **static静态文件里面一般防止的我们网站样式的文件，包括ccs，js，网站样式图片****

****上传资源是用户操作上传的图片等资源****



******上传资源的配置******

******1，首先在项目里创建一个名称叫 media的文件夹专门保存用户上传******

******2，settings.py文件配置上传资源的路径******

[code]

     # 上传资源路径，如果图片，上传文件等
    MEDIA_URL = '/media/'                           # 设置上传资源前缀名称
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')    # 设置上传文件路径
[/code]

**这样配置好后，当用户上传文件时，会根据数据表类的上传字段设置来，将文件上传到， ** ** **media文件夹里，如下********

**数据表类**

[code]

     class CourseOrg(models.Model):
        name = models.CharField(max_length=50, verbose_name='机构名称')
        desc = models.TextField(verbose_name='机构描述')
        category = models.CharField(max_length=20, verbose_name='机构类别', default='pxjg', choices=(('pxjg', '培训机构'), ('gx', '高校'), ('gr', '个人')))
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        image = models.ImageField(upload_to='org/%Y/%m', verbose_name='封面图', max_length=100)
        address = models.CharField(max_length=150, verbose_name='机构地址')
        city = models.ForeignKey(CityDict, verbose_name='外键城市表')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程机构表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170917105920547-526599002.png)

**此时可以看到上传文件安装年月来保存文件，那么怎么设置文件名**



**设置上传文件名称**

**1、先在你项目中添加一个文件夹如：`system` 在文件夹下添加`__init__.py`
和`storage.py`文件,并在`storage.py`中添加如下代码：**

[code]

     # -*- coding: UTF-8 -*-
    from django.core.files.storage import FileSystemStorage
    from django.http import HttpResponse  
    
    class ImageStorage(FileSystemStorage):
        from django.conf import settings
        
        def __init__(self, location=settings.MEDIA_ROOT, base_url=settings.MEDIA_URL):
            # 初始化
            super(ImageStorage, self).__init__(location, base_url)
    
        # 重写 _save方法        
        def _save(self, name, content):
            #name为上传文件名称
            import os, time, random
            # 文件扩展名
            ext = os.path.splitext(name)[1]
            # 文件目录
            d = os.path.dirname(name)
            # 定义文件名，年月日时分秒随机数
            fn = time.strftime('%Y%m%d%H%M%S')
            fn = fn + '_%d' % random.randint(0,100)
            # 重写合成文件名
            name = os.path.join(d, fn + ext)
            # 调用父类方法
            return super(ImageStorage, self)._save(name, content)
[/code]

**2、在`models.py`文件中添加如下代码：**

**在数据库文件导入我们设置的类**

**在上传字段里设置 storage=ImageStorage()执行类，就是我们自定义 **`storage.py`中的类****

[code]

     from system.storage import ImageStorage
    pic=models.ImageField(upload_to='img/%Y/%m/%d',storage=ImageStorage())  #如果上传文件可以将ImageField换为FileField
[/code]



**上传文件显示**

**上传的文件如图片，要在前台或者后台显示，就需要配置才能显示**

**要给上传文件访问配置一个专门的url路由映射**

[code]

     from django.conf.urls import url, include                   # 导入django自在的include逻辑
    from django.contrib import admin
    from django.views.generic import TemplateView               # 导入django自带的TemplateView逻辑
    from django.views.static import serve                       # 导入django自带的serve静态资源逻辑
    import xadmin                                               # 导入xadmin
    
    from app_users.views import deng_lu, zhu_ce, active_code, logout                 # 导入登录逻辑处理类
    from app_organization.views import org_list                                      # 导入授课机构逻辑
    from MxOnline.settings import MEDIA_ROOT
    
    
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        # 注册
        url(r'^register.html', zhu_ce.as_view(), name='register'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
        url(r'^active/(?P<active_de>.*)/$', active_code.as_view(), name="user_active"),
    
        # 登录
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
        url(r'^logout', logout.as_view(), name='deng_lu'),
    
        # 授课机构
        url(r'^org_list.html', org_list.as_view(), name='org_list'),
    
        # 专门处理静态资源请求映射，也就是media上传文件夹里的请求映射
        url(r'media/(?P<path>.*)$', serve, {'document_root': MEDIA_ROOT})　　# MEDIA_ROOT为配置上传文件的路径变量
    ]
[/code]

**此时后台可以显示图片了**



**前台显示可以通过settings.py配置的上传资源前缀名称来拼接路径显示**

**HTML文件**

[code]

                                    <a href= "org-detail-homepage.html">
                                        <img width="200" height="120" class="scrollLoading"
                                             data-url="{{ MEDIA_URL }}{{ ji.image }}"/>         {# 需要拼接静态资源路径 #}
                                    </a>
[/code]

**注意：如果在html文件要获取到settings.py配置的MEDIA_URL，需要在配置文件设置一个静态资源处理类**

[code]

    TEMPLATES = [
        {
             'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')],                      # 配置模板文件路径，也就是html路径
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                    'django.template.context_processors.media',                 # 配置html页面获取MEDIA_URL路径
                ],
            },
        },
    ]
[/code]



** **



