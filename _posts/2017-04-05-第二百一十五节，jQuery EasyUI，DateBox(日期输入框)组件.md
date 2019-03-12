
---
layout: post
title: " 第二百一十五节，jQuery EasyUI，DateBox(日期输入框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQuery EasyUI，DateBox(日期输入框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406124927082-1173118420.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 DateBox(日期输入框)组件的使用方法， 这个组件依赖于 Combo(自定义下拉框)和
Calendar(日历)。**



**一．加载方式**

**class 加载方式**

[code]

     <input id="box" type="text" class="easyui-datebox" required="required">
[/code]

**datebox()将一个输入框元素执行日期输入框方法**



**JS 加载调用**

[code]

    $('#box' ).datebox({
    });
[/code]



**二．属性列表**

**Datebox 属性，扩展自 Combo(自定义下拉框)组件，所以 **Combo(自定义下拉框)组件的属性也是有效的****

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170405190447144-1716740785.png)

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170405190501519-1138229458.png)**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170405190556675-139441292.png)

**panelWidth   number 下拉日历面板宽度。默认值180。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth:147,
            panelHeight:200
        });
    });
[/code]



**panelHeight   number 下拉日历面板高度。默认值 auto。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth:147,
            panelHeight:200
        });
    });
[/code]



**currentText   string 显示当天按钮。默认值 Today。设置今天按钮文字**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth:147,
            panelHeight:200,
            currentText:'T',
            closeText:'C'
        });
    });
[/code]



**closeText   string 显示关闭按钮。默认值 Close。设置关闭按钮文字**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth:147,
            panelHeight:200,
            currentText:'T',
            closeText:'C'
        });
    });
[/code]



**okText   string 显示 OK 按钮。默认值 Ok。异常**



**disabled   boolean 该属性值为 true 时禁用该字段。默认值 false。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth:147,
            panelHeight:200,
            disabled:true   //该属性值为 true 时禁用该字段。默认值 false。
        });
    });
[/code]



**buttons   array 在日历下面的按钮。拓展日历下面的按钮**

[code]

    $(function () {
        //插入拓展按钮
        var buttons = $.extend([], $.fn.datebox.defaults.buttons);
        buttons.splice(1, 0, {
            text: '确定',   //按钮名称
            handler: function (target) {
                alert('确定');
            }
        });
    
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
            buttons: buttons   //自定义拓展按钮
        });
    });
[/code]



**sharedCalendar   string,selector 将 一 个 日 历 控 件 共 享 给 多 个datebox 控件使用。默认值
null。就是将一个设置好的日历组件共用到多个输入框**

 html

[code]

    <input class="box">
    <input class="box">
    <!--一个div-->
    <div id="sc"></div>
[/code]

js

[code]

    $(function () {
        $('.box').datebox({             //将两个输入框，执行日期输入框方法
            panelWidth: 147,
            panelHeight: 200,
            sharedCalendar:'#sc'        //将日历控件指向id为sc的元素
        });
        $('#sc').calendar({             //将id为sc元素执行日历方法
            firstDay:1
        })
    });
[/code]



**formatter   function该函数用于格式化日期，它有一个'date'参数并且会返回一个字符串类型的值。下面的一个例子展示了如何重写默认的
formatter 函数。格式化日期**

[code]

    $(function () {
        $('#box').datebox({             
            panelWidth: 147,
            panelHeight: 200,
            formatter:function (date) {  //重新格式化如果，以/作为分隔符
                return date.getFullYear() + '/' + date.getMonth() + 1 + '/' + date.getDate();
            }
        });
    });
[/code]



**parser
function该函数用于解析一个日期字符串，它有一个'date'字符串参数并且会返回一个日期类型的值。将输入框的日期固定一个日期值，无论怎么选择它都是这个值**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
            parser:function (date) {
                return new Date(2015,6,1);
            }
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406123439191-1899493546.png)**

**onSelect   date 在用户选择一天的时候触发。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
            onSelect:function (date) {      //在用户选择一天的时候触发
                alert(date.getFullYear() + ":" + (date.getMonth() + 1) + ":" + date.getDate());
            }
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406123724957-1370862893.png)**



**options   none 返回参数对象。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
        });
        alert($('#box').datebox('options'));
    });
[/code]



  
**calendar   none 返回日历对象。**

[code]

    $(function () {
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
        });
        //得到日历对象，再将日历的星期一放到最前面
        $('#box').datebox('calendar').calendar({
            firstDay: 1,
        });
    });
[/code]



  
**setValue   value 设置日期输入的值。初始化日历输入框里的 **value值****



[code]

    $(function () {
        $('#box').datebox({
            panelWidth: 147,
            panelHeight: 200,
        });
        $('#box').datebox('setValue','2015-6-1');   //初始化日历输入框里的value值
    });
[/code]





**我们可以使用$.fn.databox.defaults 重写默认值对象。**



