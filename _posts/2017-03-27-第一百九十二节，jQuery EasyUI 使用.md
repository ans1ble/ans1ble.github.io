---
layout: post
title: " 第一百九十二节，jQuery EasyUI 使用 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI 使用**



**学习要点：**

**1.引入必要的文件**

**2.加载 UI 组件的方式**

**3.使用 easyload.js 智能加载**

**4.Parser 解析器**



**本节课重点了解 EasyUI 的两种使用方法，包含不同的加载已经 easyload 智能按需加 载。最后了解一下 Parser 解析器的用法。**



**一．引入必要的文件**

[code]

         <!--引入 jQuery 核心库，这里采用的是 2.0-->
        <script type="text/javascript" src="jQueryEasyUI/jquery.min.js" charset="UTF-8"></script>
        <!--引入 jQuery EasyUI 核心库，这里采用的是 1.3.6-->
        <script type="text/javascript" src="jQueryEasyUI/jquery.easyui.min.js" charset="UTF-8"></script>
        <!--引入 EasyUI 中文提示信息-->
        <script type="text/javascript" src="jQueryEasyUI/locale/easyui-lang-zh_CN.js" charset="UTF-8"></script>
        <!--引入 EasyUI 核心 UI 文件 CSS-->
        <link rel="stylesheet" type="text/css" href="jQueryEasyUI/themes/default/easyui.css"/>
        <!--引入 EasyUI 图标文件-->
        <link rel="stylesheet" type="text/css" href="jQueryEasyUI/themes/icon.css"/>
[/code]

**PS：引入完毕后，我们就可以编写 jQuery EasyUI 代码了。**

** **

**二．加载 UI 组件的方式**

**加载 UI 组件有两种方式：** **1.使用 class 方式加载；2.使用 JS 调用加载。**

****1.使用 class 方式加载；****

****使用 class 加载，格式为：easyui-组件名****

[code]

     <div class="easyui-dialog" id="box" title="提示框" style="width:400px;height:200px;">
        内容部分
    </div>
[/code]

**PS：使用了规定的格式就可以生成一个 UI 组件，这是由于 jQuery EasyUI 的一个解析 器（Parser）的起到了作用。解析之后，从
Firebug 里面可以看到 UI 组件变化后的 HTML。**



****2.使用 JS 调用加载。【推荐】****

[code]

    $('#box').dialog();
[/code]

**PS：一般推荐使用第二种 JS 调用加载，因为一个 UI 组件有很多属性和方法，如果使 用 class 的用法将极大的不方便。并且根据 JS 和
HTML 分离的原则，第二种提高了代码的 可读性。**



**三．使用 easyload.js 智能加载【不推荐】**

**删除 jQuery EasyUI 的 JS 核心文件及 CSS，引入 easyloader.js 文件**

[code]

     <script type="text/javascript" src="easyui/jquery.min.js"></script>
    <script type="text/javascript" src="easyui/easyloader.js"></script>
[/code]

**easyloader.load()智能加载ui组件，参数第一个是组件名称，第二个是函数，在函数里写加载组件**



[code]

    easyloader.load('dialog', function () {
        $('#box').dialog();
    });
[/code]



**PS：使用 easyloader 智能加载，是根据你使用的 UI 组件按需加载。我们可以通过 Firebug 查看 HTML，发现加载了非常多的 js
文件，这些 js 都是 dialog 组件的必须条件。 所以，使用 easyloader 加载会减少不必要的内容加载。但问题是，使用智能加载，你编码
的难度和成本都提高了，效率降低，并且智能加载的 js 文件数量还是非常多的，并不会提 高太大的速度，反而因为 js 文件较多，被搜索引擎要求合并优化。**



**四．Parser 解析器**

**Parser 解析器是专门解析渲染各种 UI 组件了，一般来说，我们并不需要使用它即可 自动完成 UI
组件的解析工作。当然，有时可能在某些环境下需要手动解析的情况。 手动解析一般是使用 class 的情况下有效，比如设置 class="easyui-
dialog"。**

**Parser 属性**

**$.parser.auto 默认true 定义是否自动解析 EasyUI 组件**

[code]

    $( function () {
    
    
    });
    $.parser.auto = false;   //默认true 定义是否自动解析 EasyUI 组件
[/code]

放在$(function () {})外

  
**$.parser.parse() 空或 JQ 选择器 解析指定的 UI 组件**

[code]

    $( function () {
        $.parser.parse();     //解析指定的 UI 组件,没有传节点对象，就会解析所有ui
    });
    $.parser.auto = false;   //默认true 定义是否自动解析 EasyUI 组件
[/code]

PS：使用指定 UI 解析，必须要设置父类容器才可以解析到。比如：

[code]

    <div id="box">
        <div class="easyui-dialog" title="标题" style="width:400px;height:200px;">
        　　<span>内容部分</span>
        </div>
    </div>    
[/code]



  
**$.parser.onComplete回调函数 解析完毕后执行**

[code]

    $( function () {
        // $.parser.parse();     //解析指定的 UI 组件,没有传节点对象，就会解析所有ui
    });
    // $.parser.auto = false;   //默认true 定义是否自动解析 EasyUI 组件
    $.parser.onComplete = function () {
        alert('解析完毕后执行');
    };
[/code]

UI 组件解析完毕后执行，放在$(function () {})外



