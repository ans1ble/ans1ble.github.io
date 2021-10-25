---
layout: post
title: " 第二百四十三节，Bootstrap模态框插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap模态框插件**



**学习要点：**

**1.基本使用**

**2.用法说明**



**本节课我们主要学习一下 Bootstrap 中的模态框插件，这是一款交互式网站非常常见的 弹窗功能插件。**



**一．基本使用**

**使用模态框的弹窗组件需要三层 div 容器元素：**

**1分别为 modal(模态声明层)、**

**2dialog(窗口声明层)、**

**3content(内容层)。**

**在内容层里面，** **还有三层：**

**1分别为 header(头 部)、**

**2body(主体)、**

**3footer(注脚)。**

**modal样式class类，写在声明模态框 <div>里，模态框区块声明(Bootstrap)**  
 **show样式class类，写在声明模态框 <div>里，表示模态框显示,默认模态框是隐藏的(Bootstrap)**  
 **modal-dialog样式class类，写在声明模态框窗口 <div>里，模态框窗口区域声明(Bootstrap)**  
 **modal-content样式class类，写在声明模态框内容 <div>里，模态框内容区域声明(Bootstrap)**  
 **modal-header样式class类，写在模态框内容里头部 <div>里，模态框内容头部区域样式(Bootstrap)**  
 **close样式class类，写在模态框头部 <button>里，模态框内容头部区域关闭按钮样式(Bootstrap)**  
 **data-dismiss="modal"模态框事件点击后关闭模态框，写在模态框关闭按钮 <button>里(Bootstrap)**  
 **modal-title样式class类，写在模态框头部 <h1-h4>里，模态框内容头部区域标题样式(Bootstrap)**  
 **modal-body样式class类，写在模态框主体 <div>里，设置模态框主体样式(Bootstrap)**  
 **modal-footer样式class类，写在模态框底部 <div>里，设置模态框底部样式(Bootstrap)**

[code]

    <div class="modal show">                                                    <!--modal模态框区块声明，show表示模态框显示 -->
        <div class="modal-dialog">                                              <!--modal-dialog模态框窗口区域声明 -->
            <div class="modal-content">                                         <!--modal-content模态框内容区域声明 -->
                <div class="modal-header">                                      <!--modal-header模态框内容头部区域样式-->
                    <button type="button" class="close" data-dismiss="modal">   <!--close模态框内容头部区域关闭按钮样式，data-dismiss="modal"事件点击后关闭模态框-->
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>                        <!--modal-title模态框内容头部区域标题样式-->
                </div>
                <div class="modal-body">                                        <!--modal-body设置模态框主体样式-->
                    <p>暂时无法登录会员</p>
                </div>
                <div class="modal-footer">                                      <!--modal-footer设置模态框底部样式 -->
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502184217414-653252594.png)





**让模态框自动隐藏，然后通过点击按钮弹窗**

**data-toggle="modal"声明事件切换类型，modal表示模态框类型，写在 <button>里(Bootstrap)**  
 **data-target="#myModal"
>声明事件操作对象，#myModal表示点击后关闭id为#myModal的元素，写在<button>里(Bootstrap)**

[code]

    <div class="modal" id="myModal">                                                <!--模态框去掉 show，增加一个 id-->
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <div class="modal-body">
                    <p>暂时无法登录会员</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <!--data-toggle="modal"声明事件切换类型，modal表示模态框类型(Bootstrap)-->
    <!--data-target="#myModal">声明事件操作对象，#myModal表示点击后关闭id为#myModal的元素(Bootstrap)-->
    <button class="btn btn-primary btn-lg" **data-toggle ="modal" data-target="#myModal"**>
        点击弹窗
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502190242945-663740902.png)

**点击后**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502190337023-1603046919.png)**







**模态框弹窗大小**

**弹窗的大小有三种，默认情况下是正常，还有 lg(大)和 sm(小)**

**modal-lg样式class类，写在模态框窗口区域声明 <div>里，模态框大尺寸(Bootstrap)**  
 **modal-sm样式class类，写在模态框窗口区域声明 <div>里，模态框小尺寸(Bootstrap)**

[code]

    <div class="modal" id="myModal">                                                
        <div class="modal-dialog modal-sm">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <div class="modal-body">
                    <p>暂时无法登录会员</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
        点击弹窗
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502191546242-773537596.png)







**模态框弹窗淡入淡出效果**

**fade样式class类，写在声明模态框 <div>里，设置模态框弹窗淡入淡出效果(Bootstrap)**

