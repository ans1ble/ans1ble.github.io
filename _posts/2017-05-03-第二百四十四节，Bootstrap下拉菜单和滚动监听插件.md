
---
layout: post
title: " 第二百四十四节，Bootstrap下拉菜单和滚动监听插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**Bootstrap下拉菜单和滚动监听插件**



**学习要点：**

**1.下拉菜单**

**2.滚动监听**



**本节课我们主要学习一下 Bootstrap 中的下拉菜单插件，这个插件在以组件的形式我们 已经学习过，那么现在来看看怎么和 JavaScript
交互的。**



**一．下拉菜单**

**声明式用法**

[code]

     <div class="dropdown">
        <button class="btn btn-primary" data-toggle="dropdown">
            下拉菜单
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

**声明式用法的关键核心：**

**1.外围容器使用 class="dropdown"包裹；**

**2.内部点击按钮事件绑定 data-toggle="dropdown"；**

**3.菜单元素使用 class="dropdown-menu"。**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503000329289-17949866.gif)**





**如果按钮在容器外部，可以通过 data-target 进行绑定。【不推荐】**

**  缺点列表位置需要手动自己调整**

[code]

    <div class="dropdown" id="dropdown">
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
    <button class="btn btn-primary" data-toggle="dropdown" data-target="#dropdown">
        下拉菜单
        <span class="caret"></span>
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503002342320-508190304.png)



**在 JavaScript 调用中**

**方法**

**dropdown()方法，将下拉菜单按钮执，行下拉菜单方法，在button元素使用(Bootstrap)**

**不推荐，下拉展开后无法隐藏**



[code]

    <div class="dropdown" id="dropdown">
        <button class="btn btn-primary" id="ann">
            下拉菜单
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]



**js**

