---
layout: post
title: " 第三百零六节，Django框架,models.py模块，数据库操作——创建表、数据类型、索引、admin后台，补充Django目录说明以及全局配置文件配置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Django框架,models.py模块，数据库操作——创建表、数据类型、索引、admin后台，补充Django目录说明以及全局配置文件配置**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709195819509-1644743724.png)**



![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709195905103-752342081.png)



####  数据库配置  

**django默认支持 sqlite，mysql, oracle,postgresql数据库。**



**1，django默认使用sqlite的数据库，默认自带sqlite的数据库驱动**



**  引擎名称：django.db.backends.sqlite3**

**在全局配置文件settings.py可以看到确认配置 **使用 ** **的**** sqlite数据库****

[code]

    # Database
    # https://docs.djangoproject.com/en/1.10/ref/settings/#databases
    # 默认配置使用的sqlite数据库
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',                 #配置数据库引擎名称
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),           #生成数据库到当前的项目文件夹里
        }
    }
[/code]

****![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170709214250322-782819237.png)****



**所以我们首次运行程序时会在目录生成db.sqlite3数据库**





**2，MySQL数据库【重点】**

**mysql驱动程序**

**          MySQLdb(mysql python)**

**          mysqlclient**

**          MySQL**

**          PyMySQL(纯python的mysql驱动程序)**

**在django的项目中会默认使用sqlite数据库，如果要使用 **MySQL数据库需要重新配置 **MySQL数据库信息，将
**sqlite数据库注释掉********

********在 **settings.py** 配置 **MySQL数据库信息**********

[code]

     #MySQL数据库
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',       #配置数据库引擎名称
            'NAME': 'jxiou',                            #数据库名称
            'USER': 'root',                             #数据库用户名
            'PASSWORD': '279819',                       #数据库密码
            'HOST': '127.0.0.1',                        #数据库链接地址
            'PORT': '3306',                             #数据库端口
        }
    }
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710092234868-332058295.png)



**注意：NAME即数据库的名字，在mysql连接前该数据库必须已经创建，而上面的sqlite数据库下的db.sqlite3则是项目自动创建**

**USER和PASSWORD分别是数据库的用户名和密码。**

**设置完后，再启动我们的Django项目前，需要激活我们的mysql。**

**然后，启动项目， 会报错：no module named MySQLdb**

**这是因为django默认你导入的驱动是 MySQLdb，可是MySQLdb对于py3有很大问题，所以我们需要的驱动是PyMySQL**

**所以，我们只需要找到项目里的全局配置里的 __init__,py配置数据库驱动  
**

**在里面写入：**

[code]

     import pymysql
    
    pymysql.install_as_MySQLdb()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710102102900-1602541038.png)





**此时django框架连接MySQL数据库配置好了**



**给PyCharm安装MySQL数据库管理插件**

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710122612837-1729529223.png)

配置数据库信息

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710122921243-1567320497.png)

下载数据库管理插件

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710123030165-623163917.png)

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710123138509-401642096.png)

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710123213181-450710364.png)





**django创建数据库表**

**在操作数据库表之前，首先检查一下全局配置文件settings.py里的数据库表操作配置里是否配置了应用路径，如果没有需要加入应用路径**

[code]

    INSTALLED_APPS = [
         'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app1',
    ]
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710170400337-1294120471.png)



**配置好了我们开始创建表**

**对数据库表的操作都是由 django下db模块的models对象来操作的，所以需要导入这个对象**

**注意：一张表对应一个类**

**首先要创建一个类来操作一张表，而这个类必须继承 models.Model对象**

**注意创建表之前，必须要先创建好数据库**



