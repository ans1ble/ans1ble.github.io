---
layout: post
title: " 第二百二十节，jQuery EasyUI，Slider(滑动条)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Slider(滑动条)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406180113097-2046649286.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Slider(滑动条)组件的使用方法， 这个组件依赖于 Draggable(拖动)组件。**





**一．加载方式**

**class 加载方式**

[code]

     <input class="easyui-slider" value="12" style="width:300px" data-options="showTip:true,rule:[0,'|',25,'|',50,'|',75,'|',100]" />
[/code]

**slider()将一个输入框执行滑动条方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').slider({
            width: 300,
            value: 12,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
        });
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406171247691-741576599.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406171257222-1467890104.png)**

**width   number 滑动条宽度。默认值 auto。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            height: 50,
            mode:'v'
        });
    });
[/code]



**height   number 滑动条高度。默认值 auto。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            height: 50,
            mode:'v'
        });
    });
[/code]



**mode   string 声明滚动条类型。可用值有：'h'(水平)、'v'(垂直)。默认值'h'。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            height: 50,
            mode:'v'
        });
    });
[/code]



**reversed   boolean 设置为 true 时，最小值和最大值将对调他们的位置。默认值 false。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            reversed:true
        });
    });
[/code]



**showTip   boolean 定义是否显示值信息提示。默认值 false。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true
        });
    });
[/code]



**disabled   boolean 定义是否禁用滑动条。默认值 false。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            disabled:true
        });
    });
[/code]



**value   number 默认值。默认值0。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            value:10
        });
    });
[/code]



**min   number 允许的最小值。默认值0。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            min:10,     //允许的最小值
            max:90,     //允许的最大值
        });
    });
[/code]



**max   number 允许的最大值。默认值100。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            min:10,     //允许的最小值
            max:90,     //允许的最大值
        });
    });
[/code]



**step   number 增加或减少 **值** 。默认值1。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            step:10,     //增加或减少值。默认值1。
        });
    });
[/code]



**rule   array显示标签旁边的滑块，'|' — 只显示一行。默认值[]。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
    });
[/code]



**tipFormatter   function 该函数用于格式化滑动条。返回的字符串值将显示提示。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            tipFormatter:function (value) {
                return value + '%';
            }
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406173850863-1380199255.png)**

**onChange   newValue, oldValue 在字段值更改的时候触发。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            onChange:function (newValue, oldValue) {
                alert('接收更改后的值'+newValue);
                alert('接收更改前的值'+oldValue);
            }
        });
    });
[/code]



**onSlideStart   value 在开始拖拽滑动条的时候触发。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            onSlideStart:function (value) {
                alert(value);
            }
        });
    });
[/code]



**onSlideEnd   value 在结束拖拽滑动条的时候触发。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
            onSlideEnd:function (value) {
                alert(value);
            }
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406174653550-381954003.png)**

**options   none 返回滑动条属性。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        alert($('#box').slider('options'));
    });
[/code]



**destroy   none 销毁滑动条对象。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('destroy');
    });
[/code]



**resize   param设置滑动条大小。'param'参数包含一下属性：width：新滑动条宽度。height：新滑动条高度。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('resize',{
            width:500,
            height:20
        });
    });
[/code]



**getValue   none 获取滑动条的值。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        alert($('#box').slider('getValue'));
    });
[/code]



**setValue   value 设置滑动条的值。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('setValue',90);
    });
[/code]



**clear   none 清除滑动条的值。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('clear');
    });
[/code]



**reset   none 重置滑动条的值。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('reset');
    });
[/code]



**enable   none 启用滑动条控件。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('enable');
    });
[/code]



**disable   none 禁用滑动条控件。**

[code]

    $(function () {
        $('#box').slider({
            width: 300,
            rule: [0, '|', 25, '|', 50, '|', 75, '|', 100],
            showTip:true,
        });
        $('#box').slider('disable');
    });
[/code]





**使用$.fn.slider.defaults 重写默认值对象。**

