
---
layout: post
title: " 第二百五十四节，Bootstrap项目实战--案例 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Bootstrap项目实战--案例**

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
        <link rel="stylesheet" href="css/anl.css">
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
    
    
    <!--案例-->
    <div id="case">
        <div class="container">
            <div class="row">
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case1.jpg" alt="">
                        <div class="caption">
                            <h4>中国移动通信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case2.jpg" alt="">
                        <div class="caption">
                            <h4>中国石化</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case3.jpg" alt="">
                        <div class="caption">
                            <h4>中国联通</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case4.jpg" alt="">
                        <div class="caption">
                            <h4>中国电信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case3.jpg" alt="">
                        <div class="caption">
                            <h4>中国联通</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case4.jpg" alt="">
                        <div class="caption">
                            <h4>中国电信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case2.jpg" alt="">
                        <div class="caption">
                            <h4>中国石化</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case1.jpg" alt="">
                        <div class="caption">
                            <h4>中国移动通信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case4.jpg" alt="">
                        <div class="caption">
                            <h4>中国电信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case3.jpg" alt="">
                        <div class="caption">
                            <h4>中国联通</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case4.jpg" alt="">
                        <div class="caption">
                            <h4>中国电信</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">
                    <div class="thumbnail">
                        <img src="img/case2.jpg" alt="">
                        <div class="caption">
                            <h4>中国石化</h4>
                            <p>参与了本机构的总裁管理培训课程，学员反馈意见良好。</p>
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

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170509211747910-1434509916.png)**



**重点：利用栅格系统布局**

