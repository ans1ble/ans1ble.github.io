---
layout: post
title: " 第三百零七节，Django框架,models.py模块，数据库操作——表类容的增删改查 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Django框架,models.py模块，数据库操作——表类容的增删改查**



**增加数据**

**create()方法，增加数据**

**save()方法，写入数据**

**第一种方式**

****表类名称(字段=值)****

****需要 **save()方法，写入数据******

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
    
        a = yhubiao(anem='张三',mim='279819')   #第一种添加数据，实例化表类，在实例化里传参为字段和值
        a.save()                                #写入数据库
    
        return render(request,'index.html')   #打开页面
[/code]

**第二种方式：表类名称.objects.create（字段=值）**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        yhubiao.objects.create(anem='张三2',mim='279819')
    
        return render(request,'index.html')   #打开页面
[/code]

**第三种方式【推荐】**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
    
    
        a = {'anem':'李四',               #将要写入的数据组合成字典，键为字段值为数据
             'mim':'279819'
             }
        yhubiao.objects.create(**a)       #添加到数据库，注意字典变量名称一定要加**
    
        return render(request,'index.html')   #打开页面
[/code]





**查询数据**



**get() 获取单条数据，不存在报错，存在多条也报错【不推荐】**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.get(id=2)    #获取单条数据，不存在报错，存在多条也报错
        print(a)
    
        return render(request,'index.html',locals())   #打开页面  
    
[/code]

[code]

    #返回：张三
[/code]

[code]

     
[/code]

**all() 获取表里的全部信息**

**【重点】注意：查询数据库返回的
QuerySet对象，而且每一行数据又是一个对象，所以我们需要通过values()方法，和values_list()方法来将每行数据转换**

****values()方法 ，获取 **QuerySet对象
里的，行数据返回字典，无参返回整行数据字典，有参参数是要获取的字段，返回要获取的字段字典******

****values_list()方法 ， ** **获取 **QuerySet对象 里的， ** ** **行数据返回列表，无参返回整行数据 ** **
** ** ** ** ** **列表**************** ，有参参数是要获取的字段，返回要获取的字段 ** ** ** ** ** ** **
**列表********************************

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.all()    #获取表里的全部信息
        print(a)                     #返回的QuerySet对象，而且每一行数据又是一个对象
    
        b = a.values()               #将每一行数据对象转换成字典
        print(b)
    
        c = a.values_list()          #将每一行数据对象转换成列表
        print(c)
    
        #一般我们使用字典的方式，我们通过循环得到数据
        for i in b:
            print(i['id'],i['anem'],i['mim'])
    
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三>, <yhubiao: 张三2>, <yhubiao: 李四>]>
    # <QuerySet [{'id': 1, 'mim': '279819', 'anem': '张三'}, {'id': 2, 'mim': '279819', 'anem': '张三2'}, {'id': 3, 'mim': '279819', 'anem': '李四'}]>
    # <QuerySet [(1, '张三', '279819'), (2, '张三2', '279819'), (3, '李四', '279819')]>
    # 1 张三 279819
    # 2 张三2 279819
    # 3 李四 279819
[/code]

**filter() 获取指定条件的数据**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(id=2)   #获取指定条件的数据
        print(a)                           #返回的QuerySet对象，而且每一行数据又是一个对象
    
        b = a.values()
        print(b)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三2>]>
    # <QuerySet [{'id': 2, 'mim': '279819', 'anem': '张三2'}]>
[/code]

**count() 获取数据个数，一般在获取到数据后面使用**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(mim=279819)   #获取指定条件的数据
        print(a)                                 #返回的QuerySet对象，而且每一行数据又是一个对象
    
        b = a.count()
        print(b)                                 #获取数据个数
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三>, <yhubiao: 张三2>, <yhubiao: 李四>]>
    # 3
[/code]

**查询条件：大于小于**

**需要结合， **filter() 获取指定条件的方法****

**__gt 大于**  
 **__gte 大于等于**  
 **__lt 小于**  
 **__lte 小于等于**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(id__gt=1)              # 获取id大于1的值
        # yhubiao.objects.filter(id__gte=1)              # 获取id大于等于1的值
        # yhubiao.objects.filter(id__lt=10)             # 获取id小于10的值
        # yhubiao.objects.filter(id__lte=10)             # 获取id小于10的值
        # yhubiao.objects.filter(id__lt=10, id__gt=1)   # 获取id大于1 且 小于10的值
    
        print(a)                                        #返回的QuerySet对象，而且每一行数据又是一个对象
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三2>, <yhubiao: 李四>]>
[/code]

