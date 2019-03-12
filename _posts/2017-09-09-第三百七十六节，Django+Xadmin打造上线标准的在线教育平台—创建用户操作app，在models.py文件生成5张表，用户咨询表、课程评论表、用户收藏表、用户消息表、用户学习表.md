
---
layout: post
title: " 第三百七十六节，Django+Xadmin打造上线标准的在线教育平台—创建用户操作app，在models.py文件生成5张表，用户咨询表、课程评论表、用户收藏表、用户消息表、用户学习表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十六节，Django+Xadmin打造上线标准的在线教育平台—创建用户操作app，在models.py文件生成5张表，用户咨询表、课程评论表、用户收藏表、用户消息表、用户学习表**



******创建名称为app_operation的 **用户操作** APP，写数据库操作文件 **models.py********

********![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909112825476-584924650.png)********





****models.py **文件******

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models            # 导入models对象
    
    from app_users.models import Users      # 导入用户信息表
    from app_courses.models import Course   # 导入课程表
    
    
    class UserAsk(models.Model):
        name = models.CharField(max_length=20, verbose_name='姓名')
        mobile = models.CharField(max_length=10, verbose_name='手机')
        course_name = models.CharField(max_length=50, verbose_name='课程名')
        add_time = models.DateTimeField(default=datetime.now)
    
        class Meta:
            verbose_name = '用户咨询表'
            verbose_name_plural = verbose_name
    
    
    class CourseComments(models.Model):
        user = models.ForeignKey(Users, verbose_name='评论用户')
        course = models.ForeignKey(Course, verbose_name='评论课程')
        comments = models.CharField(max_length=200, verbose_name='评论内容')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='评论时间')
    
        class Meta:
            verbose_name = '课程评论表'
            verbose_name_plural = verbose_name
    
    
    class UserFavorite(models.Model):
        user = models.ForeignKey(Users, verbose_name='用户收藏')
        fav_id = models.IntegerField(default=0, verbose_name='收藏数据ID')
        fav_type = models.IntegerField(choices=((1, '课程'), (2, '课程机构'), (3, '讲师')), default=1, verbose_name='用户收藏类型')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='收藏时间')
    
        class Meta:
            verbose_name = '用户收藏表'
            verbose_name_plural = verbose_name
    
    
    class UserMessage(models.Model):
        user = models.IntegerField(default=0, verbose_name='接收用户id')    # 0表示所有用户
        message = models.CharField(max_length=500, verbose_name='消息内容')
        has_read = models.BooleanField(default=False, verbose_name='是否已读')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='消息时间')
    
        class Meta:
            verbose_name = '用户消息表'
            verbose_name_plural = verbose_name
    
    
    class UserCourse(models.Model):
        user = models.ForeignKey(Users, verbose_name='学习用户')
        course = models.ForeignKey(Course, verbose_name='学习课程')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='学习时间')
    
        class Meta:
            verbose_name = '用户学习表'
            verbose_name_plural = verbose_name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909113134351-1276761649.png)



