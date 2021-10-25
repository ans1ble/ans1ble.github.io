---
layout: post
title: " 第二百三十七节，Bootstrap图标菜单按钮组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap图标菜单按钮组件**



**学习要点：**

**1.小图标组件**

**2.下拉菜单组件**

**3.按钮组组件**

**4.按钮式下拉菜单**



**本节课我们主要学习一下 Bootstrap 的三个组件功能：小图标组件、下拉菜单组件和各 种按钮组件。**



**一．小图标组件**

**Bootstrap 提供了免费的 263 个小图标（数了两次），具体可以参考中文官网的组件
链接：http://v3.bootcss.com/components/#glyphicons。**

**所有图标**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429154429725-1055379417.png)**





**图标使用方法**

**我们建议使用 <i>或<span>标签来配合使用图标**

**使用图标要定义两个class参数，glyphicon（声明图标样式），参数2要使用的图标名称**

**glyphicon样式class类，写在 <i>或<span>里，声明图标样式，第二个参数图标名称(Bootstrap)**



[code]

    <i class="glyphicon glyphicon-user a"></i>
    <span class="glyphicon glyphicon-trash a"></span>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429155801881-1033549963.png)





**也可以结合按钮图标**



[code]

    <button class="btn btn-default btn-lg">
        <span class="glyphicon glyphicon-star"></span>
    </button>
    <button class="btn btn-default btn">
        <span class="glyphicon glyphicon-star"></span>
    </button>
    <button class="btn btn-default btn-sm">
        <span class="glyphicon glyphicon-star"></span>
    </button>
    <button class="btn btn-default btn-xs">
        <span class="glyphicon glyphicon-star"></span>
    </button>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429160202834-117757641.png)









**二．下拉菜单组件**

**下拉菜单，就是点击一个元素或按钮，触发隐藏的列表显示出来。**

**dropdown样式class类，写在下拉菜单 <div>里，声明下拉菜单div(Bootstrap)**  
 **data-toggle="dropdown"属性和值，写在下拉菜单 <div>里，点击后展开下拉菜单(Bootstrap)**  
 **dropdown-menu样式class类，写在下拉菜单 <div>里的<ul>里，将列表关联下拉菜单(Bootstrap)**

[code]

    <div class="dropdown">                                          <!--dropdown声明下拉菜单div-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429162409490-161341320.png)

**按钮和菜单需要包裹在.dropdown 的容器里，而作为被点击的元素按钮需要设置 data-
toggle="dropdown"才能有效。对于菜单部分，设置 class="dropdown-menu"才能 自动隐藏并添加固定样式。设置
class="caret"表示箭头，可上可下。**



**设置下拉菜单设置向上触发**

**dropup样式class类，写在下拉菜单 <div>里，声明下拉菜单向上触发(Bootstrap)**

[code]

    <div class="dropup">                                          <!--dropup声明下拉菜单向上触发-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429163436037-2124109250.png)



**菜单项居右对齐，默认值是 dropdown-menu-left**

**dropdown-menu-left样式class类，写在下拉菜单 <ul>里，菜单左对齐(Bootstrap)**  
 **dropdown-menu-right样式class类，写在下拉菜单 <ul>里，菜单右对齐，以100%尺寸右对齐(Bootstrap)**

[code]

    <div class="dropdown">                                          <!--dropdown声明下拉菜单-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu dropdown-menu-right">              <!--将列表关联下拉菜单-->
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429164325428-1791589121.png)







**设置菜单的标题，不要加超链接**

**dropdown-header样式class类，写在下拉菜单 <li>里，设置菜单标题，会自动去除超链接(Bootstrap)**

[code]

    <div class="dropdown">                                          <!--dropdown声明下拉菜单-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li class="dropdown-header">网站导航</li>
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429165003694-1507754652.png)



**设置菜单的分割线**

**divider样式class类，写在下拉菜单 <li>里，设置菜单的分割线(Bootstrap)**

[code]

    <div class="dropdown">                                          <!--dropdown声明下拉菜单-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li class="dropdown-header">网站导航</li>
            <li class="divider"></li>
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429165623553-2069444764.png)





**设置菜单的禁用项**

**disabled样式class类，写在下拉菜单 <li>里，设置菜单的禁用项(Bootstrap)**

[code]

    <div class="dropdown">                                          <!--dropdown声明下拉菜单-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li class="dropdown-header">网站导航</li>
            <li class="divider"></li>
            <li><a href="#">首页</a></li>
            <li class="disabled"><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429165935881-471813930.png)



**让菜单默认显示**

**open样式class类，写在声明下拉菜单 <div>里，让菜单默认显示(Bootstrap)**

[code]

    <div class="dropdown open">                                          <!--dropdown声明下拉菜单-->
        <button class="btn btn-default" data-toggle="dropdown">     <!--data-toggle="dropdown"点击后展开下拉菜单-->
            下拉菜单
            <span class="caret"></span>                             <!--三角图标-->
        </button>
        <ul class="dropdown-menu">                                  <!--将列表关联下拉菜单-->
            <li class="dropdown-header">网站导航</li>
            <li class="divider"></li>
            <li><a href="#">首页</a></li>
            <li class="disabled"><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429170200240-1130347380.png)





**三．按钮组组件**

**按钮组就是多个按钮集成在一个容器里形成独有的效果。**

