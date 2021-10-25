---
layout: post
title: " 第二百零三节，jQuery EasyUI，Window(窗口)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Window(窗口)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401173118477-1222626233.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Window(窗口)组件的使用方法，这个组件依赖于 Panel（面 板）组件、resizable(调整大小)和
draggable(拖动)组件。这个组件扩展与 Panel 组件， 最大的优势就是调整大小和拖动以及内部布局。**



**一．加载方式**

**class 加载方式**

[code]

     <div id="box" class="easyui-window" title="My Window"
         style="width:600px;height:400px"
         data-options="iconCls:'icon-save',modal:true">
        窗口
    </div>
[/code]

**window()让一个元素，执行窗口方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').window({
            width: 600,
            height: 400,
            modal: true
        });
    });
[/code]





**二．属性列表**

**窗口属性扩展自 Panel(面板)，窗口新增或重新定义的属性如下：**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401152452742-850446016.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401152500602-1189319152.png)**

**title   string 窗口的标题文本。默认值为“New Window”。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
        });
    });
[/code]



**collapsible   boolean 定义是否显示可折叠按钮。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            collapsible:false   //定义是否显示可折叠按钮。默认值为 true。
        });
    });
[/code]



**minimizable   boolean 定义是否显示最小化按钮。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            collapsible:false,   //定义是否显示可折叠按钮。默认值为 true。
            minimizable:false   //定义是否显示最小化按钮。默认值为 true。
        });
    });
[/code]



**maximizable   boolean 定义是否显示最大化按钮。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            collapsible:false,   //定义是否显示可折叠按钮。默认值为 true。
            minimizable:false,   //定义是否显示最小化按钮。默认值为 true。
            maximizable:false   //定义是否显示最大化按钮。默认值为 true。
        });
    });
[/code]



**closable   boolean 定义是否显示关闭按钮。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            collapsible:false,   //定义是否显示可折叠按钮。默认值为 true。
            minimizable:false,   //定义是否显示最小化按钮。默认值为 true。
            maximizable:false,   //定义是否显示最大化按钮。默认值为 true。
            closable:false      //定义是否显示关闭按钮。默认值为 true。
        });
    });
[/code]



**closed   boolean 定义是否可以关闭窗口。默认值为 false。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            collapsible:false,   //定义是否显示可折叠按钮。默认值为 true。
            minimizable:false,   //定义是否显示最小化按钮。默认值为 true。
            maximizable:false,   //定义是否显示最大化按钮。默认值为 true。
            closable:false,      //定义是否显示关闭按钮。默认值为 true。
            closed:true         //定义是否关闭窗口。默认值为 false。
        });
    });
[/code]



**zIndex   number 窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
        });
    });
[/code]



**draggable   boolean 定义是否能够拖拽窗口。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999,          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
            draggable:false     //定义是否能够拖拽窗口。默认值为 true。
        });
    });
[/code]



**resizable   boolean 定义是否能够改变窗口大小。默认值为true。**

[code]

    $(function () {
        $('#box').window({
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999,          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
            draggable:false,     //定义是否能够拖拽窗口。默认值为 true。
            resizable:false     //定义是否能够改变窗口大小。默认值为true。
        });
    });
[/code]



**shadow   boolean 如果设置为 true，在窗体显示的时候显示阴影。默认值为 true。**

[code]

    $(function () {
        $('#box').window({
            width: 600,
            height: 400,
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999,          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
            draggable:false,     //定义是否能够拖拽窗口。默认值为 true。
            resizable:false,     //定义是否能够改变窗口大小。默认值为true。
            shadow:false        //如果设置为 true，在窗体显示的时候显示阴影。默认值为 true。
        });
    });
[/code]



**inline   boolean定义如何布局窗口，如果设置为 true，窗口将显示在它的父容器中，否则将显示在所有元素的上面。默认值为 false。**

[code]

    $(function () {
        $('#box').window({
            width: 400,
            height: 200,
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999,          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
            draggable:false,     //定义是否能够拖拽窗口。默认值为 true。
            resizable:false,     //定义是否能够改变窗口大小。默认值为true。
            shadow:false,        //如果设置为 true，在窗体显示的时候显示阴影。默认值为 true。
            inline:false         //定义如何布局窗口，如果设置为 true，窗口将显示在它的父容器中，否则将显示在所有元素的上面。默认值为 false。
        });
    });
[/code]



**modal   boolean 定义是否将窗体显示为模式化窗口。默认值为 true。是否显示遮罩**

