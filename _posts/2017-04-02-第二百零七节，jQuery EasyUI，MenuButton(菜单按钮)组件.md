---
layout: post
title: " 第二百零七节，jQuery EasyUI，MenuButton(菜单按钮)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，MenuButton(菜单按钮)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402215001414-707132435.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 MenuButton(菜单按钮)组件的使用方法， 这个组件依赖于 Menu(菜单)组件和
LinkButton(按钮)组件。**



**一．加载方式**

**class 加载方式**



[code]

    <a href="javascript:void(0)" id="edit" class="easyui-menubutton"
       data-options="menu:'#box',iconCls:'icon-edit'">编辑</a>
    <div id="box" style="width:150px;">
        <div data-options="iconCls:'icon-undo'">撤销</div>
        <div data-options="iconCls:'icon-redo'">恢复</div>
        <div class="menu-sep"></div>
        <div>剪切</div>
        <div>复制</div>
        <div>粘贴</div>
        <div class="menu-sep"></div>
        <div data-options="iconCls:'icon-remove'">删除</div>
        <div>全选</div>
    </div>
[/code]



**menubutton()方法，将一个符合规则的元素执行菜单按钮方法**

**html代码**

[code]

     <a id="bt" href="javascript:void(0)">编辑</a>
    <div id="box">
        <div id="i1">撤销</div>
        <div id="i2">恢复</div>
        <div id="i3">剪切</div>
        <div id="i4">复制</div>
        <div id="i5">粘贴</div>
        <div class="menu-sep"></div>
        <div id="i6">删除</div>
        <div id="i7">全选</div>
    </div>
[/code]

**js代码**

[code]

    $( function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false          //按钮不扁平化，显示按钮轮廓
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            onClick:function (item) {
                alert('在菜单项被点击的时候触发');
                alert(item); //接收点击的对象
            }
        });
        //菜单项部分
        $('#box').menu('setIcon', {
            target: '#i1',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i2',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i3',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i4',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i5',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i6',
            iconCls: 'icon-add'
        });
            $('#box').menu('setIcon', {
            target: '#i7',
            iconCls: 'icon-add'
        });
    
    });
[/code]

**注意：菜单按钮，是按钮和菜单的组合，所以菜单的属性，方法，事件等参照上一节，菜单来使用即可**





**二．菜单按钮属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402213522852-79771014.png)**

**plain   boolean 为 true 时显示简易效果。默认为 true。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false          //按钮不扁平化，显示按钮轮廓
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
    });
[/code]



**menu   string 用来创建一个对应菜单的选择器。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false          //按钮不扁平化，显示按钮轮廓
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
    });
[/code]



**duration   number 定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
    });
[/code]

**属性列表，其他属性，参考依赖组件 LinkButton**



**三．菜单按钮方法**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402214249961-213363324.png)**

**options   none 返回属性对象。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        alert($('#bt').menubutton('options'));   //返回属性对象
    });
[/code]



**disable   none 禁用菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').menubutton('disable');   //禁用菜单按钮
    });
[/code]



**enable   none 启用菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').menubutton('enable');   //启用菜单按钮
    });
[/code]



**destroy   none 销毁菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').menubutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').menubutton('destroy');   //销毁菜单按钮。
    });
[/code]





**重写默认值**

扩展自$.fn.linkbutton.defaults。使用$.fn.menubutton.defaults 重写默认值 对象。



