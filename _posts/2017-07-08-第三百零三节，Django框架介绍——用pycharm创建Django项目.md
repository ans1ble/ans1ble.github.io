---
layout: post
title: " 第三百零三节，Django框架介绍——用pycharm创建Django项目 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Django框架介绍**



**Django是一个开放源代码的Web应用框架，由Python写成。采用了MVC的软件设计模式，即模型M，视图V和控制器C。它最初是被开发来用于管理劳伦斯出版集团旗下的一些以新闻内容为主的网站的，即是CMS（内容管理系统）软件。并于2005年7月在BSD许可证下发布。**

**这套框架是以比利时的吉普赛爵士吉他手Django Reinhardt来命名的。**

  **更多** **Django框架**[ **http://code.ziqiangxuetang.com/django/django-
qrcode.html**](http://code.ziqiangxuetang.com/django/django-qrcode.html)

****Django框架，流程图****

****![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170708203424925-1350920754.png)****



****Django框架安装****



****Django框架，安装，Python3.5集成了 ** **Django框架，不需要安装，如果没有集成就需要安装 **
**Django************





************利用pycharm创建 ** **Django项目****************

****************第一步，文件——新项目****************

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170708210551362-112823807.png)



****************创建项目后说明****************

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170708210407565-1360182527.png)



**使用命令创建项目**

**首先将python安装目录下的Scripts目录里的 django-admin.exe，添加到系统环境变量**

**如：C:\Users\admin\AppData\Local\Programs\Python\Python35\Scripts\django-
admin.exe**

**然后cd 进入到要创建项目的路径里**

**进入目录后，输入： django-admin.py startproject sitename(项目名称)**

**然后cd 进入 **sitename(项目名称) ，目录****

****输入命令： python manage.py startapp blog(应用app名称)****

****大功告成****



****运行程序以及，设置端口****

**python manage.py runserver 127.0.0.1:8009**



