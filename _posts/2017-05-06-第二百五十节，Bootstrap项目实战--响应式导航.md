---
layout: post
title: " 第二百五十节，Bootstrap项目实战--响应式导航 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap项目实战--响应式导航**



**学习要点：**

**1.响应式导航**



**一．响应式导航**

**基本导航组件+响应式**



**第一步，声明导航区域，设置导航默认样式，设置导航条固定在顶部**  
 **navbar样式class类，写在导航 <nav>里，声明导航区域(项目实战Bootstrap)**  
 **navbar-default样式class类，写在导航 <nav>里，设置导航默认样式(项目实战Bootstrap)**  
 **navbar-fixed-top样式class类，写在导航 <nav>里，设置导航条固定在顶部(项目实战Bootstrap)**



**第二步，设置导航内容区域固定布局，最大宽度1140**  
 **container样式class类，写在导航内容区域 <div>里，设置导航内容区域固定布局，最大宽度1140(项目实战Bootstrap)**



**第三步，设置导航标题区域**  
 **navbar-header样式class类，写在导航标题区域 <div>里，设置导航标题区域样式(项目实战Bootstrap)**  
 **navbar-brand样式class类，写在导航标题内容 <a>里，设置导航标题内容样式(项目实战Bootstrap)**  
 **navbar-toggle样式class类，写在导航标题 <button>里，设置导航标题里响应式按钮样式(项目实战Bootstrap)**  
 **icon-bar样式class类，写在导航标题按钮
<span>里，设置导航响应式按钮文字样式，也就是一横，写3个就是三横(项目实战Bootstrap)**



**第四步，设置导航折叠区域来写导航列表**  
 **collapse样式class类，写在导航列表区域 <div>里，设置导航列表折叠区域(项目实战Bootstrap)**  
 **navbar-collapse样式class类，写在导航列表区域 <div>里，设置导航列表折叠样式(项目实战Bootstrap)**  
 **nav样式class类，写在导航列表区域 <ul>里，设置导航列表区域(项目实战Bootstrap)**  
 **navbar-nav样式class类，写在导航列表区域 <ul>里，设置导航列表样式(项目实战Bootstrap)**  
 **navbar-right样式class类，写在导航列表区域 <ul>里，设置导航列表右浮动(项目实战Bootstrap)**  
 **active样式class类，写在导航列表区域 <li>里，设置当前导航列表项首选(项目实战Bootstrap)**  
 **glyphicon样式class类，写在导航列表区域 <li>里，设置当前导航列表项图标(项目实战Bootstrap)**



**第五步，事件绑定**  
 **将导航列表的折叠区域设置一个id,在导航按钮上关联折叠区域的id**  
 **data-target="#navbar-collapse"写在导航按钮
<button>里，将按钮事件关联折叠区域的id(项目实战Bootstrap)**  
 **data-toggle="collapse"写在导航按钮 <button>里，设置导航事件，点击折叠和收缩(项目实战Bootstrap)**

**html**

[code]

     <nav class="navbar navbar-default navbar-fixed-top">                <!--声明导航区域，设置导航默认样式，设置导航条固定在顶部-->
        <div class="container">                                            <!--设置固定布局，最大宽度1140-->
            <div class="navbar-header">                                    <!--设置导航标题区域-->
                <a href="#" class="navbar-brand" style="padding:0;"><img src="img/logo.png" alt="瓢城企训网"></a>    <!--设置导航标内容-->
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#navbar-collapse">    <!--设置导航按钮-->
                    <span class="icon-bar"></span>        <!--设置导航按钮样式-->
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
            </div>
            <div class="collapse navbar-collapse" id="navbar-collapse">                <!--设置导航折叠区域，设置导航折叠样式-->
                <ul class="nav navbar-nav navbar-right" style="margin-top:0">        <!--设置列表区域，导航列表默认样式，导航列表右浮动-->
                    <li class="active"><a href="#"><span class="glyphicon glyphicon-home"></span> 首页</a></li>    <!--设置当前列表首先-->
                    <li><a href="#"><span class="glyphicon glyphicon-list"></span> 资讯</a></li>                    <!--设置当前列表图标-->
                    <li><a href="#"><span class="glyphicon glyphicon-fire"></span> 案例</a></li>
                    <li><a href="#"><span class="glyphicon glyphicon-question-sign"></span> 关于</a></li>
                </ul>
            </div>
        </div>
    </nav>
[/code]

**css**

[code]

     @charset "utf-8";
    /*导航部分-------------------------------------------------------------------------------------------------------------*/
    /*导航区域背景色*/
    .navbar{
        background-color: #2056AC;
    }
    /*导航a首选标签，聚集光标和鼠标放上去背景色*/
    .navbar-default .navbar-nav > .active > a, .navbar-default .navbar-nav > .active > a:focus, .navbar-default .navbar-nav > .active > a:hover{
        background-color: #FE7C19;
        color: #FFFFFF;
    }
    /*导航a标签，聚集光标和鼠标放上去背景色*/
    .navbar-default .navbar-nav > li > a:focus, .navbar-default .navbar-nav > li > a:hover{
        background-color: #FE7C19;
        color: #FFFFFF;
    }
    /*导航条文字颜色*/
    .navbar-default .navbar-nav > li > a{
        color: #FFFFFF;
    }
    /*导航条按钮背景色*/
    .navbar-toggle, .navbar-default .navbar-toggle:focus, .navbar-default .navbar-toggle:hover{
        background-color: #ddd;
    }
    /*导航条按钮文字三横背景和文字颜色*/
    .navbar-default .navbar-toggle .icon-bar{
        background-color: #f5f5f5;
        border-radius: 1px;
        box-shadow: 0 1px 0 rgba(0, 0, 0, 0.25);
        display: block;
        height: 2px;
        width: 18px;
    }
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170506184510664-2076614412.gif)

