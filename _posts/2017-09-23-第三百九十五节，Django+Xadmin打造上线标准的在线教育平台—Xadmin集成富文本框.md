
---
layout: post
title: " 第三百九十五节，Django+Xadmin打造上线标准的在线教育平台—Xadmin集成富文本框 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十五节，Django+Xadmin打造上线标准的在线教育平台—Xadmin集成富文本框**



**首先安装DjangoUeditor3模块**

**Ueditor HTML编辑器是百度开源的HTML编辑器**



**下载地址  https://github.com/andyzsf/DjangoUeditor3**

**下载后解压下载包，找到 DjangoUeditor3-master\DjangoUeditor文件夹**

**  将DjangoUeditor文件夹，整个文件夹复制到 **Xadmin同级目录****

****![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923174953478-1149284164.png)****





**安装好后在settings.py将 DjangoUeditor添加到app**

[code]

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
        'xadmin',                           # 注册xadmin的app
        'crispy_forms',                     # 注册xadmin的依赖app
        'captcha',                          # 注册验证码app
        'pure_pagination',                  # 注册分页app
        'DjangoUeditor'                     # 注册DjangoUeditor的APP
    ]
[/code]





**然后在全局的urls.py文件配置路由映射**

[code]

    urlpatterns = [
        url(r '^xadmin/', xadmin.site.urls),
    
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
        url(r'media/(?P<path>.*)$', serve, {'document_root': MEDIA_ROOT}),
    
        # 配置静态文件访问
        # url(r'static/(?P<path>.*)$', serve, {'document_root': STATIC_ROOT}),
    
        url(r'course_comment.html', course_comment.as_view(), name='course_comment'),
        url(r'usercenter_info.html', usercenter_info.as_view(), name='usercenter_info'),
    
        # 上传头像
        url(r'touxiang/', touxiang.as_view(), name='touxiang'),
    
        # 配置DjangoUeditor富文本路由映射
        url(r'^ueditor/',include('DjangoUeditor.urls' ))
    ]
[/code]





**在models.py文件，在要使用 **富文本框** 的字段使用UEditorField**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    from DjangoUeditor.models import UEditorField
    from system.storage import ImageStorage
    
    
    class Course(models.Model):
        name = models.CharField(max_length=50, verbose_name='课程名称')
        desc = models.CharField(max_length=300, verbose_name='课程描述')
        detail = UEditorField(verbose_name='内容',
                              width=900,height=300,
                              imagePath="neird/tup/",
                              filePath="neird/wjian/",
                              default='',
                              toolbars='mini')
        degree = models.CharField(verbose_name='课程级别', choices=(('cj', '初级'), ('zj', '中级'), ('gj', '高级')), max_length=3)
        learn_times = models.IntegerField(default=0, verbose_name='学习时长(分钟)')
        students = models.IntegerField(default=0, verbose_name='学习人数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏人数')
        image = models.ImageField(upload_to='courses/%Y/%m', verbose_name='课程封面图', max_length=100)
        click_nums = models.IntegerField(default=0, verbose_name='点击数')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加时间')
    
        class Meta:
            verbose_name = '课程'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name        # 设置在xadmin后台显示字段, 注意如果此表被另外的了外键关联了，这个返回字段就是外键表的外键名称
[/code]





**在adminx.py文件里找到对应的数据表管理器，在管理器里指定字段用 **富文本框****

**style_fields = {'字段名称':'ueditor'}指定字段使用富文本框**

[code]

     class CourseAdmin(object):               # 自定义数据表管理器类
    
        # 设置xadmin后台显示字段
        list_display = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                        'fav_nums', 'image', 'click_nums', 'add_time']
    
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                         'fav_nums', 'image', 'click_nums']
    
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                       'fav_nums', 'image', 'click_nums', 'add_time']
        model_icon = 'fa fa-clone'
        style_fields = {'detail':'ueditor'}
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
[/code]





****富文本框参数说明****

