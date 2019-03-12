---
layout: post
title: " 第一百九十八节，jQuery EasyUI，ProgressBar(进度条)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，ProgressBar(进度条)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329164317311-1591283086.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 ProgressBar(进度条)组件的使用方法，这个组件不依赖 于其他组件。**





**一．加载方式**

[code]

     //class 加载方式
    <div class="easyui-progressbar"
    　　data-options="value:60" style="width:400px;">
    </div>
[/code]



[code]

    //JS 加载调用
    $('#box').progressbar({
    　　value : 60,
    });
[/code]





**二．属性列表**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329155047342-32107971.png)

**width  string 设置进度条宽度。默认为 auto。**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width:500,               //设置进度条宽度
            height:20                //设置进度条高度
        });
    });
[/code]



**height  number 设置进度条高度。默认为 22。**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width:500,               //设置进度条宽度
            height:20                //设置进度条高度
        });
    });
[/code]



**value  number 设置进度条值。默认为 0。， **设置进度条值****

[code]

     /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width:500,               //设置进度条宽度
            height:20,                //设置进度条高度
            value:50                //设置进度条值
        });
    });
[/code]





**text  string 设置进度条百分比模版：默认{value}%，就是设置进度条的提示文字，默认是获取进度条的值加上%号**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width:500,               //设置进度条宽度
            height:20,                //设置进度条高度
            value:50,                //设置进度条值
            text : '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329161530889-1053631848.png)**

**onChange  newValue,oldValue 在值更改的时候触发，接收两个参数，分别接收进度新值，和旧值**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 50,                //设置进度条值
            text: '{value}%',       //设置进度条的提示文字，默认是获取进度条的值加上%号
            onChange: function (newValue, oldValue) {           //在值更改的时候触发
                alert('新:' + newValue + ',旧:' + oldValue);     //分别接收进度新值，和旧值
            }
        });
        setTimeout(function () {   //定时器1秒钟
            $('#box').progressbar('setValue', 70);  //将进度改变为70%
        }, 1000);
    });
[/code]

**动画进度效果**

[code]

     /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 50,                //设置进度条值
            text: '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
        setInterval(function () {  //定时器200毫秒，获取当前进度值加5，循环设置成新值
            $('#box').progressbar('setValue',$('#box').progressbar('getValue') + 5);
        }, 200);
    });
[/code]





**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329163635936-1959530217.png)**

**options  none 返回属性对象**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 5,                //设置进度条值
            text: '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
        alert($('#box').progressbar('options'));       //返回属性对象
    });
[/code]



**resize  width 组件大小**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 5,                //设置进度条值
            text: '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
        $('#box').progressbar('resize',800);       //设置组件大小
    });
[/code]



**getValue  none 返回当前进度值**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 5,                //设置进度条值
            text: '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
        alert($('#box').progressbar('getValue'));       //返回当前进度值
    });
[/code]



**setValue  value 设置一个新的进度值**

[code]

    /**
    <div id="box"></div>
     **/
    
    $(function () {
        $('#box').progressbar({
            width: 500,               //设置进度条宽度
            height: 20,                //设置进度条高度
            value: 5,                //设置进度条值
            text: '{value}%'       //设置进度条的提示文字，默认是获取进度条的值加上%号
        });
        $('#box').progressbar('setValue',80);       //设置一个新的进度值
    });
[/code]



**$.fn.progressbar.defaults 重写默认值对象。**

[code]

    $.fn.progressbar.defaults.value = '60';
[/code]



