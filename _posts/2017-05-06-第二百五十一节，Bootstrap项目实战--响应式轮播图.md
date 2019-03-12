---
layout: post
title: " 第二百五十一节，Bootstrap项目实战--响应式轮播图 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap项目实战--响应式轮播图**



**学习要点：**

**1.响应式轮播图**



**本节课我们要在导航条的下方做一张轮播图，自动播放最新的重要动态。**



**一．响应式轮播图**

**响应式轮播图**



**第一步，设置轮播器区域**  
 **carousel样式class类，写在轮播器 <div>里，设置轮播器区域样式(项目实战Bootstrap)**  
 **slide样式class类，写在轮播器 <div>里，设置轮播器滚动样式(项目实战Bootstrap)**



**第二步，设置轮播器列表区域，就是小圆点区域**  
 **carousel-indicators样式class类，写在轮播器列表
<ol>里，设置轮播器列表区域样式，就是小圆点区域样式(项目实战Bootstrap)**  
 **active样式class类，写在轮播器列表 <li>里，设置当前列表项首选(项目实战Bootstrap)**



**第三步，设置轮播器图片区域**  
 **carousel-inner样式class类，写在轮播器图片区域 <div>里，设置轮播器图片区域(项目实战Bootstrap)**  
 **item样式class类，写在轮播器图片区域里 <div>里，设置轮播器图片样式(项目实战Bootstrap)**  
 **active样式class类，写在轮播器图片区域里 <div>里，设置轮播器当前图片首选(项目实战Bootstrap)**



**第四步，设置轮播器箭头区域**  
 **carousel-control样式class类，写在轮播器箭头 <a>里，设置轮播器箭头样式(项目实战Bootstrap)**  
 **left样式class类，写在轮播器箭头 <a>里，设置轮播器箭头靠左(项目实战Bootstrap)**  
 **right样式class类，写在轮播器箭头 <a>里，设置轮播器箭头靠右(项目实战Bootstrap)**



**第五步，事件绑定**  
 **列表绑定**  
 **data-target="#myCarousel"写在轮播器列表li标签里，将轮播绑定轮播器区域div的id(项目实战Bootstrap)**  
 **data-slide-to="0"写在轮播器列表li标签里，将轮播器列表编号，默认从0开始(项目实战Bootstrap)**  
 **箭头绑定**  
 **href="#myCarousel"写在轮播器箭头a标签里，将a标签连接href=轮播器区域div的id(项目实战Bootstrap)**  
 **data-slide="prev"写在轮播器箭头a标签里，设置箭头左点击事件(项目实战Bootstrap)**  
 **data-slide="next"写在轮播器箭头a标签里，设置箭头右点击事件(项目实战Bootstrap)**



**第六步，重写css**  
 **1.将轮播器头部外边距设置成导航条的高度，使其轮播器不被导航覆盖**  
 **2.将轮播器里的图片img标签外边距方式居中**  
 **3.将图片外层div设置成图片渐变背景色，将所有图片渐变处理，使其图片与外围div融合**



**第七步，写js**  
 **在js文件设置轮播器自动播放，和播放间隔时间**



**第八步，重点，关于箭头响应式自动居中问题**  
 **在箭头a标签里用span标签设置图标glyphicon-chevron-left和glyphicon-chevron-
right，或自动实现箭头响应式居中**

**  html**

[code]

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
[/code]

**css**

[code]

     /*轮播器--------------------------------------------------------------------------------------------------------------*/
    /*将轮播器头部外边距设置50像素*/
    #myCarousel {
        margin: 50px 0 0 0;
    }
    .carousel-inner .item img {
        margin: 0 auto;
    }
    .tp1{
        background:#ECEDF1;
    }
    .tp2{
        background:#88AED3;
    }
    .tp3{
        background:#22AEE3;
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

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170507162754867-980379828.gif)



