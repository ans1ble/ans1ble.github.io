---
layout: post
title: " 第二百三十八节，Bootstrap输入框和导航组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap输入框和导航组件**



**学习要点：**

**1.输入框组件**

**2.导航组件**

**3.导航条组件**



**本节课我们主要学习一下Bootstrap的两个个组件功能：输入框组件和导航导航条组件。**



**一．输入框组件**

**文本输入框就是可以在 <input>元素前后加上文字或按钮，可以实现对表单控件的扩展。**

**在左侧添加文字**

**input-group-addon样式class类，写在input同级的span里，给输入框添加一个片段(Bootstrap)**  
 **input-group样式class类，写在input外层div里，将输入框和片段整合(Bootstrap)**

[code]

     <div class="input-group">
        <span class="input-group-addon">@</span>
        <input type="text" class="form-control">
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429213315709-1426727379.png)



**在右侧添加文字**

[code]

     <div class="input-group">
        <input type="text" class="form-control">
        <span class="input-group-addon">@</span>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429213815819-1424062260.png)



**在两侧添加文字**

[code]

     <div class="input-group">
        <span class="input-group-addon">$</span>
        <input type="text" class="form-control">
        <span class="input-group-addon">.00</span>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429213933569-1482870857.png)



**设置尺寸**

**input-group-lg样式class类，写在input外层div里，设置片段输入框大尺寸(Bootstrap)**  
 **input-group-xs样式class类，写在input外层div里，设置片段输入框中尺寸(Bootstrap)**  
 **input-group-sm样式class类，写在input外层div里，设置片段输入框小尺寸(Bootstrap)**

[code]

     <div class="input-group input-group-lg">
        <span class="input-group-addon">$</span>
        <input type="text" class="form-control">
        <span class="input-group-addon">.00</span>
    </div>
    <div class="input-group input-group-xs">
        <span class="input-group-addon">$</span>
        <input type="text" class="form-control">
        <span class="input-group-addon">.00</span>
    </div>
    <div class="input-group input-group-sm">
        <span class="input-group-addon">$</span>
        <input type="text" class="form-control">
        <span class="input-group-addon">.00</span>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429214651428-1712372548.png)



**左侧使用复选框和单选框，在片段里加入单选框或复选框标签即可**

[code]

     <div class="input-group">
        <span class="input-group-addon"><input type="checkbox"></span>
        <input type="text" class="form-control">
    </div>
    <div class="input-group">
        <span class="input-group-addon"><input type="radio"></span>
        <input type="text" class="form-control">
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429215153022-940455070.png)



**左侧使用按钮，在片段里加入按钮标签设置按钮样式即可**

**input-group-btn样式class类，写在input同级span里，设置输入框按钮片段(Bootstrap)**

[code]

     <div class="input-group">
        <span class="input-group-btn">
            <button type="button" class="btn btn-default">按钮</button>
        </span>
        <input type="text" class="form-control">
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429215731990-1556452483.png)



**左侧使用下拉菜单或分列式**

**divider样式class类，写在li里，隐藏当前元素(Bootstrap)**  
 **disabled样式class类，写在li里，禁用列表(Bootstrap)**

[code]

     <div class="input-group">
        <span class="input-group-btn">
            <button class="btn btn-default dropdown-toggle" data-toggle="dropdown">
                下拉菜单
                <span class="caret"></span>
            </button>
            <ul class="dropdown-menu">
                <li class="dropdown-header">网站导航</li>
                <li><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="divider"><a href="#">产品</a></li>
                <li class="disabled"><a href="#">关于</a></li>
            </ul>
        </span>
        <input type="text" class="form-control">
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429221243834-692395691.png)





**二．导航组件**

**Bootstrap 提供了一组导航组件，用于实现 Web 页面的栏目操作。**

**基本导航标签页**

**nav样式class类，写在ul里，设置导航基础样式(Bootstrap)**  
 **nav-tabs样式class类，写在ul里，设置标签样式导航(Bootstrap)**  
 **active样式class类，写在li里，首选项样式(Bootstrap)**

[code]

     <ul class="nav nav-tabs">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">产品</a></a></li>
        <li><a href="#">关于</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429222433881-2007097588.png)

**胶囊式导航**

**nav-pills样式class类，写在ul里，设置胶囊样式导航(Bootstrap)**

[code]

     <ul class="nav nav-pills">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">产品</a></a></li>
        <li><a href="#">关于</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429222712350-1243854482.png)





**垂直胶囊式导航**

**nav-stacked样式class类，写在ul里，设置垂直样式导航(Bootstrap)**

[code]

     <ul class="nav nav-pills nav-stacked">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">产品</a></a></li>
        <li><a href="#">关于</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429223252037-679036608.png)



**导航两端对齐**

**nav-justified样式class类，写在ul里，设置导航文字居中，并且导航自适应100%宽度显示(Bootstrap)**

[code]

     <ul class="nav nav-pills nav-justified">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">产品</a></a></li>
        <li><a href="#">关于</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429223915303-1691074946.png)





**禁用导航中的项目**

**disabled样式class类，写在li里，禁用导航中的项目(Bootstrap)**

[code]

     <ul class="nav nav-pills nav-justified">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li><a href="#">产品</a></a></li>
        <li class="disabled"><a href="#">关于</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429224153678-288084016.png)



**带下拉菜单的导航**

[code]

     <ul class="nav nav-tabs">
        <li class="active"><a href="#">首页</a></li>
        <li><a href="#">资讯</a></li>
        <li class="dropdown">
            <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                下拉菜单
                <span class="caret"></span>
            </a>
            <ul class="dropdown-menu">
                <li><a href="#">菜单一</a></li>
                <li><a href="#">菜单二</a></li>
            </ul>
        </li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429224504365-1828331461.png)





