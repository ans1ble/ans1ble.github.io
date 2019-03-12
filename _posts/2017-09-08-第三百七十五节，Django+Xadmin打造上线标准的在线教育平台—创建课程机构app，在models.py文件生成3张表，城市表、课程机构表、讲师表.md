
---
layout: post
title: " 第三百七十五节，Django+Xadmin打造上线标准的在线教育平台—创建课程机构app，在models.py文件生成3张表，城市表、课程机构表、讲师表 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十五节，Django+Xadmin打造上线标准的在线教育平台—创建课程机构app，在models.py文件生成3张表，城市表、课程机构表、讲师表**



****创建名称为app_organization的 **课程机构** APP，写数据库操作文件 **models.py******

******![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170908201253007-338095099.png)******





****models.py **文件******

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from __future__ import unicode_literals
    from datetime import datetime
    
    from django.db import models        # 导入models对象
    
    
    class CityDict(models.Model):
        name = models.CharField(max_length=20, verbose_name='城市')
        desc = models.CharField(max_length=200, verbose_name='描述')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '城市表'
            verbose_name_plural = verbose_name
    
    
    class CourseOrg(models.Model):
        name = models.CharField(max_length=50, verbose_name='机构名称')
        desc = models.TextField(verbose_name='机构描述')
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        image = models.ImageField(upload_to='org/%Y/%m', verbose_name='封面图', max_length=100)
        address = models.CharField(max_length=150, verbose_name='机构地址')
        city = models.ForeignKey(CityDict, verbose_name='外键城市表')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程机构表'
            verbose_name_plural = verbose_name
    
    
    class Teacher(models.Model):
        org = models.ForeignKey(CourseOrg, verbose_name='外键课程机构表')
        name = models.CharField(max_length=50, verbose_name='讲师名称')
        work_years = models.IntegerField(default=0, verbose_name='工作年限')
        work_company = models.CharField(max_length=50, verbose_name='就职公司')
        work_position = models.CharField(max_length=50, verbose_name='公司职位')
        points = models.CharField(max_length=50, verbose_name='教学特点')
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '讲师表'
            verbose_name_plural = verbose_name
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170908201448194-1067223502.png)



