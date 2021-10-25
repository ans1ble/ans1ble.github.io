---
layout: post
title: " 第一百五十五节，封装库--JavaScript，轮播器 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，轮播器**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170227204133001-471785456.png)**



html

[code]

    <div id="banner">
            <img src="img/banner1.jpg" alt="轮播器第一张" />
            <img src="img/banner2.jpg" alt="轮播器第二张" />
            <img src="img/banner3.jpg" alt="轮播器第三张" />
            <ul>
                <li>●</li>
                <li>●</li>
                <li>●</li>
            </ul>
            <span></span>
            <strong></strong>
        </div>
[/code]

css

[code]

    /*轮播图*/
    #banner {
        width:900px;
        height:150px;
        float:left;
        margin:10px 0;
        position:relative;
        overflow: hidden;
    }
    #banner img {
        display:block;
        position:absolute;
        top:0;
        left:0;
        z-index:1
    }
    #banner ul {
        position:absolute;
        top:128px;
        left:420px;
        z-index:4;
    }
    #banner ul li {
        float:left;
        padding:0 5px;
        font-size:16px;
        color:#999;
        cursor:pointer;
    }
    #banner span {
        width:900px;
        height:25px;
        position:absolute;
        top:125px;
        left:0;
        background:#333;
        opacity:0.3;
        filter:alpha(opacity=30);
        z-index:3;
    }
    #banner strong {
        position:absolute;
        top:130px;
        left:10px;
        color:#fff;
        z-index:4;
    }
[/code]

前台js

[code]

    //轮播器初始化
        $('#banner img').shzh_tou_ming_du(0);                                     //将全部图片透明度设置成0
        $('#banner img').guo_lv_jie_dian(0).shzh_tou_ming_du(100);                //将第一张图片透明度设置成100
        $('#banner ul li').guo_lv_jie_dian(0).c_css('color','#333');              //将第一个li改变成选择颜色
        $('#banner strong').wen_ben($('#banner img').guo_lv_jie_dian(0).qh_shu_xing_zhi('alt'));  //将第一张图片的alt属性值赋值给strong
    
        //轮播器计数器
        var banner_index = 1;
    
        //轮播器的种类
        var banner_type = 1;               //1表示透明度轮播器，2表示上下滚动轮播器
    
        //自动轮播器
        var banner_timer = setInterval(befang_fn, 3000);                      //创建定时器
    
        //手动轮播器
        $('#banner ul li').shu_biao_yi_ru_yi_chu(function () {                //鼠标移入移出事件
            clearInterval(banner_timer);                                      //清除定时器
            if ($(this).c_css('color') != 'rgb(51, 51, 51)' && $(this).c_css('color') != '#333'){
                befang(this,banner_index == 0 ? $('#banner ul li').jd_length() -1 : banner_index -1);
            }
        },function () {
            banner_index = $(this).hq_suo_yin() + 1;
            banner_timer = setInterval(befang_fn, 3000);
        });
    
        function befang(obj,prev) {
    
    
            $('#banner ul li').c_css('color', '#999');                //将全部li改变成初始颜色
            $(obj).c_css('color', '#333');         //根据索引改变对应的li颜色
            $('#banner strong').wen_ben($('#banner img').guo_lv_jie_dian($(obj).hq_suo_yin()).qh_shu_xing_zhi('alt'));  //将对应图片的alt属性值赋值给strong
    
            if (banner_type == 1) {
                $('#banner img').guo_lv_jie_dian(prev).yi_dong_tou_ming({
                    attr: 'o',
                    target: 0,
                    t: 100,
                    step: 2
                }).c_css('z-index', 1);
    
                $('#banner img').guo_lv_jie_dian($(obj).hq_suo_yin()).yi_dong_tou_ming({
                    attr: 'o',
                    target: 100,
                    t: 100,
                    step: 2
                }).c_css('z-index', 2);
            }else if(banner_type == 2){
                $('#banner img').guo_lv_jie_dian(prev).yi_dong_tou_ming({
                    attr: 'y',
                    target: 150,
                    t: 100,
                    step: 2
                }).c_css('z-index', 1).shzh_tou_ming_du(100);
    
                $('#banner img').guo_lv_jie_dian($(obj).hq_suo_yin()).yi_dong_tou_ming({
                    attr: 'y',
                    target: 0,
                    t: 100,
                    step: 2
                }).c_css('top','-150px').c_css('z-index', 2).shzh_tou_ming_du(100);
            }
        }
    
        function befang_fn() {
            if (banner_index >= $('#banner ul li').jd_length()) banner_index = 0;   //计数器数值大于等于轮播图总量是，计数器为0
            befang($('#banner ul li').guo_lv_jie_dian(banner_index).sh_jd(),banner_index == 0 ? $('#banner ul li').jd_length() -1 : banner_index -1);
            banner_index ++;
        }
[/code]

 首先引入封装库

