
---
layout: post
title: " 第三百八十节，Django+Xadmin打造上线标准的在线教育平台—将所有app下的models数据库表注册到xadmin后台管理 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十节，Django+Xadmin打造上线标准的在线教育平台—将所有app下的models数据库表注册到xadmin后台管理**



****将一个app下的models数据库表注册到xadmin后台管理****

********重点： xadmin的数据表注册，是到app下查找的adminx文件，所以我们必须在app下创建一个 ** ** **
**adminx.py文件 ，所有关于数据表注册到 ** ** ** **xadmin 后台的代码都是写在 ** ** ** ** ** ** **
**adminx.py 文件里****************************************

****************************************![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911002402288-667778559.png)****************************************





****************adminx.py文件编写****************

**1、自定义一个类来继承object对象，这个类叫做数据表管理器**  
 ** 数据表管理器里面，专门配置当前数据表的各种功能**

** list_display = ['models数据表里的字段名称','models数据表里的字段名称'] 设置数据表在后台显示的字段**

** 注意：第一个字段是后台编辑入口**



** search_fields = ['models数据表里的字段名称','models数据表里的字段名称'] 设置在后台可以搜素的字段，**

** 注意：搜索字段不能有时间和外键类型的字段，不然会报错，所以时间和外键类型的字段搜索我们一般用过滤器来做**



******list_filter = ['models数据表里的字段名称','models数据表里的字段名称']**
**设置在后台可以通过条件帅选查看的字段**



**xadmin.site.register(数据库表类名称, 自定义数据表管理器类名称) 方法：将制定表注册到xadmin后台**



[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import xadmin
    
    from .models import Course, Lesson, Video, CourseResource
    
    
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
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911005409069-1753403877.png)





**外键字段设置**

**  如果一张表里的一个字段，外键关联了另外一张表，那么另外一张表的def __str__(self) 返回字段的值，就是外键字段的可选值**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    
    
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
    
        def __str__(self):
            return self.name        # 设置在xadmin后台显示字段, 注意如果此表被另外的了外键关联了，这个返回字段就是外键表的外键名称
    
    
    class Lesson(models.Model):
        course = models.ForeignKey(Course, verbose_name='外键课程表')      # 外键链表，外键连接Course表的主键，一对多关系
        name = models.CharField(max_length=100, verbose_name='章节名')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程章节'
            verbose_name_plural = verbose_name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911023125641-1564832767.png)



![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911023354453-966592396.png)





**外键字段用过滤器跨表查询**

**如果要通过当前表的外键字段，查询到关联表的指定字段内容，可以通过
adminx.py里的过滤器，在过滤器里的，外键字段名称__关联表名称，也就是用双下划线跨表查询**

****adminx.py****

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import xadmin
    
    from .models import Course, Lesson, Video, CourseResource
    
    
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
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
    
    
    class LessonAdmin(object):
        list_display = ['course', 'name', 'add_time']
        search_fields = ['name']
        list_filter = ['course__name', 'name', 'add_time']      # course__name 表示通过course外键字段查询关联表里的name字段
    xadmin.site.register(Lesson, LessonAdmin)
[/code]

**models.py**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    
    
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
    
        def __str__(self):
            return self.name        # 设置在xadmin后台显示字段, 注意如果此表被另外的了外键关联了，这个返回字段就是外键表的外键名称
    
    
    class Lesson(models.Model):
        course = models.ForeignKey(Course, verbose_name='外键课程表')      # 外键链表，外键连接Course表的主键，一对多关系
        name = models.CharField(max_length=100, verbose_name='章节名')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程章节'
            verbose_name_plural = verbose_name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911025448657-192648413.png)



  
**后台编辑一条数据时，数据路径显示设置**  
 **当后台编辑一条数据时，数据路径显就是def __str__(self) 返回字段的值， 所以每张表都要设置def __str__(self) 返回**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170911133120266-1229404215.png)**



[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    
    
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
    
        def __str__(self):
            return self.name
[/code]



