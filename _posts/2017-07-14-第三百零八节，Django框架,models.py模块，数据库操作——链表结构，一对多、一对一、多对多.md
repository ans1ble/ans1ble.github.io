---
layout: post
title: " 第三百零八节，Django框架,models.py模块，数据库操作——链表结构，一对多、一对一、多对多 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---



  
**第三百零八节，Django框架,models.py模块，数据库操作——链表结构，一对多、一对一、多对多**





**链表操作**

**链表，就是一张表的外键字段，连接另外一张表的主键字段**

****一对多****

**models.ForeignKey() 外键字段一对多，值是要外键的表类**

[code]

    from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    
    class yong_hu_shen_fen(models.Model):                        #创建用户是否表类
        id = models.AutoField('id',primary_key=True)             #自增id
        shen_fen = models.CharField('身份',max_length=16)         #字符串类型字段，记录用户身份
    
        class Meta:
            verbose_name = '用户身份表'
            verbose_name_plural = verbose_name
    
    
    class yong_hu_biao(models.Model):
        yong_hu = models.CharField('用户',max_length=32)
        you_xiang = models.EmailField('邮箱',max_length=32)
        mi_ma = models.CharField('密码',max_length=64)
        wai_jian_yong_hu_shen_fen = models.ForeignKey(yong_hu_shen_fen)     #外键链表
    
        class Meta:
            verbose_name = '用户表'
            verbose_name_plural = verbose_name
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170713133535993-1048857528.png)



****正向查找，也就是通过表的外键，查找到外键连接的表里的数据****

**链表查询之了不起的 __双下划线**

**也就是一般普通查询外键字段时，得到的是另外一张表的主键值，**

****__双下划线 ，表示跨表查询的意思，注意， ** **__双下划线跨表查询**** 必须是外键连接的表****

****查询一张表的外键字段时可以通过，外键字段名称__连接表的字段名称，查询到外键连接表里的指定字段值****

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yong_hu_biao.objects.all().values('yong_hu','wai_jian_yong_hu_shen_fen_id')             #获取用户名字段，和外键字段
        print(a)
        b = yong_hu_biao.objects.all().values('yong_hu','wai_jian_yong_hu_shen_fen_id__shen_fen')   #获取用户名字段，和外键字段连接的表里的指定字段
        print(b)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [{'yong_hu': '林贵秀', 'wai_jian_yong_hu_shen_fen_id': 1}, {'yong_hu': '马云', 'wai_jian_yong_hu_shen_fen_id': 2}, {'yong_hu': '张三', 'wai_jian_yong_hu_shen_fen_id': 3}]>
    # <QuerySet [{'wai_jian_yong_hu_shen_fen_id__shen_fen': '普通用户', 'yong_hu': '林贵秀'}, {'wai_jian_yong_hu_shen_fen_id__shen_fen': 'vip用户', 'yong_hu': '马云'}, {'wai_jian_yong_hu_shen_fen_id__shen_fen': '超级用户', 'yong_hu': '张三'}]>
[/code]

**  注意：__双下划线跨表查询，都是用过外键关系跨表的**

**举例：如果a表外键连接b表，b表又外键连接c表，这就有了三张表，也就是多层一对多的关系**

**如果我们要从a表跨表查询到c表的字段，那么就是： a表外键字段__b表外键字段__c表字段    ，无论多少层继续__**



**filter()条件，加__双下划线 ，跨表查询**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yong_hu_biao.objects.filter(wai_jian_yong_hu_shen_fen_id__shen_fen='普通用户').values()  #获取当前表里外键字段跨表的shen_fen字段等于普通用户的数据
        print(a)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [{'you_xiang': '729088188@qq.com', 'id': 1, 'wai_jian_yong_hu_shen_fen_id': 1, 'mi_ma': '279819', 'yong_hu': '林贵秀'}]>
[/code]



**反向查找，从一张表查到它，被那张表外键连接，然后查出 **外键连接表里的信息****

****外键表类名称_set ，链表反向查找****

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        obj = yong_hu_shen_fen.objects.filter(shen_fen='超级用户').first()   #通过条件查找到符合条件的对象，获取到第一个对象
        print(obj)
        a = obj.yong_hu_biao_set.all().values()   #通过查找到的对象，找外键表里符合这个对象的数据，反向查找
        print(a)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [{'yong_hu': '张三', 'wai_jian_yong_hu_shen_fen_id': 3, 'mi_ma': '279819', 'id': 3, 'you_xiang': '123456@qq.com'}]>
[/code]

