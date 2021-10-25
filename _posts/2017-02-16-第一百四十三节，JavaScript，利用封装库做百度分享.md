---
layout: post
title: " 第一百四十三节，JavaScript，利用封装库做百度分享 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，利用封装库做百度分享**

效果图

![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170216163507004-476903344.png)

html代码

[code]

    <div id="share">
        <h2>分享到</h2>
        <ul>
            <li><a href="###" class="a">一键分享</a></li>
            <li><a href="###" class="b">新浪微博</a></li>
            <li><a href="###" class="c">人人网</a></li>
            <li><a href="###" class="d">百度相册</a></li>
            <li><a href="###" class="e">腾讯朋友</a></li>
            <li><a href="###" class="f">豆瓣网</a></li>
            <li><a href="###" class="g">百度首页</a></li>
            <li><a href="###" class="h">和讯微博</a></li>
            <li><a href="###" class="i">QQ 空间</a></li>
            <li><a href="###" class="j">百度搜藏</a></li>
            <li><a href="###" class="k">腾讯微博</a></li>
            <li><a href="###" class="l">开心网</a></li>
            <li><a href="###" class="m">百度贴吧</a></li>
            <li><a href="###" class="n">搜狐微博</a></li>
            <li><a href="###" class="o">QQ 好友</a></li>
            <li><a href="###" class="p">更多...</a></li>
        </ul>
        <div class="share_footer"><a href="###">百度分享</a><span></span></div>
    </div>
[/code]

css代码

[code]

    /*百度分享*/
    #share {
        width:210px;
        height:315px;
        border:1px solid #ccc;
        position:absolute;
        top: 0;
        left:-211px;
        background:#fff;
    }
    #share h2 {
        height:30px;
        line-height:30px;
        background:#eee;
        padding:0;
        margin:0;
        font-size:14px;
        color:#666;
        text-indent:10px;
    }
    #share ul {
        height:254px;
        padding:3px 0 2px 5px;
    }
    #share ul li {
        width:96px;
        height:28px;
        float:left;
        padding:2px;
    }
    #share ul li a {
        display:block;
        width:95px;
        height:26px;
        line-height:26px;
        text-decoration:none;
        color:#666;
        background-image:url('img/share_bg.png');
        background-repeat:no-repeat;
        text-indent:30px;
    }
    #share ul li a.a {
        background-position:5px 4px;
    }
    #share ul li a.b {
        background-position:5px -26px;
    }
    #share ul li a.c {
        background-position:5px -56px;
    }
    #share ul li a.d {
        background-position:5px -86px;
    }
    #share ul li a.e {
        background-position:5px -116px;
    }
    #share ul li a.f {
        background-position:5px -146px;
    }
    #share ul li a.g {
        background-position:5px -176px;
    }
    #share ul li a.h {
        background-position:5px -206px;
    }
    #share ul li a.i {
        background-position:5px -236px;
    }
    #share ul li a.j {
        background-position:5px -266px;
    }
    #share ul li a.k {
        background-position:5px -296px;
    }
    #share ul li a.l {
        background-position:5px -326px;
    }
    #share ul li a.n {
        background-position:5px -356px;
    }
    #share ul li a.m {
        background-position:5px -386px;
    }
    #share ul li a.o {
        background-position:5px -416px;
    }
    #share ul li a.p {
        background-position:5px -446px;
    }
    #share ul li a:hover {
        opacity:0.7;
        filter:alpha(opacity=70);
        background-color:#eee;
        color:#06f;
    }
    #share .share_footer {
        height:26px;
        background:#eee;
        position:relative;
    }
    #share .share_footer a {
        position:absolute;
        top:7px;
        left:140px;
        padding:0 0 0 13px;
        background:#eee url('img/share_bg.png') no-repeat 0 -477px;
        text-decoration:none;
        color:#666;
    }
    #share .share_footer a:hover {
        color:#06f;
        opacity:0.7;
        filter:alpha(opacity=70);
    }
    #share .share_footer span {
        display:block;
        width:24px;
        height:88px;
        position:absolute;
        top:-178px;
        left:210px;
        background:url('img/share.png') no-repeat;
        cursor:pointer;
    }
[/code]

前台js代码

[code]

    // 百度分享
        $('#share').c_css('top',(getInner().height - yuan_su_da_xiao($('#share').jie_dian[0]).height) / 2 + 'px');
        $('#share').chuang_kou_shi_jian(function () {
            $('#share').c_css('top',(getInner().height - yuan_su_da_xiao($('#share').jie_dian[0]).height) / 2 + 'px');
        });
        $('#share').shu_biao_yi_ru_yi_chu(function () {
            $(this).yi_dong_tou_ming({
                'attr': 'x',  //动画模式
                'target': 0   //目标量
            });
        },function () {
            $(this).yi_dong_tou_ming({
                'attr': 'x',     //动画模式
                'target': -211   //目标量
            });
        });
[/code]

首先要引入函数库和封装库

