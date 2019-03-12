---
layout: post
title: " 第一百九十六节，jQuery EasyUI，Tooltip(提示框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Tooltip(提示框)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329132202451-1304101779.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Tooltip(提示框)组件的使用方法，，这个组件不依赖于其 他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <a href="http://www.ycku.com" title="这是一个提示信息！"
    　　class="easyui-tooltip">Hover Me
    </a>
[/code]



[code]

    //JS 加载调用
    $('#box').tooltip({
    　　content : '这里可以输入提示内容',
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329115241436-478482963.png)**

**position string 消息框位置。默认 bootom，还有 left、right、top， 设置提示框位置**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            position:'right'                    //设置提示框位置
        });
    });
[/code]



**content string 消息框内容。默认为 null，可以包含 html 标签， 设置提示内容可以包含html标签**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容'
        });
    });
[/code]



**trackMouse boolean 为true时，允许提示框跟随鼠标移动。默认为false**

[code]

    $( function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            position:'right',                    //设置提示框位置
            trackMouse:true                      //允许提示框跟随鼠标移动
        });
    });
[/code]



**deltaX number 水平方向提示框的位置。默认为 0， 设置提示框水平位置**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            position:'right',                    //设置提示框位置
            deltaX:20,                          //设置提示框水平位置
            deltaY:20                           //设置提示框垂直位置
        });
    });
[/code]



**deltaY number 垂直方向提示框的位置。默认为 0， 设置提示框垂直位置**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            position:'right',                    //设置提示框位置
            deltaX:20,                          //设置提示框水平位置
            deltaY:20                           //设置提示框垂直位置
        });
    });
[/code]



**showEvent string 当激活事件的时候显示提示框。默认为 mouseenter， 设置什么事件显示提示框**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            // position:'right',                    //设置提示框位置
            // deltaX:20,                          //设置提示框水平位置
            // deltaY:20                           //设置提示框垂直位置
            showEvent:'mouseenter',                 //鼠标移入显示
            hideEvent:'mouseleave'                 //鼠标移出隐藏
        });
    });
[/code]



**hideEvent string 当激活事件的时候隐藏提示框。默认为 mouseleave， **设置什么事件隐藏提示框****

[code]

    $( function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            // position:'right',                    //设置提示框位置
            // deltaX:20,                          //设置提示框水平位置
            // deltaY:20                           //设置提示框垂直位置
            showEvent:'mouseenter',                 //鼠标移入显示
            hideEvent:'mouseleave'                 //鼠标移出隐藏
        });
    });
[/code]



**showDelay number 延时多少秒显示提示框。默认 200， 设置延迟显示时间**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            // position:'right',                    //设置提示框位置
            // deltaX:20,                          //设置提示框水平位置
            // deltaY:20                           //设置提示框垂直位置
            // showEvent:'mouseenter',                 //鼠标移入显示
            // hideEvent:'mouseleave'                 //鼠标移出隐藏
            showDelay:200,                          //设置延迟显示时间
            hideDelay:200                           //设置延迟隐藏时间
        });
    });
[/code]



**hideDelay number 延时多少秒隐藏提示框。默认 100， 设置延迟隐藏时间**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            // position:'right',                    //设置提示框位置
            // deltaX:20,                          //设置提示框水平位置
            // deltaY:20                           //设置提示框垂直位置
            // showEvent:'mouseenter',                 //鼠标移入显示
            // hideEvent:'mouseleave'                 //鼠标移出隐藏
            showDelay:200,                          //设置延迟显示时间
            hideDelay:200                           //设置延迟隐藏时间
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329123325998-1311252620.png)**

**onShow  e 在显示提示框的时候触发**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            onShow:function () {
                alert('在显示提示框的时候触发');
            }
        });
    });
[/code]



**onHide  e 在隐藏提示框的时候触发**

[code]

    $(function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            onHide:function () {
                alert('在隐藏提示框的时候触发');
            }
        });
    });
[/code]



**onUpdate  content 在提示框内容更新的时候触发， **content接收更新后提示内容****

[code]

    $( function () {
        $('#box').tooltip({
            content : '这里可以输入提示内容',
            onUpdate:function (content) {
                alert('在提示框内容更新的时候触发：'+content);
            }
        });
    });
[/code]



**onPosition  left、top 在提示框位置改变的时候触发，接收两个参数，分别接收左位置和上位置**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容',
            onPosition: function (left, top) {                  //在提示框位置改变的时候触发
                console.log('left:' + left + ',top:' + top);
            }
        });
    });
[/code]



**onDestroy  none 在提示框被销毁的时候触发**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容',
            onDestroy: function (none) {            //在提示框被销毁的时候触发
                alert('提示框被销毁的时候触发');
            }
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329125003061-719608730.png)**

**options  none 返回属性对象**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容'
        });
        $('#box').tooltip('options');       //返回一个对象，里面是tooltip的属性
    });
[/code]



**tip  none 返回 tip 元素对象**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容',
            onShow: function () {                   //在显示时触发
                alert($('#box').tooltip('tip'));    //返回 tip 元素对象
            }
        });
    });
[/code]



**arrow  none 返回箭头元素对象**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容',
            onShow: function () {                   //在显示时触发
                alert($('#box').tooltip('arrow'));    //返回箭头元素对象
            }
        });
    });
[/code]



**show  e 显示提示框**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容'
        });
        $('#box').tooltip('hide');      //默认隐藏提示框
        $('#box').tooltip('show');      //默认显示提示框
    });
[/code]



**hide  e 隐藏提示框**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容'
        });
        $('#box').tooltip('hide');      //默认隐藏提示框
        $('#box').tooltip('show');      //默认显示提示框
    });
[/code]



**update  content 更新提示框内容**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容'
        });
        $('#box').tooltip('update','要更新的提示内容');      //更新提示框内容
    });
[/code]



**reposition  none 重置提示框位置**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容',
            onHide: function (e) {                   //当隐藏提示框时
                $('#box').tooltip('reposition');     //重置提示框位置
            }
        });
    });
[/code]



**destroy  none 销毁提示框**

[code]

    $(function () {
        $('#box').tooltip({
            content: '这里可以输入提示内容'
        });
        $('#box').tooltip('destroy');      //销毁提示框
    });
[/code]



**$.fn.tooltip.defaults 重写默认值对象。**

[code]

    $.fn.tooltip.defaults.position = 'top';
[/code]



