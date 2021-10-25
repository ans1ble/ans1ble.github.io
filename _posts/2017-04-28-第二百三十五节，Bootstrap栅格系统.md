---
layout: post
title: " 第二百三十五节，Bootstrap栅格系统 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap栅格系统**



**学习要点：**

**1.移动设备优先**

**2.布局容器**

**3.栅格系统**



**本节课我们主要学习一下 Bootstrap 的栅格系统，提供了一套响应式、移动设备优先的流 式栅格系统。**



**一．移动设备优先**

**在 HTML5 的项目中，我们做了移动端的项目。它有一份非常重要的 meta，用于设置屏 幕和设备等宽以及是否运行用户缩放，及缩放比例的问题。**

**分别为：屏幕宽度和设备一致、初始缩放比例、最大缩放比例和禁止用户缩放**



**viewport视口视窗的意思**  
 **width=device-width以设备宽度相等显示，也就是设备宽度多大就以多大显示**  
 **initial-scale=1初始缩放以100%，这样移动端文字才能看清楚**  
 **maximum-scale=1最大缩放100%**  
 **user-scalable=no禁止用户缩放**

**这段代码一般复制即可**

[code]

     <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1, user-scalable=no">
        <title>Bootstrap 介绍</title>
        <!--引入bootstrap样式文件-->
        <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
        <link rel="stylesheet" href="css/ceshi.css">
    </head>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428150614178-2116832406.png)





**二．布局容器，布局div**

**Bootstrap 需要为页面内容和栅格系统包裹一个.container 容器。由于 padding 等 属性的原因，这两种容器类不能相互嵌套。**

**注意：两个布局容器不能嵌套**

**container样式class类，写在布局 <div>里，固定宽度1140x20布局(Bootstrap)**

[code]

    <div class="container cshi">
    ....
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428153312787-967204407.png)



**container-fluid样式class类，写在布局 <div>里，100%宽度布局(Bootstrap)**

[code]

    <div class="container-fluid cshi">
    ....
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428153540865-388471696.png)



**栅格系统中，浏览器会随着屏幕的大小的增减自动分配最多12列。通过一系列的行(row) 与列(column)的组合来创建页面布局。工作原理如下：**

**1.“行（row）”必须包含在 .container （固定宽度）或 .container-fluid （100%
宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。**

**2.通过“行（row）”在水平方向创建一组“列（column）”。**

**3.你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为 行（row）”的直接子元素。**

**4.类似 .row 和 .col-xs-4 这种预定义的类，可以用来快速创建栅格布局。 Bootstrap 源码中定义的 mixin
也可以用来创建语义化的布局。**

**5.通过为“列（column）”设置 padding 属性，从而创建列与列之间的间隔（gutter）。通过为 .row 元素设置负值 margin
从而抵消掉为 .container 元素设置的 padding， 也就间接为“行（row）”所包含的“列（column）”抵消掉了 padding。**

**6.负值的 margin 就是下面的示例为什么是向外突出的原因。在栅格列中的内容排成 一行。**

** 7.栅格系统中的列是通过指定 1 到 12 的值来表示其跨越的范围。例如，三个等宽的列 可以使用三个 .col-xs-4 来创建。 **

** 8.如果一“行（row）”中包含了的“列（column）”大于 12，多余的“列（column）” 所在的元素将被作为一个整体另起一行排列。 **

**9.栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆 盖栅格类。 因此，在元素上应用任何 .col-md-*
栅格类适用于与屏幕宽度大于或等于分 界点大小的设备 ，并且针对小屏幕设备覆盖栅格类。因此，在元素上应用任何 .col-lg-* 不存在，
也影响大屏幕设备。**



**创建一个响应式行**

**row样式class类，写在布局div里的 <div>里，在布局div里设置一行(Bootstrap)**

[code]

    <div class="container">
        <div class="row a">
            ...
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428164025647-1847772649.png)



**创建最多 12 列的响应式行**

**col-md-1样式class类，写在列 <div>里，设置1列，最多设置12列，刚好一行的宽度(Bootstrap)**

**最多只能创建12列，超出则换行**

