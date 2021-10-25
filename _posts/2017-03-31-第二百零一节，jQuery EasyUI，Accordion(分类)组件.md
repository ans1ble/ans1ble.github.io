---
layout: post
title: " 第二百零一节，jQuery EasyUI，Accordion(分类)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Accordion(分类)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331175706570-1844410142.png)

**学习要点：**

**1.加载方式**

**2.容器属性**

**3.事件列表**

**4.方法列表**

**5.面板属性**



**本节课重点了解 EasyUI 中 Accordion(选项卡)组件的使用方法，这个组件依赖于 Panel（面板）组件。**



**一．加载方式**

**class 加载方式**

[code]

     <div id="box" class="easyui-accordion"
         style="width:300px;height:200px;">
        <div title="标题1">内容1</div>
        <div title="标题2">内容2</div>
        <div title="标题3">内容3</div>
    </div>
[/code]

**accordion()将一个符合规则的元素执行分类方法**

**JS 加载调用**

[code]

    $( function () {
        $('#box').accordion({
            //...
        });
    });
[/code]





**二．容器属性，也就是最外层区块**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331162324414-953729212.png)

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331162331086-1804455733.png)

**width   number 分类容器的宽度。默认值 auto。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400      //分类容器的高度
        });
    });
[/code]



**height   number 分类容器的高度。默认值 auto。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400      //分类容器的高度
        });
    });
[/code]



**fit   boolean 如果设置为 true，分类容器大小将自适应父容器。默认值 false。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            fit:true        //如果设置为 true，分类容器大小将自适应父容器。默认值 false。
        });
    });
[/code]



**border   boolean 定义是否显示边框。默认值 true。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            border:false     //定义是否显示边框。默认值 true。
        });
    });
[/code]



**animate   boolean 定义在展开和折叠的时候是否显示动画效果。默认值 true。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            animate:false     //定义在展开和折叠的时候是否显示动画效果。默认值 true。
        });
    });
[/code]



**multiple   boolean 如果为 true 时，同时展开多个面板。默认值 false。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            multiple:true   //如果为 true 时，同时展开多个面板。默认值 false。
        });
    });
[/code]



**selected   number 设置初始化时默认选中的面板索引号。默认值0。默认展开**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1   //设置初始化时默认选中的面板索引号。默认值0。
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331163454492-1087418083.png)**

**onSelect   title,index 在面板被选中的时候触发。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1,   //设置初始化时默认选中的面板索引号。默认值0。
            onSelect:function (title,index) {
                alert('在面板被选中的时候触发。');
                alert(title + '：' + '接收被选中的面板标题');
                alert(index + '：' + '接收被选中的面板索引');
            }
        });
    });
[/code]



**onUnselect   title,index 在面板被取消选中的时候触发。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1,   //设置初始化时默认选中的面板索引号。默认值0。
            onUnselect:function (title,index) {
                alert('在面板被取消选中的时候触发。');
                alert(title + '：' + '接收被取消选中的面板标题');
                alert(index + '：' + '接收被取消选中的面板索引');
            }
        });
    });
[/code]



**onAdd   title,index 在添加新面板的时候触发。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1,   //设置初始化时默认选中的面板索引号。默认值0。
            onAdd:function (title,index) {
                alert('在添加新面板的时候触发。');
                alert(title + '：' + '接收添加的面板标题');
                alert(index + '：' + '接收添加的面板索引');
            }
        });
        $('#box').accordion('add', {
            title: '新分类',
            closable: true,
            content: '123',
            collapsible: false,
            selected: false
        });
    });
[/code]



**onBeforeRemove   title,index 在移除面板之前触发，返回 false 可以取消移除操作。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1,   //设置初始化时默认选中的面板索引号。默认值0。
            onBeforeRemove:function (title,index) {
                alert('在移除面板之前触发，返回 false 可以取消移除操作。');
                alert(title + '：' + '接收移除的面板标题');
                alert(index + '：' + '接收移除的面板索引');
            }
        });
        $('#box').accordion('remove', 0);
    });
