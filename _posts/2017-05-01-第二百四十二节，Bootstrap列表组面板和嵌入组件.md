---
layout: post
title: " 第二百四十二节，Bootstrap列表组面板和嵌入组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap列表组面板和嵌入组件**



**学习要点：**

**1.列表组组件**

**2.面板组件**

**3.响应式嵌入组件**



**本节课我们主要学习一下 Bootstrap 的三个组件功能：列表组组件、面板组件、 响应 式嵌入组件。**



**一．列表组组件**

**列表组组件用于显示一组列表的组件。**

**基本实例**

**list-group样式class类，写在 <ul>里，声明列表组(Bootstrap)**  
 **list-group-item样式class类，写在列表组 <li>里，设置列表组里的列表样式(Bootstrap)**

[code]

    <ul class="list-group">
        <li class="list-group-item">1.这是起始</li>
        <li class="list-group-item">2.这是第二条数据</li>
        <li class="list-group-item">3.这是第三排信息</li>
        <li class="list-group-item">4.这是末尾</li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501165947117-179926409.png)





**列表项带勋章**

**badge样式class类，写在列表组 <span>里，设置列表组里的列表徽章样式(Bootstrap)**

[code]

    <ul class="list-group">
        <li class="list-group-item">1.这是起始<span class=" **badge** ">10</span></li>
        <li class="list-group-item">2.这是第二条数据</li>
        <li class="list-group-item">3.这是第三排信息</li>
        <li class="list-group-item">4.这是末尾</li>
    </ul>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501170251429-2030346645.png)





**链接和首选**

**active样式class类，写在列表组 <li>或<a>里，设置列表组里的列表首选样式(Bootstrap)**



[code]

    <div class="list-group">
        <a href="#" class="list-group-item active">1.这是起始<span class="badge">10</span></a>
        <a href="#" class="list-group-item">2.这是第二条数据</a>
        <a href="#" class="list-group-item">3.这是第三排信息</a>
        <a href="#" class="list-group-item">4.这是末尾</a>
    </div>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501170549726-729642867.png)





**按钮式列表**

[code]

     <div class="list-group">
        <button class="list-group-item active">1.这是起始 <span class="badge">10</span></button>
        <button class="list-group-item">2.这是第二条数据</button>
        <button class="list-group-item">3.这是第三排信息</button>
        <button class="list-group-item">4.这是末尾</button>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501171728617-425699176.png)







**设置项目被禁用**

**disabled样式class类，写在列表组 <li>或<a>里，禁用列表项(Bootstrap)**

[code]

    <div class="list-group">
        <a href="#" class="list-group-item active">1.这是起始<span class="badge">10</span></a>
        <a href="#" class="list-group-item disabled">2.这是第二条数据</a>
        <a href="#" class="list-group-item">3.这是第三排信息</a>
        <a href="#" class="list-group-item">4.这是末尾</a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501184602492-608688258.png)





**情景类**

**list-group-item-success样式class类，写在 <li>或者<a>元素里，设置列表组项绿色(Bootstrap)**  
 **list-group-item-info样式class类，写在 <li>或者<a>元素里，设置列表组项蓝色(Bootstrap)**  
 **list-group-item-warning样式class类，写在 <li>或者<a>元素里，设置列表组项橙色(Bootstrap)**  
 **list-group-item-danger样式class类，写在 <li>或者<a>元素里，设置列表组项红色(Bootstrap)**

[code]

    <div class="list-group">
        <a href="#" class="list-group-item active">1.这是起始<span class="badge">10</span></a>
        <a href="#" class="list-group-item list-group-item-success">2.这是第二条数据</a>
        <a href="#" class="list-group-item list-group-item-info">3.这是第三排信息</a>
        <a href="#" class="list-group-item list-group-item-warning">4.这是末尾</a>
        <a href="#" class="list-group-item list-group-item-danger">4.这是末尾</a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501190712695-354552502.png)







**定制内容**

**list-group-item-text样式class类，写在列表组里 <p>元素里，给列表项设置文本内容(Bootstrap)**

[code]

    <div class="list-group">
        <a href="#" class="list-group-item active">
            <h4>内容标题</h4>
            <p class="list-group-item-text">这里是相关内容详情！</p>
        </a>
        <a href="#" class="list-group-item">
            <h4>内容标题</h4>
            <p class="list-group-item-text">这里是相关内容详情！</p>
        </a>
        <a href="#" class="list-group-item">
            <h4>内容标题</h4>
            <p class="list-group-item-text">这里是相关内容详情！</p>
        </a>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501191701695-540939368.png)





