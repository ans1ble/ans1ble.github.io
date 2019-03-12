---
layout: post
title: " 第二百一十三节，jQuery EasyUI，NumberBox(数值输入框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，NumberBox(数值输入框)组件**

**功能：只能输入数值，和各种数值的计算**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404220104175-1562894432.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 NumberBox(数值输入框)组件的使用方法， 这个组件依赖 于 ValidateBox(验证框)组件。**





**一．加载方式**

**class 加载方式**

[code]

     <input type="text" class="easyui-numberbox" value="100" data-options="min:0,precision:2">
[/code]

**numberbox()将一个输入框执行数值输入框组件方法**



**JS 加载调用**

[code]

    $('#box' ).numberbox({
    　　min : 0,
    　　precision : 2,
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404205511269-2147059616.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404205520128-1040130646.png)**

**disabled   boolean 是否禁用该字段。默认值 false。**

[code]

    /**
    <input id="box" type="text"  value="100">
     **/
    
    $(function () {
        $('#box').numberbox({
            disabled:true       //是否禁用该字段。默认值 false。
        });
    });
[/code]



**value   number 默认值。**

[code]

    /**
    <input id="box" type="text"  value="100">
     **/
    
    $(function () {
        $('#box').numberbox({
            value:100       //默认值。
        });
    });
[/code]



**min   number 允许的最小值。默认值 null。**



[code]

    $(function () {
        $('#box').numberbox({
            value:100,       //默认值。
            min:200,        //允许的最小值
        });
    });
[/code]





**max   number 允许的最大值。默认值 null。**

[code]

    $(function () {
        $('#box').numberbox({
            value:1000,       //默认值。
            max:200,        //允许的最大值
        });
    });
[/code]



**precision   number
在十进制分隔符之后显示的最大精度。（即小数点后的显示精度）默认值0。小数点后面保留几位，超过保留位数的进行四舍五入**

[code]

    $(function () {
        $('#box').numberbox({
            value:10,       //默认值。
            precision:2     //小数点后面保留几位
        });
    });
[/code]



**decimalSeparator   string 使用哪一种十进制字符分隔数字的整数和小数部分。默认值为小数点。整数与小数部分的分隔符**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            decimalSeparator:':'        //默认值为小数点。正数与小数部分的分隔符
        });
    });
[/code]



**groupSeparator
string使用哪一种字符分割整数组，以显示成千上万的数据。(比如：99,999,999.00中的','就是该分隔符设置。)**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            groupSeparator:','        //使用哪一种字符分割整数组，以显示成千上万的数据。(比如：99,999,999.00中的','就是该分隔符设置。)
        });
    });
[/code]



**prefix   string 前缀字符。(比如：金额的$或者￥)**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥'
        });
    });
[/code]



**suffix   string 后缀字符。(比如：后置的欧元符号€)**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥',
            suffix:'€'
        });
    });
[/code]



**filter   function(e) 定义如何过滤按键，当返回 true 时则允许输入，反之禁止。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥',
            filter:function (e) {
                return false
            }
        });
    });
[/code]



**formatter   function(v) 用于格式化数值的函数。返回字符串值以显示到输入框中。自定义前置或者后缀字符，不写入value里**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥',
            formatter:function (value) {
                return '###' + value;
            }
        });
    });
[/code]



**parser   function(s) 用于解析字符串的函数。 **自定义前置或者后缀字符，写入value里****



[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥',
            parser:function (s) {
                return '###' + s;
            }
        });
    });
[/code]







**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404213907160-2096666842.png)**

**onChange   newvalue,oldValue 当字段值更改的时候触发。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥',
            onChange:function (newvalue,oldValue) {
                alert('当字段值更改的时候触发');
                alert('接收改变后的值' + newvalue);
                alert('接收改变前的值' + oldValue);
            }
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404214326535-1956715631.png)**



**options   none 返回数值输入框属性。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥'
        });
        alert($('#box').numberbox('options'));  //返回数值输入框属性对象
    });
[/code]



**destroy   none 销毁数值输入框对象。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥'
        });
        $('#box').numberbox('destroy');  //销毁数值输入框对象
    });
[/code]



**disable   none 禁用字段。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥'
        });
        $('#box').numberbox('disable');  //禁用字段
    });
[/code]



**enable   none 启用字段。**

[code]

    $(function () {
        $('#box').numberbox({
            precision:2,                //小数点后面保留几位
            prefix:'￥'
        });
        $('#box').numberbox('enable');  //启用字段
    });
[/code]



**fix   none 将输入框中的值修正为有效的值。，也就是自动修正可以自定义方式**

[code]

    $(function () {
        $('#box').numberbox({
            precision: 2,                //小数点后面保留几位
            prefix: '￥'
        });
        $(document).dblclick(function () {
            $('#box').numberbox('fix');  //将输入框中的值修正为有效的值。，也就是自动修正可以自定义方式
        });
    });
[/code]



**setValue   value 设置数值输入框的值。**

[code]

    $(function () {
        $('#box').numberbox({
            precision: 2,                //小数点后面保留几位
            prefix: '￥'
        });
        $('#box').numberbox('setValue',800);  //设置数值输入框的值。
    });
[/code]



**getValue   none 获取数值输入框的值。**

[code]

    $(function () {
        $('#box').numberbox({
            precision: 2,                //小数点后面保留几位
            prefix: '￥'
        });
        alert($('#box').numberbox('getValue'));  //获取数值输入框的值
    });
[/code]



**clear   none 清除数值输入框的值。**

[code]

    $(function () {
        $('#box').numberbox({
            precision: 2,                //小数点后面保留几位
            prefix: '￥'
        });
        $('#box').numberbox('clear');  //清除数值输入框的值
    });
[/code]



**reset   none 重置数值输入框的值。**

[code]

    $(function () {
        $('#box').numberbox({
            precision: 2,                //小数点后面保留几位
            prefix: '￥'
        });
        $('#box').numberbox('reset');  //重置数值输入框的值
    });
[/code]



**我们可以使用$.fn.numberbox.defaults 重写默认值对象。**



