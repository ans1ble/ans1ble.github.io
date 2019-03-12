---
layout: post
title: " 第二百四十一节，Bootstrap进度条媒体对象和 Well 组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第二百四十一节，Bootstrap进度条媒体对象和 Well 组件**



**学习要点：**

**1.Well 组件**

**2.进度条组件**

**3.媒体对象组件**



**本节课我们主要学习一下 Bootstrap 的三个组件功能：Well 组件、进度条组件、媒体对 象组件。**



**一．Well 组件**

**这个组件可以实现简单的嵌入效果。**

**嵌入效果**

**well样式class类，写在 <div>里，设置一个div区块嵌入效果(Bootstrap)**  
 **well-lg样式class类，写在 <div>里，设置一个div区块嵌入效果大尺寸(Bootstrap)**  
 **well-sm样式class类，写在 <div>里，设置一个div区块嵌入效果小尺寸(Bootstrap)**

[code]

    <div class="well">
        Bootstrap
    </div>
    
    <div class="well well-lg">
        Bootstrap
    </div>
    <div class="well well-sm">
        Bootstrap
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501015236304-304538093.png)





**二．进度条组件**

**进度条组件为当前工作流程或动作提供时时反馈。**

**基本进度条**



**progress样式class类，写在 <div>里，声明一个进度条区域(Bootstrap)**



**progress-bar样式class类，写在 <div>里，设置一个进度条默认样式(Bootstrap)**

[code]

    <div class="progress">
        <div class="progress-bar" style="width: 60%;">60%</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501093704211-880953461.png)





**最低值进度条**

[code]

     <div class="progress">
        <div class="progress-bar" style="min-width:20px; width: 0%;">0%</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501162332820-1883093179.png)





**结合情景的进度条**

**progress-bar-success样式class类，写在 <div>元素里，设置进度条绿色(Bootstrap)**  
 **progress-bar-info样式class类，写在 <div>元素里，设置进度条蓝色(Bootstrap)**  
 **progress-bar-warning样式class类，写在 <div>元素里，设置进度条橙色(Bootstrap)**  
 **progress-bar-danger样式class类，写在 <div>元素里，设置进度条红色(Bootstrap)**

[code]

    <div class="progress">
        <div class="progress-bar progress-bar-success" style="min-width:20px;width:60%">60%
        </div>
    </div>
    <div class="progress">
        <div class="progress-bar progress-bar-info" style="min-width:20px;width:60%">60%
        </div>
    </div>
    <div class="progress">
        <div class="progress-bar progress-bar-warning" style="min-width:20px;width:60%">60%
        </div>
    </div>
    <div class="progress">
        <div class="progress-bar progress-bar-danger" style="min-width:20px;width:60%">60%
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501094809742-683600836.png)





**条纹状， IE10+支持， **IE10以下不支持****

**progress-bar-striped样式class类，写在 <div>元素里，设置条纹状进度条(Bootstrap)**

[code]

    <div class="progress">
        <div class="progress-bar progress-bar-success progress-bar-striped" style="min-width:20px;width:60%">60%
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501095232976-888053022.png)





**条纹状动画效果， 必须将进度条设置 **条纹状****

**active样式class类，写在进度条 <div>里，设置进度条，条纹状动画效果(Bootstrap)**

[code]

    <div class="progress">
        <div class="progress-bar progress-bar-success progress-bar-striped active" style="min-width:20px;width:60%">60%
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501095707898-669615351.png)





**进度条堆叠效果**

[code]

     <div class="progress">
        <div class="progress-bar progress-bar-success" style="min-width:20px;width:30%">30%</div>
        <div class="progress-bar progress-bar-warning" style="min-width:20px;width:20%">20%</div>
        <div class="progress-bar progress-bar-danger" style="min-width:20px;width:50%">50%</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501100100023-1312694814.png)







**三．媒体对象组件， 论坛常用**

**媒体对象可以包含图片、视频或音频等媒体，以达到对象和文本组合显示的样式效果。**

**基本实例**

**media样式class类，写在 <div>里，声明一个媒体对象div(Bootstrap)**  
 **media-left样式class类，写在 <div>里，设置一个媒体对象里的媒体区域左边显示(Bootstrap)**  
 **media-object样式class类，写在 <img>里，设置一个媒体样式(Bootstrap)**  
 **media-body样式class类，写在 <div>里，声明一个媒体内容div(Bootstrap)**  
 **media-heading样式class类，写在 <h1-h4>里，设置一个媒体内容标题样式(Bootstrap)**

[code]

    <div class="media">
        <div class="media-left">
            <img src="img/small.png" alt="" class="media-object">
        </div>
        <div class="media-body">
            <h4 class="media-heading">标题</h4>
            <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老
                的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有 17
                种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；
                脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；
                羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个
                种的主要区别在于头部色型和个体大小。</p>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501104636320-1794232939.png)







**媒体对象在右边**

**media-right样式class类，写在 <div>里，设置一个媒体对象里的媒体区域右边显示(Bootstrap)**

[code]

    <div class="media">
        <div class="media-body">
            <h4 class="media-heading">标题</h4>
            <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老
                的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有 17
                种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；
                脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；
                羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个
                种的主要区别在于头部色型和个体大小。</p>
        </div>
        <div class="media-right">
            <img src="img/small.png" alt="" class="media-object">
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501105147007-1401353312.png)







**媒体对象列表， 也就是声明一个媒体对象列表然后嵌套媒体对象**

**media-list样式class类，写在 <ul>里，声明一个媒体对象列表(Bootstrap)**



[code]

    <ul class="media-list">
        <li class="meida">
            <div class="media-left">
                <img src="img/small.png" alt="" class="media-object">
            </div>
            <div class="media-body">
                <h4 class="meida-heading">内容标题</h4>
                <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有17种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个种的主要区别在于头部色型和个体大小。</p>
                <div class="meida">
                    <div class="media-left">
                        <img src="img/small.png" alt="" class="media-object">
                    </div>
                    <div class="media-body">
                        <h4 class="meida-heading">内容标题</h4>
                        <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有17种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个种的主要区别在于头部色型和个体大小。</p>
                        <div class="meida">
                            <div class="media-left">
                                <img src="img/small.png" alt="" class="media-object">
                            </div>
                            <div class="media-body">
                                <h4 class="meida-heading">内容标题</h4>
                                <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有17种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个种的主要区别在于头部色型和个体大小。</p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="meida">
                    <div class="media-left">
                        <img src="img/small.png" alt="" class="media-object">
                    </div>
                    <div class="media-body">
                        <h4 class="meida-heading">内容标题</h4>
                        <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有17种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个种的主要区别在于头部色型和个体大小。</p>
                    </div>
                </div>
            </div>
        </li>
        <li class="meida">
            <div class="media-left">
                <img src="img/small.png" alt="" class="media-object">
            </div>
            <div class="media-body">
                <h4 class="meida-heading">内容标题</h4>
                <p>企鹅（学名：Spheniscidae）：有“海洋之舟”美称的企鹅是一种最古老的游禽，它们很可能在地球穿上冰甲之前，就已经在南极安家落户。全世界的企鹅共有17种，大多数都分布在南半球。主要生活在南半球，属于企鹅目，企鹅科。特征为不能飞翔；脚生于身体最下部，故呈直立姿势；趾间有蹼；跖行性（其他鸟类以趾着地）；前肢成鳍状；羽毛短，以减少摩擦和湍流；羽毛间存留一层空气，用以保温。背部黑色，腹部白色。各个种的主要区别在于头部色型和个体大小。</p>
            </div>
        </li>
    </ul>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501161723476-372956560.png)