[code]

    from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class userinfo(models.Model):       #创建类必须继承models.Model，类名将是在数据库里的表名称
        #不设置主键id将自动创建
        anem = models.CharField("用户名",max_length=50)       #设置一个anem名称的字符串字段,最大长度50位，在django后台显示名称为：用户名
        address = models.CharField("地址", max_length=50)
        city = models.CharField('城市', max_length=60)
        country = models.CharField(max_length=50)
    
        class Meta:
            verbose_name = '用户表'                           #设置表名称在django后台显示的中文名称
            verbose_name_plural = verbose_name
    
        def __str__(self):                                   #设置在django后台显示字段名称
            return self.anem
[/code]



**设置好操作表的类后，我们需要生成表，生成表需要在PyCharm的终端输入命令，先输入  makemigrations  然后在输入   migrate
来生成表**



**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711102026368-779196364.png)**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711102037697-2057634074.png)**

**此时表就生成了**



**注意：我们已经生成了需要的表，也包含我们自定义的userinfo表，此时数据库里的 django_migrations表记录了，我们生成表时的信息，**

**如果我们将我们的 **userinfo表，删除后，在执行命令重建我们的 **userinfo表 ，将无法生成，因为
**django_migrations表 记录了你已经生成了********

********解决方法：********

********现将项目里 ** ** ** **migrations目录 下的缓存删除****************

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711102921900-942189502.png)**

**在重新执行命令， **makemigrations   然后在输入   migrate   来生成表，会提示你已经生成了这个表****

****![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711103214415-830873593.png)****

****我们打开 ** ** ** **django_migrations表 里找到，与现在 ** ** ** ** ** ** **
**migrations目录 下缓存名称相同的记录****************************

****![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711103548759-1127892425.png)****

****我们把 ** ** ** ** ** **django_migrations表
里的这条记录，删除后，就可以再次生成了****************

****************重点：注意只删除 ** ** ** ** ** **django_migrations表 里，与现在 ** ** ** **
** ** ** **migrations目录
下缓存名称相同的记录，否则将出问题********************************************





**配置django的admin数据库管理后台**

**首先配置数据库后台路由映射**

[code]

    from django.conf.urls import url
    from django.contrib import admin
    from app1 import views
    
    urlpatterns = [
         url(r'admin/', admin.site.urls),   #路由映射admin数据库管理
        url(r'articles/', views.special)     #路由映射第三个参数，额外传参，字典方式，逻辑处理函数以参数方式接收字典键
    ]
[/code]

**然后在PyCharm终端输入命令  Python manage.py createsuperuser**

**1、设置用户名**

**2、设置邮箱**

**3、设置密码，8位以上，不能纯数字**

**4、确认密码**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710183316181-1871518023.png)**

**然后用刚才设置的用户名和密码登录**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710183700728-1119795449.png)**

**只能看到刚才创建的用户登录数据，数据库数据需要在项目的admin.py里注册才能看到**

**admin.site.register(参数是数据库操作表的类)，注册数据库到admin数据库管理，参数是models.py里操作数据库表的类**

[code]

    from django.contrib import admin
    from app1.models import *
    
    admin.site.register(userinfo) #注册数据库到admin数据库管理，参数是models.py里操作数据库表的类
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170710185344431-1875529835.png)



**此时，可以看到admin管理页面已经出现了我们刚才创建的，用户表，显示的是中文，而且字段，也是中文，因为我们在用户表类里设置了admin显示中文的名称**

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class userinfo(models.Model):       #创建类必须继承models.Model，类名将是在数据库里的表名称
        #不设置主键id将自动创建
        anem = models.CharField("用户名",max_length=50)       #设置一个anem名称的字符串字段,最大长度50位，在django后台显示名称为：用户名
        address = models.CharField("地址", max_length=50)
        city = models.CharField('城市', max_length=60)
        country = models.CharField(max_length=50)
    
        class Meta:
            verbose_name = '用户表'                           #设置表名称在django后台显示的中文名称
            verbose_name_plural = verbose_name
    
        def __str__(self):                                   #设置在django后台显示字段名称
            return self.anem
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711105516790-1663334621.png)

**我们创建一条数据看看**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711105919322-808502176.png)**

