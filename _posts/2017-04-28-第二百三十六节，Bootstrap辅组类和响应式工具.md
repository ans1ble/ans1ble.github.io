
---
layout: post
title: " 第二百三十六节，Bootstrap辅组类和响应式工具 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Bootstrap辅组类和响应式工具**



**学习要点：**

**1.辅组类**

**2.响应式工具**



**本节课我们主要学习一下 Bootstrap 的辅组类和响应式工具，辅助类提供了一组类来辅 组页面设计，而响应式工具则利用媒体查询显示或隐藏某些内容。**



**一．辅助类**

**Bootstrap 在布局方面提供了一些细小的辅组样式，用于文字颜色以及背景色的设置、 显示关闭图标等等。**

**1.文本颜色**



**text-muted样式class类，写在当前元素里，文字颜色柔和灰(Bootstrap)**  
 **text-primary样式class类，写在当前元素里，文字颜色主要蓝(Bootstrap)**  
 **text-success样式class类，写在当前元素里，文字颜色成功绿(Bootstrap)**  
 **text-info样式class类，写在当前元素里，文字颜色信息蓝(Bootstrap)**  
 **text-warning样式class类，写在当前元素里，文字颜色警告黄(Bootstrap)**  
 **text-danger样式class类，写在当前元素里，文字颜色危险红(Bootstrap)**

[code]

     <p class="text-muted">Bootstrap 柔和灰</p>
    <p class="text-primary">Bootstrap 主要蓝</p>
    <p class="text-success">Bootstrap 成功绿</p>
    <p class="text-info">Bootstrap 信息蓝</p>
    <p class="text-warning">Bootstrap 警告黄</p>
    <p class="text-danger">Bootstrap 危险红</p>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429005820881-918643399.png)



**2.背景色**

**bg-primary样式class类，写在当前元素里，背景颜色主要蓝(Bootstrap)**  
 **bg-success样式class类，写在当前元素里，背景颜色成功绿(Bootstrap)**  
 **bg-info样式class类，写在当前元素里，背景颜色信息蓝(Bootstrap)**  
 **bg-warning样式class类，写在当前元素里，背景颜色警告黄(Bootstrap)**  
 **bg-danger样式class类，写在当前元素里，背景颜色危险红(Bootstrap)**

[code]

     <p class="bg-primary">Bootstrap 主要蓝</p>
    <p class="bg-success">Bootstrap 成功绿</p>
    <p class="bg-info">Bootstrap 信息蓝</p>
    <p class="bg-warning">Bootstrap 警告黄</p>
    <p class="bg-danger">Bootstrap 危险红</p>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429010329444-1301990654.png)





**3.关闭按钮**

**close样式class类，写在当前元素里，关闭按钮样式(Bootstrap)**

[code]

     <button type="button" class="close">&times;</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429010751725-857538957.png)



**4.三角符号**

**caret样式class类，写在 <span>元素里，三角符号样式(Bootstrap)**

[code]

    <span class="caret"></span>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429011006600-1927252430.png)



**5.快速浮动**

**pull-left样式class类，写在当前元素里，左浮动(Bootstrap)**  
 **pull-right样式class类，写在当前元素里，右浮动(Bootstrap)**

**注：这个浮动其实就是 float，只不过使用了!important 加强了优先级。**

[code]

     <div class="pull-left a">左边</div>
    <div class="pull-right a">右边</div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429012045850-544098110.png)



**6.块级居中**

**center-block样式class类，写在当前元素里，块级居中(Bootstrap)**

**注：就是 margin:x auto；并且设置了 display:block;。**

[code]

     <div class="center-block a">居中</div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429033406490-330537367.png)



**7.清理浮动**

**clearfix样式class类，写在用于清除浮动的 <div>素里,将此div放在要清除浮动的前面即可(Bootstrap)**

**注：这个 div 可以放在需要清理浮动区块的前面即可。**

[code]

     <div class="pull-left a">左边</div>
    <div class="clearfix"></div>
    <div class="a">右边</div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429140622162-1263005857.png)



**8.显示和隐藏**

**show样式class类，写在当前素里,显示元素(Bootstrap)**  
 **hidden样式class类，写在当前素里,隐藏元素(Bootstrap)**

[code]

     <div class="hidden">左边</div>
[/code]





**二．响应式工具**

**在媒体查询时，针对不同的屏幕大小，有时需要显示和隐藏部分内容。响应式工具类， 就提供了这种解决方案。**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429141141084-877212518.png)**

**一般用于显示**

**visible-xs-*样式class类，写在当前素里,小于768可见，大于等于768隐藏(Bootstrap)**  
 **visible-sm-*样式class类，写在当前素里,大于等于768可见，大于等于992隐藏(Bootstrap)**  
 **visible-md-*样式class类，写在当前素里,大于等于992可见，大于等于1200隐藏(Bootstrap)**  
 **visible-lg-*样式class类，写在当前素里,大于等于1200可见(Bootstrap)**

**以上类*有可选参数显示类型：block（显示为区块）、inline-block（显示为内联块）、inline（显示为内联）。**

[code]

     <div class="visible-xs-block a">元素区块</div>  <!--visible-xs-*样式class类，写在当前素里,小于768可见，大于等于768隐藏-->
[/code]



**一般用于隐藏**  
 **hidden-xs样式class类，写在当前素里,小于768隐藏，大于等于768可见(Bootstrap)**  
 **hidden-sm样式class类，写在当前素里,小于768可见，大于等于768隐藏，大于等于992显示(Bootstrap)**  
 **hidden-md样式class类，写在当前素里,小于大于768可见，大于等于992隐藏，大于等于1200可见(Bootstrap)**  
 **hidden-lg样式class类，写在当前素里,小于1200可见，大于等于1200隐藏(Bootstrap)**

**以上类没有可选参数**

[code]

     <div class="hidden-lg a">元素区块</div>  <!--hidden-lg样式class类，写在当前素里,小于1200可见，大于等于1200隐藏-->
[/code]



