---
layout: post
title: " 第二百一十六节，jQuery EasyUI，Spinner(微调)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Spinner(微调)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406135640707-445539972.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Spinner(微调)组件的使用方法， 这个组件依赖于 ValidateBox(验证框)组件。**

**这个组件是其他微调组件的基础组件，所以一般不会直接使用这个组件**



**一．加载方式**

**Spinner(微调)组件是其他两款高级微调组件的基础组件，默认情况下无法微调。这个 组件不支持 class 加载方式。**

**html**

[code]

     <input id="box" value="2">
[/code]

**JS 加载调用**

**spinner()将一个元素执行微调组件**

[code]

    $( function () {
        $('#box').spinner({
            required: true,
        });
    });
[/code]



**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406132159582-1835418730.png)**

**width   number 组件宽度。默认值 auto。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30
        });
    });
[/code]



**height   number 组件高度。默认值22。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30
        });
    });
[/code]



**value   string 默认值。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30,
            value:5
        });
    });
[/code]



**min   string 允许的最小值。默认值 null。单独使用没有效果**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30,
            min:5,
            max:50
        });
    });
[/code]



**max   string 允许的最大值。默认值 null。 **单独使用没有效果****

[code]

    $( function () {
        $('#box').spinner({
            width: 200,
            height:30,
            min:5,
            max:50
        });
    });
[/code]



**increment   number 在点击微调按钮的时候的增量值。默认值1。 ** **单独使用没有效果******

[code]

    $( function () {
        $('#box').spinner({
            width: 200,
            height:30,
            increment:5     //在点击微调按钮的时候的增量值。默认值1
        });
    });
[/code]



**editable   boolean 定义用户是否可以直接输入值到字段。默认值 true。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30,
            editable:false     
        });
    });
[/code]



**disabled   boolean 定义是否禁用字段。默认值 false。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30,
            disabled:true
        });
    });
[/code]



**spin   function(down)
在用户点击微调按钮的时候调用的函数。'down'参数对应用户点击的向下按钮。可以判断用户点击微调的上按钮还是下按钮，点击下按钮返回true，点击上按钮返回false**



[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height:30,
            spin:function (down) {
                alert(down);
            }
        });
    });
[/code]







**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406133903488-825027488.png)**

**onSpinUp none 在用户点击向上微调按钮的时候触发。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30,
            onSpinUp: function () {     //在用户点击向上微调按钮的时候触发
                //当用户点击上按钮时，获取到输入框的值加1，在赋值给输入框
                $('#box').spinner('setValue', parseInt($('#box').spinner('getValue')) + 1);
            },
            onSpinDown: function () {   //在用户点击向下微调按钮的时候触发
                //当用户点击下按钮时，获取到输入框的值减1，在赋值给输入框
                $('#box').spinner('setValue', parseInt($('#box').spinner('getValue')) - 1);
            },
        });
    });
[/code]



**onSpinDown none 在用户点击向下微调按钮的时候触发。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30,
            onSpinUp: function () {     //在用户点击向上微调按钮的时候触发
                //当用户点击上按钮时，获取到输入框的值加1，在赋值给输入框
                $('#box').spinner('setValue', parseInt($('#box').spinner('getValue')) + 1);
            },
            onSpinDown: function () {   //在用户点击向下微调按钮的时候触发
                //当用户点击下按钮时，获取到输入框的值减1，在赋值给输入框
                $('#box').spinner('setValue', parseInt($('#box').spinner('getValue')) - 1);
            },
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406134550066-2025330411.png)**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406134559222-1117489497.png)

**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        alert($('#box').spinner('options'));
    });
[/code]



  
**destroy   none 销毁微调组件。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('destroy');
    });
[/code]



  
**resize   width 返回组件宽度。通过'width'参数重写原始宽度。重写或者重置组件**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('resize',100);  //重写宽度
    });
[/code]



  
**enable   none 启用组件。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('disable');
        $('#box').spinner('enable');
    });
[/code]



  
**disable   none 禁用组件。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('disable');
        $('#box').spinner('enable');
    });
[/code]



  
**getValue   none 获取组件值。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        alert($('#box').spinner('getValue'));  //获取组件值
    });
[/code]



  
**setValue   value 设置组件值。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('setValue',500);
    });
[/code]



  
**clear   none 清空组件值。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('clear');
    });
[/code]



  
**reset   none 重置组件值。**

[code]

    $(function () {
        $('#box').spinner({
            width: 200,
            height: 30
        });
        $('#box').spinner('reset');
    });
[/code]





**我们可以使用$.fn.spinner.defaults 重写默认值对象。**