**此时我们看到只显示了一个字段**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711110104712-2060046994.png)**



**此时，我们需要配置admin显示所有字段**

**方法：找到项目应用里的 admin.py文件，在注册表到admin哪里添加一个类，类继承admin.ModelAdmin类**

**配置好相应字段后，将类同表一起注册到admin**

[code]

     from django.contrib import admin
    from app1.models import *
    
    #配置userinfo表在admin的显示信息
    class userinfoAdmin(admin.ModelAdmin):
        # 配置显示字段,
        list_display = ('anem', 'address','city','country')
        # 配置查询字段
        search_fields = ('anem','city')
        # 配置排序字段
        ordering = ('-id',)
        # 配置右边是否有过滤条件字段
        list_filter = ('address',)
    admin.site.register(userinfo,userinfoAdmin) #注册数据库到admin数据库管理，参数是models.py里操作数据库表的类
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711111916150-834503106.png)

** **

**下面介绍表的数据类型，以及参数**



[code]

    from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class userinfo(models.Model):       #创建类必须继承models.Model，类名将是在数据库里的表名称
        #不设置主键id将自动创建
        anem = models.CharField("用户名",max_length=50)       #设置一个anem名称的字符串字段,最大长度50位，在django后台显示名称为：用户名
        address = models.CharField("地址", max_length=50)
        city = models.CharField('城市', max_length=60)
        country = models.CharField('性别',max_length=50)
    
        class Meta:
            verbose_name = '用户表'                           #设置表名称在django后台显示的中文名称
            verbose_name_plural = verbose_name
    
        def __str__(self):                                   #设置在django后台显示字段名称
            return self.anem
[/code]



**上面我们只用到了 CharField()，也就是varchar字符串类型，参数也只用到** **max_length=50 ，最大长度50位**





**models对象的数据类型**

