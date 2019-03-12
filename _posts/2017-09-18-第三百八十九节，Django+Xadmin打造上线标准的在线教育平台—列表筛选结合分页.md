
---
layout: post
title: " 第三百八十九节，Django+Xadmin打造上线标准的在线教育平台—列表筛选结合分页 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百八十九节，Django+Xadmin打造上线标准的在线教育平台—列表筛选结合分页**

**根据用户的 **筛选条件来结合分页****

****![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170918115142603-437839867.png)****





**实现原理就是，当用户点击一个筛选条件时，通过get请求方式传参将筛选的id或者值，传入逻辑处理就行数据库条件查询，将查询条件值在返回html页面判断是否是选中样式，最后将所有需要关联的筛选请求加上彼此逻辑处理传回来的查询条件值**

**html请求传参**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170918120802696-326359768.png)**

**黄色背景为请求传参**

**红色背景为逻辑处理传过来的查询条件判断样式**

[code]

     <div class="wp butler_list_box list">
                <div class='left'>
                    <div class="listoptions">
                        <ul>
                            <li>
                                <h2>机构类别</h2>
                                <div class="cont">
                                    <a href="?leib=&chsh={{ chsh_id }}"><span class="{% ifequal lei_bie '' %}active2{% endifequal %}">全部</span></a>
    
                                    <a href="?leib=pxjg&chsh={{ chsh_id }}"><span class="{% ifequal lei_bie 'pxjg' %}active2{% endifequal %}">培训机构</span></a>
    
                                    <a href="?leib=gx&chsh={{ chsh_id }}"><span class="{% ifequal lei_bie 'gx' %}active2{% endifequal %}">高校</span></a>
    
                                    <a href="?leib=gr&chsh={{ chsh_id }}"><span class="{% ifequal lei_bie 'gr' %}active2{% endifequal %}">个人</span></a>
    
                                </div>
                            </li>
                            <li>
                                <h2>所在地区</h2>
                                <div class="more">更多</div>
                                <div class="cont">
                                    <a href="?chsh=&leib={{ lei_bie }}"><span class="{% ifequal chsh_id '' %}active2{% endifequal %}">全部</span></a>
                                    {# 循环城市 #}
                                    {% for ch in cheng_shi %}
                                        <a href="?chsh={{ ch.id }}&leib={{ lei_bie }}"><span class="{% ifequal chsh_id ch.id|stringformat:'i' %}active2{% endifequal %}">{{ ch.name }}</span></a>
                                    {% endfor %}
                                </div>
                            </li>
                        </ul>
                    </div>
[/code]



**逻辑处理**

[code]

     from django.shortcuts import render, HttpResponse, redirect                                 # 导入django向浏览器返回方法
    from django.views.generic.base import View
    from django.db.models import F,Q
    from pure_pagination import Paginator, EmptyPage, PageNotAnInteger
    
    from app_organization.models import CityDict, CourseOrg                       # 数据库表
    
    
    class org_list(View):
        def get(self, request):
    
            # 课程机构
            ji_gou = CourseOrg.objects.all()                # 获取数据库的所有数据
    
            # 城市帅选
            cheng_shi = CityDict.objects.all()
            chsh_id = request.GET.get('chsh', '')           # 获取用户点击了城市传过来的城市id
            if chsh_id:
                ji_gou = ji_gou.filter(city_id=chsh_id)     # 帅选出指定城市的数据
    
            # 类别帅选
            lei_bie = request.GET.get('leib', '')           # 获取用户点击了城市传过来的城市id
            if lei_bie:
                ji_gou = ji_gou.filter(category=lei_bie)     # 帅选出指定城市的数据
    
            ji_gou_shu = ji_gou.count()                   # 统计获取到的数量
    
            # 分页功能
            try:
                page = request.GET.get('page', 1)           # 获取当前页码,如果没有默认1
            except PageNotAnInteger:                        # 如果获取页码出错，默认1
                page = 1
    
            p = Paginator(ji_gou, 4, request=request)       # 执行分页函数，参数1数据库的数据，参数2显示多少条数据，参数3request
    
            people = p.page(page)                           # 返回一个，包含了分页数据和分页导航的对象
    
            return render(request, 'org_list.html', {
                'cheng_shi': cheng_shi,                 # 城市数据
                'people': people,                       # 将分页对象传到html页面
                'ji_gou_shu': ji_gou_shu,               # 机构数量
                'chsh_id': chsh_id,                     # 城市帅选ID
                'lei_bie': lei_bie                      # 类别
            })
    
        def post(self, request):
            pass
[/code]