**三．导航条组件**

**导航条是网站中作为导航页头的响应式基础组件。**

**基本格式**

**navbar样式class类，写在 <nav>标签里，声明导航条(Bootstrap)**  
 **navbar-default样式class类，写在 <nav>标签里，设置导航条默认样式(Bootstrap)**

[code]

    <nav class="navbar navbar-default">
    导航
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429225547334-1211128086.png)



**反色调导航**

**navbar-inverse样式class类，写在 <nav>标签里，反色调导航样式(Bootstrap)**



[code]

    <nav class="navbar navbar-inverse">
    导航
    </nav>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429225738694-707296290.png)





**基本导航条，包含标题和列表**

**container样式class类，写在导航条里面的一级 <div>标签里，初始化导航内容样式(Bootstrap)**  
 **navbar-header样式class类，写在导航标题 <div>标签里，设置导航标题div样式，内置有一个左浮动(Bootstrap)**  
 **navbar-brand样式class类，写在导航标题 <div>标签里的<a>标签里，设置导航标题内容样式(Bootstrap)**  
 **navbar-nav样式class类，写在导航的 <ul>标签里，设置导航条里的导航样式(Bootstrap)**

[code]

    <nav class="navbar navbar-default">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
        </div>
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429232218131-1875615690.png)





**导航条中使用表单**

**navbar-form样式class类，写在导航条里 <form>标签里，设置导航条里的表单样式(Bootstrap)**  
 **navbar-left样式class类，写在导航条里元素标签里，设置导航条里元素左对齐(Bootstrap)**  
 **navbar-right样式class类，写在导航条里元素标签里，设置导航条里元素右对齐(Bootstrap)， 所有导航条里的区块元素都适用**

[code]

    <nav class="navbar navbar-default">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
            <form action="" class="navbar-form navbar-left">
                <div class="input-group">
                    <input type="text" class="form-control">
                    <span class="input-group-btn">
                        <button type="submit" class="btn btn-default">提交</button>
                    </span>
                </div>
            </form>
        </div>
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429233849037-33732323.png)



**导航中使用按钮**

**navbar-btn样式class类，写在导航条里 <button>标签里，设置导航条里的按钮样式(Bootstrap)**

[code]

    <nav class="navbar navbar-default">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
            <form action="" class="navbar-form navbar-right">
                <div class="input-group">
                    <input type="text" class="form-control">
                    <span class="input-group-btn">
                        <button type="submit" class="btn btn-default">提交</button>
                    </span>
                </div>
            </form>
            <button class="btn btn-default navbar-btn">按钮</button>
        </div>
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429234720475-475927484.png)



**导航中使用一段文本**

**navbar-text样式class类，写在导航条里 <p>标签里，设置导航条里的文本样式(Bootstrap)**

[code]

    <nav class="navbar navbar-default">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
            <form action="" class="navbar-form navbar-right">
                <div class="input-group">
                    <input type="text" class="form-control">
                    <span class="input-group-btn">
                        <button type="submit" class="btn btn-default">提交</button>
                    </span>
                </div>
            </form>
            <button class="btn btn-default navbar-btn">按钮</button>
            <p class="navbar-text">我是一段文本</p>
        </div>
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429235048240-1498389838.png)





**非导航链接，一般需要置入文本区域内**

**navbar-link样式class类，写在导航条里 <a>标签里，设置导航条里的非导航链接样式(Bootstrap)**

[code]

    <nav class="navbar navbar-default">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
            <form action="" class="navbar-form navbar-right">
                <div class="input-group">
                    <input type="text" class="form-control">
                    <span class="input-group-btn">
                        <button type="submit" class="btn btn-default">提交</button>
                    </span>
                </div>
            </form>
            <button class="btn btn-default navbar-btn">按钮</button>
            <p class="navbar-text"><a href="#" class=" **navbar-link** ">非导航链接</a></p>
        </div>
    </nav>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429235646506-1725585471.png)





**将导航固定在顶部，下面的内容会自动上移**

**navbar-fixed-top样式class类，写在 <nav>标签里，设置导航条固定在顶部(Bootstrap)**



[code]

    <nav class="navbar navbar-default navbar-fixed-top">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
        </div>
    </nav>
    <p>1</p><p>2</p><p>4</p><p>5</p><p>6</p><p>7</p><p>8</p><p>9</p><p>10</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430011058100-1771418488.png)



**将导航固定在底部**



**navbar-fixed-bottom样式class类，写在 <nav>标签里，设置导航条固定在底部(Bootstrap)**



[code]

    <nav class="navbar navbar-default navbar-fixed-bottom">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
        </div>
    </nav>
    <p>1</p><p>2</p><p>4</p><p>5</p><p>6</p><p>7</p><p>8</p><p>9</p><p>10</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430011309678-1007975436.png)







**静态导航，和页面等宽的导航条，去掉了圆角**

**navbar-static-top样式class类，写在 <nav>标签里，设置静态导航，和页面等宽的导航条，去掉了圆角(Bootstrap)**



[code]

    <nav class="navbar navbar-default navbar-static-top">
        <div class="container">
            <div class="navbar-header">
                <a href="#" class="navbar-brand">标题</a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li class="disabled"><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
        </div>
    </nav>
    <p>1</p><p>2</p><p>4</p><p>5</p><p>6</p><p>7</p><p>8</p><p>9</p><p>10</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
    <p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p><p>1</p>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430011601662-230898888.png)



