
---
layout: post
title: " 第二百五十三节，Bootstrap项目实战-资讯 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Bootstrap项目实战-资讯**

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
        <link rel="stylesheet" href="css/zix.css">
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
                    <li><a href="#"><span class="glyphicon glyphicon-fire"></span> 案例</a></li>
                    <li><a href="#"><span class="glyphicon glyphicon-question-sign"></span> 关于</a></li>
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
    
    <!--资讯内容-->
    <div id="information">
        <div class="container">
            <div class="row">
                <div class="col-md-8 info-left">
                    <div class="container-fluid" style="padding:0;">
                        <div class="row info-content">
                            <div class="col-md-5 col-sm-5 col-xs-5">
                                <img src="img/info1.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7">
                                <h4>广电总局发布 TVOS2.0 华为阿里参与研发</h4>
                                <p class="hidden-xs">TVOS2.0 是在 TVOS1.0 与华
                                    为 MediaOS 及阿里巴巴 YunOS 融合的基础上，打造的新一代智能电视操作系统。华为主要
                                    承担开发工作，内置的电视购物商城由阿里方面负责。</p>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                        <div class="row info-content">
                            <div class="col-md-5 col-sm-5 col-xs-5">
                                <img src="img/info1.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7">
                                <h4>广电总局发布 TVOS2.0 华为阿里参与研发</h4>
                                <p class="hidden-xs">TVOS2.0 是在 TVOS1.0 与华
                                    为 MediaOS 及阿里巴巴 YunOS 融合的基础上，打造的新一代智能电视操作系统。华为主要
                                    承担开发工作，内置的电视购物商城由阿里方面负责。</p>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                        <div class="row info-content">
                            <div class="col-md-5 col-sm-5 col-xs-5">
                                <img src="img/info1.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7">
                                <h4>广电总局发布 TVOS2.0 华为阿里参与研发</h4>
                                <p class="hidden-xs">TVOS2.0 是在 TVOS1.0 与华
                                    为 MediaOS 及阿里巴巴 YunOS 融合的基础上，打造的新一代智能电视操作系统。华为主要
                                    承担开发工作，内置的电视购物商城由阿里方面负责。</p>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                        <div class="row info-content">
                            <div class="col-md-5 col-sm-5 col-xs-5">
                                <img src="img/info1.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7">
                                <h4>广电总局发布 TVOS2.0 华为阿里参与研发</h4>
                                <p class="hidden-xs">TVOS2.0 是在 TVOS1.0 与华
                                    为 MediaOS 及阿里巴巴 YunOS 融合的基础上，打造的新一代智能电视操作系统。华为主要
                                    承担开发工作，内置的电视购物商城由阿里方面负责。</p>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                        <div class="row info-content">
                            <div class="col-md-5 col-sm-5 col-xs-5">
                                <img src="img/info1.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7">
                                <h4>广电总局发布 TVOS2.0 华为阿里参与研发</h4>
                                <p class="hidden-xs">TVOS2.0 是在 TVOS1.0 与华
                                    为 MediaOS 及阿里巴巴 YunOS 融合的基础上，打造的新一代智能电视操作系统。华为主要
                                    承担开发工作，内置的电视购物商城由阿里方面负责。</p>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                    </div>
                </div>
    
    
                <div class="col-md-4 info-right hidden-xs hidden-sm">
                    <blockquote>
                        <h2>热门资讯</h2>
                    </blockquote>
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-5 col-sm-5 col-xs-5"
                                 style="margin:12px 0;padding:0;">
                                <img src="img/info3.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7"
                                 style="padding-right:0">
                                <h4>标题</h4>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                         <div class="row">
                            <div class="col-md-5 col-sm-5 col-xs-5"
                                 style="margin:12px 0;padding:0;">
                                <img src="img/info3.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7"
                                 style="padding-right:0">
                                <h4>标题</h4>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
                         <div class="row">
                            <div class="col-md-5 col-sm-5 col-xs-5"
                                 style="margin:12px 0;padding:0;">
                                <img src="img/info3.jpg" class="img-responsive" alt="">
                            </div>
                            <div class="col-md-7 col-sm-7 col-xs-7"
                                 style="padding-right:0">
                                <h4>标题</h4>
                                <p>admin 15 / 10 / 11</p>
                            </div>
                        </div>
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

**css**

[code]

     @charset "utf-8";
    /*资讯内容 CSS*/
    #information {
        padding: 40px 0;
        background: #eee;
    }
    
    .info-right {
        background-color: #fff;
        box-shadow: 2px 2px 3px #ccc;
    }
    
    .info-right blockquote {
        padding: 0;
        margin: 0;
    }
    
    .info-right h2 {
        font-size: 20px;
        padding: 5px;
    }
    
    .info-right h4 {
        line-height: 1.6;
    }
    
    .info-content {
        background-color: #fff;
        box-shadow: 2px 2px 3px #ccc;
        margin: 0 0 20px 0;
    }
    
    .info-content img {
        margin: 12px 0;
    }
    
    .info-content h4 {
        font-size: 14px;
        padding: 2px 0 0 0;
    }
    
    .info-content p {
        line-height: 1.6;
        color: #666;
    }
    
    /*对于.info-content h4，在中屏和大屏需要保持一行。*/
    .info-content h4 {
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }
    blockquote{
        border-left:5px solid #0f68ee;
    }
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170509204034379-1995354383.png)**

**重点：用栅格系统布局**

