---
layout: post
title: " 第一百五十七节，封装库--JavaScript，预加载图片 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，预加载图片**

**首先了解一个 Image对象，为图片对象**

****Image对象****

**var temp_img = new Image();   //创建一个临时区域的图片对象**  
 **alert(temp_img);                        //[object HTMLImageElement]对象**



******Image对象src属性,属性值是src地址，这个src地址会在后台加载到本地缓存******

********var temp_img = new Image();   //创建一个临时区域的图片对象**  
 **temp_img.src =
'http://www.wallcoo.com/animal/Dogs_Summer_and_Winter/wallpapers/1920x1200/DogsB10_Lucy.jpg';  
********



************Image对象，事件************

**onload //事件，当图片加载成功时触发事件函数**  
 **onerror //事件，当图片加载失败时触发事件函数**



**如：下列  **

[code]

    var temp_img = new Image();            //创建一个临时区域的图片对象
        temp_img.onload = function () {
            alert('图片加载成功，显示图片');
        };
        temp_img.onerror = function () {
            alert('图片加载失败，什么都不干');
        };
        temp_img.src = 'http://www.wallcoo.com/animal/Dogs_Summer_and_Winter/wallpapers/1920x1200/DogsB10_Lucy.jpg';
        //注意：最好把src，写在事件后面，否则ie不兼容
[/code]



**预加载图片,就是当用户查看当前图片时，提前将上一张和下一张图片加载好，当用户查看上一张或者下一张是不用等待加载，**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170302162722173-2113930237.png)**



html

[code]

    <!--预加载-->
        <div id="photo">
            <dl>
                <dt><img xsrc="img/p1.jpg" yjz="img/p1big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>预加载图片</dd>
            </dl>
            <dl>
                <dt><img xsrc="img/p2.jpg" yjz="img/p2big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p3.jpg" yjz="img/p3big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p4.jpg" yjz="img/p4big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p5.jpg" yjz="img/p5big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p6.jpg" yjz="img/p6big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p7.jpg" yjz="img/p7big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p8.jpg" yjz="img/p8big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p9.jpg" yjz="img/p9big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p10.jpg" yjz="img/p10big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p11.jpg" yjz="img/p11big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p12.jpg" yjz="img/p12big.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
        </div>
        <div id="photo_big">
            <h2 class="tuo"><img src="img/close.png" alt="" class="close"/>预加载图片</h2>
            <div class="big">
                <img src="img/loading.gif" alt=""/>
                <strong class="sl">&lt;</strong>
                <strong class="sr">&gt;</strong>
                <span class="left"></span>
                <span class="right"></span>
                <em class="index">22222</em>
            </div>
        </div>
[/code]

css

[code]

    /*预加载图片*/
    #photo_big {
        width:620px;
        height:511px;
        border:1px solid #ccc;
        position:absolute;
        display:none;
        z-index:9999;
        background:#fff;
    }
    #photo_big h2 {
        height:40px;
        line-height:40px;
        text-align:center;
        font-size:14px;
        letter-spacing:1px;
        color:#666;
        background:url(img/login_header.png) repeat-x;
        margin:0;
        padding:0;
        border-bottom:1px solid #ccc;
        /*margin:0 0 20px 0;*/
        cursor:move;
    }
    #photo_big h2 img {
        float:right;
        position:relative;
        top:14px;
        right:8px;
        cursor:pointer;
    }
    #photo_big .big {
        width:620px;
        height:460px;
        padding:10px 0 0 0;
        background-color: #333;
    }
    #photo_big .big img {
        display:block;
        margin:0 auto;
        position:relative;
        top:190px;
    }
    #photo_big .big strong {
        display:block;
        width:100px;
        height:100px;
        line-height:100px;
        text-align:center;
        background:#000;
        opacity:0;
        filter:alpha(opacity=0);
        font-size:60px;
        color:#fff;
        cursor:pointer;
        position:absolute;
        border-radius: 20px;
    }
    #photo_big .big strong.sl {
        top:210px;
        left:20px;
    }
    #photo_big .big strong.sr {
        top:210px;
        right:20px;
    }
    #photo_big .big span {
        display:block;
        width:300px;
        height:450px;
        background:#000;
        opacity:0;
        filter:alpha(opacity=0);
        position:absolute;
        cursor:pointer;
    }
    #photo_big .big span.left {
        top:50px;
        left:10px;
    }
    #photo_big .big span.right {
        top:50px;
        right:10px;
    }
    #photo_big .big em {
        position:absolute;
        top:470px;
        right:20px;
        color:#fff;
        font-size:20px;
        font-style:normal;
    }
[/code]

前台js