[code]

    <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <div class="modal-body">
                    <p>暂时无法登录会员</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
        点击弹窗
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502195325617-1082450876.gif)





**模态框在主体部分使用栅格系统中的流体**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <!--在模态框主体里使用流体删格系统-->
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
        点击弹窗
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502201012007-1411429132.gif)





**二．用法说明**

**基本使用介绍结束之后，我们就来看下插件的各种重要用法。所有的插件，都是基于 JavaScript/jQuery
的。那么，就有四个要素：用法、参数、方法和事件。**

**1.用法**

**第一种：可以通过 data 属性，在触发模态框按钮上使用**

**data-toggle 表示触发类型**

**data-target 表示触发的节点**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <!--在模态框主体里使用流体删格系统-->
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
        点击弹窗
    </button>
[/code]

**如果不是使用 <button>，而是<a>，其中 data-target 也可以使用 href="#myModal"，取代。当然，我们建议使用
data-target。除了 data-toggle 和 data-target 两个声明 属性外，还有一些可以用选项。**



**2.选用参数，写在触发模态框的按钮里**

**可以通过在 HTML 元素上设置 data-*的属性声明来控制效果。**

**data-backdrop 布尔值或'static' true默认值 true，表示背景存在黑灰透明遮罩，且单击空白背景可关闭弹窗；如果为
false，表示背景不存在黑灰透明遮罩，且点击空白背景不可关闭弹窗；如果是字符串'static'，表示背景存在黑灰透明遮罩，且点击空白不可关闭弹窗。**

[code]

     <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="true">
        点击弹窗
    </button>
[/code]

[code]

    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="false">
        点击弹窗
    </button>
[/code]

[code]

    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="static">
        点击弹窗
    </button>
[/code]





**data-keyboard 布尔值 true 如果是 true，按 esc 键会关闭窗口；如果是 false，按 esc 键会不会关闭。**

[code]

     <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop='static' data-keyboard="false">
        点击弹窗
    </button>
[/code]

[code]

    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop='static' data-keyboard="true">
        点击弹窗
    </button>
[/code]





**data-show 布尔值 true 如果是 true，初始化时，默认显示；如果是 false，初始化时，默认隐藏。**

**在按钮触发，不是很明显**

[code]

     <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="static" data-show="true">
        点击弹窗
    </button>
[/code]

[code]

    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="static" data-show="false">
        点击弹窗
    </button>
[/code]





**href url 路径 空值如果值不是以#号开头，则表示一个url 地址，加载 url 内容到modal-content
模态框内容区域div里，并只加载一次。如果是#号，就是取代data-target 的方法。**

**如果值是以#开头就是代替data-target属性后面跟事件指向id名称**

[code]

     <button class="btn btn-primary btn-lg" data-toggle="modal" data-backdrop="static" href="#myModal">
        点击弹窗
    </button>
[/code]

**如果href值不是以#开头，是一个远程地址如bfq.html，就是将远程bfq.html文件里的内容加载到modal-content
模态框内容区域div里**

****bfq.html文件****

[code]

     <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal">
            <span>&times;</span>
        </button>
        <h4 class="modal-title">远程加载</h4>
    </div>
    <!--在模态框主体里使用流体删格系统-->
    <div class="modal-body">
        <div class="container-fluid">
            <div class="row">
                <div class="col-md-4">6</div>
                <div class="col-md-4">6</div>
                <div class="col-md-4">6</div>
            </div>
        </div>
    </div>
    <div class="modal-footer">
        <button type="button" class="btn btn-default">
            注册
        </button>
        <button type="button" class="btn btn-primary">
            登录
        </button>
    </div>
[/code]



**模态框页面**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <!--<div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                &lt;!&ndash;在模态框主体里使用流体删格系统&ndash;&gt;
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>-->
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal" data-backdrop="static" **href ="bfq.html"**>
        点击弹窗
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502213602242-342822600.png)







**当然，也可以在 JavaScript 直接设置。**

**modal()将指定元素执行模态框方法，参数是一个对象，里写各种需要属性参数(Bootstrap)**



**backdrop 布尔值或'static'true默认值 true，表示背景存在黑灰透明遮罩，且单击空白背景可关闭弹窗；如果为
false，表示背景不存在黑灰透明遮罩，且点击空白背景不可关闭弹窗；如果是字符串'static'，表示背景存在黑灰透明遮罩，且点击空白不可关闭弹窗。**



**keyboard 布尔值 true 如果是 true，按 esc 键会关闭窗口；如果是 false，按 esc 键会不会关闭。**