[code]

     AutoField(Field)
            - int自增列，必须填入参数 primary_key=True
    
        BigAutoField(AutoField)
            - bigint自增列，必须填入参数 primary_key=True
    
            注：当model中如果没有自增列，则自动会创建一个列名为id的列
            from django.db import models
    
            class UserInfo(models.Model):
                # 自动创建一个列名为id的且为自增的整数列
                username = models.CharField(max_length=32)
    
            class Group(models.Model):
                # 自定义自增列
                nid = models.AutoField(primary_key=True)
                name = models.CharField(max_length=32)
    
        SmallIntegerField(IntegerField):
            - 小整数 -32768 ～ 32767
    
        PositiveSmallIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
            - 正小整数 0 ～ 32767
        IntegerField(Field)
            - 整数列(有符号的) -2147483648 ～ 2147483647
    
        PositiveIntegerField(PositiveIntegerRelDbTypeMixin, IntegerField)
            - 正整数 0 ～ 2147483647
    
        BigIntegerField(IntegerField):
            - 长整型(有符号的) -9223372036854775808 ～ 9223372036854775807
    
        自定义无符号整数字段
    
            class UnsignedIntegerField(models.IntegerField):
                def db_type(self, connection):
                    return 'integer UNSIGNED'
    
            PS: 返回值为字段在数据库中的属性，Django字段默认的值为：
                'AutoField': 'integer AUTO_INCREMENT',
                'BigAutoField': 'bigint AUTO_INCREMENT',
                'BinaryField': 'longblob',
                'BooleanField': 'bool',
                'CharField': 'varchar(%(max_length)s)',
                'CommaSeparatedIntegerField': 'varchar(%(max_length)s)',
                'DateField': 'date',
                'DateTimeField': 'datetime',
                'DecimalField': 'numeric(%(max_digits)s, %(decimal_places)s)',
                'DurationField': 'bigint',
                'FileField': 'varchar(%(max_length)s)',
                'FilePathField': 'varchar(%(max_length)s)',
                'FloatField': 'double precision',
                'IntegerField': 'integer',
                'BigIntegerField': 'bigint',
                'IPAddressField': 'char(15)',
                'GenericIPAddressField': 'char(39)',
                'NullBooleanField': 'bool',
                'OneToOneField': 'integer',
                'PositiveIntegerField': 'integer UNSIGNED',
                'PositiveSmallIntegerField': 'smallint UNSIGNED',
                'SlugField': 'varchar(%(max_length)s)',
                'SmallIntegerField': 'smallint',
                'TextField': 'longtext',
                'TimeField': 'time',
                'UUIDField': 'char(32)',
    
        BooleanField(Field)
            - 布尔值类型
    
        NullBooleanField(Field):
            - 可以为空的布尔值
    
        CharField(Field)
            - 字符类型
            - 必须提供max_length参数， max_length表示字符长度
    
        TextField(Field)
            - 文本类型
    
        EmailField(CharField)：
            - 字符串类型，Django Admin以及ModelForm中提供验证机制
    
        IPAddressField(Field)
            - 字符串类型，Django Admin以及ModelForm中提供验证 IPV4 机制
    
        GenericIPAddressField(Field)
            - 字符串类型，Django Admin以及ModelForm中提供验证 Ipv4和Ipv6
            - 参数：
                protocol，用于指定Ipv4或Ipv6， 'both',"ipv4","ipv6"
                unpack_ipv4， 如果指定为True，则输入::ffff:192.0.2.1时候，可解析为192.0.2.1，开启刺功能，需要protocol="both"
    
        URLField(CharField)
            - 字符串类型，Django Admin以及ModelForm中提供验证 URL
    
        SlugField(CharField)
            - 字符串类型，Django Admin以及ModelForm中提供验证支持 字母、数字、下划线、连接符（减号）
    
        CommaSeparatedIntegerField(CharField)
            - 字符串类型，格式必须为逗号分割的数字
    
        UUIDField(Field)
            - 字符串类型，Django Admin以及ModelForm中提供对UUID格式的验证
    
        FilePathField(Field)
            - 字符串，Django Admin以及ModelForm中提供读取文件夹下文件的功能
            - 参数：
                    path,                      文件夹路径
                    match=None,                正则匹配
                    recursive=False,           递归下面的文件夹
                    allow_files=True,          允许文件
                    allow_folders=False,       允许文件夹
    
        FileField(Field)
            - 字符串，路径保存在数据库，文件上传到指定目录
            - 参数：
                upload_to = ""      上传文件的保存路径
                storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
    
        ImageField(FileField)
            - 字符串，路径保存在数据库，文件上传到指定目录
            - 参数：
                upload_to = ""      上传文件的保存路径
                storage = None      存储组件，默认django.core.files.storage.FileSystemStorage
                width_field=None,   上传图片的高度保存的数据库字段名（字符串）
                height_field=None   上传图片的宽度保存的数据库字段名（字符串）
    
        DateTimeField(DateField)
            - 日期+时间格式 YYYY-MM-DD HH:MM[:ss[.uuuuuu]][TZ]
    
        DateField(DateTimeCheckMixin, Field)
            - 日期格式      YYYY-MM-DD
    
        TimeField(DateTimeCheckMixin, Field)
            - 时间格式      HH:MM[:ss[.uuuuuu]]
    
        DurationField(Field)
            - 长整数，时间间隔，数据库中按照bigint存储，ORM中获取的值为datetime.timedelta类型
    
        FloatField(Field)
            - 浮点型
    
        DecimalField(Field)
            - 10进制小数
            - 参数：
                max_digits，小数总长度
                decimal_places，小数位长度
    
        BinaryField(Field)
            - 二进制类型
[/code]



**数据类型参数**

[code]

    　　 null                数据库中字段是否可以为空
        db_column           数据库中字段的列名
        db_tablespace
        default             数据库中字段的默认值
        primary_key         数据库中字段是否为主键  
    
