---
layout: post
title: " 第三百一十一节，Django框架，Form表单验证 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百一十一节，Django框架，Form表单验证**



**表单提交**

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" type="text/css" href="/static/css/tou.css">
    </head>
    <body>
    <form action="/bugarticles/" method="post">
        <div>
            <input type="text" name="user"/>
        </div>
        <div>
            <input type="text" name="pwd"/>
        </div>
        <div>
            <input type="submit" value="提交"/>
        </div>
    </form>
    </body>
    </html>
[/code]

**路由映射**

[code]

    urlpatterns = [
        url(r 'admin/', admin.site.urls),   #路由映射admin数据库管理
        url(r'articles/', views.special)    
    ]
[/code]

**逻辑处理**

**method 属性获取用户请求方式，post或者get**  
 **使用方式：请求对象.method**

**POST 获取用户post请求方式的信息**  
 **使用方式：请求对象.POST**

**POST.get() 获取用户POST请求方式的表单name名称对应的值，参数是表单name名**

[code]

    from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    
    #逻辑处理模块
    def special(request):  　　　　　　　　　　　　　 #自定义参数接收用户请求对象
        if request.method == "POST":　　　　　　　　 #判断用户请求如果是post方式
            print(request.POST.get('user',None))  #接收用户表单提交的name名称对应的值
            print(request.POST.get('pwd', None))  #接收用户表单提交的name名称对应的值
        return render(request, 'app1/index.html', locals())  # 打开页面
[/code]





**表单提交验证，获取数据与获取错误信息**

**1、创建表单验证模块，必须继承** **Django的表单验证forms.Form类**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField()    #接收逻辑处理时，创建yhbd类时传进来的POST对象，里的表单name名对应的值进行验证
        pwd = forms.CharField()     ##接收逻辑处理时，创建yhbd类时传进来的POST对象，里的表单name名对应的值进行验证
[/code]

**2、逻辑处理，创建表单验证模块里的验证类，并将用户请求的 POST对象，传入验证类进行验证，验证后获取验证通过的提交信息，或者验证没通过的错误信息**

**如果出现错误，将错误信息对象以字典方式传到html页面**



**is_valid() 返回验证是否通过的布尔值**  
 **使用方式：验证类.is_valid()**



**cleaned_data 获取验证通过后的所有提交数据，返回字典**  
 **使用方式：验证类.cleaned_data**



**errors 获取验证错误信息，返回所有表单的错误信息对象**  
 **使用方法：验证类.errors**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        if request.method == 'GET':
            return render(request, 'app1/index.html', locals())  # 打开页面
    
        if request.method == "POST":
            # print(request.POST.get('user',None))          #接收用户表单提交的name名称对应的值
            # print(request.POST.get('pwd', None))          #接收用户表单提交的name名称对应的值
    
            f = yhbd(request.POST)                          #创建验证表单类，将用户请求POST对象传进表单验证类进行验证
    
            # ret = f.is_valid()                            #返回验证是否通过
            # print(ret)                                    #返回布尔值
    
            if f.is_valid():                                #判断验证如果通过
                print(f.cleaned_data)                       #获取到用户提交信息,字典方式
            else:                                           #如果没通过
                print(f.errors)                             #获取错误对象
    
            return render(request, 'app1/index.html',{'cuow':f.errors})  # 打开页面，将错误信息用字典方式传到html页面
[/code]

**3、在html页面接收逻辑处理 以字典形式传过来的错误对象，分别获取不同表单的错误信息**

[code]

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" type="text/css" href="/static/css/tou.css">
    </head>
    <body>
    
    <form action="/bugarticles/" method="post">
        <div>
            <input type="text" name="user"/>
            <span>{{ cuow.user.0 }}</span>     <!-- 接收错误信息里的user的错误信息 -->
        </div>
        <div>
            <input type="text" name="pwd"/>
            <span>{{ cuow.pwd.0 }}</span>      <!-- 接收错误信息里的pwd的错误信息 -->
        </div>
        <div>
            <input type="submit" value="提交"/>
        </div>
    </form>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170716170032722-817776133.png)



