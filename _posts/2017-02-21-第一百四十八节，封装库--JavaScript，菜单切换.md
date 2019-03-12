---
layout: post
title: " 第一百四十八节，封装库--JavaScript，菜单切换 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第一百四十八节，封装库--JavaScript，菜单切换**



**首先在封装库封装点击切换方法**



[code]

    /** dian_ji_qie_huan()方法，设置点击切换，将元素设置成点击切换，也就是点击目标元素后，循环执行方法里的函数
     * 参数是点击后要执行的函数，可以是多个函数，点击一次循环执行一个函数，从第一个开始，循环完毕后再次循环从第一个开始
     **/
    feng_zhuang_ku.prototype.dian_ji_qie_huan = function () {
        for (var i = 0; i < this.jie_dian.length; i++) {
            (function (jiedian, args) {
                var count = 0;                                          //计数器
                addEvent(jiedian, 'click', function () {                //给对象添加点击事件
                    args[count++ % args.length].call(this);             //点击后计数器数值求于作为下标执行传入的函数，计数器在累加,将对象传入
                });
            })(this.jie_dian[i], arguments);                            //通过arguments接收传入方法的函数
        }
        return this;
    };
[/code]





**菜单切换效果图**

![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170221203446163-1197715460.png)

html

[code]

    <div id="sidebar">
            <h2>教育博文1</h2>
            <ul>
                <li><a href="###">靠自己95 后女生被16 所国外名校录取</a></li>
                <li><a href="###">00 后的成长烦恼：压力巨大成隐形杀手</a></li>
                <li><a href="###">一年自学MIT 的33 门课? 疯狂学习方法</a></li>
                <li><a href="###">申请赴美读研人数下降5% 7 年来首遇冷</a></li>
                <li><a href="###">西政“萌招聘”秀出辣椒与美女被赞</a></li>
            </ul>
            <h2>教育博文2</h2>
            <ul>
                <li><a href="###">靠自己95 后女生被16 所国外名校录取</a></li>
                <li><a href="###">00 后的成长烦恼：压力巨大成隐形杀手</a></li>
                <li><a href="###">一年自学MIT 的33 门课? 疯狂学习方法</a></li>
                <li><a href="###">申请赴美读研人数下降5% 7 年来首遇冷</a></li>
                <li><a href="###">西政“萌招聘”秀出辣椒与美女被赞</a></li>
            </ul>
            <h2>教育博文3</h2>
            <ul>
                <li><a href="###">靠自己95 后女生被16 所国外名校录取</a></li>
                <li><a href="###">00 后的成长烦恼：压力巨大成隐形杀手</a></li>
                <li><a href="###">一年自学MIT 的33 门课? 疯狂学习方法</a></li>
                <li><a href="###">申请赴美读研人数下降5% 7 年来首遇冷</a></li>
                <li><a href="###">西政“萌招聘”秀出辣椒与美女被赞</a></li>
            </ul>
        </div>
[/code]

css

[code]

    /*左边列表*/
    #sidebar {
        width:250px;
        height:500px;
        float:left;
    }
    #sidebar h2 {
        width:248px;
        height:30px;
        line-height:30px;
        font-size:14px;
        background:url(img/side_h.png);
        text-indent:10px;
        border:1px solid #ccc;
        border-bottom:none;
        margin:0;
    }
    #sidebar ul {
        height:150px;
        border:1px solid #ccc;
        margin:0 0 10px 0;
        overflow:hidden;
        opacity:1;
        filter:alpha(opacity=100);
    }
    #sidebar ul li {
        height:30px;
        line-height:30px;
        background:url(img/arrow4.gif) no-repeat 12px 45%;
        text-indent:30px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
    #sidebar ul li a {
        text-decoration:none;
        color:#333;
    }
[/code]

前台js

[code]

    // 左侧列表
        $('#sidebar h2').dian_ji_qie_huan(function () {
            $(this).xia_jd().yi_dong_tou_ming({
                t : 50,
                step : 10,
                mul:{
                    h:0,
                    o:0
                }
            });
        },function () {
            $(this).xia_jd().yi_dong_tou_ming({
                t : 50,
                step : 10,
                mul:{
                    h:150,
                    o:100
                }
            });
        })
[/code]

首先引入封装库