[/code]

auto_now 和 auto_now_add  
auto_now 会自动创建时间字段，无论添加或者修改，都是系统当前时间  
auto_now_add 会自动创建时间字段，永远是创建时的时间

[code]

        db_index            数据库中字段是否可以建立索引
         unique              数据库中字段是否可以建立唯一索引
        unique_for_date     数据库中字段【日期】部分是否可以建立唯一索引
        unique_for_month    数据库中字段【月】部分是否可以建立唯一索引
        unique_for_year     数据库中字段【年】部分是否可以建立唯一索引
    
        verbose_name        Admin中显示的字段名称
        blank               Admin中是否允许用户输入为空
        editable            Admin中是否可以编辑
        help_text           Admin中该字段的提示信息
        choices             Admin中显示选择框的内容，用不变动的数据放在内存中从而避免跨表操作
                            如：gf = models.IntegerField(choices=[(0, '何穗'),(1, '大表姐'),],default=1)
    
        error_messages      自定义错误信息（字典类型），从而定制想要显示的错误信息；
                            字典健：null, blank, invalid, invalid_choice, unique, and unique_for_date
                            如：{'null': "不能为空.", 'invalid': '格式错误'}
    
        validators          自定义错误验证（列表类型），从而定制想要的验证规则
                            from django.core.validators import RegexValidator
                            from django.core.validators import EmailValidator,URLValidator,DecimalValidator,\
                            MaxLengthValidator,MinLengthValidator,MaxValueValidator,MinValueValidator
                            如：
                                test = models.CharField(
                                    max_length=32,
                                    error_messages={
                                        'c1': '优先错信息1',
                                        'c2': '优先错信息2',
                                        'c3': '优先错信息3',
                                    },
                                    validators=[
                                        RegexValidator(regex='root_\d+', message='错误了', code='c1'),
                                        RegexValidator(regex='root_112233\d+', message='又错误了', code='c2'),
                                        EmailValidator(message='又错误了', code='c3'), ]
                                )
[/code]





**创建表索引**

**普通索引，和联合普通索引**

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class yhubiao(models.Model):
        id = models.AutoField('id',primary_key=True)
        anem = models.CharField("用户名",max_length=50)
        mim = models.CharField("地址", max_length=50)
        country = models.CharField('性别',max_length=50)
    
        class Meta:
            # 联合索引
            index_together = [
                ("anem", "mim"),        #一个字段是普通索引，两个字段是联合普通索引
            ]
    
            verbose_name = '用户表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.anem
[/code]



**唯一索引和联合唯一索引**

[code]

     from __future__ import unicode_literals
    
    from django.db import models        #导入models对象
    
    class yhubiao(models.Model):
        id = models.AutoField('id',primary_key=True)
        anem = models.CharField("用户名",max_length=50)
        mim = models.CharField("地址", max_length=50)
        country = models.CharField('性别',max_length=50)
    
        class Meta:
            # 联合唯一索引
            unique_together = (("mim", "anem"),)        #一个字段是唯一索引，两个字段是联合唯一索引
    
            verbose_name = '用户表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.anem
[/code]

**触发验证**

