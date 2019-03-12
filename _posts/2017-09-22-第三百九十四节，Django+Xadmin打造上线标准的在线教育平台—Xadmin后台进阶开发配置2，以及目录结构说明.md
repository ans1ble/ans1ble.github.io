
---
layout: post
title: " 第三百九十四节，Django+Xadmin打造上线标准的在线教育平台—Xadmin后台进阶开发配置2，以及目录结构说明 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十四节，Django+Xadmin打造上线标准的在线教育平台—Xadmin后台进阶开发配置2，以及目录结构说明**



**设置后台列表页面可以直接修改字段内容**

**在当前APP里的adminx.py文件里的数据表管理器里设置**

**list_editable = ['可以修改的字段','可以修改的字段']**

[code]

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
        list_editable = ['username','email']
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]





**设置后台列表页面，自定义列也就是自定义一个非数据表的字段**

**在 **adminx.py文件里的数据表管理器里设置
list_display=要显示的数据字段名称，当然也可以设置一个函数名称，在models里定义函数，在后台就会多一列，显示的函数返回值****

********models文件********

********自定义函数名称.short_description = '后台显示名称'********

[code]

     class Course(models.Model):
        name = models.CharField(max_length=50, verbose_name='课程名称')
        desc = models.CharField(max_length=300, verbose_name='课程描述')
        detail = models.TextField(verbose_name='课程详情')
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
    
        # 自定义列
        def hqzhjie(self):
            return 555
        hqzhjie.short_description = '章节数'
    
        def __str__(self):
            return self.name        # 设置在xadmin后台显示字段, 注意如果此表被另外的了外键关联了，这个返回字段就是外键表的外键名称
[/code]

****adminx.py****

[code]

     class CourseAdmin(object):               # 自定义数据表管理器类
    
        # 设置xadmin后台显示字段
        list_display = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                        'fav_nums', 'image', 'click_nums', 'add_time', 'hqzhjie']
    
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                         'fav_nums', 'image', 'click_nums']
    
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                       'fav_nums', 'image', 'click_nums', 'add_time']
        model_icon = 'fa fa-clone'
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
[/code]

**结果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923081510040-1118425068.png)**





**********设置后台列表页面，自定义列也就是自定义一个非数据表的字段，统计当前id被多少条数据外键关联**********

**********self.外键类名称(小写).all().count()  统计外键关联了当前主键的数据**********

**********注意：只能统计外键关联了当前主键的数据**********

**models文件**

[code]

     class Course(models.Model):
        name = models.CharField(max_length=50, verbose_name='课程名称')
        desc = models.CharField(max_length=300, verbose_name='课程描述')
        detail = models.TextField(verbose_name='课程详情')
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
    
        # 自定义列
        def hqzhjie(self):
            return self.lesson_set.all().count()
        hqzhjie.short_description = '章节数'
    
        def __str__(self):
            return self.name        # 设置在xadmin后台显示字段, 注意如果此表被另外的了外键关联了，这个返回字段就是外键表的外键名称
[/code]

**adminx.py**

[code]

     class CourseAdmin(object):               # 自定义数据表管理器类
    
        # 设置xadmin后台显示字段
        list_display = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                        'fav_nums', 'image', 'click_nums', 'add_time', 'hqzhjie']
    
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                         'fav_nums', 'image', 'click_nums']
    
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                       'fav_nums', 'image', 'click_nums', 'add_time']
        model_icon = 'fa fa-clone'
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923084936025-1639997412.png)





************设置后台列表页面，自定义列也就是自定义一个非数据表的字段，获取一个字段值拼接成超链接************

**mark_safe() 允许执行里面html代码**  
 **self.image(字段名称) 获取当前字段值**

**models文件**

[code]

     class Users(models.Model):       # 创建类必须继承models.Model，类名将是在数据库里的表名称
        username = models.CharField(max_length=150, verbose_name='用户名', default='', null=False, blank=False)
        password = models.CharField(max_length=128, verbose_name='密码', default='', blank=False)         # 密码字段，长度128，默认值为空字符，前端不允许用户输入空
        last_login = models.DateTimeField(verbose_name='登录日期', null=True, blank=True)                 # 允许为空
        first_name = models.CharField(max_length=30, verbose_name='拓展1', null=False)
        last_name = models.CharField(max_length=30, verbose_name='拓展2', null=False)
        email = models.EmailField(max_length=254, verbose_name='邮箱', null=False, blank=False)
        is_active = models.BooleanField(max_length=1, default=0, verbose_name='是否激活', null=False)
        date_joined = models.DateTimeField(verbose_name='注册日期', null=True)
        nick_name = models.CharField(max_length=50, verbose_name='昵称', default='')
        birday = models.DateField(verbose_name='生日', null=True)
        gender = models.CharField(max_length=6, verbose_name='性别', choices=(("male", "男"), ("female", "女")), default='male')
        address = models.CharField(max_length=100, verbose_name='地区', default='')
        mobile = models.CharField(max_length=11, verbose_name='手机', null=True, blank=True)
        image = models.ImageField(upload_to='image/%Y/%m', verbose_name='头像', default='image/default.png', max_length=100,storage=ImageStorage())
    
        class Meta:
            verbose_name = '用户信息'
            verbose_name_plural = verbose_name
    
        # 自定义列
        def hqzhjie(self):
            from django.utils.safestring import mark_safe                   # 允许执行html代码
            pj_url = '<a href="/media/{0}">跳转</a>'.format(self.image)     # 获取头像字段拼接成连接地址
            return mark_safe(pj_url)                                        # 返回当前头像的连接地址
        hqzhjie.short_description = '头像'
    
        def __str__(self):
            return self.username
[/code]

**adminx.py**

[code]

     class UsersAdmin(object):               # 自定义用户信息数据表管理器类
        # 设置xadmin后台显示字段
        list_display = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined','hqzhjie']
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

**结果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923094858696-1991979170.png)**





**设置后台列表页面，设置自动刷新**

**这是一个插件，放在xadmin/plugins/refresh.py**

****在当前APP里的adminx.py文件里的 数据表管理器里设置**refresh_times参数即可使用该插件**

[code]

    class UsersAdmin(object):               # 自定义用户信息数据表管理器类
        # 设置xadmin后台显示字段
        list_display = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined','hqzhjie']
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile']
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['username', 'password', 'nick_name', 'gender', 'email', 'address', 'mobile',
                        'first_name', 'last_name', 'is_active', 'birday', 'last_login', 'date_joined']
        model_icon = 'fa fa-user-plus'
        ordering = ['-id']
        readonly_fields = ['password']
        exclude = ['first_name','last_name']
        refresh_times = [3, 5]
    xadmin.site.register(Users, UsersAdmin)     # 将户信息数据表注册到xadmin后台显示
[/code]

**结果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923100122540-1658878137.png)**





**Xadmin目录结构说明**

**plugins是最重要的一个目录**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170923104619228-377298221.png)**