[code]

     Ueditor HTML编辑器是百度开源的HTML编辑器，
    
    本模块帮助在Django应用中集成百度Ueditor HTML编辑器。
    安装包中已经集成Ueditor v1.3.6
    
    使用Django-Ueditor非常简单，方法如下：
    
    1、安装方法
        
        **方法一：下载安装包，在命令行运行：
            python setup.py install
        **方法二：使用pip工具在命令行运行(推荐)：
               pip install DjangoUeditor
    
    2、在INSTALL_APPS里面增加DjangoUeditor app，如下：
         
            INSTALLED_APPS = (
                #........
                'DjangoUeditor',
            )
    
    
    3、在urls.py中增加：
    
        url(r'^ueditor/',include('DjangoUeditor.urls' )),
    
    4、在models中这样定义：
        
        from DjangoUeditor.models import UEditorField
        class Blog(models.Model):
            Name=models.CharField(,max_length=100,blank=True)
            Content=UEditorField('内容    ',height=100,width=500,default='test',imagePath="uploadimg/",imageManagerPath="imglib",toolbars='mini',options={"elementPathEnabled":True},filePath='upload',blank=True)
    
        说明：
        UEditorField继承自models.TextField,因此你可以直接将model里面定义的models.TextField直接改成UEditorField即可。
        UEditorField提供了额外的参数：
            toolbars:配置你想显示的工具栏，取值为mini,normal,full,besttome, 代表小，一般，全部,涂伟忠贡献的一种样式。如果默认的工具栏不符合您的要求，您可以在settings里面配置自己的显示按钮。参见后面介绍。
            imagePath:图片上传的路径,如"images/",实现上传到"{{MEDIA_ROOT}}/images"文件夹
            filePath:附件上传的路径,如"files/",实现上传到"{{MEDIA_ROOT}}/files"文件夹
            scrawlPath:涂鸦文件上传的路径,如"scrawls/",实现上传到"{{MEDIA_ROOT}}/scrawls"文件夹,如果不指定则默认=imagepath
            imageManagerPath:图片管理器显示的路径，如"imglib/",实现上传到"{{MEDIA_ROOT}}/imglib",如果不指定则默认=imagepath。
            options：其他UEditor参数，字典类型。参见Ueditor的文档ueditor_config.js里面的说明。
            css:编辑器textarea的CSS样式
            width，height:编辑器的宽度和高度，以像素为单位。
    
    5、在表单中使用非常简单，与常规的form字段没什么差别，如下：
        
        class TestUeditorModelForm(forms.ModelForm):
            class Meta:
                model=Blog
        ***********************************
        如果不是用ModelForm，可以有两种方法使用：
    
        1: 使用forms.UEditorField
    
        from  DjangoUeditor.forms import UEditorField
        class TestUEditorForm(forms.Form):
            Description=UEditorField("描述",initial="abc",width=600,height=800)
        
        2: widgets.UEditorWidget
    
        from  DjangoUeditor.widgets import UEditorWidget
        class TestUEditorForm(forms.Form):
            Content=forms.CharField(label="内容",widget=UEditorWidget(width=800,height=500, imagePath='aa', filePath='bb',toolbars={}))
        
        widgets.UEditorWidget和forms.UEditorField的输入参数与上述models.UEditorField一样。
    
    6、Settings配置
         
          在Django的Settings可以配置以下参数：
                UEDITOR_SETTINGS={
                    "toolbars":{           #定义多个工具栏显示的按钮，允行定义多个
                        "name1":[[ 'source', '|','bold', 'italic', 'underline']],
                        "name2",[]
                    },
                    "images_upload":{
                        "allow_type":"jpg,png",    #定义允许的上传的图片类型
                        "max_size":"2222kb"        #定义允许上传的图片大小，0代表不限制
                    },
                    "files_upload":{
                         "allow_type":"zip,rar",   #定义允许的上传的文件类型
                         "max_size":"2222kb"       #定义允许上传的文件大小，0代表不限制
                     },,
                    "image_manager":{
                         "location":""         #图片管理器的位置,如果没有指定，默认跟图片路径上传一样
                    },
                }
    7、在模板里面：
    
        <head>
            ......
            {{ form.media }}        #这一句会将所需要的CSS和JS加进来。
            ......
        </head>
        注：运行collectstatic命令，将所依赖的css,js之类的文件复制到{{STATIC_ROOT}}文件夹里面。
    
    8、高级运用：
    
         ****************
         动态指定imagePath、filePath、scrawlPath、imageManagerPath
         ****************
         这几个路径文件用于保存上传的图片或附件，您可以直接指定路径，如：
              UEditorField('内容',imagePath="uploadimg/")
         则图片会被上传到"{{MEDIA_ROOT}}/uploadimg"文件夹，也可以指定为一个函数，如：
    
          def getImagePath(model_instance=None):
              return "abc/"
          UEditorField('内容',imagePath=getImagePath)
          则图片会被上传到"{{MEDIA_ROOT}}/abc"文件夹。
         ****************
         使上传路径(imagePath、filePath、scrawlPath、imageManagerPath)与Model实例字段值相关
         ****************
            在有些情况下，我们可能想让上传的文件路径是由当前Model实例字值组名而成，比如：
            class Blog(Models.Model):
                Name=models.CharField('姓名',max_length=100,blank=True)
                Description=UEditorField('描述',blank=True,imagePath=getUploadPath,toolbars="full")
    
         id  |   Name    |       Description
         ------------------------------------
         1   |   Tom     |       ...........
         2   |   Jack    |       ...........
    
          我们想让第一条记录上传的图片或附件上传到"{{MEDIA_ROOT}}/Tom"文件夹,第2条记录则上传到"{{MEDIA_ROOT}}/Jack"文件夹。
          该怎么做呢，很简单。
          def getUploadPath(model_instance=None):
              return "%s/" % model_instance.Name
          在Model里面这样定义：
          Description=UEditorField('描述',blank=True,imagePath=getUploadPath,toolbars="full")
          这上面model_instance就是当前model的实例对象。
          还需要这样定义表单对象：
          from  DjangoUeditor.forms import UEditorModelForm
          class UEditorTestModelForm(UEditorModelForm):
                class Meta:
                    model=Blog
          特别注意：
             **表单对象必须是继承自UEditorModelForm，否则您会发现model_instance总会是None。
             **同时在Admin管理界面中，此特性无效，model_instance总会是None。
             **在新建表单中，model_instance由于还没有保存到数据库，所以如果访问model_instance.pk可能是空的。因为您需要在getUploadPath处理这种情况
    
    
    class UEditorTestModelForm(UEditorModelForm):
        class Meta:
            model=Blog
    
    
    
    
    8、其他事项：
    
        **本程序版本号采用a.b.ccc,其中a.b是本程序的号，ccc是ueditor的版本号，如1.2.122，1.2是DjangoUeditor的版本号，122指Ueditor 1.2.2.
        **本程序安装包里面已经包括了Ueditor，不需要再额外安装。
        **目前暂时不支持ueditor的插件
        **别忘记了运行collectstatic命令，该命令可以将ueditor的所有文件复制到{{STATIC_ROOT}}文件夹里面
        **Django默认开启了CSRF中间件，因此如果你的表单没有加入{% csrf_token %}，那么当您上传文件和图片时会失败
       
[/code]

**效果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923180146150-1761417760.png)**



