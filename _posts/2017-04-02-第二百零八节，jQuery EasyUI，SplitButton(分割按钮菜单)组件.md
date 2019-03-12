---
layout: post
title: " 第二百零八节，jQuery EasyUI，SplitButton(分割按钮菜单)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，SplitButton(分割按钮)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402223607977-637290989.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 SplitButton(分割按钮)组件的使用方法，这个组件依赖 于 Menu(菜单)组件和
LinkButton(按钮)组件。**

**注意： **SplitButton(分割按钮)组件与， **MenuButton(菜单按钮)是一样的，不同是 **
**(分割按钮)组件多了一个分隔符**********



**一加载方式**

**class 加载方式**

[code]

     <a href="javascript:void(0)" id="edit" class="easyui-splitbutton"
       data-options="menu:'#box',iconCls:'icon-edit'">编辑</a>
    <div id="box" style="width:100px;">
        <div data-options="iconCls:'icon-ok'">Ok</div>
        <div data-options="iconCls:'icon-cancel'">Cancel</div>
    </div>
[/code]

**splitbutton()给一个符号规则的元素实现分割按钮菜单**

**JS 加载方式**

[code]

    $('#bt' ).splitbutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
[/code]



**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402222153039-120230302.png)**

**plain   boolean 为 true 时显示简易效果。默认为 true。**

**menu   string 用来创建一个对应菜单的选择器。**

**duration   number 定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。**

[code]

    $(function () {
        //按钮部分
        $('#bt').splitbutton({
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





**三．菜单方法**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402222543133-538175917.png)**

**options   none 返回属性对象。**

[code]

    $(function () {
        //按钮部分
        $('#bt').splitbutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        alert($('#bt').splitbutton('options'));    //返回属性对象
    });
[/code]





**disable   none 禁用菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').splitbutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').splitbutton('disable');    //禁用菜单按钮。
    });
[/code]





**enable   none 启用菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').splitbutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').splitbutton('enable');    //启用菜单按钮。
    });
[/code]





**destroy   none 销毁菜单按钮。**

[code]

    $(function () {
        //按钮部分
        $('#bt').splitbutton({
            menu:'#box',         //在按钮里指向菜单元素
            iconCls:'icon-edit', //设置按钮图标
            plain:false,          //按钮不扁平化，显示按钮轮廓
            duration:50         //定义鼠标划过按钮时显示菜单所持续的时间，单位为毫秒。默认为100。
        });
        //菜单部分
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
        });
        $('#bt').splitbutton('destroy');    //销毁菜单按钮
    });
[/code]



**重写默认**

**扩展自$.fn.linkbutton.defaults。使用$.fn.splitbutton.defaults 重写默认 值对象。**



**注意：菜单部分的属性，方法，事件，参照菜单即可**

