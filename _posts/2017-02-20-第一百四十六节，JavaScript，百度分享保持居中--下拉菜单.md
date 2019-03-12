
---
layout: post
title: " 第一百四十六节，JavaScript，百度分享保持居中--下拉菜单 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，百度分享保持居中--下拉菜单**



****百度分享保持居中****

****效果图****

****![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170220164926679-1274119717.png)****



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
        //获取百度分享区块让它垂直居中，滚动条头部位置加浏览器窗口高度，减去百度分享高度除以2，等于居中位置
        $('#share').c_css('top',gun_dong_tiao_wei_zhi().top + (getInner().height - yuan_su_da_xiao($('#share').jie_dian[0]).height) / 2 + 'px');
    
        addEvent(window,'scroll',function () {   //滚动条事件，当拖动滚动条时执行居中
            $('#share').yi_dong_tou_ming({
                'attr': 'y',  //动画方式
                'target': gun_dong_tiao_wei_zhi().top + (getInner().height - yuan_su_da_xiao($('#share').jie_dian[0]).height) / 2,  //目标量
                't': 50,      //每次动画时间
                'step':20     //跨度
            });
        });
    
        $('#share').chuang_kou_shi_jian(function () {     //窗口变化事件，当拖窗口变化时执行居中
            $('#share').yi_dong_tou_ming({
                'attr': 'y',  //动画方式
                'target': gun_dong_tiao_wei_zhi().top + (getInner().height - yuan_su_da_xiao($('#share').jie_dian[0]).height) / 2,  //目标量
                't': 50,      //每次动画时间
                'step':20     //跨度
            });
        });
        $('#share').shu_biao_yi_ru_yi_chu(function () {  //鼠标移入移出事件
            $(this).yi_dong_tou_ming({
                'attr': 'x',  //动画方式
                'target': 0   //目标量
            });
        },function () {
            $(this).yi_dong_tou_ming({
                'attr': 'x',     //动画方式
                'target': -211   //目标量
            });
        });
[/code]





**下拉菜单**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170220165350163-1418604025.png)**



html

[code]

    <div class="ge_ren_zhong_xin">个人中心
            <ul class="xg">
                <li><a href="#">设置</a></li>
                <li><a href="#">换肤</a></li>
                <li><a href="#">帮助</a></li>
                <li><a href="#">退出</a></li>
            </ul>
        </div>
[/code]



css

[code]

    .ge_ren_zhong_xin{
        position: relative;
        width: 70px;
        height: 30px;
        line-height: 30px;
        float: right;
        background: url("img/arrow.png") no-repeat right center;
        cursor: pointer;
    }
    .ge_ren_zhong_xin ul{
        width: 100px;
        height: 0;
        position: absolute;
        top:30px;
        right: -15px;
        background:#FBF7E1;
        border:1px solid #999;
        border-top:none;
        padding:10px 0 0 0;
        filter:alpha(opacity=0);
        opacity:0;
        display:none;
        overflow:hidden;
    }
    .ge_ren_zhong_xin ul li {
        height:25px;
        line-height:25px;
        text-indent:20px;
        letter-spacing:1px;
    }
    .ge_ren_zhong_xin ul li a {
        display:block;
        text-decoration:none;
        color:#333;
        background:url("img/arrow3.gif") no-repeat 5px 45%;
    }
    .ge_ren_zhong_xin ul li a:hover {
        background:#fc0 url("img/arrow4.gif") no-repeat 5px 45%;
    }
[/code]

前台js

[code]

    // 个人中心
        $('#tou .ge_ren_zhong_xin').shu_biao_yi_ru_yi_chu(function () {
            $(this).c_css('background','url("img/arrow2.png") no-repeat right center');
            $('#tou .xg').xian_shi().yi_dong_tou_ming({
                't': 50,           //每次动画时间
                'step': 20,        //跨度
                mul:{
                    'h':110,
                    'o':100
                }
            });
        },function () {
            $(this).c_css('background','url("img/arrow.png") no-repeat right center');
            $('#tou .xg').xian_shi().yi_dong_tou_ming({
                't': 50,           //每次动画时间
                'step': 20,        //跨度
                mul:{
                    'h':0,
                    'o':0
                },
                fn:function () {
                    $('#tou .xg').yin_cang();
                }
            });
        });
[/code]



先必须引入函数库和封装库



