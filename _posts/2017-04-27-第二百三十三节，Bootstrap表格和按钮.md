---
layout: post
title: " 第二百三十三节，Bootstrap表格和按钮 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap表格和按钮**



**学习要点：**

**1.表格**

**2.按钮**



**本节课我们主要学习一下 Bootstrap 表格和按钮功能，通过内置的 CSS 定义，显示各 种丰富的效果。**



**一．表格**

**Bootstrap 提供了一些丰富的表格样式供开发者使用。**

**1.基本格式**

**实现基本的表格样式**

**table样式class类，写在 <table>标签里，将表格执行表格基本样式并且自适应(Bootstrap)**

[code]

    <table class="table">
        <thead>
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427183037506-116274639.png)



**2.条纹状表格**

**让里的行产生一行隔一行加单色背景效果**

**table-striped样式class类，写在 <table>标签里，让<tbody>里的行产生一行隔一行加单色背景效果(Bootstrap)**

[code]

    <table class="table table-striped">
        <thead>
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427183446209-1045438779.png)



**3.带边框的表格**

**给表格增加边框**

**table-bordered样式class类，写在 <table>标签里，给表格增加边框(Bootstrap)**

[code]

    <table class="table table-striped table-bordered">
        <thead>
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427183940928-1928952896.png)



**4.悬停鼠标**

**让下的表格悬停鼠标实现背景效果**

**table-hover样式class类，写在 <table>标签里，让<tbody>下的表格悬停鼠标实现背景效果(Bootstrap)**

[code]

    <table class="table table-striped table-bordered table-hover">
        <thead>
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427184958553-118096566.png)



**5.状态类**

**可以单独设置每一行的背景样式**

**success样式class类，写在 <tr>标签里，可以单独设置每一行的背景样式(Bootstrap)**

**一共五种不同的样式可供选择。每一种背景颜色不同**

**active样式class类，写在 <tr>标签里，鼠标悬停在行或单元格上(Bootstrap)**  
 **info样式class类，写在 <tr>标签里，标识普通的提示信息或动作(Bootstrap)**  
 **warning样式class类，写在 <tr>标签里，标识警告或需要用户注意(Bootstrap)**  
 **danger样式class类，写在 <tr>标签里，表示危险或潜在的带来负面影响的动作(Bootstrap)**

[code]

    <table class="table table-striped table-bordered table-hover">
        <thead>
            <tr class="success">
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427185427428-1147595011.png)



**6.隐藏某一行**

**隐藏行**

**sr-only样式class类，写在 <tr>标签里，隐藏某一行(Bootstrap)**

[code]

    <table class="table table-striped table-bordered table-hover">
        <thead>
            <tr class="success">
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr class="sr-only">
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427190537647-158161642.png)



**7.响应式表格**

**表格父元素设置响应式，小于 768px 出现边框**

**table-responsive样式class类，写在 <body>标签里，表格父元素设置响应式，小于 768px 出现边框(Bootstrap)**

[code]

    <body class="table-responsive">
    
    <table class="table table-striped table-hover">
        <thead>
            <tr class="success">
                <th>编号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>张三</td>
                <td>男</td>
                <td>50</td>
            </tr>
            <tr>
                <td>2</td>
                <td>李四</td>
                <td>女</td>
                <td>48</td>
            </tr>
            <tr>
                <td>3</td>
                <td>王五</td>
                <td>男</td>
                <td>52</td>
            </tr>
            <tr>
                <td>4</td>
                <td>马六</td>
                <td>男</td>
                <td>55</td>
            </tr>
        </tbody>
    </table>
    
    <!--引入jquery文件-->
    <script src="jquery/jquery.min.js"></script>
    <!--引入bootstrap里的js-->
    <script src="bootstrap/js/bootstrap.min.js"></script>
    </body>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427191310865-1480086758.png)

** **

**二．按钮**

**Bootstrap 提供了很多丰富按钮供开发者使用。**

