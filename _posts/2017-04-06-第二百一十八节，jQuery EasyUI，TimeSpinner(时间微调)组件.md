---
layout: post
title: " 第二百一十八节，jQuery EasyUI，TimeSpinner(时间微调)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，TimeSpinner(时间微调)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406151433660-2000984774.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 **TimeSpinner(时间微调)** 组件的使用方法，这个组件依赖于 Spinner(微调)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <input id="box" class="easyui-timespinner">
[/code]

**timespinner()将一个输入框执行时间微调组件方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').timespinner({
            value: '00:00',
            min: '00:00',
            max: '23:59',
            editable: false,
        });
    });
[/code]





**二．属性列表**

**TimeSpinner 属性，扩展自 Spinner(微调)组件，所以微调组件也是可以用的**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406145046816-481419456.png)**

**separator   string 定义在小时、分钟和秒之间的分隔符。默认值为‘：’。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            separator:'/'
        });
    });
[/code]



**showSeconds   boolean 定义是否显示秒钟信息。默认值为 false。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            separator:'/',
            showSeconds:true
        });
    });
[/code]



**highlight   number 初始选中的字段 0=小时,1=分钟...默认值为0。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight:1,
    
        });
    });
[/code]





**三．事件列表**

**TimeSpinner(时间微调)组件继承自 Spinner(微调)组件。**

**事件列表**

[code]

    $( function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
            onSpinUp: function () {
                alert('点击了上微调按钮');
            },
            onSpinDown: function () {
                alert('点击了下微调按钮');
            },
        });
    });
[/code]



**四．方法列表**

**TimeSpinner 方法，扩展自 ValidateBox(验证框)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406150348847-1622740693.png)**

**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
        });
        alert($('#box').timespinner('options'));
    });
[/code]



  
**setValue   value 设置时间微调组件的值。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
        });
        $('#box').timespinner('setValue','12:23:45');
    });
[/code]



  
**getHours   none 获取当前的小时数。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
        });
        $(document).click(function () {
            alert($('#box').timespinner('getHours'));
            alert($('#box').timespinner('getMinutes'));
            alert($('#box').timespinner('getSeconds'));
        });
    });
[/code]



  
**getMinutes   none 获取当前的分钟数。**

[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
        });
        $(document).click(function () {
            alert($('#box').timespinner('getHours'));
            alert($('#box').timespinner('getMinutes'));
            alert($('#box').timespinner('getSeconds'));
        });
    });
[/code]



  
**getSeconds   none 获取当前的秒数。**



[code]

    $(function () {
        $('#box').timespinner({
            value: '00:00',     //初始时间
            min: '00:00',       //最小值
            max: '23:59',       //最大值
            highlight: 1,
        });
        $(document).click(function () {
            alert($('#box').timespinner('getHours'));
            alert($('#box').timespinner('getMinutes'));
            alert($('#box').timespinner('getSeconds'));
        });
    });
[/code]







**我们可以使用$.fn.timespinner.defaults 重写默认值对象。**



