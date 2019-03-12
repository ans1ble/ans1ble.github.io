
---
layout: post
title: " 第二百二十五节，jQuery EasyUI，PropertyGird(属性表格)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQuery EasyUI，PropertyGird(属性表格)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416132521477-744822291.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 PropertyGird(属性表格)组件的使用方法， 这个组件依赖 于 DataGrid(数据表格)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <table id="box" class="easyui-propertygrid" style="width:300px" data-options="url:'content.json',showGroup:true"></table>
[/code]

**content.json**

[code]

     [
      {
        "name": "PHP 版本",
        "value": "5.4",
        "group": "系统信息",
        "editor": "text"
      },
      {
        "name": "CPU 核心",
        "value": "双核四线程",
        "group": "系统信息",
        "editor": "text"
      },
      {
        "name": "超级管理员",
        "value": "Admin",
        "group": "管理信息",
        "editor": "text"
      },
      {
        "name": "管理密码",
        "value": "******",
        "group": "管理信息",
        "editor": "text"
      }
    ]
[/code]

**属性表格扩展自 datagrid(数据表格)。它的行数据格式和数据表格相同。作为一个属 性行，以下字段是必须的：**

** name：字段名称。 **

** value：字段值。 **

** group：分组字段值。 **

** editor：在编辑属性值的时候使用的编辑器对象。**



**JS 加载方式**

[code]

     <table id="box" style="width:300px"></table>
[/code]

**propertygrid()将一个table元素执行(属性表格)组件**

[code]

    $( function () {
        $('#box').propertygrid({
            url: 'content.json',
        });
    });
[/code]





**二．属性列表**

**属性表格的属性扩展自 datagrid(数据表格)，属性表格新增的的属性如下：**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416121505006-1391819395.png)**



**showGroup   boolean 定义是否显示属性分组。默认值 false。**

[code]

    $(function () {
        $('#box').propertygrid({
            url: 'content.json',        //加载远程数据
            showGroup:true,             //定义是否显示属性分组。默认值 false。
            groupField:'group',         //定义分组的字段名
            groupFormatter:function (group,rows) {      //定义如何格式化分组的值
                return '['+group+']';
            }
        });
    });
[/code]



**groupField   string 定义分组的字段名。默认值为 group。**

[code]

    $(function () {
        $('#box').propertygrid({
            url: 'content.json',        //加载远程数据
            showGroup:true,             //定义是否显示属性分组。默认值 false。
            groupField:'group',         //定义分组的字段名
            groupFormatter:function (group,rows) {      //定义如何格式化分组的值
                return '['+group+']';
            }
        });
    });
[/code]



**groupFormatter
function(group,rows)定义如何格式化分组的值。该函数拥有如下参数：group：分组字段值。rows：属于该分组的所有行。**

[code]

    $(function () {
        $('#box').propertygrid({
            url: 'content.json',        //加载远程数据
            showGroup:true,             //定义是否显示属性分组。默认值 false。
            groupField:'group',         //定义分组的字段名
            groupFormatter:function (group,rows) {      //定义如何格式化分组的值
                return '['+group+']';
            }
        });
    });
[/code]





**三，事件**

**PropertyGrid事件，完全继承 **DataGrid(数据表格)组件的事件****





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416122959724-253461867.png)**

**expandGroup   groupIndex 展开指定分组。如果'groupIndex'参数未指定，则展开所有分组。**

[code]

    $(function () {
        $('#box').propertygrid({
            url: 'content.json',        //加载远程数据
            showGroup: true,             //定义是否显示属性分组。默认值 false。
            groupField: 'group',         //定义分组的字段名
            groupFormatter: function (group, rows) {      //定义如何格式化分组的值
                return '[' + group + ']';
            }
        });
        $('#ann').click(function () {
            abc();
        });
    
        function abc() {
            $('#box').propertygrid('expandGroup');     //展开指定分组。如果'groupIndex'参数未指定，则展开所有分组。
        }
    });
[/code]



**collapseGroup   groupIndex 折叠指定分组。如果'groupIndex'参数未指定，则折叠所有分组。**

[code]

    $(function () {
        $('#box').propertygrid({
            url: 'content.json',        //加载远程数据
            showGroup: true,             //定义是否显示属性分组。默认值 false。
            groupField: 'group',         //定义分组的字段名
            groupFormatter: function (group, rows) {      //定义如何格式化分组的值
                return '[' + group + ']';
            }
        });
        $('#ann').click(function () {
            abc();
        });
    
        function abc() {
            $('#box').propertygrid('collapseGroup', 0);     //折叠指定分组。如果'groupIndex'参数未指定，则折叠所有分组
        }
    });
[/code]



**注意：其他属性，事件，方法，用DataGrid(数据表格)组件的即可**