**利用表单类自动创建表单标签**

**以上表单的
<input>是我们自己手动写的，还可以用表单类来自动创建表单标签，好处是不用自己写表单标签，还有就是当用户填写的表单不合法提交时提示错误信息不清空表单**



**注意：表单类根据字段创建的表单标签，当用户输入内容时，首先要经过浏览器默认行为的表单验证，如果浏览器
**默认行为的表单验证都没有通过那么将无法提交****

******浏览器 **默认行为的表单验证，通过了在进行我们定义的表单类验证，验证合法获取用户提交信息，不合法返回错误信息********

********利用表单类自动创建表单标签********

********1、首先在get访问页面时，创建表单类不传参数，然后把这个表单类传到html页面，在html页面通过，
表单类.字段名称，来自动创建表单标签********

********每一种表单字段类型，都有一个默认的表单标签，这个标签是可以更改的，所以表单类可以创建任何表单标签********

********2、在post访问时，再次创建表单类需要传参，将post请求对象传入表单类进行验证表单，如果表单不合法，将错误信息对象传到html显示错误信息，将这次创建的表单类传到html页面替换get时创建的表单类********

**逻辑处理**

[code]

     from django.shortcuts import render
    from app1.models import *    #导入数据库操作模块
    from app1.biaodan import *   #导入自定义表单验证模块
    #逻辑处理模块
    def special(request):
        if request.method == 'GET':
            f = yhbd()                                            #创建表单验证类，不传参
            return render(request, 'app1/index.html',{'form':f})  # 打开页面，并将表单验证类传到html生成表单标签
    
        if request.method == "POST":
            f = yhbd(request.POST)                          #创建验证表单类，将用户请求POST对象传进表单验证类进行验证
    
            if f.is_valid():                                #判断验证如果通过
                print(f.cleaned_data)                       #获取到用户提交信息,字典方式
            else:                                           #如果没通过
                # print(f.errors)                           #获取错误对象
                pass
    
            return render(request, 'app1/index.html',{'cuow':f.errors,'form':f})  # 打开页面，将错误信息用字典方式传到html页面，并且将表单类传到html页面替换没传参的表单验证类
[/code]

**html**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <link rel="stylesheet" type="text/css" href="/static/css/tou.css">
    </head>
    <body>
    
    <form action="/bugarticles/" method="post">
        <div>
            {{ form.user }}                                     <!-- 接收get请求时创建的表单类，生成表单标签 -->
            {% if cuow.user.0 %}
                <span class="cuow">{{ cuow.user.0 }}</span>     <!-- 接收错误信息里的user的错误信息 -->
            {% endif %}
        </div>
        <div>
            {{ form.pwd }}                                      <!-- 接收get请求时创建的表单类，生成表单标签 -->
            {% if cuow.pwd.0 %}
                <span class="cuow">{{ cuow.pwd.0 }}</span>      <!-- 接收错误信息里的pwd的错误信息 -->
            {% endif %}
        </div>
        <div>
            <input type="submit" value="提交"/>
        </div>
    </form>
    </body>
    </html>
[/code]





**常用的内置验证字段**

**EmailField() 验证邮箱字段**  
 **CharField() 验证字符串字段**  
 **URLField() 验证url地址字段**  
 **IntegerField() 验证数字字段**  
 **GenericIPAddressField() 验证IP字段**

**注意：虽然有很多内置验证字段，但是我们还是要根据我们自己的需求来验证，所以**



**验证字段的参数**

**required 设置字段是否可以为空**  
 **True不可以为空**  
 **False可以为空**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(required=True)   #True不可以为空
        pwd = forms.CharField()
[/code]