**  __双下划线反向查找**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yong_hu_shen_fen.objects.all().values('id','shen_fen','yong_hu_biao__yong_hu')  #反向查找
        # a = yong_hu_shen_fen.objects.all().values('id', 'shen_fen', '外键表类名称__外键表字段')
        print(a)
    
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    #<QuerySet [{'yong_hu_biao__yong_hu': '林贵秀', 'shen_fen': '普通用户', 'id': 1}, {'yong_hu_biao__yong_hu': '马云', 'shen_fen': 'vip用户', 'id': 2}, {'yong_hu_biao__yong_hu': '张三', 'shen_fen': '超级用户', 'id': 3}]>
[/code]



* * *



**链表操作一对一**

**OneToOneField() 外键链表，一对一类型，也就是相当于，在外键字段加了一个唯一索引，在添加数据时不能有重复类容，只能一对一**

[code]

    from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    
    class yong_hu_shen_fen(models.Model):                        #创建用户是否表类
        id = models.AutoField('id',primary_key=True)             #自增id
        shen_fen = models.CharField('身份',max_length=16)         #字符串类型字段，记录用户身份
    
        class Meta:
            verbose_name = '用户身份表'
            verbose_name_plural = verbose_name
    
    
    class yong_hu_biao(models.Model):
        yong_hu = models.CharField('用户',max_length=32)
        you_xiang = models.EmailField('邮箱',max_length=32)
        mi_ma = models.CharField('密码',max_length=64)
        wai_jian_yong_hu_shen_fen = models.OneToOneField(yong_hu_shen_fen)     #外键链表一对一
    
        class Meta:
            verbose_name = '用户表'
            verbose_name_plural = verbose_name
[/code]

**其他链表操作与上面相同**



* * *





**链表操作多对多**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170713175546009-1826464143.png)**





**ManyToManyField() 多对多字段类型**

**创建一对多结构有3中方式**

**方式一，传统方式【不推荐】**

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class yu_wen_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '语文老师表'
            verbose_name_plural = verbose_name
    
    
    class shu_xue_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '数学老师表'
            verbose_name_plural = verbose_name
    
    
    class tong_xue_biao(models.Model):　　　　　　　　　　　　　　　　  #关系表
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
        wj_yu_wen_lao_shi = models.ForeignKey(yu_wen_lao_shi)      #外键语文老师表
        WJ_shu_xue_lao_shi = models.ForeignKey(shu_xue_lao_shi)    #外键数学老师表
    
        class Meta:
            verbose_name = '同学表'
            verbose_name_plural = verbose_name
[/code]

**  方式二ManyToManyField()多对多字段类型，自动生成关系表【不推荐】**

**将 **ManyToManyField(另外一张表的名称) 写在，要建立关系的任意一张表里，参数是另外的要建立关系的表类名称****

[code]

    from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class yu_wen_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '语文老师表'
            verbose_name_plural = verbose_name
    
    
    class shu_xue_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        guan_xi = models.ManyToManyField(yu_wen_lao_shi)     #注意不会生成guan_xi这个字段，只会自动生成一张多对多关系表
    
        class Meta:
            verbose_name = '数学老师表'
            verbose_name_plural = verbose_name
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170713183419118-1333912088.png)

**  可以看到，这个方式虽然简单，但是自动生成的关系表，只有外键关系的字段，如果我们需要有其他字段，无法满足**



**方式三，上面两种方式的结合【推荐】**

****将 **ManyToManyField(另外一张表的名称，through='关系表名称')
写在，要建立关系的任意一张表里，参数是另外的要建立关系的表类名称******