[/code]



**onRemove   title,index 在面板被移除后候触发。**

[code]

    $(function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1,   //设置初始化时默认选中的面板索引号。默认值0。
            onRemove:function (title,index) {
                alert('在面板被移除后候触发。');
                alert(title + '：' + '接收移除的面板标题');
                alert(index + '：' + '接收移除的面板索引');
            }
        });
        $('#box').accordion('remove', 1);
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331165452274-1227787630.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331165503180-367301020.png)**

**options none 返回分类组件的属性对象。**

[code]

    $( function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('options'));   //返回分类组件的属性对象。
    });
[/code]



**panels none 获取所有面板对象。**

[code]

    $( function () {
        $('#box').accordion({
            width:500,      //分类容器的宽度
            height:400,      //分类容器的高度
            selected:1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('panels'));   //获取所有面板对象
    });
[/code]



**resize none 调整分类组件大小和布局。 重要也就是分类变形后可以重置**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('resize');      //调整分类组件大小和布局。重要也就是分类变形后可以重置
    });
[/code]



**getSelected none 获取选中的面板对象。**

[code]

    $( function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('getSelected'));      // 获取选中的面板对象。
    });
[/code]



**getSelections   none 获取所有选中的面板对象。**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('getSelections'));      // 获取所有选中的面板。
    });
[/code]



**getPanel   which 获取指定的面板，'which'参数可以是面板的标题或者索引。**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('getPanel',2));      // 获取指定的面板，'which'参数可以是面板的标题或者索引。
    });
[/code]



**getPanelIndex   panel 获取指定面板的索引。值是要获取的面板id**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        alert($('#box').accordion('getPanelIndex','#pox'));      // 获取指定面板的索引。值是要获取的面板id
    });
[/code]



**select   which 选择指定面板。'which'参数可以是面板标题或者索引。**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('select',2);   //选择指定面板。'which'参数可以是面板标题或者索引。
    });
[/code]



**unselect   which 取消选择指定面板。'which'参数可以是面板标题或者索引。**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('unselect',1);   //取消选择指定面板。'which'参数可以是面板标题或者索引。
    });
[/code]



**add   options添加一个新面板。在默认情况下，新增的面板会变成当前面板。如果要添加一个非选中面板，不要忘记将'selected'属性设置为
false。添加一个分类面板**

**因为分类组件继承了 **Panel（面板）组件，** 新增面板属性可以用 ** **（面板）组件属性，其他属性见，五．面板属性******

[code]

    $( function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('add', {
            title: '新分类',
            // closable: true,
            content: '123',
            // collapsible: false,
            // selected: false
        });
    });
[/code]



**remove   which 移除指定面板。'which'参数可以使面板的标题或者索引。**

[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('remove',0);    //移除指定面板。'which'参数可以使面板的标题或者索引。
    });
[/code]





**$.fn.accordion.defaults 重写默认值对象。**

[code]

    $.fn.accordion.defaults.border =  false;
[/code]





**五．面板属性**

**分类组件面板继承了 panel 属性，我们参考 panel 属性即可，对分类的面板同样有效。 并且提供了新增的两个属性。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331173707086-773484481.png)**

**selected boolean 如果设置为 true 将展开面板。**

[code]

    $( function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('add', {
            title: '新分类',
            content: '123',
            collapsible: true,     //如果设置为 true 将显示折叠按钮。
            selected: true     //如果设置为 true 将展开面板。
        });
    });
[/code]



  
**collapsible boolean 如果设置为 true 将显示折叠按钮。**



[code]

    $(function () {
        $('#box').accordion({
            width: 500,      //分类容器的宽度
            height: 400,      //分类容器的高度
            selected: 1   //设置初始化时默认选中的面板索引号。默认值0。
        });
        $('#box').accordion('add', {
            title: '新分类',
            content: '123',
            collapsible: true,     //如果设置为 true 将显示折叠按钮。
            selected: true     //如果设置为 true 将展开面板。
        });
    });
[/code]