**__in 在里面的 **

**exclude() 排除取反 **

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(id__in=[2,3])        # 获取id在里面的数据
        print(a)                                        #返回的QuerySet对象，而且每一行数据又是一个对象
    
        b = yhubiao.objects.exclude(id__in=[2, 3])      #获取id不在里面的数据，exclude()排除取反
        print(b)
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三2>, <yhubiao: 李四>]>
    # <QuerySet [<yhubiao: 张三>]>
[/code]

**__isnull 获取字段可以为空，没有设置数据，默认为null的字段**  
 **True获取默认为null的字段**  
 **False获取不为null的字段**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(mim__isnull=True)    # 获取mim字段为null，也就是默认空的字段
        print(a)                                        #返回的QuerySet对象，而且每一行数据又是一个对象
        b = yhubiao.objects.filter(mim__isnull=False)   #获取字段不为null的字段
        print(b)
    
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 王五>]>
    # <QuerySet [<yhubiao: 张三>, <yhubiao: 张三2>, <yhubiao: 李四>]>
[/code]

**__contains 包含，区分大小写**  
 **__icontains 包含，不区分大小写**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(anem__contains='a')    # 获取字段包含5的数据,区分大小写
        print(a)
        b = yhubiao.objects.filter(anem__icontains='a')    #包含，不区分大小写
        print(b)
        c = yhubiao.objects.exclude(anem__contains='a')    #取反，获取字段不包含a的数据
        print(c)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: adc>]>
    # <QuerySet [<yhubiao: adc>, <yhubiao: ADC>]>
    # <QuerySet [<yhubiao: 张三>, <yhubiao: 张三2>, <yhubiao: 李四>, <yhubiao: 王五>, <yhubiao: ADC>]>
[/code]

**__range 范围**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(id__range=[1,6])    #获取id范围在1至6的数据
        print(a)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 张三>, <yhubiao: 张三2>, <yhubiao: 李四>, <yhubiao: 王五>, <yhubiao: adc>, <yhubiao: ADC>]>
[/code]

**__istartswith 以...开头**  
 **__iendswith 以…结尾**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(anem__istartswith='李')    #获取字段以李开头的数据
        print(a)
        b = yhubiao.objects.filter(anem__iendswith=2)         #获取字段以2结尾的数据
        print(b)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [<yhubiao: 李四>]>
    # <QuerySet [<yhubiao: 张三2>]>
[/code]

**order_by() 排序，参数：'字段名' 称升序、'-字段名' 称降序**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(id__range=[1,6]).order_by('id')  #order_by()排序，参数：'字段名'称升序、'-字段名'称降序
        print(a.values())
        b = yhubiao.objects.filter(id__range=[1,6]).order_by('-id')
        print(b.values())
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # <QuerySet [{'anem': '张三', 'id': 1, 'mim': '279819'}, {'anem': '张三2', 'id': 2, 'mim': '2345'}, {'anem': '李四', 'id': 3, 'mim': '279819'}, {'anem': '王五', 'id': 4, 'mim': None}, {'anem': 'adc', 'id': 5, 'mim': '1988'}, {'anem': 'ADC', 'id': 6, 'mim': '8868'}]>
    # <QuerySet [{'anem': 'ADC', 'id': 6, 'mim': '8868'}, {'anem': 'adc', 'id': 5, 'mim': '1988'}, {'anem': '王五', 'id': 4, 'mim': None}, {'anem': '李四', 'id': 3, 'mim': '279819'}, {'anem': '张三2', 'id': 2, 'mim': '2345'}, {'anem': '张三', 'id': 1, 'mim': '279819'}]>
[/code]

**  group by，分组**

**字段**  
 **nid   cl   id    num**

[code]

     # from django.db.models import Count, Min, Max, Sum
     # models.Tb1.objects.filter(c1=1).values('id').annotate(c=Count('num'))
     # SELECT "app01_tb1"."id", COUNT("app01_tb1"."num") AS "c" FROM "app01_tb1" WHERE "app01_tb1"."c1" = 1 GROUP BY "app01_tb1"."id"