[code]

     <div class="container">
        <div class="row a">
            <div class="col-md-1 a">1</div>
            <div class="col-md-1 a">2</div>
            <div class="col-md-1 a">3</div>
            <div class="col-md-1 a">4</div>
            <div class="col-md-1 a">5</div>
            <div class="col-md-1 a">6</div>
            <div class="col-md-1 a">7</div>
            <div class="col-md-1 a">8</div>
            <div class="col-md-1 a">9</div>
            <div class="col-md-1 a">10</div>
            <div class="col-md-1 a">11</div>
            <div class="col-md-1 a">12</div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428165002662-1828142548.png)





**列所占分配**

****col-md-1至 ** **col-md-12 **样式class类，写在列 <div>里，分别代表当前列所占多少列，如col-
md-12，就是当前列所占12列位置，也就是1列占完所有行(Bootstrap)**********

**col-md-1~12样式class类，写在列 <div>里，分别代表当前列所占多少列，如col-
md-12，就是当前列所占12列位置，也就是1列占完所有行(Bootstrap)**

[code]

    <div class="container">
        <div class="row b">
            <div class="col-md-1 a">1</div>     <!--col-md-1表示所占1列-->
            <div class="col-md-1 a">2</div>
            <div class="col-md-1 a">3</div>
            <div class="col-md-1 a">4</div>
            <div class="col-md-1 a">5</div>
            <div class="col-md-1 a">6</div>
            <div class="col-md-1 a">7</div>
            <div class="col-md-1 a">8</div>
            <div class="col-md-1 a">9</div>
            <div class="col-md-1 a">10</div>
            <div class="col-md-1 a">11</div>
            <div class="col-md-1 a">12</div>
        </div>
    
        <div class="row b">
            <div class="col-md-4 a">1</div>     <!--col-md-4表示所占4列-->
            <div class="col-md-4 a">1</div>
            <div class="col-md-4 a">1</div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428171121006-353509988.png)





**栅格参数表，也就是媒体查询自适应所占列**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428171637553-1894406704.png)**

**col-xs-1~12样式class类，写在列 <div>里，(手机)表示屏幕小于768所占多少列(Bootstrap)**  
 **col-sm-1~12样式class类，写在列 <div>里，(平板)表示屏幕大于或等于768所占多少列(Bootstrap)**  
 **col-md-1~12样式class类，写在列 <div>里，(中等屏幕)表示屏幕大于或等于992所占多少列(Bootstrap)**  
 **col-lg-1~12样式class类，写在列 <div>里，(大屏幕)表示屏幕大于或等于1200所占多少列(Bootstrap)**

[code]

    <div class="container">
        <div class="row b">
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">1</div>     <!--col-xs-12屏幕小于768将12列全占为一行-->
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">2</div>     <!--col-sm-6屏幕大于或等于768占6列为两行-->
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">3</div>     <!--col-md-4屏幕大于或等于992占4列为三行-->
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">4</div>     <!--col-lg-3屏幕大于或等于1200占3列为四行-->
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">5</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">6</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">7</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">8</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">9</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">10</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">11</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 a">12</div>
        </div>
    </div>
[/code]

**屏幕小于768将12列全占为一行**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428175056506-1399215505.png)**

**屏幕大于或等于768占6列为两行**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428175152740-2117588411.png)**

**屏幕大于或等于992占4列为三行**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428175227772-1117203780.png)**

**屏幕大于或等于1200占3列为四行**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428175256428-1967562067.png)**





**有时我们可以设置列偏移，让中间保持空隙**

**col-md-offset-1~12样式class类，写在列 <div>里，设置列向右便宜多少个列位置(Bootstrap)**

[code]

    <div class="container">
        <div class="row">
            <div class="col-md-8 a">8</div>
            <div class="col-md-3 col-md-offset-1 a">3</div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428184108912-1469488714.png)



**也可以嵌套，嵌满也是 12 列**

[code]

     <div class="container">
        <div class="row">
            <div class="col-md-9 a">
                <div class="col-md-8 a">1-8</div>
                <div class="col-md-4 a">9-12</div>
            </div>
            <div class="col-md-3 a">
                11-12
            </div>
        </div>
    </div>
[/code]



**可以把两个列交换位置，push 向左移动，pull 向右移动**

**col-md-push样式class类，写在列 <div>里，向左移动后面跟移动的目的列(Bootstrap)**  
 **col-md-pull样式class类，写在列 <div>里，向右移动后面跟移动的目的列(Bootstrap)**

[code]

    <div class="container">
        <div class="row">
            <div class="col-md-9 col-md-push-3 a">9</div>
            <div class="col-md-3 col-md-pull-9 a">3</div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428190231037-1988499031.png)