**show 布尔值 true 如果是 true，初始化时，默认显示；如果是 false，初始化时，默认隐藏。**



**remote #路径 url远程获取指定内容填充到modal-content 容器内。**



******bfq.html文件******

[code]

     <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal">
            <span>&times;</span>
        </button>
        <h4 class="modal-title">远程加载</h4>
    </div>
    <!--在模态框主体里使用流体删格系统-->
    <div class="modal-body">
        <div class="container-fluid">
            <div class="row">
                <div class="col-md-4">6</div>
                <div class="col-md-4">6</div>
                <div class="col-md-4">6</div>
            </div>
        </div>
    </div>
    <div class="modal-footer">
        <button type="button" class="btn btn-default">
            注册
        </button>
        <button type="button" class="btn btn-primary">
            登录
        </button>
    </div>
[/code]

**模态框页面**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
        点击弹窗
    </button>
[/code]

**js文件**

[code]

    $( function () {
        $('#myModal').modal({
            backdrop:"static",  //背景存在黑灰透明遮罩，且点击空白不可关闭弹窗。
            keyboard:false,     //false，按 esc 键会不会关闭模态框
            show:false,         //如果是 false，初始化时，默认隐藏
            remote:"bfq.html"   //远程获取指定内容填充到modal-content 容器内
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170502220043164-1556758543.png)







**3.方法**

**toggle .modal('toggle'); 触发时，反转切换弹窗状态(Bootstrap)**  
 **show .modal('show'); 触发时，显示弹窗(Bootstrap)**  
 **hide .modal('hide'); 触发时，关闭弹窗(Bootstrap)**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <!--在模态框主体里使用流体删格系统-->
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" id="sdfg">
        点击弹窗
    </button>
[/code]

**js**

[code]

    $( function () {
        $('#sdfg').on('click', function () {  //获取按钮执行点击事件
            $('#myModal').modal('show');      //点击按钮后将模态框，反转切换弹窗状态，也就是隐藏显示切换
        });
        $('#myModal').modal({
            backdrop:"static",  //背景存在黑灰透明遮罩，且点击空白不可关闭弹窗。
            keyboard:false,     //false，按 esc 键会不会关闭模态框
            show:false,         //如果是 false，初始化时，默认隐藏
        });
    });
[/code]

**其他两个方法使用相同**







**4.事件**

**模态框支持 4 种事件，分别对应弹出前、弹出后、关闭前和关闭后。**

**show.bs.modal 在 show 方法调用时立即触发。(Bootstrap)**  
 **shown.bs.modal 在模态框完全显示出来，并且等 CSS 动画完成之后触发。(Bootstrap)**  
 **hide.bs.modal 在 hide 方法调用时，但还未关闭隐藏时触发。(Bootstrap)**  
 **hidden.bs.modal 在模态框完全隐藏之后，并且等 CSS 动画完成之后触发。(Bootstrap)**  
 **loaded.bs.modal '远程数据加载完毕后触发(Bootstrap)**

**js**

[code]

    $( function () {
        $('#sdfg').on('click', function () {  //获取按钮执行点击事件
            $('#myModal').modal('show');      //点击按钮后将模态框，反转切换弹窗状态，也就是隐藏显示切换
        });
        $('#myModal').modal({
            backdrop:"static",  //背景存在黑灰透明遮罩，且点击空白不可关闭弹窗。
            keyboard:false,     //false，按 esc 键会不会关闭模态框
            show:false,         //如果是 false，初始化时，默认隐藏
        });
        $('#myModal').on('show.bs.modal', function () {
            alert('在 show 方法调用时立即触发！');
        });
        $('#myModal').on('shown.bs.modal', function () {
            alert('在模态框显示完毕后触发！');
        });
        $('#myModal').on('hide.bs.modal', function () {
            alert('在 hide 方法调用时立即触发！');
        });
        $('#myModal').on('hiden.bs.modal', function () {
            alert('在模态框显示完毕后触发！');
        });
        $('#myModal').on('loaded.bs.modal', function () {
            alert('远程数据加载完毕后触发！');
        });
    });
[/code]

**HTML**

[code]

     <div class="modal fade" id="myModal">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <h4 class="modal-title">会员登录</h4>
                </div>
                <!--在模态框主体里使用流体删格系统-->
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                            <div class="col-md-4">1</div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default">
                        注册
                    </button>
                    <button type="button" class="btn btn-primary">
                        登录
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <button class="btn btn-primary btn-lg" id="sdfg">
        点击弹窗
    </button>
[/code]