[code]

    $( function () {
        $('#ann').dropdown();
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503003759336-842604291.png)







  
**toggle将下拉菜单默认展开，在button元素使用(Bootstrap)**

**不推荐，默认是展开的，也无法隐藏**

[code]

     <div class="dropdown" id="dropdown">
        <button class="btn btn-primary" id="ann">
            下拉菜单
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

**js**

[code]

    $( function () {
        $('#ann').dropdown('toggle');
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503004105367-114682507.png)





**事件**

**下拉菜单支持 4 种事件，分别对应弹出前、弹出后、关闭前和关闭后。**

**show.bs.dropdown 在 show 方法调用时立即触发。(Bootstrap)**  
 **shown.bs.dropdown 在下拉菜单完全显示出来，并且等 CSS 动画完成之后触发。(Bootstrap)**  
 **hide.bs.dropdown 在 hide 方法调用时，但还未关闭隐藏时触发。(Bootstrap)**  
 **hidden.bs.dropdown 在下拉菜单完全隐藏之后，并且等 CSS 动画完成之后触发。(Bootstrap)**

[code]

     <div class="dropdown" id="dropdown">
        <button class="btn btn-primary" data-toggle="dropdown">
            下拉菜单
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

**js**

[code]

    $( function () {
        $('#dropdown').on('show.bs.dropdown', function () {
            alert('在调用 show 方法时立即触发！');
        });
        $('#dropdown').on('shown.bs.dropdown', function () {
            alert('在下拉菜单完全显示出来，并且等 CSS 动画完成之后触发！');
        });
        $('#dropdown').on('hide.bs.dropdown', function () {
            alert('在 hide 方法调用时，但还未关闭隐藏时触发！');
        });
        $('#dropdown').on('hidden.bs.dropdown', function () {
            alert('在下拉菜单完全隐藏之后，并且等 CSS 动画完成之后触发！');
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503004935007-209915506.png)





**二．滚动监听**

**滚动监听插件是用来根据滚动条所处在的位置自动更新导航项目，显示导航项目高亮显示。**

**基本实例**

**实现滚动监听，将导航条 li标签里的a标签的href=对应文本标题h4标签的id即可**

[code]

    <nav id="nav" class="navbar navbar-default">                        <!--声明导航，设置导航默认样式-->
        <a href="#" class="navbar-brand">Web 开发</a>                   <!--设置导航标题样式-->
        <ul class="nav navbar-nav">                                     <!--设置导航里的导航样式-->
            <li><a href=" **#html5** ">HTML5</a></li>
            <li><a href=" **#bootstrap** ">Bootstrap</a></li>
            <li class="dropdown">                                       <!--设置声明一个下来列表-->
                <a href="#" data-toggle="dropdown">                     <!--点击打开下来列表-->
                    JavaScript
                    <span class="caret"></span>                         <!--设置一个三角样式-->
                </a>
                <ul class="dropdown-menu">                              <!--设置下来列表样式-->
                    <li><a href=" **#jquery** ">jQuery</a></li>
                    <li><a href=" **#yui** ">Yui</a></li>
                    <li><a href=" **#extjs** ">Extjs</a></li>
                </ul>
            </li>
        </ul>
    </nav>
    <div style="height: 200px; overflow: auto; position: relative;padding: 0 10px;">
        <h4 id="html5">HTML5</h4>
        <p>标准通用标记语言下的一个应用 HTML 标准自 1999 年 12 月发布的 HTML4.01
            后，后继的 HTML5 和其它标准被束之高阁，为了推动 Web 标准化运动的发展，一些公司联
            合起来，成立了一个叫做 Web Hypertext Application Technology Working Group
            （Web 超文本应用技术工作组 -WHATWG） 的组织。WHATWG 致力于 Web 表单和应用程序，
            而 W3C（World Wide Web Consortium，万维网联盟） 专注于 XHTML2.0。在 2006 年，
            双方决定进行合作，来创建一个新版本的 HTML。</p>
        <h4 id="bootstrap">Bootstrap</h4>
        <p>Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基
            于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[1] 它由 Twitter
            的设计师 Mark Otto 和 Jacob Thornton 合作开发，是一个 CSS/HTML 框架。Bootstrap
            提供了优雅的 HTML 和 CSS 规范，它即是由动态 CSS 语言 Less 写成。Bootstrap 一经推出
            后颇受欢迎，一直是 GitHub 上的热门开源项目，包括 NASA 的 MSNBC（微软全国广播公司）
            的 Breaking News 都使用了该项目。[2] 国内一些移动开发者较为熟悉的框架，如 WeX5
            前端开源框架等，也是基于 Bootstrap 源码进行性能优化而来。[3] </p>
        <h4 id="jquery">jQuery</h4>
        <p>JQuery 是继 prototype 之后又一个优秀的 Javascript 库。它是轻量级的 js
            库 ，它兼容 CSS3，还兼容各种浏览器（IE 6.0+, FF 1.5+, Safari 2.0+, Opera 9.0+），
            jQuery2.0 及后续版本将不再支持 IE6/7/8 浏览器。jQuery 使用户能更方便地处理 HTML
            （标准通用标记语言下的一个应用）、events、实现动画效果，并且方便地为网站提供 AJAX
            交互。jQuery 还有一个比较大的优势是，它的文档说明很全，而且各种应用也说得很详细，
            同时还有许多成熟的插件可供选择。jQuery 能够使用户的 html 页面保持代码和 html 内容
            分离，也就是说，不用再在 html 里面插入一堆 js 来调用命令了，只需要定义 id 即可。</p>
        <h4 id="yui">Yui</h4>
        <p>近几年随着 jQuery、Ext 以及 CSS3 的发展，以 Bootstrap 为代表的前端
            开发框架如雨后春笋般挤入视野，可谓应接不暇。不论是桌面浏览器端还是移动端都涌现出
            很多优秀的框架，极大丰富了开发素材，也方便了大家的开发。这些框架各有特点，本文对
            这些框架进行初步的介绍与比较，希望能够为大家选择框架提供一点帮助，也为后续详细研
            究这些框架的抛砖引玉。</p>
        <h4 id="extjs">Extjs</h4>
        <p>ExtJS 可以用来开发 RIA 也即富客户端的 AJAX 应用，是一个用 javascript
            写的，主要用于创建前端用户界面，是一个与后台技术无关的前端 ajax 框架。因此，可以
            把 ExtJS 用在.Net、Java、Php 等各种开发语言开发的应用中。ExtJs 最开始基于 YUI 技
            术，由开发人员 JackSlocum 开发，通过参考 JavaSwing 等机制来组织可视化组件，无论
            从 UI 界面上 CSS 样式的应用，到数据解析上的异常处理，都可算是一款不可多得的
            JavaScript 客户端技术的精品。</p>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503025651070-1610589826.png)





**滚动监听属性，都是写在监听内容区域最外层div里**

**data-offset 默认值为 10，固定内容距滚动容器 10 像素以内，
也就是内容出现多少像素高亮对应菜单，一般会设置成0。(Bootstrap)**  
 **data-spy 设置 scroll，将设置滚动容器监听。 必须否则将不会监听(Bootstrap)**  
 **data-target 设置#nav，绑定指定监听的菜单的id， 防止监听多个菜单(Bootstrap)**

[code]

    <nav id="nav" class="navbar navbar-default">                        <!--声明导航，设置导航默认样式-->
        <a href="#" class="navbar-brand">Web 开发</a>                   <!--设置导航标题样式-->
        <ul class="nav navbar-nav">                                     <!--设置导航里的导航样式-->
            <li><a href="#html5">HTML5</a></li>
            <li><a href="#bootstrap">Bootstrap</a></li>
            <li class="dropdown">                                       <!--设置声明一个下来列表-->
                <a href="#" data-toggle="dropdown">                     <!--点击打开下来列表-->
                    JavaScript
                    <span class="caret"></span>                         <!--设置一个三角样式-->
                </a>
                <ul class="dropdown-menu">                              <!--设置下来列表样式-->
                    <li><a href="#jquery">jQuery</a></li>
                    <li><a href="#yui">Yui</a></li>
                    <li><a href="#extjs">Extjs</a></li>
                </ul>
            </li>
        </ul>
    </nav>
    <div data-target="#nav" data-offset="0" data-spy="scroll" style="height: 200px; overflow: auto; position: relative;">
        <h4 id="html5">HTML5</h4>
        <p>标准通用标记语言下的一个应用 HTML 标准自 1999 年 12 月发布的 HTML4.01
            后，后继的 HTML5 和其它标准被束之高阁，为了推动 Web 标准化运动的发展，一些公司联
            合起来，成立了一个叫做 Web Hypertext Application Technology Working Group
            （Web 超文本应用技术工作组 -WHATWG） 的组织。WHATWG 致力于 Web 表单和应用程序，
            而 W3C（World Wide Web Consortium，万维网联盟） 专注于 XHTML2.0。在 2006 年，
            双方决定进行合作，来创建一个新版本的 HTML。</p>
        <h4 id="bootstrap">Bootstrap</h4>
        <p>Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基
            于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[1] 它由 Twitter
            的设计师 Mark Otto 和 Jacob Thornton 合作开发，是一个 CSS/HTML 框架。Bootstrap
            提供了优雅的 HTML 和 CSS 规范，它即是由动态 CSS 语言 Less 写成。Bootstrap 一经推出
            后颇受欢迎，一直是 GitHub 上的热门开源项目，包括 NASA 的 MSNBC（微软全国广播公司）
            的 Breaking News 都使用了该项目。[2] 国内一些移动开发者较为熟悉的框架，如 WeX5
            前端开源框架等，也是基于 Bootstrap 源码进行性能优化而来。[3] </p>
        <h4 id="jquery">jQuery</h4>
        <p>JQuery 是继 prototype 之后又一个优秀的 Javascript 库。它是轻量级的 js
            库 ，它兼容 CSS3，还兼容各种浏览器（IE 6.0+, FF 1.5+, Safari 2.0+, Opera 9.0+），
            jQuery2.0 及后续版本将不再支持 IE6/7/8 浏览器。jQuery 使用户能更方便地处理 HTML
            （标准通用标记语言下的一个应用）、events、实现动画效果，并且方便地为网站提供 AJAX
            交互。jQuery 还有一个比较大的优势是，它的文档说明很全，而且各种应用也说得很详细，
            同时还有许多成熟的插件可供选择。jQuery 能够使用户的 html 页面保持代码和 html 内容
            分离，也就是说，不用再在 html 里面插入一堆 js 来调用命令了，只需要定义 id 即可。</p>
        <h4 id="yui">Yui</h4>
        <p>近几年随着 jQuery、Ext 以及 CSS3 的发展，以 Bootstrap 为代表的前端
            开发框架如雨后春笋般挤入视野，可谓应接不暇。不论是桌面浏览器端还是移动端都涌现出
            很多优秀的框架，极大丰富了开发素材，也方便了大家的开发。这些框架各有特点，本文对
            这些框架进行初步的介绍与比较，希望能够为大家选择框架提供一点帮助，也为后续详细研
            究这些框架的抛砖引玉。</p>
        <h4 id="extjs">Extjs</h4>
        <p>ExtJS 可以用来开发 RIA 也即富客户端的 AJAX 应用，是一个用 javascript
            写的，主要用于创建前端用户界面，是一个与后台技术无关的前端 ajax 框架。因此，可以
            把 ExtJS 用在.Net、Java、Php 等各种开发语言开发的应用中。ExtJs 最开始基于 YUI 技
            术，由开发人员 JackSlocum 开发，通过参考 JavaSwing 等机制来组织可视化组件，无论
            从 UI 界面上 CSS 样式的应用，到数据解析上的异常处理，都可算是一款不可多得的
            JavaScript 客户端技术的精品。</p>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503164959961-1725575915.gif)



**使用js方式定义以上监听属性**

**scrollspy()方法，将菜单执行滚动监听，在内容区域最外层div上使用(Bootstrap)**  
 **offset滚动监听属性，设置内容出现多少像素高亮对应菜单，一般会设置成0(Bootstrap)**  
 **target滚动监听属性，绑定指定监听的菜单的id，防止监听多个菜单(Bootstrap)**

**js**

[code]

    $( function () {
        $('#content').scrollspy({       //获取内容区域执行滚动监听
            offset: 0,                  //设置内容出现多少像素高亮对应菜单，一般会设置成0
            target: '#nav',             //绑定指定监听的菜单的id，防止监听多个菜单
        });
    });
[/code]

**html**

[code]

     <nav id="nav" class="navbar navbar-default">                        <!--声明导航，设置导航默认样式-->
        <a href="#" class="navbar-brand">Web 开发</a>                   <!--设置导航标题样式-->
        <ul class="nav navbar-nav">                                     <!--设置导航里的导航样式-->
            <li><a href="#html5">HTML5</a></li>
            <li><a href="#bootstrap">Bootstrap</a></li>
            <li class="dropdown">                                       <!--设置声明一个下来列表-->
                <a href="#" data-toggle="dropdown">                     <!--点击打开下来列表-->
                    JavaScript
                    <span class="caret"></span>                         <!--设置一个三角样式-->
                </a>
                <ul class="dropdown-menu">                              <!--设置下来列表样式-->
                    <li><a href="#jquery">jQuery</a></li>
                    <li><a href="#yui">Yui</a></li>
                    <li><a href="#extjs">Extjs</a></li>
                </ul>
            </li>
        </ul>
    </nav>
    <div id="content" style="height: 200px; overflow: auto; position: relative;">
        <h4 id="html5">HTML5</h4>
        <p>标准通用标记语言下的一个应用 HTML 标准自 1999 年 12 月发布的 HTML4.01
            后，后继的 HTML5 和其它标准被束之高阁，为了推动 Web 标准化运动的发展，一些公司联
            合起来，成立了一个叫做 Web Hypertext Application Technology Working Group
            （Web 超文本应用技术工作组 -WHATWG） 的组织。WHATWG 致力于 Web 表单和应用程序，
            而 W3C（World Wide Web Consortium，万维网联盟） 专注于 XHTML2.0。在 2006 年，
            双方决定进行合作，来创建一个新版本的 HTML。</p>
        <h4 id="bootstrap">Bootstrap</h4>
        <p>Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基
            于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[1] 它由 Twitter
            的设计师 Mark Otto 和 Jacob Thornton 合作开发，是一个 CSS/HTML 框架。Bootstrap
            提供了优雅的 HTML 和 CSS 规范，它即是由动态 CSS 语言 Less 写成。Bootstrap 一经推出
            后颇受欢迎，一直是 GitHub 上的热门开源项目，包括 NASA 的 MSNBC（微软全国广播公司）
            的 Breaking News 都使用了该项目。[2] 国内一些移动开发者较为熟悉的框架，如 WeX5
            前端开源框架等，也是基于 Bootstrap 源码进行性能优化而来。[3] </p>
        <h4 id="jquery">jQuery</h4>
        <p>JQuery 是继 prototype 之后又一个优秀的 Javascript 库。它是轻量级的 js
            库 ，它兼容 CSS3，还兼容各种浏览器（IE 6.0+, FF 1.5+, Safari 2.0+, Opera 9.0+），
            jQuery2.0 及后续版本将不再支持 IE6/7/8 浏览器。jQuery 使用户能更方便地处理 HTML
            （标准通用标记语言下的一个应用）、events、实现动画效果，并且方便地为网站提供 AJAX
            交互。jQuery 还有一个比较大的优势是，它的文档说明很全，而且各种应用也说得很详细，
            同时还有许多成熟的插件可供选择。jQuery 能够使用户的 html 页面保持代码和 html 内容
            分离，也就是说，不用再在 html 里面插入一堆 js 来调用命令了，只需要定义 id 即可。</p>
        <h4 id="yui">Yui</h4>
        <p>近几年随着 jQuery、Ext 以及 CSS3 的发展，以 Bootstrap 为代表的前端
            开发框架如雨后春笋般挤入视野，可谓应接不暇。不论是桌面浏览器端还是移动端都涌现出
            很多优秀的框架，极大丰富了开发素材，也方便了大家的开发。这些框架各有特点，本文对
            这些框架进行初步的介绍与比较，希望能够为大家选择框架提供一点帮助，也为后续详细研
            究这些框架的抛砖引玉。</p>
        <h4 id="extjs">Extjs</h4>
        <p>ExtJS 可以用来开发 RIA 也即富客户端的 AJAX 应用，是一个用 javascript
            写的，主要用于创建前端用户界面，是一个与后台技术无关的前端 ajax 框架。因此，可以
            把 ExtJS 用在.Net、Java、Php 等各种开发语言开发的应用中。ExtJs 最开始基于 YUI 技
            术，由开发人员 JackSlocum 开发，通过参考 JavaSwing 等机制来组织可视化组件，无论
            从 UI 界面上 CSS 样式的应用，到数据解析上的异常处理，都可算是一款不可多得的
            JavaScript 客户端技术的精品。</p>
    </div>
[/code]





**滚动监听事件**

**activate.bs.scrollspy 每当一个新条目被激活后都将由滚动监听插件触发此事件。在菜单最外层div上使用(Bootstrap)**

[code]

    $( function () {
        $('#content').scrollspy({       //获取内容区域执行滚动监听
            offset: 0,                  //设置内容出现多少像素高亮对应菜单，一般会设置成0
            target: '#nav',             //绑定指定监听的菜单的id，防止监听多个菜单
        });
        $('#nav').on('activate.bs.scrollspy', function () {
            alert('新条目被激活后触发此事件！');
        });
    });
[/code]





****更** 新容器方法**

**删除内容时，刷新一下 DOM，避免导航监听错位**

**注意：此方法只有在内容div的html里写属性才有效 <div data-target="#nav" data-offset="0" data-
spy="scroll"> **

**refresh 更新容器 DOM 的方法。在菜单最外层div上使用(Bootstrap)**

**js**

[code]

    $( function () {
        $('#html5 a').click(function () {          //获取id为html5下面的a标签，执行一个点击事件
            removeSec(this);                       //点击后执行removeSec方法，将当前点击元素传递到方法
        });
        function removeSec(e) {                    //定义removeSec方法
            $(e).parents('.sec').remove();         //获取到点击元素上面class为sec的元素删除节点
            $('#content').scrollspy('refresh');    //refresh更新容器方法，获取到内容区域更新一下容器
        }
    });
[/code]

**HTML**



[code]

    <nav id="nav" class="navbar navbar-default">                        <!--声明导航，设置导航默认样式-->
        <a href="#" class="navbar-brand">Web 开发</a>                   <!--设置导航标题样式-->
        <ul class="nav navbar-nav">                                     <!--设置导航里的导航样式-->
            <li><a href="#html5">HTML5</a></li>
            <li><a href="#bootstrap">Bootstrap</a></li>
            <li class="dropdown">                                       <!--设置声明一个下来列表-->
                <a href="#" data-toggle="dropdown">                     <!--点击打开下来列表-->
                    JavaScript
                    <span class="caret"></span>                         <!--设置一个三角样式-->
                </a>
                <ul class="dropdown-menu">                              <!--设置下来列表样式-->
                    <li><a href="#jquery">jQuery</a></li>
                    <li><a href="#yui">Yui</a></li>
                    <li><a href="#extjs">Extjs</a></li>
                </ul>
            </li>
        </ul>
    </nav>
    <div id="content" data-target="#nav" data-offset="0" data-spy="scroll" style="height: 200px; overflow: auto; position: relative;">
        <section class="sec">
            <h4 id="html5">HTML5<a href="#" >删除此项</a></h4>
            <p>标准通用标记语言下的一个应用 HTML 标准自 1999 年 12 月发布的 HTML4.01
                后，后继的 HTML5 和其它标准被束之高阁，为了推动 Web 标准化运动的发展，一些公司联
                合起来，成立了一个叫做 Web Hypertext Application Technology Working Group
                （Web 超文本应用技术工作组 -WHATWG） 的组织。WHATWG 致力于 Web 表单和应用程序，
                而 W3C（World Wide Web Consortium，万维网联盟） 专注于 XHTML2.0。在 2006 年，
                双方决定进行合作，来创建一个新版本的 HTML。</p>
        </section>
        <section class="sec">
            <h4 id="bootstrap">Bootstrap</h4>
            <p>Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基
                于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。[1] 它由 Twitter
                的设计师 Mark Otto 和 Jacob Thornton 合作开发，是一个 CSS/HTML 框架。Bootstrap
                提供了优雅的 HTML 和 CSS 规范，它即是由动态 CSS 语言 Less 写成。Bootstrap 一经推出
                后颇受欢迎，一直是 GitHub 上的热门开源项目，包括 NASA 的 MSNBC（微软全国广播公司）
                的 Breaking News 都使用了该项目。[2] 国内一些移动开发者较为熟悉的框架，如 WeX5
                前端开源框架等，也是基于 Bootstrap 源码进行性能优化而来。[3] </p>
        </section>
        <section class="sec">
            <h4 id="jquery">jQuery</h4>
            <p>JQuery 是继 prototype 之后又一个优秀的 Javascript 库。它是轻量级的 js
                库 ，它兼容 CSS3，还兼容各种浏览器（IE 6.0+, FF 1.5+, Safari 2.0+, Opera 9.0+），
                jQuery2.0 及后续版本将不再支持 IE6/7/8 浏览器。jQuery 使用户能更方便地处理 HTML
                （标准通用标记语言下的一个应用）、events、实现动画效果，并且方便地为网站提供 AJAX
                交互。jQuery 还有一个比较大的优势是，它的文档说明很全，而且各种应用也说得很详细，
                同时还有许多成熟的插件可供选择。jQuery 能够使用户的 html 页面保持代码和 html 内容
                分离，也就是说，不用再在 html 里面插入一堆 js 来调用命令了，只需要定义 id 即可。</p>
        </section>
        <section class="sec">
            <h4 id="yui">Yui</h4>
            <p>近几年随着 jQuery、Ext 以及 CSS3 的发展，以 Bootstrap 为代表的前端
                开发框架如雨后春笋般挤入视野，可谓应接不暇。不论是桌面浏览器端还是移动端都涌现出
                很多优秀的框架，极大丰富了开发素材，也方便了大家的开发。这些框架各有特点，本文对
                这些框架进行初步的介绍与比较，希望能够为大家选择框架提供一点帮助，也为后续详细研
                究这些框架的抛砖引玉。</p>
        </section>
        <section class="sec">
            <h4 id="extjs">Extjs</h4>
            <p>ExtJS 可以用来开发 RIA 也即富客户端的 AJAX 应用，是一个用 javascript
                写的，主要用于创建前端用户界面，是一个与后台技术无关的前端 ajax 框架。因此，可以
                把 ExtJS 用在.Net、Java、Php 等各种开发语言开发的应用中。ExtJs 最开始基于 YUI 技
                术，由开发人员 JackSlocum 开发，通过参考 JavaSwing 等机制来组织可视化组件，无论
                从 UI 界面上 CSS 样式的应用，到数据解析上的异常处理，都可算是一款不可多得的
                JavaScript 客户端技术的精品。</p>
        </section>
    </div>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503181118773-824560948.gif)