**max_length 最大字符数**  
 **min_length 最小字符数**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(max_length=4,min_length=2)
        pwd = forms.CharField()
[/code]

**error_messages 自定义错误提示信息**  
 **参数是一个字典{'验证名称':'错误提示'}**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
        pwd = forms.CharField()
[/code]

**invalid 设置邮箱格式错误提示信息**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
        pwd = forms.EmailField(
            error_messages={
                'required': '邮箱不能为空',
                'invalid':'邮箱格式不正确'
            }
        )
[/code]

**widget 设置表单字段在html页面的类型**  
 **使用方式：widget=forms.Textarea()**  
 **Textarea(): <textarea>标签类型**  
 **TextInput()： <input>标签类型**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
        pwd = forms.CharField(
            widget=forms.TextInput(),
        )
[/code]

**attrs 给表单标签设置属性，可以给标签元素设置class样式，和input标签的各种type属性**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
        pwd = forms.CharField(
            widget=forms.TextInput(attrs={'type':'password','class':'c1'}),
        )
[/code]

**Select 生成表单，select标签，下拉选项框**  
 **参数:**  
 ** choices设置下拉数据，元组类型**  
 ** attrs设置select标签属性**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
    
        zhi = (
            (0, '普通会员'),
            (1, '超级会员'),
            (2, '黄金会员'),
            (3, '白银会员'),
            (4, 'vip会员')
        )
        pwd = forms.CharField(
            widget=forms.widgets.Select(choices=zhi,attrs={'class':'c1'})
        )
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170717194742910-289353552.png)



**下拉框结合数据库应用**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    from app1.models import *       #导入数据库操作
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
    
        a = shengf.objects.all().values_list('id','shf') #获取数据库里shengf表里的id和shf字段的数据
        pwd = forms.CharField(
            widget=forms.widgets.Select(choices=a,attrs={'class':'c1'}) #将数据库的数据显示到下拉框
        )
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170717194742910-289353552.png)



**下拉框结合数据库应用，防止数据库添加了数据，或者删除了数据，页面缓存了下拉框数据，无法事实数据同步**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    from app1.models import *       #导入数据库操作
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
    
        a = shengf.objects.all().values_list('id','shf') #获取数据库里shengf表里的id和shf字段的数据
        pwd = forms.CharField(
            widget=forms.widgets.Select(choices=a,attrs={'class':'c1'}) #将数据库的数据显示到下拉框
        )
    
        #防止数据库添加了数据，或者删除了数据，页面缓存了下拉框数据，无法事实数据同步
        def __init__(self,*args, **kwargs):                                     #创建类的__init__方法，每次创建类时都会执行
            super(yhbd,self).__init__(*args, **kwargs)                          #获取当前类的父类里的__init__方法执行
            a = shengf.objects.all().values_list('id', 'shf')                   #重新获取数据库里shengf表里的id和shf字段的数据
            self.fields['pwd'] = forms.CharField(widget=forms.widgets.Select(choices=a,attrs={'class':'c1'}))  #更新一下表单pwd字段的数据
[/code]



**自定义验证规则**

**validators 设置自定义验证规则，参数是一个列表，列表里是自定义验证方法名称**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    #表单验证
    from django import forms        #导入Django的表单验证模块
    from django.core.exceptions import ValidationError
    import re
    
    class yhbd(forms.Form):         #自定义验证表单类，继承Django的表单验证类
        user = forms.CharField(
            required=True,
            max_length=4,
            min_length=2,
            error_messages={
                'required':'用户名不能为空',
                'max_length':'最大长度不得超过4个字符',
                'min_length':'最小长度不得少于2个字符'
            }
        )
    
    
        #自定义验证规则
        def shouji(value):
            mobile_re = re.compile(r'^(13[0-9]|15[012356789]|17[678]|18[0-9]|14[57])[0-9]{8}$')
            if not mobile_re.match(value):
                raise ValidationError('手机号码格式错误')   #如果不匹配返回错误信息
    
    
        pwd = forms.CharField(
            validators=[shouji, ],   #设置自定义验证规则
            required=True,
            widget=forms.TextInput(
                attrs={
                    'class': "cl",
                    'placeholder': u'手机号码'
                }
            ),
            error_messages={
                'required':'手机不能为空',
            }
        )