[/code]

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    from django.db.models import F,Q   #导入F和Q
    
    from django.db.models import Count, Min, Max, Sum
    
    #逻辑处理模块
    def special(request):
        #获取表里shf字段等于普通会员的数据，以shf字符分组，计算出所属普通会员的数据有多少条
        a = yu_wen_lao_shi.objects.filter(shf='普通会员').values('shf').annotate(c=Count('shf'))
        print(a)
    
        # 获取表里的所有数据，以shf字符分组，计算出所分组的数据有多少条
        b = yu_wen_lao_shi.objects.all().values('shf').annotate(c=Count('shf'))
        print(b)
    
        return render(request,'index.html',locals())   #打开页面
    # 返回：
    # <QuerySet [{'shf': '普通会员', 'c': 4}]>
    # <QuerySet [{'shf': '普通会员', 'c': 4}, {'shf': '黄金会员', 'c': 2}, {'shf': '超级会员', 'c': 1}]>
[/code]



**limit 、offset，分页**

[code]

             # limit 、offset
            #
            # models.Tb1.objects.all()[10:20]
[/code]



[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    from django.db.models import F,Q   #导入F和Q
    
    from django.db.models import Count, Min, Max, Sum
    
    #逻辑处理模块
    def special(request):
        #从第二条开始，获取到第五条
        b = yu_wen_lao_shi.objects.all()[2:5]
        print(b.values())
    
        return render(request,'index.html',locals())   #打开页面
    # 返回：
    # <QuerySet [{'xm': '张三3', 'id': 3, 'shf': '黄金会员'}, {'xm': '张三4', 'id': 4, 'shf': '普通会员'}, {'xm': '张三5', 'id': 5, 'shf': '超级会员'}]>
[/code]









**regex正则匹配，iregex 不区分大小写**

[code]

             # Entry.objects.get(title__regex=r'^(An?|The) +')
            # Entry.objects.get(title__iregex=r'^(an?|the) +')
[/code]

**date日期**

[code]

             # Entry.objects.filter(pub_date__date=datetime.date(2005, 1, 1))
            # Entry.objects.filter(pub_date__date__gt=datetime.date(2005, 1, 1))
[/code]

**year年**

[code]

             # Entry.objects.filter(pub_date__year=2005)
            # Entry.objects.filter(pub_date__year__gte=2005)
[/code]

**month月**

[code]

             # Entry.objects.filter(pub_date__month=12)
            # Entry.objects.filter(pub_date__month__gte=6)
[/code]

**day天**

[code]

             # Entry.objects.filter(pub_date__day=3)
            # Entry.objects.filter(pub_date__day__gte=3)
[/code]

**week_day**

[code]

             # Entry.objects.filter(pub_date__week_day=2)
            # Entry.objects.filter(pub_date__week_day__gte=2)
[/code]

**hour小时**

[code]

             # Event.objects.filter(timestamp__hour=23)
            # Event.objects.filter(time__hour=5)
            # Event.objects.filter(timestamp__hour__gte=12)
[/code]

**minute**

[code]

             # Event.objects.filter(timestamp__minute=29)
            # Event.objects.filter(time__minute=46)
            # Event.objects.filter(timestamp__minute__gte=29)
[/code]

**second**

[code]

             # Event.objects.filter(timestamp__second=31)
            # Event.objects.filter(time__second=2)
            # Event.objects.filter(timestamp__second__gte=31)
[/code]



**删除数据**

**delete() 删除数据**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(mim=2345).delete()  #删除mim字段等于2345的条数据
        print(a)
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
[/code]



**修改数据**

**update(字段=值) 修改数据**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        a = yhubiao.objects.filter(mim=1988).update(mim=123)  #找到mim字段等于1988的数据，将mim字段值改为123，将指定条件的数据更新，均支持 **kwargs，支持字典
[/code]

[code]

     print(a) return render(request,'index.html',locals()) #打开页面 #返回
[/code]

**方式二【不推荐】**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        obj = yhubiao.objects.get(id=6)
        obj.mim = '111'
        obj.save()
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
[/code]



**query  查看sql语句**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):
        obj = yhubiao.objects.all()
        print(obj.query)         #查看sql语句
    
        return render(request,'index.html',locals())   #打开页面
    
    #返回
    # SELECT `app1_yhubiao`.`id`, `app1_yhubiao`.`anem`, `app1_yhubiao`.`mim` FROM `app1_yhubiao`
[/code]



