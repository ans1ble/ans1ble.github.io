---
layout: post
title: " 第二百五十二节，Bootstrap项目实战-首页 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap项目实战-首页**

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
                    <li class="active"><a href="#"><span class="glyphicon glyphicon-home"></span> 首页</a></li>    <!--设置当前列表首先-->
                    <li><a href="#"><span class="glyphicon glyphicon-list"></span> 资讯</a></li>                    <!--设置当前列表图标-->
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
    <!--内容1-->
    <div class="tab1">
        <div class="container">
            <h2 class="tab-h2">「 为什么选择瑞佳商务 」</h2>
            <p class="tab-p">20年经验，专人专办，上面服务，后续记账业务多！</p>
            <div class="row">
                <div class="col-md-6 col">
                    <div class="media">
                        <div class="media-left media-top">
                            <a href="#">
                                <img class="media-object" src="img/zhzhao.png" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            <h4 class="media-heading">代办证照</h4>
                            <p>工商代办、工商注册、执照代办、公司注册、资质代理、年检等 ！</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col">
                    <div class="media">
                        <div class="media-left media-top">
                            <a href="#">
                                <img class="media-object" src="img/shb.png" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            <h4 class="media-heading">商标注册</h4>
                            <p>代理注册各种商标！</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col">
                    <div class="media">
                        <div class="media-left media-top">
                            <a href="#">
                                <img class="media-object" src="img/jzhshw.png" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            <h4 class="media-heading">记账税务</h4>
                            <p>代理公司账务，税务申报！</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col">
                    <div class="media">
                        <div class="media-left media-top">
                            <a href="#">
                                <img class="media-object" src="img/qt.png" alt="...">
                            </a>
                        </div>
                        <div class="media-body">
                            <h4 class="media-heading">其他业务</h4>
                            <p>其他各种业务！</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!--两段内容-->
    <div class="tab2">
        <div class="container">
            <div class="row">
                <div class="col-md-6 col-sm-6 tab2-img">
                    <img src="img/tab2.png" alt="" class="auto img-responsive center-block">
                </div>
                <div class="text col-md-6 col-sm-6 tab2-text">
                    <h3>强大的学习体系</h3>
                    <p>经过管理学大师层层把关、让您的企业突飞猛进。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="tab3">
        <div class="container">
            <div class="row">
                <div class="col-md-6 col-sm-6">
                    <img src="img/tab3.png" alt="" class="auto img-responsive center-block">
                </div>
                <div class="text col-md-6 col-sm-6">
                    <h3>完美的管理方式</h3>
                    <p>最新的管理培训方案，让您的企业赶超同行。</p>
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
    </html
[/code]

**css**

[code]

     @charset "utf-8";
    /*通用----------------------------------------------------------------------------------------------------------------*/
    /*将a标签去掉点击后的虚线边框*/
    body {
        font-family: "Helvetica Neue", Helvetica, Arial, "Microsoft Yahei UI", "Microsoft YaHei", SimHei, "\5B8B\4F53", simsun, sans-serif;
    }
    a:focus {
        outline: none;
    }
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
    /*网站名称*/
    .navbar-default .navbar-brand:focus, .navbar-default .navbar-brand:hover, .navbar-default .navbar-brand {
        color: #FFFFFF;
        font-size:15px;
    }
    /*去除导航ul头部内边距*/
    .dhul{
        margin-top:0;
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
    
    /*轮播器--------------------------------------------------------------------------------------------------------------*/
    /*将轮播器头部外边距设置50像素*/
    #myCarousel {
        margin: 50px 0 0 0;
    }
    .carousel-inner .item img {
        margin: 0 auto;
    }
    .tp1{
        background:#D6E5EA;
    }
    .tp2{
        background:#F4F3F1;
    }
    .tp3{
        background:#E2E1E7;
    }
    
    /*经营业务-------------------------------------------------------------------------------------------------------------*/
    .tab-h2 {
        font-size: 20px;
        color: #0059B2;
        text-align: center;
        letter-spacing: 1px;
    }
    
    .tab-p {
        font-size: 15px;
        color: #999;
        text-align: center;
        letter-spacing: 1px;
        margin: 20px 0 40px 0;
    }
    
    .tab1 {
        margin: 30px 0;
        color: #666;
    }
    
    .tab1 .media-heading {
        margin: 5px 0 20px 0;
    }
    
    .tab1 .text-muted {
        color: #999;
        text-decoration: line-through;
    }
    
    .tab1 .media-heading {
        margin: 5px 0 20px 0;
    }
    
    .tab1 .text-muted {
        color: #999;
        text-decoration: line-through;
    }
    
    .tab1 .col {
        padding: 20px;
    }
    .media {
        box-shadow: 0 1px 0 rgba(0, 0, 0, 0.25);
    }
    /*两段内容部分*/
    .tab2 {
        background: #eee;
        padding: 60px 20px;
        text-align: center;
    }
    
    .tab2 img {
        width: 40%;
        height: 40%;
    }
    
    .tab3 {
        padding: 40px 0;
        text-align: center;
    }
    
    .tab3 img {
        width: 65%;
        height: 65%;
    }
    
    .text h3 {
        font-size: 20px;
    }
    
    .text p {
        font-size: 14px;
    }
    
    /*底部-----------------------------------------------------------------------------------------------------------------*/
    .dibu{
        background-color:#222222;
    }
    .dibu .row{
        color: #FFFFFF;
    }
    .dibu .row h4{
        box-shadow: 0 1px 0 rgba(255, 255, 255, 0.97);
        padding:10px 0;
    }
    /*版权*/
    .banq{
        background-color: #000000;
    }
    .banq .banq{
        padding: 10px 0 0 0;
    }
    .banq p{
        color: #777777;
    }
    
    /* 小屏幕（平板，大于等于 768px） */
    @media (min-width: 768px) {
        /*网站名称*/
        .navbar-default .navbar-brand:focus, .navbar-default .navbar-brand:hover, .navbar-default .navbar-brand {
            color: #FFFFFF;
            font-size: 20px;
        }
        .tab-h2 {
            font-size: 26px;
        }
    
        .tab-p {
            font-size: 16px;
        }
    }
    
    /* 中等屏幕（桌面显示器，大于等于 992px） */
    @media (min-width: 992px) {
        /*网站名称*/
        .navbar-default .navbar-brand:focus, .navbar-default .navbar-brand:hover, .navbar-default .navbar-brand {
            color: #FFFFFF;
            font-size: 23px;
        }
        .tab-h2 {
            font-size: 28px;
        }
    
        .tab-p {
            font-size: 17px;
        }
    }
    
    /* 大屏幕（大桌面显示器，大于等于 1200px） */
    @media (min-width: 1200px) {
        .tab-h2 {
            font-size: 30px;
        }
    
        .tab-p {
            font-size: 18px;
        }
    }
[/code]

**js**

[code]

     /**
     * Created by admin on 2017/5/2.
     */
    $(function () {
        $('#myCarousel').carousel({
            //设置自动播放/3 秒
            interval: 3000,
        });
    });
[/code]



**总结：主要用到，导航条组件，轮播器组件，栅格系统，和媒体对象组件**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170509110437691-905696783.png)**