**1.可作为按钮使用的标签或元素**

**转化成普通按钮**

**btn样式class类，写在 <a,button,input>标签里，按钮基本样式(Bootstrap)**

[code]

    <a href="###" class="btn btn-default">Link</a>
    <button class="btn btn-default">Button</button>
    <input type="button" class="btn btn-default" value="input">
[/code]

**注意事项有三点：**

**(1).针对组件的注意事项**  
 **虽然按钮类可以应用到 <a> 和 <button> 元素上，但是，导航和导航条组件只支持<button> 元素。**

  
**(2).链接被作为按钮使用时的注意事项**  
 **如果 <a> 元素被作为按钮使用 -- 并用于在当前页面触发某些功能 -- 而不是用于链接其他页面或链接当前页面中的其他部分，那么，务必为其设置
role="button" 属性。**

  
**(3).跨浏览器展现**  
 **我们总结的最佳实践是：强烈建议尽可能使用 <button> 元素来获得在各个浏览器上获得相匹配的绘制效果。另外，我们还发现了 Firefox <30
版本的浏览器上出现的一个 bug，其表现是：阻止我们为基于 <input> 元素所创建的按钮设置 line-height 属性，这就导致在Firefox
浏览器上不能完全和其他按钮保持一致的高度。**

** **

**2.按钮预定义样式**

**首先要设置基本class样式 **btn****

**btn-default样式class类，写在 <a,button,input>标签里，按钮默认样式(Bootstrap)**  
 **btn-success样式class类，写在 <a,button,input>标签里，按钮成功样式(Bootstrap)**  
 **btn-info样式class类，写在 <a,button,input>标签里，按钮一般信息样式(Bootstrap)**  
 **btn-warning样式class类，写在 <a,button,input>标签里，按钮警告样式(Bootstrap)**  
 **btn-danger样式class类，写在 <a,button,input>标签里，按钮危险样式(Bootstrap)**  
 **btn-primary样式class类，写在 <a,button,input>标签里，按钮首选项样式(Bootstrap)**  
 **btn-link样式class类，写在 <a,button,input>标签里，按钮链接样式(Bootstrap)**

[code]

    <button class="btn btn-default">Button</button>
    <button class="btn btn-success">Button</button>
    <button class="btn btn-info">Button</button>
    <button class="btn btn-warning">Button</button>
    <button class="btn btn-danger">Button</button>
    <button class="btn btn-primary">Button</button>
    <button class="btn btn-link">Button</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427214119834-159519051.png)



**3.按钮尺寸大小**

**从大到小的尺寸**

**btn-lg样式class类，写在 <a,button,input>标签里，按钮最大样式(Bootstrap)**  
 **btn样式class类，写在 <a,button,input>标签里，按钮默认大小样式(Bootstrap)**  
 **btn-sm样式class类，写在 <a,button,input>标签里，按钮小号样式(Bootstrap)**  
 **btn-xs样式class类，写在 <a,button,input>标签里，按钮最小号样式(Bootstrap)**

[code]

    <button class="btn btn-lg">Button</button>
    <button class="btn">Button</button>
    <button class="btn btn-sm">Button</button>
    <button class="btn btn-xs">Button</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427214945569-1094721244.png)



**4.块级按钮**

**块级换行**

**btn-block样式class类，写在 <a,button,input>标签里，块级换行(Bootstrap)**

[code]

    <button class="btn btn-block">Button</button>
    <button class="btn btn-block">Button</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427215328959-1797786949.png)



**5.激活状态按钮**

**激活按钮**

**active样式class类，写在 <a,button,input>标签里，激活按钮(Bootstrap)**

[code]

    <button class="btn active">Button</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427215750959-31748294.png)



**6.禁用状态**

**禁用按钮**

**disabled样式class类，写在 <a,button,input>标签里，禁用按钮(Bootstrap)**

[code]

    <button class="btn active disabled">Button</button>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427220038131-972383350.png)

