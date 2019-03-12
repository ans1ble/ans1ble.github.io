---
layout: post
title: " 第二百一十七节，jQuery EasyUI，NumberSpinner(数字微调)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，NumberSpinner(数字微调)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170406142430753-1359801641.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 **NumberSpinner(数字微调)** 组件的使用方法，这个组件依赖于 Numberbox(数值输入框)和
Spinner(微调)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <input id="box" class="easyui-numberspinner">
[/code]

**numberspinner()将一个输入框执行数字微调组件方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').numberspinner({
            value: 10,
            increment: 10,
            min: 10,
            max: 500,
        });
    });
[/code]





**二．属性列表**

**注意：数字微调组件，属性，方法，事件继承微调组件的属性，和验证框组件的属性，关于验证方面的参照验证框属性，关于微调的参照微调属性**

[code]

    $( function () {
        $('#box').numberspinner({
            required: true,     //继承验证框组件的，不能为空
            width: 200,         //继承微调组件的，宽度
            height: 30,         //继承微调组件的，高度
            value: 2,           //继承微调组件的，设置值
            min: 1,             //继承微调组件的，最小值
            max: 500,           //继承微调组件的，最大值
            increment: 1,       //继承微调组件的，增量
            spin: function (down) {     //继承微调组件的，点击微调按钮事件
                alert(down);
            },
        });
    });
[/code]





**三．事件列表**

**NumberSpinner(数字微调)组件继承自 Spinner(微调)组件。**

[code]

    $( function () {
        $('#box').numberspinner({
            required: true,     //继承验证框组件的，不能为空
            width: 200,         //继承微调组件的，宽度
            height: 30,         //继承微调组件的，高度
            value: 2,           //继承微调组件的，设置值
            min: 1,             //继承微调组件的，最小值
            max: 500,           //继承微调组件的，最大值
            increment: 1,       //继承微调组件的，增量
            onSpinUp: function () {
                alert('点击了上微调按钮');
            },
            onSpinDown: function () {
                alert('点击了下微调按钮');
            },
        });
    });
[/code]





**四．方法列表**

**NumberSpinner(数字微调)组件继承自 Spinner(微调)组件方法**

**如：取值赋值**

[code]

    $( function () {
        $('#box').numberspinner({
            required: true,     //继承验证框组件的，不能为空
            width: 200,         //继承微调组件的，宽度
            height: 30,         //继承微调组件的，高度
            value: 2,           //继承微调组件的，设置值
            min: 1,             //继承微调组件的，最小值
            max: 500,           //继承微调组件的，最大值
            increment: 1,       //继承微调组件的，增量
        });
        $('#box').numberspinner('setValue', 100);
        alert($('#box').numberspinner('getValue'));
    });
[/code]





**我们可以使用$.fn.numberspinner.defaults 重写默认值对象。**