[code]

    1.触发Model中的验证和错误提示有两种方式：
            a. Django Admin中的错误信息会优先根据Admiin内部的ModelForm错误信息提示，如果都成功，才来检查Model的字段并显示指定错误信息
            b. 调用Model对象的 clean_fields 方法，如：
                 # models.py
                class UserInfo(models.Model):
                    nid = models.AutoField(primary_key=True)
                    username = models.CharField(max_length=32)
    
                    email = models.EmailField(error_messages={'invalid': '格式错了.'})
    
                # views.py
                def index(request):
                    obj = models.UserInfo(username='11234', email='uu')
                    try:
                        print(obj.clean_fields())
                    except Exception as e:
                        print(e)
                    return HttpResponse('ok')
    
               # Model的clean方法是一个钩子，可用于定制操作，如：上述的异常处理。
    
        2.Admin中修改错误提示
            # admin.py
            from django.contrib import admin
            from model_club import models
            from django import forms
    
    
            class UserInfoForm(forms.ModelForm):
                username = forms.CharField(error_messages={'required': '用户名不能为空.'})
                email = forms.EmailField(error_messages={'invalid': '邮箱格式错误.'})
                age = forms.IntegerField(initial=1, error_messages={'required': '请输入数值.', 'invalid': '年龄必须为数值.'})
    
                class Meta:
                    model = models.UserInfo
                    # fields = ('username',)
                    fields = "__all__"
    
    
            class UserInfoAdmin(admin.ModelAdmin):
                form = UserInfoForm
    
    
            admin.site.register(models.UserInfo, UserInfoAdmin)
[/code]



**  补充Django目录说明以及全局配置文件**

  **Django目录说明**

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170711220955181-1129209645.png)  

**全局配置文件配置**

[code]

     """
    Django settings for Xiangmu project.
    
    Generated by 'django-admin startproject' using Django 1.10.
    
    For more information on this file, see
    https://docs.djangoproject.com/en/1.10/topics/settings/
    
    For the full list of settings and their values, see
    https://docs.djangoproject.com/en/1.10/ref/settings/
    """
    
    import os
    
    # Build paths inside the project like this: os.path.join(BASE_DIR, ...)
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    
    
    # Quick-start development settings - unsuitable for production
    # See https://docs.djangoproject.com/en/1.10/howto/deployment/checklist/
    
    # SECURITY WARNING: keep the secret key used in production secret!
    SECRET_KEY = '!eco91o+^k9q#^j79@oymxltu-%osux)dpet_qv9kp88e)2o*7'
    
    # SECURITY WARNING: don't run with debug turned on in production!
    DEBUG = True
    
    ALLOWED_HOSTS = []
    
    
    # Application definition
    # 注册APP，也就是注册应用项目，只有注册了的应用才能操作数据库
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app1',
    ]
    
    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        # 'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]
    
    ROOT_URLCONF = 'Xiangmu.urls'
    
    #配置模板
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')]           #配置模板文件路径，也就是html路径
            ,
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]
    
    WSGI_APPLICATION = 'Xiangmu.wsgi.application'
    
    
    # Database
    # https://docs.djangoproject.com/en/1.10/ref/settings/#databases
    # 默认配置使用的sqlite数据库
    # DATABASES = {
    #     'default': {
    #         'ENGINE': 'django.db.backends.sqlite3',                 #配置数据库引擎名称
    #         'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),           #生成数据库到当前的项目文件夹里
    #     }
    # }
    
    #MySQL数据库
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',       #配置数据库引擎名称
            'NAME': 'jxiou',                            #数据库名称
            'USER': 'root',                             #数据库用户名
            'PASSWORD': '279819',                       #数据库密码
            'HOST': '127.0.0.1',                        #数据库链接地址
            'PORT': '3306',                             #数据库端口
        }
    }
    
    
    # Password validation
    # https://docs.djangoproject.com/en/1.10/ref/settings/#auth-password-validators
    
    AUTH_PASSWORD_VALIDATORS = [
        {
            'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
        },
    ]
    
    
    # Internationalization
    # https://docs.djangoproject.com/en/1.10/topics/i18n/
    
    LANGUAGE_CODE = 'en-us'
    
    TIME_ZONE = 'UTC'
    
    USE_I18N = True
    
    USE_L10N = True
    
    USE_TZ = True
    
    
    # Static files (CSS, JavaScript, Images)
    # https://docs.djangoproject.com/en/1.10/howto/static-files/
    
    #配置静态文件前缀
    STATIC_URL = '/static/'
    #配置静态文件目录
    STATICFILES_DIRS = (
        os.path.join(BASE_DIR,'static')
    )
[/code]









[/code]

[code]

