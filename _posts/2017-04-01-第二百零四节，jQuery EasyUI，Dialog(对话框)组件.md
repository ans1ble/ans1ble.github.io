---
layout: post
title: " 第二百零四节，jQuery EasyUI，Dialog(对话框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Dialog(对话框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401211129820-1064569713.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解EasyUI中Dialog(窗口)组件的使用方法，这个组件依赖于 Window(窗 口)组件、linkbutton (按钮)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <div class="easyui-dialog" title="My Dialog"
         style="width:400px;height:200px;"
         data-options="iconCls:'icon-save',resizable:true,modal:true">
        对话框
    </div>
[/code]

**dialog()方法，将元素执行对话框方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').dialog({
            title: '标题',
            width: 400,
            height: 250,
            modal: true,
        });
    });
[/code]





**二．属性列表**

**窗口属性扩展自 Window(面板)，窗口新增或重新定义的属性如下：**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401194002274-1689408263.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401194010555-540771690.png)**

**title   string 对话框窗口标题文本。默认值New Dialog。**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title:'对话框标题'   //对话框窗口标题文本。默认值New Dialog。
        });
    });
[/code]



**collapsible   boolean 定义是否显示可折叠按钮。默认值 false。**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title:'对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible:true    //定义是否显示可折叠按钮。默认值 false。
        });
    });
[/code]



**minimizable   boolean 定义是否显示最小化按钮。默认值 false。**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title:'对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible:true,    //定义是否显示可折叠按钮。默认值 false。
            minimizable:true    //定义是否显示最小化按钮。默认值 false。
        });
    });
[/code]



**maximizable   boolean 定义是否显示最大化按钮。默认值 false。**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title:'对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible:true,    //定义是否显示可折叠按钮。默认值 false。
            maximizable:true    //定义是否显示最大化按钮。默认值 false。
        });
    });
[/code]



**resizable   boolean 定义是否可以改变对话框窗口大小。默认值 false。**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title:'对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible:true,    //定义是否显示可折叠按钮。默认值 false。
            resizable:true    //定义是否可以改变对话框窗口大小。默认值 false。
        });
    });
[/code]



**toolbar   array,selector设置对话框窗口顶部工具栏，可用值有：(1) 一个数组，每一个工具栏中的工具属性都和 linkbutton
相同。(2) 一个选择器指定工具栏。默认值 null。工具栏组**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title: '对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible: true,    //定义是否显示可折叠按钮。默认值 false。
            resizable: true,    //定义是否可以改变对话框窗口大小。默认值 false。
            toolbar: [{
                text: '编辑',
                iconCls: 'icon-edit',
                handler: function () {
                    alert('点击后触发');
                }
            }],
            buttons: [{
                text: '保存',
                iconCls: 'icon-ok',
                handler: function () {
                    alert('点击后触发');
                }
            }]
        });
    });
[/code]



**buttons   array,selector对话框窗口底部按钮，可用值有：(1) 一个数组，每一个按钮的属性都和linkbutton 相同。(2)
一个选择器指定按钮栏。默认值 null。按钮组**



[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title: '对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible: true,    //定义是否显示可折叠按钮。默认值 false。
            resizable: true,    //定义是否可以改变对话框窗口大小。默认值 false。
            toolbar: [{
                text: '编辑',
                iconCls: 'icon-edit',
                handler: function () {
                    alert('点击后触发');
                }
            }],
            buttons: [{
                text: '保存',
                iconCls: 'icon-ok',
                handler: function () {
                    alert('点击后触发');
                }
            }]
        });
    });
[/code]





**Dialog 是继承自 Window 组件的，所以 Window 组件和 Panel 组件均可用。 其他属性见 **Window 组件和 Panel
组件均可用****





****三．事件列表****

****窗口的事件完整继承自 Window(面板)。所以，直接参考 Window 面板的事件即可。****

****如：****

[code]

     //Dialog 事件
    $('#box').dialog({
        width : 600,
        height : 400,
        modal : true,
        onClose : function () {
            alert('关闭后触发！');
        },
    });
[/code]



**四．方法列表**

****对话框的方法扩展自 Window(窗口)，对话框新增方法如下： 其他方法见 ** **Window(窗口)方法********

****![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401203935664-1202295276.png)****



**dialog   none 返回外部对话框对象**

[code]

    $(function () {
        $('#box').dialog({
            width: 500,
            height: 250,
            title: '对话框标题',   //对话框窗口标题文本。默认值New Dialog。
            collapsible: true,    //定义是否显示可折叠按钮。默认值 false。
            resizable: true,    //定义是否可以改变对话框窗口大小。默认值 false。
        });
        alert($('#box').dialog('dialog'));  //返回外部对话框对象
    });
[/code]



**其他属性见 **Window 组件和 Panel 组件均可用****





********$.fn.window.defaults 重写默认值对象。 与前面相同********

