---
layout: post
title: " 第二百零五节，jQuery EasyUI，Messager(消息窗口)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Messager(消息窗口)组件**



**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 Messager(消息窗口)组件的使用方法， 这个组件依赖于
Window(窗口)组件、progressbar(进度条)组件。**



**一．加载方式**

**消息窗口提供了不同的消息框风格， 包含 alert(警告框)、confirm(确认框)、
prompt(提示框)、progress(进度框)等。所有消息框都是异步的，用户可以在交互消息之 后使用回调函数去处理结果。**

**由于这个组件的特殊性，没有 class 加载方式，全部在 JS 端完成！ 不需要获取html区块元素，是直接在js里写的**



**二．属性列表， 自定义所有消息框的确认和取消两个按钮的文字**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401220848695-1634154639.png)**

[code]

    $( function () {
        $.messager.defaults = { ok: "是", cancel: "否" }; //自定义所有消息框的确认和取消两个按钮的文字
        $.messager.show({
            title: '我的消息',
            msg: '消息在 5 秒后关闭',
            timeout: 5000,
            showType: 'slide'
        });
    });
[/code]







**三．方法列表**

**方法就是定义消息框的类型**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401220941195-1989902431.png)**

**$.messager.show   options  使用消息框**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401232501039-1772099257.png)**

**在屏幕右下角显示一条消息窗口。该选项参数是一个可配置的对象：**  
 **showType：定义将如何显示该消息。可用值有：null,slide,fade,show。默认：slide。消息框出现的方式**  
 **showSpeed：定义窗口显示的过度时间。默认：600 毫秒。**  
 **width：定义消息窗口的宽度。默认：250px。**  
 **height：定义消息窗口的高度。默认：100px。**  
 **title：在头部面板显示的标题文本。**  
 **msg：显示的消息文本。**  
 **style：定义消息窗体的自定义样式。**

**timeout：如果定义为 0，消息窗体将不会自动关闭，除非用户关闭他。如果定义成非 0 的数，消息窗体将在超时后自动关闭。默认：4 秒。
设置对少时间自动关闭**

[code]

    $(function () {
        $.messager.show({
            title: '我的消息',
            msg: '消息在 5 秒后关闭',
            timeout: 5000,
            showType: 'slide',
        });
    });
[/code]

**style：定义消息窗体的自定义样式。**

[code]

    $( function () {
        $.messager.show({
            title: '我的消息',
            msg: '消息在 5 秒后关闭',
            timeout: 5000,
            showType: 'slide',
            style: {
                top: 0
            }
        });
    });
[/code]







**$.messager.alert   title, msg, icon, fn   **使用警告框，四个参数均为可选****

****![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401223609914-861314343.png)****

****显示警告窗口。参数：****

****title：在头部面板显示的标题文本。****

****msg：显示的消息文本。****

****icon：显示的图标图像。可用值有：**** ** **error,question,info,warning。****

****![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401222655180-827081940.png)****

****fn: 在窗口关闭的时候触发该回调函数。****

[code]

    $( function () {
        $.messager.alert('警告框','这是一个警告框！','warning',function () {
            alert('点击确定后触发');
        });
    });
[/code]





  
**$.messager.confirm   title, msg, fn  使用确认框，三个参数均可选**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401224524820-347623713.png)**

**显示一个包含“确定”和“取消”按钮的确认消息窗口。参数：**

**title：在头部面板显示的标题文本。**

**msg：显示的消息文本。**

**fn(b): 当用户点击“确定”按钮的时侯将传递一个 true 值给回调函数，否则传递一个 false 值。函数的参数可以自定义**

[code]

    $( function () {
        $.messager.confirm('确认对话框','你真的要删除吗？',function (jesho) {
            if (jesho){
                alert('点击的确定');
            }else {
                alert('点击的取消');
            }
        });
    });
[/code]





  
**$.messager.prompt   title, msg, fn   **使用提示框，三个参数均可选****

****![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401225443008-1839665115.png)****

**显示一个用户可以输入文本的并且带“确定”和“取消”按钮的消息窗体。参数：**

**title：在头部面板显示的标题文本。**

**msg：显示的消息文本。**

**fn(val): 在用户输入一个值参数的时候执行的回调函数。参数接收用户输入的值**

[code]

    $( function () {
        $.messager.prompt('提示信息框','请输入你的名字：',function (val) {
            if (val){   //判断如果有输入值
                alert(val);
            }
        });
    });
[/code]





  
**$.messager.progress   options or method  进度条信息框**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401231121336-2072177066.png)**

**显示一个进度消息窗体。 属性定义为：**

**title：在头部面板显示的标题文本。默认：空。**

**msg：显示的消息文本。默认：空。**

**text：在进度条上显示的文本。默认：undefined。**

**interval：每次进度更新的间隔时间。默认：300 毫秒。**

**  方法定义为： **

**bar：获取进度条对象。 $.messager.progress('bar'); **

**close：关闭进度窗口。 $.messager.progress('close');**

[code]

    $(function () {
        $.messager.progress({
            title: '执行中',
            msg: '努力加载中...',
            text: '{value}%',
            interval: 100,
        });
        // $.messager.progress('bar');
        // $.messager.progress('close');
    });
[/code]