[code]

    //预加载图片
        //点击弹窗
        $('.wait_load').on_click(function () {
            $('#suo_ping').xian_shi().zhe_zhao_suo_ping().yi_dong_tou_ming({
                'attr': 'o',  //动画方式
                'target': 50, //目标量
                't': 50,      //每次动画时间
                'step': 5,     //跨度
                fn: function () {
                    $('#suo_ping').chuang_kou_shi_jian(function () {
                        $('#suo_ping').zhe_zhao_suo_ping();
                        $('#photo_big').yuan_su_ju_zhong();
                    })
                }
            });
            $('#photo_big').c_css('display', 'block').yuan_su_ju_zhong().tuo_zhuai('tuo');
    
            var temp_img = new Image();                           //创建临时图片对象
    
            $(temp_img).yuan_su_shi_jian('load',function () {     //当图片加载成功时
                $('#photo_big .big img').hq_shu_xing_zhi('src',temp_img.src).yi_dong_tou_ming({
                    attr:'o',
                    target:100,
                    t:30,
                    step:10
                }).c_css('width','600px').c_css('height','450px').c_css('top',0).shzh_tou_ming_du(0);
            });
            temp_img.src = $(this).hq_shu_xing_zhi('yjz');        //图片加载地址
    
            //图片鼠标划过
            //左边
            $('#photo_big .big .left').shu_biao_yi_ru_yi_chu(function () {
                $('#photo_big .big .sl').yi_dong_tou_ming({
                    attr:'o',
                    target:50,
                    t:30,
                    step:10
                });
            }, function () {
                $('#photo_big .big .sl').yi_dong_tou_ming({
                    attr:'o',
                    target:0,
                    t:30,
                    step:10
                });
            });
            //右边
            $('#photo_big .big .right').shu_biao_yi_ru_yi_chu(function () {
                $('#photo_big .big .sr').yi_dong_tou_ming({
                    attr:'o',
                    target:50,
                    t:30,
                    step:10
                });
            }, function () {
                $('#photo_big .big .sr').yi_dong_tou_ming({
                    attr:'o',
                    target:0,
                    t:30,
                    step:10
                });
            });
    
            //预加载设置
            var children = this.parentNode.parentNode;   //获取当前元素的父节点的父节点，也就是dl
            prev_next(children);
    
            //上一张
            $('#photo_big .big .left').on_click(function () {
                shang_xian(this);
                var children = $('#photo_big dl dt img').hq_jd(sh_jd_suo_yin($('#photo_big .big img').hq_shu_xing_zhi('suoy'), $('#photo').sh_jd())).parentNode.parentNode;
                prev_next(children);
            });
    
            //下一张
            $('#photo_big .big .right').on_click(function () {
                shang_xian(this);
                var children = $('#photo_big dl dt img').hq_jd(xia_jd_suo_yin($('#photo_big .big img').hq_shu_xing_zhi('suoy'), $('#photo').sh_jd())).parentNode.parentNode;
                prev_next(children);
            });
    
            //共用函数
            function shang_xian(_this) {
                $('#photo_big .big img').hq_shu_xing_zhi('src', 'img/loading.gif').c_css('width', '32px').c_css('height', '32px').c_css('top', '190px');
                var current_img = new Image();
    
                $(current_img).yuan_su_shi_jian('load', function () {    //当前图片加载完毕后执行
                    $('#photo_big .big img').hq_shu_xing_zhi('src', current_img.src).yi_dong_tou_ming({     //从显示图片获取到索引
                        attr: 'o',
                        target: 100,
                        t: 30,
                        step: 10
                    }).shzh_tou_ming_du(0).c_css('width', '600px').c_css('height', '450px').c_css('top', 0);
                });
    
                current_img.src = $(_this).hq_shu_xing_zhi('src');
            }
    
            //共用函数
            function prev_next(children) {
                var prev = sh_jd_suo_yin($(children).hq_suo_yin(), children.parentNode);   //获取当前节点的，上一个节点在父元素的索引
                var next = xia_jd_suo_yin($(children).hq_suo_yin(), children.parentNode);  //获取当前节点的，下一个节点在父元素的索引
    
                var prev_img = new Image();  //预加载上一张图片
                var next_img = new Image();  //预加载下一张图片
    
                prev_img.src = $('#photo dl dt img').guo_lv_jie_dian(prev).hq_shu_xing_zhi('yjz');  //预加载上一张图片
                next_img.src = $('#photo dl dt img').guo_lv_jie_dian(next).hq_shu_xing_zhi('yjz');  //预加载下一张图片
                $('#photo_big .big .left').hq_shu_xing_zhi('src', prev_img.src);  //将上一张地址赋值给左点击
                $('#photo_big .big .right').hq_shu_xing_zhi('src', next_img.src); //将下一张地址赋值给右点击
                $('#photo_big .big img').hq_shu_xing_zhi('suoy', $(children).hq_suo_yin()); //将当前索引赋值给显示图片
                //显示图片张数
                $('#photo_big .big .index').wen_ben(parseInt($(children).hq_suo_yin()) + 1 + '/' + $('#photo dl dt img').jd_length());
            }
    
        });
    
        //关闭弹窗
        $('#photo_big .close').on_click(function () {
            $('#photo_big').c_css('display', 'none');
            $('#suo_ping').yi_dong_tou_ming({
                'attr': 'o',  //动画方式
                'target': 0, //目标量
                't': 50,      //每次动画时间
                'step': 5     //跨度
            });
            $('#photo_big .big img').hq_shu_xing_zhi('src','img/loading.gif').c_css('width','32px').c_css('height','32px').c_css('top','190px');  //关闭弹窗后，恢复默认图片
            $('#suo_ping').jie_chu_suo_ping();
        });
[/code]

首先引入封装库

