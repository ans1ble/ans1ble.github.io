
---
layout: post
title: " 第二百五十五节，Bootstrap项目实战--关于 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Bootstrap项目实战--关于**

**html**

[code]

     <!DOCTYPE html>
    <html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1, user-scalable=no">
        <title>Bootstrap 介绍</title>
        <!--引入bootstrap样式文件-->
        <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
        <link rel="stylesheet" href="css/ceshi.css">
        <link rel="stylesheet" href="css/gyu.css">
    </head>
    <body>
    <!--导航-->
    <nav class="navbar navbar-default navbar-fixed-top">                <!--声明导航区域，设置导航默认样式，设置导航条固定在顶部-->
        <div class="container">                                            <!--设置固定布局，最大宽度1140-->
            <div class="navbar-header">                                    <!--设置导航标题区域-->
                <a href="#" class="navbar-brand logo">自贡瑞佳财务咨询有限公司</a>    <!--设置导航标内容-->
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#navbar-collapse">    <!--设置导航按钮-->
                    <span class="icon-bar"></span>        <!--设置导航按钮样式-->
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
            </div>
            <div class="collapse navbar-collapse" id="navbar-collapse">                <!--设置导航折叠区域，设置导航折叠样式-->
                <ul class="nav navbar-nav navbar-right dhul">        <!--设置列表区域，导航列表默认样式，导航列表右浮动-->
                    <li class="active"><a href="ceshi.html"><span class="glyphicon glyphicon-home"></span> 首页</a></li>    <!--设置当前列表首先-->
                    <li><a href="zix.html"><span class="glyphicon glyphicon-list"></span> 资讯</a></li>                    <!--设置当前列表图标-->
                    <li><a href="anl.html"><span class="glyphicon glyphicon-fire"></span> 案例</a></li>
                    <li><a href="gyu.html"><span class="glyphicon glyphicon-question-sign"></span> 关于</a></li>
                </ul>
            </div>
        </div>
    </nav>
    <!--轮播图-->
    <div id="myCarousel" class="carousel slide">                        <!--设置轮播器区域样式，设置轮播器滚动样式-->
        <ol class="carousel-indicators">                                <!--设置轮播器列表区域样式，就是小圆点区域样式-->
            <li data-target="#myCarousel" data-slide-to="0" class="active"></li>    <!--设置当前列表首选-->
            <li data-target="#myCarousel" data-slide-to="1"></li>
            <li data-target="#myCarousel" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">                                    <!--设置轮播器图片区域-->
            <div class="item active tp1">                                <!--设置轮播器图片样式-->
                <a href="#"><img src="img/1.jpg" alt="第一张"></a>
            </div>
            <div class="item tp2">
                <a href="#"><img src="img/2.jpg" alt="第二张"></a>
            </div>
            <div class="item tp3">
                <a href="#"><img src="img/3.jpg" alt="第三张"></a>
            </div>
        </div>
        <!--设置轮播器箭头区域-->
        <a href="#myCarousel" data-slide="prev" class="carousel-control left">
            <span class="glyphicon glyphicon-chevron-left"></span>
        </a>
        <a href="#myCarousel" data-slide="next" class="carousel-control right">
            <span class="glyphicon glyphicon-chevron-right"></span>
        </a>
    </div>
    
    <!--左右两栏即可-->
    <div id="about">
        <div class="container">
            <div class="row">
                <div class="col-md-3 hidden-sm hidden-xs">
                    <div class="list-group">
                        <a class="list-group-item" href="#1">1.机构介绍</a>
                        <a class="list-group-item" href="#2">2.加入我们</a>
                        <a class="list-group-item" href="#3">3.联系方式</a>
                    </div>
                </div>
                <div class="col-md-9 about">
                    <a name="1"></a>
                    <h3>机构简介</h3>
                    <p>瓢城企业培训有限公司是一家专业以智能化弱电工程为主的高科技民营企业，公司自创立以来一直专业致力于智能化弱电工程；始终坚持发扬"诚信、创新、沟通"为企业宗旨，以"技术、服务"为立业之本的团体精神，并形成一套完整的设计、安装、调试、培训、维护一站式服务体系。</p>
                    <a name="2"></a>
                    <h3>加入我们</h3>
                    <p>网络已深刻改变着人们的生活，本地化生活服务市场前景巨大，生活半径团队坚信本地化生活服务与互联网的结合将会成就一家梦幻的公司，我们脚踏实地的相信梦想，我们相信你的加入会让生活半径更可能成为那家梦幻公司！生活半径人有梦想，有魄力，强执行力，但是要实现这个伟大的梦想，需要更多的有创业精神的你一路前行。公司将提供有竞争力的薪酬、完善的福利（五险一金）、期权、广阔的上升空间。只要你有能力、有激情、有梦想，愿意付出，愿意与公司共同成长，请加入我们！</p>
                    <p>请发送您的简历到：hr@xxx.com，我们会在第一时间联系您！</p>
                    <a name="3"></a>
                    <h3>联系方式</h3>
                    <p>地址：江苏省盐城市亭湖区大庆中路1234 号</p>
                    <p>邮编：1234567</p>
                    <p>电话：010-88888888</p>
                    <p>传真：010-88666666</p>
                </div>
            </div>
        </div>
    </div>
    
    
    
        <!--底部-->
    <div class="dibu">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <h4 class="text-center">联系方式</h4>
                    <p>联系人:游先生</p>
                    <p>手机:18681395066     13096006150</p>
                    <p>座机:0813-8287339</p>
                    <p>Q Q:350016919</p>
                    <p>邮箱:350016919@qq.com</p>
                    <p>地址:自贡市自流井区丹桂东段泰丰大厦1区8层7号 </p>
                </div>
                <div class="col-md-6">
                    <h4 class="text-center">友情链接</h4>
                    <ul class="list-unstyled">
                        <li><a href="http://www.scaic.gov.cn/" target="_blank">四川工商局</a></li>
                        <li><a href="http://www.baidu.com" target="_blank">百度</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
    <div class="banq">
        <div class="container text-center banq">
            <p>版权所有 © 自贡瑞佳财务咨询有限公司 未经许可 严禁复制</p>
            <p><a href="http://www.jxiou.com/" target="_blank">自贡玉秀文化传播技术支持</a></p>
            <p>蜀ICP备16022718号-1 </p>
        </div>
    </div>
    
    <!--引入jquery文件-->
    <script src="jquery/jquery.min.js"></script>
    <!--引入bootstrap里的js-->
    <script src="bootstrap/js/bootstrap.min.js"></script>
    <script src="ceshi.js"></script>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170509212013894-1501293560.png)

**重点：栅格系统布局**

