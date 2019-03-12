
---
layout: post
title: " 第二百一十九节，jQuery EasyUI，DateTimeBox(日期时间输入框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQuery EasyUI，DateTimeBox(日期时间输入框)组件**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406155436988-1420682386.png)**

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 DateTimeBox(日期时间输入框)组件的使用方法， 这个组 件依赖于 DateBox(日期输入框)组件和
TimeSpinner(时间微调)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <input id="box" class="easyui-datetimebox">
[/code]

**datetimebox()将一个输入框执行日期时间输入框组件方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').datetimebox({
            value: '2015-6-1 15:11:12',
        });
    });
[/code]





**二．属性列表**

**DataTimeBox 属性，扩展自 DateBox(日期输入框)组件**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406153812207-1786923656.png)**

**showSeconds   boolean 定义是否显示秒钟信息。默认值为 false。**

[code]

    $(function () {
        $('#box').datetimebox({
            showSeconds:true
        });
    });
[/code]



**timeSeparator   String 定义在小时、分钟和秒之间的时间分割线。默认为“：”。**

[code]

    $(function () {
        $('#box').datetimebox({
            showSeconds:true,
            timeSeparator:'/'
        });
    });
[/code]





**三．方法列表**

**DateTimeBox 方法，扩展自 DateBox(验证框)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406154206285-755190071.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406154217253-714782240.png)

**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').datetimebox({
            showSeconds:true,
        });
        alert($('#box').datetimebox('options'));
    });
[/code]



  
**setValue   value 设置日期时间输入框的值。**

[code]

    $(function () {
        $('#box').datetimebox({
            showSeconds: true,
        });
        //取值赋值
        $('#box').datetimebox('setValue', '2015-6-1 11:11:11');
        alert($('#box').datetimebox('getValue'));
    });
[/code]



  
**spinner   None 返回时间微调器对象。**



[code]

    $(function () {
        $('#box').datetimebox({
            showSeconds: true,
        });
        $('#box').datetimebox('spinner').spinner('getValue');  //返回时间微调器对象,设置时间微调值
    });
[/code]







**我们可以使用$.fn.datetimebox.defaults 重写默认值对象。**