******同时也在关系表设置外键字段******

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    
    class yu_wen_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '语文老师表'
            verbose_name_plural = verbose_name
    
    
    class shu_xue_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        guan_xi = models.ManyToManyField('yu_wen_lao_shi', through='tong_xue_biao')
        # guan_xi = models.ManyToManyField('另外一张表的名称', through='关系表名称')
    
        class Meta:
            verbose_name = '数学老师表'
            verbose_name_plural = verbose_name
    
    
    class tong_xue_biao(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
        wj_yu_wen_lao_shi = models.ForeignKey(yu_wen_lao_shi)       #外键表
        wj_shu_xue_lao_shi = models.ForeignKey(shu_xue_lao_shi)     #外键表
    
        class Meta:
            verbose_name = '同学表'
            verbose_name_plural = verbose_name
[/code]

**  这样关系表就可以设置其他字段了，注意：此时看起来既然关系表已经外键链表了，干嘛还要用 ** ** **ManyToManyField()，
感觉是多余的，放心以后查询等操作的时候它能帮到你的********



**多对对添加数据**



**自动创建关系表添加数据，关系表类不存在**

****方式二
ManyToManyField()多对多字段类型，自动生成关系表，因为关系表是自动生成的，而数据库表类，里没有这个关系表的类，所以无法实现向关系表添加数据，这样我们就需要用
** ** ** **ManyToManyField() 变量通道********来添加数据了****

****数据库表类里没有关系表类****

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class yu_wen_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '语文老师表'
            verbose_name_plural = verbose_name
    
    
    class shu_xue_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        guan_xi = models.ManyToManyField(yu_wen_lao_shi)     #注意不会生成guan_xi这个字段，只会自动生成一张多对多关系表
    
        class Meta:
            verbose_name = '数学老师表'
            verbose_name_plural = verbose_name
[/code]

**************ManyToManyField() 变量************添加数据到关系表**

**ManyToManyField()变量.add() 正向添加关系表数据**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        #向yu_wen_lao_shi表插入数据
        # yu_wen_lao_shi.objects.create(xing_ming='张三', you_xiang='123')
        # yu_wen_lao_shi.objects.create(xing_ming='李四', you_xiang='456')
        # yu_wen_lao_shi.objects.create(xing_ming='王五', you_xiang='789')
        # yu_wen_lao_shi.objects.create(xing_ming='马六', you_xiang='101112')
    
        #向shu_xue_lao_shi表插入数据
        # shu_xue_lao_shi.objects.create(xing_ming='赵好', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='钱的', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='孙客', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='李是', you_xiang='101112')
    
        #向关系表插入数据
        a = shu_xue_lao_shi.objects.get(id=1)    #获取表类里有ManyToManyField那张表，返回的一条数据对象
        print(a.guan_xi.all())                   #通过数据对象，找到ManyToManyField的变量，得到另外一张表的对象
    
        b = yu_wen_lao_shi.objects.get(id=1)     #获取第二张表里的数据
        a.guan_xi.add(b)                         #将第二张表里的数据对象通过ManyToManyField的变量通道添加到关系表
    
        #a.guan_xi 将第一张表对应的数据添加到关系表
        #a.guan_xi.add(b) 将第二张表对应的数据添加到关系表
    
    
        return render(request,'index.html',locals())   #打开页面
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170714124848509-1827168535.png)

**  如果是要添加多条用*接收**

[code]

    #向关系表插入数据
        a = shu_xue_lao_shi.objects.get(id=1)    #获取表类里有ManyToManyField那张表，返回的一条数据对象
        print(a.guan_xi.all())                   #通过数据对象，找到ManyToManyField的变量，得到另外一张表的对象
    
        b = yu_wen_lao_shi.objects.filter(id__gt=1)     #获取第二张表里的数据
        a.guan_xi.add(*b)                         #将第二张表里的数据对象通过ManyToManyField的变量通道添加到关系表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170714130434337-2050171973.png)

**  反向添加数据**

**通过另外一张表名称_set.add() 方法添加数据**

[code]

        #向关系表插入数据
        a = yu_wen_lao_shi.objects.get(id=3)       #获取没有ManyToManyField变量的那张表
        print(a.shu_xue_lao_shi_set)               #对象里有一个，另外一张表名称_set属性
    
        b = shu_xue_lao_shi.objects.filter(id__gt=1) #获取有ManyToManyField变量的那张表
        a.shu_xue_lao_shi_set.add(*b)              #通过另外一张表名称_set属性的add()方法添加数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170714132744087-1156469101.png)

**  删除数据**

**remove() 删除数据，不删除其他表里相关数据**  
 **delete() 删除数据，删除其他表里相关数据**

[code]

        #正向删除数据
        # a = shu_xue_lao_shi.objects.get(id=1)
        # b = yu_wen_lao_shi.objects.filter(id__gt=1)
        # a.guan_xi.remove(*b)    #删除关系表里shu_xue_lao_shi等于1,yu_wen_lao_shi字段大于1的数据
    
        #反向删除
        a = yu_wen_lao_shi.objects.get(id=2)
        a.shu_xue_lao_shi_set.all().delete()  #删除关系表yu_wen_lao_shi字段为1的数据，shu_xue_lao_shi表相关的数据也会被删除
[/code]





**手动创建关系表添加数据，关系表类存在**

