
---
layout: post
title: " 第三百八十八节，Django+Xadmin打造上线标准的在线教育平台—网站列表分页 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十八节，Django+Xadmin打造上线标准的在线教育平台—网站列表分页**



**分页可以用一个第三方分页模块django-pure-pagination**

**下载地址：https://github.com/jamespacileo/django-pure-pagination#settings**

**下载后安装此模块即可**



**使用 **pure-pagination分页配置****

****settings.py****

****注册分页app****

[code]

    INSTALLED_APPS = [
         'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
        'xadmin',                           # 注册xadmin的app
        'crispy_forms',                     # 注册xadmin的依赖app
        'captcha',                          # 注册验证码app
        'pure_pagination',                  # 注册分页app
    ]
[/code]

**设置分页配置**

[code]

     # 配置分页
    PAGINATION_SETTINGS = {
        'PAGE_RANGE_DISPLAYED': 10,                 # 总共显示多少个页码
        'MARGIN_PAGES_DISPLAYED': 2,                # 页面过多时间隔个数
    
        'SHOW_FIRST_PAGE_WHEN_INVALID': True,       # 超出页码范围，返回到第一页
    }
[/code]



**逻辑处理**

**注意：**

**1，说明，下面 红色背景的地方，就是分页模块的功能，是分页模块固定的写法,**

**2，** **只有 黄色背景的地方参数我们可以定义的**

**3， 最后传到html页面的people对象很重要，因为无论是显示数据，还是显示分页导航都循环的这个 **people****



[code]

    from django.shortcuts import render, HttpResponse, redirect                                 # 导入django向浏览器返回方法
    from django.views.generic.base import View
    from django.db.models import F,Q
    from pure_pagination import Paginator, EmptyPage, PageNotAnInteger　　　　　　　　　　　　　　　#导入分页模块的方法
    
    from app_organization.models import CityDict, CourseOrg                       # 数据库表
    
    
    class org_list(View):
        def get(self, request):
            # 城市
            cheng_shi = CityDict.objects.all()
    
            # 课程机构
            ji_gou = CourseOrg.objects.all()                # 获取数据库的所有数据
            ji_gou_shu = ji_gou.count()                     # 统计获取到的数量
    
            # 分页功能
            try:
                page = request.GET.get('page', 1)           # 获取当前页码,如果没有默认1
            except PageNotAnInteger:                        # 如果获取页码出错，默认1
                page = 1
    
            p = Paginator(ji_gou, 1, request=request)       # 执行分页函数，参数1数据库的数据，参数2显示多少条数据，参数3request
    
            people = p.page(page)                           # 返回一个，包含了分页数据和分页导航的对象
    
            return render(request, 'org_list.html', {
                'cheng_shi': cheng_shi,                 # 城市数据
                'people': people,                       # 将分页对象传到html页面
                'ji_gou_shu': ji_gou_shu,               # 机构数量
            })
    
        def post(self, request):
            pass
[/code]



**html页面**

**注意：**

**1，说明，下面 红色背景的地方，就是分页模块的功能，是分页模块固定的写法,**

**2，** **只有 黄色背景的地方参数我们可以定义的**

**3，最后传到html页面的people对象很重要，因为 无论是显示数据，还是显示分页导航都循环的这个 **people****



[code]

    <div class="butler_list company list">
                        <div class="layout">
                            <div class="head">
                                <ul class="tab_header">
                                    <li class="active"><a href="?ct=&city=">全部</a></li>
                                    <li class=""><a href="?sort=students&ct=&city=">学习人数 &#8595;</a></li>
                                    <li class=""><a href="?sort=courses&ct=&city=">课程数 &#8595;</a></li>
                                </ul>
                            </div>
                            {# 循环机构 #}
                            {% for ji in people.object_list %}      {# 分页对象.object_list里面是分页后的数据 #}
                                <dl class="des difdes">
                                <dt>
                                    <a href="org-detail-homepage.html">
                                        <img width="200" height="120" class="scrollLoading"
                                             data-url="{{ MEDIA_URL }}{{ ji.image }}"/>         {# 需要拼接静态资源路径 #}
                                    </a>
                                </dt>
                                <dd>
                                    <div class="clearfix">
                                        <a href="org-detail-homepage.html">
                                            <h1>{{ ji.name }}</h1>
                                            <div class="pic fl">
    
                                                <img src="/static/images/authentication.png"/>
    
                                                <img src="/static/images/gold.png"/>
    
                                            </div>
                                        </a>
                                    </div>
                                    <ul class="cont">
                                        <li class="first"><p class="pic9">课程数：<span>1</span></p>
                                            <p class="c7">学习人数：<span>1000</span></p></li>
                                        <li class="c8" style="padding-left:18px;">北京市海淀区中关村北大街</li>
                                        <li class="pic10" style="padding-left:18px;">经典课程：
    
                                            <a href="/diary/19/">c语言基础入门</a>
    
                                            <a href="/diary/16/">数据库基础</a>
    
                                        </li>
                                    </ul>
                                </dd>
                                <div class="buy start_groupbuy jsShowPerfect2" data-id="22"><br/>联系<br/>服务</div>
                            </dl>
                            {% endfor %}
    
                        </div>
                        <div class="pageturn">
                            <ul class="pagelist">
                                {% if people.has_previous %}                    {# 判断有上一页显示上一页 #}
                                    <li class="long"><a href="?{{ people.previous_page_number.querystring }}">上一页</a></li>
                                {% endif %}
    
                                {% for page in people.pages %}                  {# 循环页码 #}
                                    {% if page %}
                                        {% ifequal page people.number %}        {# 判断当前页码,显示当前页码 #}
                                            <li class="active"><a href="?{{ page.querystring }}">{{ page }}</a></li>
                                        {% else %}                              {# 显示其他页码 #}
                                            <li><a href="?{{ page.querystring }}" class="page">{{ page }}</a></li>
                                        {% endifequal %}
                                    {% else %}
                                        ...
                                    {% endif %}
                                {% endfor %}
    
                                {% if people.has_next %}                         {# 判断有下一页显示下一页 #}
                                    <li class="long"><a href="?{{ people.next_page_number.querystring }}">下一页</a></li>
                                {% endif %}
    
                            </ul>
                        </div>
                    </div>
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170917182247313-194814707.png)



