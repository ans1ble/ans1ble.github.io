---
layout: post
title: " 第二百三十九节，Bootstrap路径分页标签和徽章组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap路径分页标签和徽章组件**



**学习要点：**

**1.路径组件**

**2.分页组件**

**3.标签组件**

**4.徽章组件**



**本节课我们主要学习一下 Bootstrap 的四个组件功能：路径组件、分页组件、标签组件 和徽章组件。**



**一．路径组件**

**路径组件也叫做面包屑导航。**

**面包屑导航**

**breadcrumb样式class类，写在 <ul>或<ol>里，设置面包屑导航(Bootstrap)**

[code]

    <ol class="breadcrumb">
        <li><a href="#">首页</a></li>
        <li><a href="#">产品列表</a></li>
        <li class="active">韩版 2015 年羊绒毛衣</li>
    </ol>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430165933975-193592395.png)





**二．分页组件**

**分页组件可以提供带有展示页面的功能。**

**默认分页**

**pagination样式class类，写在 <ul>里，设置默认分页样式(Bootstrap)**

[code]

    <ul class="pagination">
        <li><a href="#">&laquo;</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">&raquo;</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430170514772-719631435.png)



**首选项和禁用**

**active样式class类，写在 <li>里，首选项样式(Bootstrap)**  
 **disabled样式class类，写在 <li>里，禁用项样式(Bootstrap)**

[code]

    <ul class="pagination">
        <li><a href="#">&laquo;</a></li>
        <li class="active"><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li class="disabled"><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">&raquo;</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430171001756-1339320269.png)





**设置尺寸，四种 lg、默认、sm 和 xs**

**pagination-lg样式class类，写在 <ul>里，设置分页样式为大尺寸(Bootstrap)**  
 **pagination-xs样式class类，写在 <ul>里，设置分页样式为中尺寸(Bootstrap)**  
 **pagination-sm样式class类，写在 <ul>里，设置分页样式为小尺寸(Bootstrap)**

[code]

    <ul class="pagination pagination-lg">
        <li><a href="#">&laquo;</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">&raquo;</a></li>
    </ul>
    <br>
    <ul class="pagination pagination-xs">
        <li><a href="#">&laquo;</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">&raquo;</a></li>
    </ul>
    <br>
    <ul class="pagination pagination-sm">
        <li><a href="#">&laquo;</a></li>
        <li><a href="#">1</a></li>
        <li><a href="#">2</a></li>
        <li><a href="#">3</a></li>
        <li><a href="#">4</a></li>
        <li><a href="#">5</a></li>
        <li><a href="#">&raquo;</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430171847975-114509229.png)





**对齐翻页链接**

**pager样式class类，写在 <ul>里，设置翻页样式(Bootstrap)**  
 **previous样式class类，写在翻页 <ul>的li里，设置翻页左对齐(Bootstrap)**  
 **next样式class类，写在翻页 <ul>的li里，设置翻页右对齐(Bootstrap)**

[code]

    <ul class="pager">
        <li class="previous"><a href="#">上一页</a></li>
        <li class="next"><a href="#">下一页</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430173132865-1986135964.png)



**翻页项禁用**

**disabled样式class类，写在翻页 <ul>的li里，禁用翻页项(Bootstrap)**

[code]

    <ul class="pager">
        <li class="previous"><a href="#">上一页</a></li>
        <li class="next disabled"><a href="#">下一页</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430173347865-950590130.png)





**三．标签**

**在文本后面带上标签**



**label样式class类，写在 <span>里，声明一个标签(Bootstrap)**  
 **label-default样式class类，写在 <span>里，设置标签默认样式(Bootstrap)**

[code]

    <h3>标签 <span class="label label-default">new</span></h3>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430174026662-510499654.png)





**不同色调的标签样式**

**label-primary样式class类，写在 <span>里，设置标签样式蓝色(Bootstrap)**  
 **label-success样式class类，写在 <span>里，设置标签样式绿色(Bootstrap)**  
 **label-info样式class类，写在 <span>里，设置标签样式浅蓝(Bootstrap)**  
 **label-warning样式class类，写在 <span>里，设置标签样式橙色(Bootstrap)**  
 **label-danger样式class类，写在 <span>里，设置标签样式红色(Bootstrap)**

[code]

    <h3>标签 <span class="label label-primary">new</span></h3>
    <h3>标签 <span class="label label-success">new</span></h3>
    <h3>标签 <span class="label label-info">new</span></h3>
    <h3>标签 <span class="label label-warning">new</span></h3>
    <h3>标签 <span class="label label-danger">new</span></h3>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430174847334-2111878609.png)





**四．徽章**

**未读信息数量徽章**

**badge样式class类，写在 <span>里，设置徽章样式(Bootstrap)**

[code]

    <a href="#">信息 <span class="badge">10</span></a>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430175653912-1700099550.png)



**按钮中使用徽章**

[code]

     <button class="btn btn-success">
        提交 <span class="badge">3</span>
    </button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430175815069-507149776.png)





**激活状态自动适配色调**

[code]

     <ul class="nav nav-pills">
        <li class="active">
            <a href="#">首页 <span class="badge">2</span></a>
        </li>
        <li><a href="#">资讯</a></li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170430180018850-2112184793.png)