**btn-group样式class类，写在群组按钮 <div>里，将多个按钮群组在一起(Bootstrap)**

[code]

    <div class="btn-group">
        <button type="button" class="btn btn-default">左</button>
        <button type="button" class="btn btn-default">中</button>
        <button type="button" class="btn btn-default">右</button>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429170809772-776957853.png)



**将多个按钮组整合起来便于管理**

**btn-toolbar样式class类，写在最外层 <div>里，将多个按钮群组，在群组在一起(Bootstrap)**

[code]

    <div class="btn-toolbar">
        <div class="btn-group">
            <button type="button" class="btn btn-default">左</button>
            <button type="button" class="btn btn-default">中</button>
            <button type="button" class="btn btn-default">右</button>
        </div>
        <div class="btn-group">
            <button type="button" class="btn btn-default">1</button>
            <button type="button" class="btn btn-default">2</button>
            <button type="button" class="btn btn-default">3</button>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429171352475-69392722.png)



**设置按钮组大小**

**btn-group-lg样式class类，写在按钮组 <div>里，将一组按钮设置大尺寸(Bootstrap)**  
 **btn-group-sm样式class类，写在按钮组 <div>里，将一组按钮设置中尺寸(Bootstrap)**  
 **btn-group-xs样式class类，写在按钮组 <div>里，将一组按钮设置小尺寸(Bootstrap)**

[code]

    <div class="btn-toolbar">
        <div class="btn-group btn-group-lg">
            <button type="button" class="btn btn-default">左</button>
            <button type="button" class="btn btn-default">中</button>
            <button type="button" class="btn btn-default">右</button>
        </div>
        <div class="btn-group btn-group-sm">
            <button type="button" class="btn btn-default">1</button>
            <button type="button" class="btn btn-default">2</button>
            <button type="button" class="btn btn-default">3</button>
        </div>
            <div class="btn-group btn-group-xs">
            <button type="button" class="btn btn-default">4</button>
            <button type="button" class="btn btn-default">5</button>
            <button type="button" class="btn btn-default">6</button>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429180448444-596757457.png)





**嵌套一个分组，比如下拉菜单**

**dropdown-toggle样式class类，写在按钮 <button>里，声明一个按钮式下拉菜单(Bootstrap)**

[code]

    <div class="btn-group">
        <button type="button" class="btn btn-default">左</button>
        <button type="button" class="btn btn-default">中</button>
        <button type="button" class="btn btn-default">右</button>
        <div class="btn-group">
            <button class="btn btn-default dropdown-toggle"
                    data-toggle="dropdown">
                下拉菜单
                <span class="caret"></span>
            </button>
            <ul class="dropdown-menu">
                <li><a href="#">首页</a></li>
                <li><a href="#">资讯</a></li>
                <li><a href="#">产品</a></li>
                <li><a href="#">关于</a></li>
            </ul>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429181544006-1356057896.png)

**注意：这里中并没有实现 class="dropdown"，通过源码分析知道嵌套本身已经 有定位就不需要再设置。而右边的圆角只要多加一个
class="dropdown-toggle"即可。**





**设置按钮组垂直排列**

**btn-group-vertical样式class类，写在群组 <div>里，将按钮群组并且按钮垂直排列(Bootstrap)**

[code]

    <div class="btn-group-vertical">
        <button type="button" class="btn btn-default">左</button>
        <button type="button" class="btn btn-default">中</button>
        <button type="button" class="btn btn-default">右</button>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429182033350-1390556353.png)



**设置两端对齐按钮组，使用 <a>标签**

**btn-group-justified样式class类，写在群组
<div>里，将按a标签按钮群组，按钮在群组里100%宽度显示(Bootstrap)**

**注意：此类只能在a标签使用，如果button标签有用，就必须给每个button群组**

[code]

     <div class="btn-group-justified">
        <a type="button" class="btn btn-default">左</a>
        <a type="button" class="btn btn-default">中</a>
        <a type="button" class="btn btn-default">右</a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429183425256-2018647480.png)



****btn-group-justified样式** 如果需要使用<button>标签，则需要对每个按钮进行群组**

[code]

    <div class="btn-group-justified">
        <div class="btn-group">
            <button type="button" class="btn btn-default">左</button>
        </div>
        <div class="btn-group">
            <button type="button" class="btn btn-default">中</button>
        </div>
        <div class="btn-group">
            <button type="button" class="btn btn-default">右</button>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429184031506-915938656.png)





**四．按钮式下拉菜单**

**这个下拉菜单其实和第二个知识点一样，只不过，这个是在群组里，不需要声明 class="dropdown"。**

**群组按钮下拉菜单**

[code]

     <div class="btn-group">
        <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            下拉菜单
            <span class="caret"></span>  
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429184616475-296821489.png)



**分裂式按钮下拉菜单**

[code]

     <div class="btn-group">
        <button type="button" class="btn btn-default">
            下拉菜单
        </button>
        <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429185402162-2075282539.png)



**向上弹出式**

[code]

     <div class="btn-group dropup">
        <button type="button" class="btn btn-default">
            下拉菜单
        </button>
        <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown">
            <span class="caret"></span>
        </button>
        <ul class="dropdown-menu">
            <li><a href="#">首页</a></li>
            <li><a href="#">资讯</a></li>
            <li><a href="#">产品</a></li>
            <li><a href="#">关于</a></li>
        </ul>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170429185603084-1762998671.png)



