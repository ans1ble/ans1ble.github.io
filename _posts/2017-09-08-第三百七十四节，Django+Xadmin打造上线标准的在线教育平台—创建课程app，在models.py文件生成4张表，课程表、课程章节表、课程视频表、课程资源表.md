
---
layout: post
title: " 第三百七十四节，Django+Xadmin打造上线标准的在线教育平台—创建课程app，在models.py文件生成4张表，课程表、课程章节表、课程视频表、课程资源表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十四节，Django+Xadmin打造上线标准的在线教育平台—创建课程app，在models.py文件生成4张表，课程表、课程章节表、课程视频表、课程资源表**



**创建名称为app_courses的课程APP，写数据库操作文件 **models.py****

****![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170908185039585-857582014.png)****





****models.py **文件******

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
            verbose_name = '课程表'
            verbose_name_plural = verbose_name
    
    
    class Lesson(models.Model):
        course = models.ForeignKey(Course, verbose_name='外键课程表')      # 外键链表，外键连接Course表的主键，一对多关系
        name = models.CharField(max_length=100, verbose_name='章节名')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程章节表'
            verbose_name_plural = verbose_name
    
    
    class Video(models.Model):
        lesson = models.ForeignKey(Lesson, verbose_name='外键章节表')
        name = models.CharField(max_length=100, verbose_name='视频名')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程视频表'
            verbose_name_plural = verbose_name
    
    
    class CourseResource(models.Model):
        course = models.ForeignKey(Course, verbose_name='外键课程表')
        name = models.CharField(max_length=100, verbose_name='课程资源名称')
        download = models.FileField(upload_to='course/resource/%Y/%m', verbose_name='资源文件', max_length=100)
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程资源表'
            verbose_name_plural = verbose_name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170908185322444-2096725374.png)