**二．面板组件**

**面板组件就是一个存放内容的容器组件。**

**基本实例**

**panel样式class类，写在面板组件 <div>元素里，声明面板组件div(Bootstrap)**  
 **panel-default样式class类，写在面板组件 <div>元素里，设置面板组件默认样式(Bootstrap)**  
 **panel-heading样式class类，写在面板组件里头部 <div>元素里，设置面板组件头部样式(Bootstrap)**  
 **panel-title样式class类，写在面板组件里头部 <h1-h4>元素里，设置面板组件头部标题样式(Bootstrap)**  
 **panel-body样式class类，写在面板组件里主体 <div>元素里，设置面板组件主体样式(Bootstrap)**  
 **panel-footer样式class类，写在面板组件里尾部 <div>元素里，设置面板组件尾部样式(Bootstrap)**

[code]

    <div class="panel panel-default">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501194907601-161745158.png)





**面板组件情景效果**

**panel-success样式class类，写在面板组件 <div>元素里，设置面板组件样式绿色(Bootstrap)**  
 **panel-info样式class类，写在面板组件 <div>元素里，设置面板组件样式浅蓝(Bootstrap)**  
 **panel-warning样式class类，写在面板组件 <div>元素里，设置面板组件样式橙色(Bootstrap)**  
 **panel-danger样式class类，写在面板组件 <div>元素里，设置面板组件样式红色(Bootstrap)**  
 **panel-primary样式class类，写在面板组件 <div>元素里，设置面板组件样式深蓝(Bootstrap)**

[code]

    <div class="panel panel-success">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
    <div class="panel panel-info">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
    <div class="panel panel-warning">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
    <div class="panel panel-danger">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
    <div class="panel panel-primary">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501200144429-798925197.png)

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501200154054-1306251189.png)







**表格类面板**

**table样式class类，写在面板组件里 <table>元素里，设置面板组件表格样式(Bootstrap)**

[code]

    <div class="panel panel-success">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <table class="table">
            <tr>
                <th>1</th>
                <th>2</th>
                <th>3</th>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </table>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501200928132-917016865.png)





**列表类面板， 在面板里嵌套一个列表组件即可**

[code]

    <div class="panel panel-success">
        <div class="panel-heading">
            <h3 class="panel-title">面板标题</h3>
        </div>
        <div class="panel-body">
            这里是详细内容区！
        </div>
        <table class="table">
            <tr>
                <th>1</th>
                <th>2</th>
                <th>3</th>
            </tr>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </table>
        <ul class="list-group">
            <li class="list-group-item">1.这里是首页</li>
            <li class="list-group-item">2.这里是第二个项目</li>
            <li class="list-group-item">3.这里是第三个项目</li>
            <li class="list-group-item">4.这里是第四个项目</li>
        </ul>
        <div class="panel-footer">
            这里是底部
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501201518804-1370970898.png)





**三．响应式嵌入组件，用于嵌入如视频swf等文件响应式【重点】**

**根据被嵌入内容的外部容器的宽度，自动创建一个固定的比例，从而让浏览器自动确定 内容的尺寸，能够在各种设备上缩放。**

**这些规则可以直接用于 <iframe>、<embed>、<video>和<object>元素。**

**panel-success样式class类，写在响应式嵌入组件 <div>元素里，声明响应式嵌入组件div(Bootstrap)**  
 **embed-responsive-16by9样式class类，写在响应式嵌入组件
<div>元素里，设置响应式嵌入组件16比9样式(Bootstrap)**  
 **embed-responsive-4by3样式class类，写在响应式嵌入组件
<div>元素里，设置响应式嵌入组件4比3样式(Bootstrap)**





**16:9 响应式**

[code]

     <div class="embed-responsive embed-responsive-16by9">
        <embed width="100%" height="100%"
               src="http://www.tudou.com/v/OUG5JBZ8udc/&bid=05&rpid=50797543&resourceId=50797543_05_05_99/v.swf"
               type="application/x-shockwave-flash"
               allowscriptaccess="always"
               allowfullscreen="true"
               wmode="opaque">
        </embed>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501205849882-917640218.png)





**4:3 响应式**

[code]

     <div class="embed-responsive embed-responsive-4by3">
        <embed width="100%" height="100%"
               src="http://www.tudou.com/v/OUG5JBZ8udc/&bid=05&rpid=50797543&resourceId=50797543_05_05_99/v.swf"
               type="application/x-shockwave-flash"
               allowscriptaccess="always"
               allowfullscreen="true"
               wmode="opaque">
        </embed>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170501210132773-1619043654.png)