[code]

    $(function () {
        $('#box').window({
            width: 400,
            height: 200,
            title:'窗口标题',   //窗口的标题文本。默认值为“New Window”。
            zIndex:99999,          //窗口 Z 轴坐标。默认值为9000。也就是外层等级，设置层级关系
            draggable:false,     //定义是否能够拖拽窗口。默认值为 true。
            resizable:false,     //定义是否能够改变窗口大小。默认值为true。
            shadow:false,        //如果设置为 true，在窗体显示的时候显示阴影。默认值为 true。
            inline:false,         //定义如何布局窗口，如果设置为 true，窗口将显示在它的父容器中，否则将显示在所有元素的上面。默认值为 false。
            modal:true          //定义是否将窗体显示为模式化窗口。默认值为 true。是否显示遮罩
        });
    });
[/code]

**还有其他属性可以用Panel(面板)的属性，因为他继承Panel(面板)**

**PS：以上属性是 Window 自行扩展或代替 Panel 的属性，本身 Window 就是依赖于 Panel 的。所以，上面没有涉及到的属性，请查看
Panel 的属性即可。比如：**

[code]

     //这里的 fit 和 iconCls 来自 Panel 属性
    $('#box').window({
        width : 600,
        height : 400,
        modal : true,
        fit : true,
        iconCls : 'icon-add',
    });
[/code]



**三．事件列表**

**窗口的事件完整继承自 Panel(面板)。所以，直接参考 Panel 面板的事件即可。 事件见 **Panel(面板)事件****

**如：**

[code]

    $( function () {
        $('#box').window({
            width: 400,
            height: 200,
            title: '窗口标题',   //窗口的标题文本。默认值为“New Window”。
            onClose: function () {
                alert('关闭后触发！');
            }
        });
    });
[/code]



**四．方法列表**

**窗口的方法扩展自 Panel(面板)，窗口新增方法如下：**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170401160255102-278495190.png)**

**window   none 返回外部窗口对象**

[code]

    $(function () {
        $('#box').window({
            width: 400,
            height: 200,
            title: '窗口标题'   //窗口的标题文本。默认值为“New Window”。
        });
        alert($('#box').window('window'));     //返回外部窗口对象
    });
[/code]



  
**hcenter   none 仅水平居中窗口。当窗口位置发生改变时，将窗口重新 **仅水平居中窗口****

[code]

    $( function () {
        $('#box').window({
            width: 400,
            height: 200,
            title: '窗口标题'   //窗口的标题文本。默认值为“New Window”。
        });
        $('#box').window('hcenter');     //仅水平居中窗口。
    });
[/code]

[code]

        //单击时调整位置
        $(document).click(function () {
            $('#box').window('move', {
                left: 0,
                top: 0,
            });
        });
        //双击时恢复各种居中
        $(document).dblclick(function () {
            //替换成 center 或 vcenter 亦可
            $('#box').window('hcenter');
        });
[/code]



  
**vcenter   none 仅垂直居中窗口。 **当窗口位置发生改变时，将窗口重新 **仅垂直居中窗口******

[code]

    $( function () {
        $('#box').window({
            width: 400,
            height: 200,
            title: '窗口标题'   //窗口的标题文本。默认值为“New Window”。
        });
        $('#box').window('vcenter');     //当窗口位置发生改变时，将窗口重新仅垂直居中窗口
    });
[/code]



  
**center   none 将窗口绝对居中。 **当窗口位置发生改变时，将窗口重新 **绝对** **居中窗口******

[code]

    $( function () {
        $('#box').window({
            width: 400,
            height: 200,
            title: '窗口标题'   //窗口的标题文本。默认值为“New Window”。
        });
        $('#box').window('center');     //当窗口位置发生改变时，将窗口重新绝对居中窗口
    });
[/code]



**其他方法见 **Panel(面板)的方法****



****使用$.fn.window.defaults 重写默认值对象。 见前面的****







****window 组件最强大的地方就是可以 内部布局和添加 linkbutton。 具体布局方法如下：****

****1.外部用 window 组件包裹一下；****

****2.内部用 layout 组件左右各分配一个，底部分配一个；****

****3.底部添加一个按钮即可。****

[code]

     <div class="easyui-window" style="width:400px;height:250px;">
        <div class="easyui-layout" data-options="fit:true,">
            <div data-options="region:'west',split:true," style="width:100px;">左边</div>
            <div data-options="region:'center'">内容</div>
            <div data-options="region:'south',border:false" style="height:40px;text-align:right;padding:5px 5px 0 0">
                <a class="easyui-linkbutton" data-options="iconCls:'icon-ok'" style="width:80px;">确认</a>
                <a class="easyui-linkbutton" data-options="iconCls:'icon-cancel'" style="width:80px;">取消</a>
            </div>
        </div>
    </div>
[/code]



