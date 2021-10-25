---
layout: post
title: " 第二百二十七节，jQuery EasyUI，ComboTree(树型下拉框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，ComboTree(树型下拉框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423181944804-1966609139.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**

**本节课重点了解EasyUI中 **ComboTree(树型下拉框)组件** 的使用方法，这个组件依赖于Combo(下拉框) 和 Tree(树)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <select id="cc" class="easyui-combotree" style="width:200px;" data-options="url:'tree.json',required:true"></select>
[/code]

**JS 加载方式**

**combotree()将一个input元素执行树型下拉框**

[code]

     <input type="text" id="box">
[/code]

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
        });
    });
[/code]



**二．属性列表**

**属性列表，下拉框属性扩展自 combo(自定义下拉框)和 tree(树形控件)，**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423131637788-1471042805.png)**

**editable   boolean 定义用户是否可以直接输入文本到字段中。默认为 false。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
    });
[/code]



**PS：该控件的 事件完全继承自 combo(自定义下拉框)和 tree(树形控件)。**





**三．方法列表**

**树形下拉框方法扩展自 combo(自定义下拉框)。**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423132017366-1580683978.png)**

**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
        alert($('#box').combotree('options'));        //返回属性对象
    });
[/code]



**tree   none 返回树形对象。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
    
        $('#ann').click(function () {
            adc();
        });
        function adc() {
            var t = $('#box').combotree('tree');        //返回树形对象
            alert(t.tree('getSelected'));                //当用户选择一个节点时，返回当前节点对象
        }
    });
[/code]



**loadData   data 读取本地树形数据。**

[code]

    $(function () {
        $('#box').combotree({
            // url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
        $('#box').combotree('loadData',[        //读取本地树形数据
            {
                text:'加载本地数据'
            }
        ]);
    
        // $('#ann').click(function () {
        //     adc();
        // });
        // function adc() {
        //
        // }
    });
[/code]



**reload   url 再次请求远程树数据。通过'url'参数重写原始 URL 值。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
        $('#box').combotree('reload','tree.json');        // url 再次请求远程树数据。通过'url'参数重写原始 URL 值。
    
        // $('#ann').click(function () {
        //     adc();
        // });
        // function adc() {
        //
        // }
    });
[/code]



**clear   none 清空控件的值。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
    
    
        $('#ann').click(function () {
            adc();
        });
        function adc() {
            $('#box').combotree('clear');        //清空控件的值
        }
    });
[/code]



**setValues   values 设置组件值数组。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
        $('#box').combotree('setValues',[1,2]);        //设置组件值数组
    
        // $('#ann').click(function () {
        //     adc();
        // });
        // function adc() {
        //     $('#box').combotree('clear');        //清空控件的值
        // }
    });
[/code]



**setValue   value 设置组件值。**

[code]

    $(function () {
        $('#box').combotree({
            url: 'tree.json',    //加载远程数据
            required: true,        //不能为空
            editable : true,    //可以输入内容
        });
        $('#box').combotree('setValue','设置值');        //设置组件值
    
        // $('#ann').click(function () {
        //     adc();
        // });
        // function adc() {
        //     $('#box').combotree('clear');        //清空控件的值
        // }
    });
[/code]



