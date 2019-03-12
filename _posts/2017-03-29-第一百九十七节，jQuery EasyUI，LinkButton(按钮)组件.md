---
layout: post
title: " 第一百九十七节，jQuery EasyUI，LinkButton(按钮)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，LinkButton(按钮)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329151538998-1557045041.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 LinkButton(按钮)组件的使用方法，这个组件不依赖于其 他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <a href="###" class="easyui-linkbutton">按钮</a>
[/code]



[code]

    //JS 加载调用
    $('#box').linkbutton({
    　　text : '提交',
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329140900967-1823369889.png)**



**id  string 组件的 ID 属性。默认为 null，给按钮重新设置id**

[code]

    $(function () {
        $('#box').linkbutton({
            id:'pox'                //给按钮重新设置id
        });
    });
[/code]



**disabled  boolean 设置 true 则禁止按钮。默认为 false**

[code]

    /**
    <a id="box" href="#">按钮</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            disabled:true           //设置 true 则禁止按钮。默认为 false
        });
    });
[/code]



**toggle  boolean 设置 true 则允许用户切换其状态是否被选中，可实现 checkbox 复选效果。默认为
false，模拟多选框效果**

[code]

    /**
    <a id="box" href="#">按钮1</a>
    <a id="pox" href="#">按钮2</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            toggle:true           //模拟多选框效果
        });
        $('#pox').linkbutton({
            toggle:true           //模拟多选框效果
        });
    });
[/code]



**selected  boolean 定义按钮初始的选择状态，true 是被选中，false为未选中。默认为 false**

[code]

    /**
    <a id="box" href="#">按钮1</a>
    <a id="pox" href="#">按钮2</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            toggle:true,           //模拟多选框效果
            selected:true           //定义按钮初始的选择状态，true 是被选中，false为未选中。默认为 false
        });
        $('#pox').linkbutton({
            toggle:true           //模拟多选框效果
        });
    });
[/code]



**group  string 指定相同组名的按钮同属于一个组，可实现 radio单选效果。默认为 null，模拟单选框效果**

[code]

    /**
    <a id="box" href="#">按钮1</a>
    <a id="pox" href="#">按钮2</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            toggle:true,
            group:'xb'           //模拟单选框效果
    
        });
        $('#pox').linkbutton({
            toggle:true,
            group:'xb'           //模拟单选框效果
        });
    });
[/code]



**plain  boolean 设置 true 时显示简洁效果。默认为 false**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            plain:true              //设置 true 时显示简洁效果。默认为 false
        });
    });
[/code]



**text  string 按钮文字。默认为空字符串**

[code]

    $(function () {
        $('#box').linkbutton({
            text:'发送'             //按钮文字
        });
    });
[/code]



**iconCls  string 显示在按钮文字左侧的图标（16x16）的 CSS 类 ID。默认为 null，设置
**按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称****

[code]

     /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok'        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
        });
    });
[/code]



**iconAlign  string 按钮图标位置。默认为 left，还有 right， **按钮图标位置****

[code]

    $( function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
    });
[/code]





**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329150122326-738848748.png)**



**options  none 返回属性对象**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
        alert($('#box').linkbutton('options'));    //返回属性对象
    });
[/code]



**disable  none 禁止按钮**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
        $('#box').linkbutton('disable');    //禁止按钮
    });
[/code]



**enable  none 启用按钮**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
        $('#box').linkbutton('disable');    //禁止按钮
        $('#box').linkbutton('enable');    //启用按钮
    });
[/code]



**select  none 选择按钮**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
        $('#box').linkbutton('select');    //选择按钮
        $('#box').linkbutton('unselect');    //取消选择按钮
    });
[/code]



**unselect  none 取消选择按钮**

[code]

    /**
    <a id="box" href="#">按钮1</a>
     **/
    
    $(function () {
        $('#box').linkbutton({
            text:'发送',             //按钮文字
            iconCls:'icon-ok',        //设置按钮文字左侧的图标，设置的jQueryEasyUI/themes/icon.css里的名称
            iconAlign:'right'         //按钮图标位置
        });
        $('#box').linkbutton('select');    //选择按钮
        $('#box').linkbutton('unselect');    //取消选择按钮
    });
[/code]





**$.fn.linkbutton.defaults 重写默认值对象。**

[code]

    $.fn.linkbutton.defaults.iconCls = 'icon-add';
[/code]