**数据表类**

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    
    class yu_wen_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        class Meta:
            verbose_name = '语文老师表'
            verbose_name_plural = verbose_name
    
    
    class shu_xue_lao_shi(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
    
        guan_xi = models.ManyToManyField('yu_wen_lao_shi', through='tong_xue_biao')
        # guan_xi = models.ManyToManyField('另外一张表的名称', through='关系表名称')
    
        class Meta:
            verbose_name = '数学老师表'
            verbose_name_plural = verbose_name
    
    
    class tong_xue_biao(models.Model):
        id = models.AutoField('id',primary_key=True)
        xing_ming = models.CharField('姓名',max_length=16)
        you_xiang = models.CharField('邮箱',max_length=16)
        wj_yu_wen_lao_shi = models.ForeignKey(yu_wen_lao_shi)       #外键表
        wj_shu_xue_lao_shi = models.ForeignKey(shu_xue_lao_shi)     #外键表
    
        class Meta:
            verbose_name = '同学表'
            verbose_name_plural = verbose_name
[/code]



**操作数据**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        #向yu_wen_lao_shi表插入数据
        # yu_wen_lao_shi.objects.create(xing_ming='张三', you_xiang='123')
        # yu_wen_lao_shi.objects.create(xing_ming='李四', you_xiang='456')
        # yu_wen_lao_shi.objects.create(xing_ming='王五', you_xiang='789')
        # yu_wen_lao_shi.objects.create(xing_ming='马六', you_xiang='101112')
    
        #向shu_xue_lao_shi表插入数据
        # shu_xue_lao_shi.objects.create(xing_ming='赵好', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='钱的', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='孙客', you_xiang='101112')
        # shu_xue_lao_shi.objects.create(xing_ming='李是', you_xiang='101112')
    
        #向关系表添加数据
        # tong_xue_biao.objects.create(xing_ming='丰收1',you_xiang='123',wj_yu_wen_lao_shi_id=1,wj_shu_xue_lao_shi_id=2)
    
        #获取数据
        #获取全部数据
        a = tong_xue_biao.objects.all().values()
        print(a)
        #通过外键跨表获取数据
        b = tong_xue_biao.objects.all().values('wj_yu_wen_lao_shi_id__xing_ming')
        print(b)
        for i in b:
            print(i)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [{'you_xiang': '123', 'wj_shu_xue_lao_shi_id': 2, 'id': 1, 'xing_ming': '丰收1', 'wj_yu_wen_lao_shi_id': 1}, {'you_xiang': '123', 'wj_shu_xue_lao_shi_id': 2, 'id': 2, 'xing_ming': '丰收2', 'wj_yu_wen_lao_shi_id': 1}, {'you_xiang': '123', 'wj_shu_xue_lao_shi_id': 1, 'id': 3, 'xing_ming': '丰收3', 'wj_yu_wen_lao_shi_id': 1}, {'you_xiang': '123', 'wj_shu_xue_lao_shi_id': 2, 'id': 4, 'xing_ming': '丰收4', 'wj_yu_wen_lao_shi_id': 3}, {'you_xiang': '123', 'wj_shu_xue_lao_shi_id': 2, 'id': 5, 'xing_ming': '丰收5', 'wj_yu_wen_lao_shi_id': 4}]>
    # <QuerySet [{'wj_yu_wen_lao_shi_id__xing_ming': '张三'}, {'wj_yu_wen_lao_shi_id__xing_ming': '张三'}, {'wj_yu_wen_lao_shi_id__xing_ming': '张三'}, {'wj_yu_wen_lao_shi_id__xing_ming': '王五'}, {'wj_yu_wen_lao_shi_id__xing_ming': '马六'}]>
    # {'wj_yu_wen_lao_shi_id__xing_ming': '张三'}
    # {'wj_yu_wen_lao_shi_id__xing_ming': '张三'}
    # {'wj_yu_wen_lao_shi_id__xing_ming': '张三'}
    # {'wj_yu_wen_lao_shi_id__xing_ming': '王五'}
    # {'wj_yu_wen_lao_shi_id__xing_ming': '马六'}
[/code]





**总结；重点**

**一对多**  
 **外键字段__连接表字段 ：正向跨表查找**  
 **连接表类名称_set : 反向跨表查找**



**一对一**  
 **与一对多相同**



**多对多**  
 **ManyToManyField() 自动创建关系表，数据库表类没有关系表类**  
 **ManyToManyField()变量.xx() ：从ManyToManyField表正向操作关系表**  
 **另外一张表名称_set.xx() :从非ManyToManyField表反向操作关系表**  
 **注意：以上操作他们之间，必须有文外键关系**