[/code]

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170717232723411-1592842803.png)



**其他**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import re
    from django import forms
    from django.core.exceptions import ValidationError
    
    
    def mobile_validate(value):
        mobile_re = re.compile(r'^(13[0-9]|15[012356789]|17[678]|18[0-9]|14[57])[0-9]{8}$')
        if not mobile_re.match(value):
            raise ValidationError('手机号码格式错误')
    
    
    class PublishForm(forms.Form):
    
        user_type_choice = (
            (0, u'普通用户'),
            (1, u'高级用户'),
        )
    
        user_type = forms.IntegerField(widget=forms.widgets.Select(choices=user_type_choice,
                                                                      attrs={'class': "form-control"}))
    
        title = forms.CharField(max_length=20,
                                min_length=5,
                                error_messages={'required': u'标题不能为空',
                                                'min_length': u'标题最少为5个字符',
                                                'max_length': u'标题最多为20个字符'},
                                widget=forms.TextInput(attrs={'class': "form-control",
                                                              'placeholder': u'标题5-20个字符'}))
    
        memo = forms.CharField(required=False,
                               max_length=256,
                               widget=forms.widgets.Textarea(attrs={'class': "form-control no-radius", 'placeholder': u'详细描述', 'rows': 3}))
    
        phone = forms.CharField(validators=[mobile_validate, ],
                                error_messages={'required': u'手机不能为空'},
                                widget=forms.TextInput(attrs={'class': "form-control",
                                                              'placeholder': u'手机号码'}))
    
        email = forms.EmailField(required=False,
                                error_messages={'required': u'邮箱不能为空','invalid': u'邮箱格式错误'},
                                widget=forms.TextInput(attrs={'class': "form-control", 'placeholder': u'邮箱'}))
[/code]



**注意：如果表单是通过Ajax提交的，页面不刷新，那么html页面将无法获取到错误信息，那么我们只能将所有错误信息构造成字典，然后以json的方式返回给Ajax，添加到页面**





**将models数据库表类转换成表单验证类【必要使用】**

**这样可以少写表单验证代码，使用的是数据库字段的验证规则**

**models.py**

[code]

     from django.db import models        # 导入models对象
    
    class CourseOrg(models.Model):
        name = models.CharField(max_length=50, verbose_name='机构名称')
        desc = models.TextField(verbose_name='机构描述')
        category = models.CharField(max_length=20, verbose_name='机构类别', default='pxjg', choices=(('pxjg', '培训机构'), ('gx', '高校'), ('gr', '个人')))
        click = models.IntegerField(default=0, verbose_name='点击数')
        fav_nums = models.IntegerField(default=0, verbose_name='收藏数')
        image = models.ImageField(upload_to='org/%Y/%m', storage=ImageStorage(), verbose_name='封面图', max_length=100)
        address = models.CharField(max_length=150, verbose_name='机构地址')
        city = models.ForeignKey(CityDict, verbose_name='外键城市表')
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程机构表'
            verbose_name_plural = verbose_name
    
        def __str__(self):
            return self.name
[/code]

**forms.py**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from django import forms                             # 导入Django的表单验证模块
    from app_organization.models import **CourseOrg**         # 导入数据库表类
    
    
    class CourseOrgForm(forms.ModelForm):
        zdyi = forms.CharField()                         # 自定义表单验证字段
    
        class Meta:
            model = CourseOrg                            # 设置要将数据库表类转换成表单验证类的名称
            fields = ['name','category','fav_nums']      # 要使用的字段
[/code]



