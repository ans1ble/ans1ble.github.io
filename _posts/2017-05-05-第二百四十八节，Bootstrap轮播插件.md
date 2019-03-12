---
layout: post
title: " 第二百四十八节，Bootstrap轮播插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap轮播插件**



**学习要点：**

**1.轮播插件**



**本节课我们主要学习一下 Bootstrap 中的轮播插件。**



**一．轮播**

**轮播插件就是将几张同等大小的大图，按照顺序依次播放。**

**基本实例。**



**第一步，给轮播器区域div设置一个id**  
 **给轮播器区域div设置样式carousel，slide**  
 **carousel样式class类，写在轮播器区域 <div>里，设置轮播器区域样式(Bootstrap)**  
 **slide样式class类，写在轮播器区域 <div>里，设置轮播器区域样式(Bootstrap)**





**第二步，设置图片区域**  
 **carousel-inner样式class类，写在轮播器图片区域 <div>里，设置轮播器图片区域样式(Bootstrap)**  
 **item样式class类，写在轮播器图片 <div>里，设置轮播器图片样式(Bootstrap)**  
 **active样式class类，写在轮播器图片 <div>里，设置轮播器图片首选(Bootstrap)**





**第三步，设置小圆点按钮区域**  
 **carousel-indicators样式class类，写在小圆点按钮区域 <div>里，设置小圆点按钮区域样式(Bootstrap)**  
 **将小圆点的li标签绑定轮播器区域div的id**  
 **data-target="#myCarousel"小圆点的li标签绑定轮播器区域div的id(Bootstrap)**  
 **data-slide-to="0"小圆点的li标签事件和编号默认从0开始(Bootstrap)**  
 **active样式class类，写在小圆点的 <li>里，设置当前小圆点首选(Bootstrap)**





**第四步，设置向左向右箭头**  
 **将箭头的a标签连接href=轮播器区域div的id进行绑定**  
 **data-slide="prev"设置左箭头点击事件(Bootstrap)**  
 **data-slide="next"设置右箭头点击事件(Bootstrap)**  
 **left样式class类，写在箭头 <a>里，设置箭头左样式(Bootstrap)**  
 **right样式class类，写在箭头 <a>里，设置箭头右样式(Bootstrap)**





**第五步，设置自动轮播**  
 **data-ride="carousel"写在轮播器区域div里，设置轮播器自动轮播(Bootstrap)**

[code]

     <div id="myCarousel" class="carousel slide" data-ride="carousel">
        <ol class="carousel-indicators">                                                <!--3个小圆点区域-->
            <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
            <li data-target="#myCarousel" data-slide-to="1"></li>
            <li data-target="#myCarousel" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">                                                     <!--3张图片区域-->
            <div class="item active">
                <img src="img/553f1.jpg" alt="第一张">
            </div>
            <div class="item">
                <img src="img/553f2.jpg" alt="第二张">
            </div>
            <div class="item">
                <img src="img/553f3.jpg" alt="第三张">
            </div>
        </div>
        <!--两个向左向右箭头-->
        <a href="#myCarousel" data-slide="prev" class="carousel-control left">&lsaquo;</a>
        <a href="#myCarousel" data-slide="next" class="carousel-control right">&rsaquo;</a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170505175226148-1705022678.gif)





**轮播器属性**

**轮播插件有三个自定义属性：注意属性写在html里没什么作用，一般写在js里**

**carousel()轮播器方法，将轮播器执行轮播器方法(Bootstrap)**

**data-interval 默认值 5000，幻灯片的等待时间(毫秒)。如果为false，轮播将不会自动开始循环。**  
 **data-pause 默认鼠标停留在幻灯片区域(hover)即暂停轮播，鼠标离开即启动轮播。**  
 **data-wrap 默认值 true，轮播是否持续循环。**

[code]

    $( function () {
        $('#myCarousel').carousel({
            //设置自动播放/2 秒
            interval: 1000,
            //设置暂停按钮的事件
            pause: 'hover',
            //只播一次
            wrap: false,
        });
    });
[/code]

[code]

    <div id="myCarousel" class="carousel slide">
        <ol class="carousel-indicators">                                                <!--3个小圆点区域-->
            <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
            <li data-target="#myCarousel" data-slide-to="1"></li>
            <li data-target="#myCarousel" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">                                                     <!--3张图片区域-->
            <div class="item active">
                <img src="img/553f1.jpg" alt="第一张">
            </div>
            <div class="item">
                <img src="img/553f2.jpg" alt="第二张">
            </div>
            <div class="item">
                <img src="img/553f3.jpg" alt="第三张">
            </div>
        </div>
        <!--两个向左向右箭头-->
        <a href="#myCarousel" data-slide="prev" class="carousel-control left">&lsaquo;</a>
        <a href="#myCarousel" data-slide="next" class="carousel-control right">&rsaquo;</a>
    </div>
[/code]





**轮播器方法**

**cycle 循环各帧(默认从左到右)**  
 **pause 停止轮播**  
 **number 轮播到指定的图片上(小标从 0 开始，类似数组)**  
 **prev 循环轮播到上一个项目**  
 **next 循环轮播到下一个项目**

[code]

    $( function () {
        //点击按钮执行
        $('button').on('click', function () {
            //点击后，自动播放
            $('#myCarousel').carousel('cycle');
            //其他雷同
        });
    });
[/code]





**轮播器事件**

**slide.bs.carousel 当调用 slide 实例方式时立即触发该事件。**  
 **slid.bs.carousel 当轮播完成一个幻灯片触发该事件。**

[code]

    $( function () {
        //事件
        $('#myCarousel').on('slide.bs.carousel', function () {
            alert('当调用 slide 实例方式时立即触发');
        });
        $('#myCarousel').on('slid.bs.carousel', function () {
            alert('当轮播完成一个幻灯片触发');
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170505182017789-732593576.png)





**给轮播图设置文字**

**carousel-caption样式class类，写在轮播图区域里 <div>里，设置轮播图文字区域(Bootstrap)**

[code]

    <div id="myCarousel" class="carousel slide">
        <ol class="carousel-indicators">                                                <!--3个小圆点区域-->
            <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
            <li data-target="#myCarousel" data-slide-to="1"></li>
            <li data-target="#myCarousel" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">                                                     <!--3张图片区域-->
            <div class="item active">
                <img src="img/553f1.jpg" alt="第一张">
                <div class="carousel-caption">
                    <h3>广告录音</h3>
                    <p>专业的广告录音设备，完善的录音流程</p>
                </div>
            </div>
            <div class="item">
                <img src="img/553f2.jpg" alt="第二张">
                <div class="carousel-caption">
                    <h3>广告录音</h3>
                    <p>专业的广告录音设备，完善的录音流程</p>
                </div>
            </div>
            <div class="item">
                <img src="img/553f3.jpg" alt="第三张">
                <div class="carousel-caption">
                    <h3>广告录音</h3>
                    <p>专业的广告录音设备，完善的录音流程</p>
                </div>
            </div>
        </div>
        <!--两个向左向右箭头-->
        <a href="#myCarousel" data-slide="prev" class="carousel-control left">&lsaquo;</a>
        <a href="#myCarousel" data-slide="next" class="carousel-control right">&rsaquo;</a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170505200031726-1994538800.png)



