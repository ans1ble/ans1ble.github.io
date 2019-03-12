---
layout: post
title: " 第二百节，jQuery EasyUI，Tabs(选项卡)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Tabs(选项卡)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330223806649-887825760.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**

**5.选项卡面板**



**本节课重点了解 EasyUI 中 Tabs(选项卡)组件的使用方法， 这个组件依赖于 Panel（面 板）组件和 LinkButton(按钮)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <div id="box" class="easyui-tabs" style="width:500px;height:250px;">
        <div title="Tab1">
            tab1
        </div>
        <div title="Tab2" data-options="closable:true">
            tab2
        </div>
        <div title="Tab3"
             data-options="iconCls:'icon-reload',closable:true">
            tab3
        </div>
    </div>
[/code]

**tabs()将符合规则的元素实现选项卡方法**

**htnl**

[code]

     <div id="box">
        <div title="Tab1">
            tab1
        </div>
        <div title="Tab2">
            tab2
        </div>
        <div title="Tab3">
            tab3
        </div>
    </div>
[/code]

**js代码**

[code]

     $('#box').tabs({
    　　//...
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330183437695-1605886309.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330183445914-2083746879.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330183459852-753830923.png)**

**width   number 选项卡容器宽度。默认值 auto。**

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400      //选项卡容器高度
        });
    });
[/code]



**height  number 选项卡容器高度。默认值 auto。**

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400      //选项卡容器高度
        });
    });
[/code]



**plain   boolean 设置为 true 时，将不显示控制面板背景。默认值 false。**

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400,      //选项卡容器高度
            plain:true      //设置为 true 时，将不显示控制面板背景。默认值 false。
        });
    });
[/code]



  
**fit   boolean 设置为 true 时，选项卡的大小将铺满它所在的容器。默认值 false。**

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400,      //选项卡容器高度
            fit:true      //设置为 true 时，选项卡的大小将铺满它所在的容器。默认值 false。
        });
    });
[/code]



**border   boolean 设置为 true 时，显示选项卡容器边框。默认值 true。**

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400,      //选项卡容器高度
            border:false      //设置为 true 时，显示选项卡容器边框。默认值 true。
        });
    });
[/code]



**scrollIncrement   number
选项卡滚动条每次滚动的像素值。默认值100。也就是按钮滚动的像素，按钮少时结合tabWidth属性使用**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330190531024-1118655991.png)

[code]

    $(function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400,      //选项卡容器高度
            tabWidth:300,    //设置按钮宽度
            scrollIncrement:50      //选项卡滚动条每次滚动的像素值。默认值100
        });
    });
[/code]



**scrollDuration   number 每次滚动动画持续的时间，单位：毫秒。默认值400。 **也就是按钮滚动的速度****

[code]

    $( function () {
        $('#box').tabs({
            width:500,      //选项卡容器宽度
            height:400,      //选项卡容器高度
            tabWidth:300,    //设置按钮宽度
            scrollIncrement:50,      //选项卡滚动条每次滚动的像素值。默认值100
            scrollDuration:500      //每次滚动动画持续的时间，单位：毫秒。默认值400。
        });
    });
[/code]



**tools   array,selector工具栏添加在选项卡面板头的左侧或右侧。可用的值有：1. 一个工具菜单数组，每个工具选项都和
linkbutton 相同。2. 一个指向<div/>容器工具菜单的选择器。默认值null。**

**给选项卡头部设置工具栏，接收一个数组，数组里接收一个对象，对象里是键值对设置图标和点击事件**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330191711820-1466705795.png)**

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tools: [{           //给选项卡头部设置工具栏，接收一个数组，数组里接收一个对象，对象里是键值对设置图标和点击事件
                iconCls: 'icon-add',
                handler: function () {
                    alert('添加!');
                }
            }]
        });
    });
[/code]



**toolPosition   string 工具栏位置。可用值：'left','right'。默认值 right。工具栏位置**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tools: [{           //给选项卡头部设置工具栏，接收一个数组，数组里接收一个对象，对象里是键值对设置图标和点击事件
                iconCls: 'icon-add',
                handler: function () {
                    alert('添加!');
                }
            }],
            toolPosition:'left'     //工具栏位置。可用值：'left','right'。默认值 right。
        });
    });
[/code]



**tabPosition   string选 项 卡 位 置 。 可 用 值
：'top','bottom','left','right'。默认值：top。按钮位置**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tabPosition:'bottom' //string选 项 卡 位 置 。 可 用 值 ：'top','bottom','left','right'。默认值：top。按钮位置
        });
    });
[/code]



**headerWidth   number选项卡标题宽度，在 tabPosition
属性设置为'left'或'right'的时候才有效。默认值：150。设置按钮标题宽度，只有在按钮设置左或者右的时候有效**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330193020070-181163009.png)

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tabPosition:'left',
            headerWidth:50     //选项卡标题宽度，在 tabPosition 属性设置为'left'或'right'的时候才有效。默认值：150。设置按钮宽度
        });
    });
[/code]





**tabWidth   number 标签条的宽度。默认值：auto。设置按钮宽度**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tabWidth:200    //标签条的宽度。默认值：auto。
        });
    });
[/code]



**tabHeight   number 标签条的高度。默认值：27。设置按钮高度**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tabWidth:200,    //标签条的宽度。默认值：auto。
            tabHeight:100   //标签条的高度。默认值：27。
        });
    });
[/code]



**selected   number 初始化选中一个 tab 页。默认值：0。默认选择，值为索引**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            selected:1      //初始化选中一个 tab 页。默认值：0。默认选择值为索引
        });
    });
[/code]



**showHeader   boolean 设置为 true 时，显示 tab 页标题。默认值：true。是否显示按钮**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            selected:1,      //初始化选中一个 tab 页。默认值：0。默认选择值为索引
            showHeader :false   //设置为 true 时，显示 tab 页标题。默认值：true。是否显示按钮
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330194320836-1095139834.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330194326539-1183742502.png)**

**onLoad  panel 在 ajax 选项卡面板加载完远程数据的时候触发。**



[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onLoad:function (panel) {
                alert('在 ajax 选项卡面板加载完远程数据的时候触发。');
                alert('接收当前选项卡的对象' + panel);
            }
        });
        $('#box').tabs('add',{      //添加一个新选项卡面板
            id:'xmb',           //设置新增id
            title:'新按钮',      //设置新增按钮标题
            content:'新内容',     //设置新增内容
            href :'is_user.php'  //加载一个外部文件
            //更多见第五节
        });
    });
[/code]







**onSelect title,index 用户在选择一个选项卡面板的时候触发。 **title,index分别接收选择的按钮标题和按钮索引****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onSelect:function (title,index) {
                alert('用户在选择一个选项卡面板的时候触发。');
                alert('接收选择的按钮标题'+title);
                alert('接收选择的按钮索引'+index);
            }
        });
    });
[/code]



**onUnselect   title,index 用户在取消选择一个选项卡面板的时候触发。 **
**title,index分别接收选择的上一个按钮标题和按钮索引******

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onUnselect:function (title,index) {
                alert('用户在取消选择一个选项卡面板的时候触发。');
                alert('接收选择的上一个按钮标题'+title);
                alert('接收选择的上一个按钮索引'+index);
            }
        });
    });
[/code]



**onBeforeClose   title,index在选项卡面板关闭的时候触发，返回false
取消关闭操作。下面的例子展示了在关闭选项卡面板之前以何种方式显示确认对话框。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onBeforeClose:function (title,index) {
                alert('在选项卡面板关闭的时候触发');
                alert('接收选择的关闭按钮标题'+title);
                alert('接收选择的关闭按钮索引'+index);
            }
        });
    });
[/code]



**onClose   title,index 在用户关闭一个选项卡面板之后触发。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onClose:function (title,index) {
                alert('在用户关闭一个选项卡面板之后触发。');
                alert('接收选择的关闭按钮标题'+title);
                alert('接收选择的关闭按钮索引'+index);
            }
        });
    });
[/code]



**onAdd   title,index 在添加一个新选项卡面板的时候触发。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onAdd:function (title,index) {   //在添加一个新选项卡面板的时候触发。
                alert('获取新添加的面板标题：'+ title + '|' + '获取新添加的面板索引：' + index);
            }
        });
        $('#box').tabs('add',{      //添加一个新选项卡面板
            id:'xmb',           //设置新增id
            title:'新按钮',      //设置新增按钮标题
            content:'新内容'     //设置新增内容
            //更多见第五节
        });
    });
[/code]



**onUpdate   title,index 在更新一个选项卡面板的时候触发。修改时触发**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onUpdate:function (title,index) {
                alert('修改时触发');
                alert(title + '|' + index);  //接收选项卡的按钮和索引
            }
        });
        $('#box').tabs('update',{
            tab:$('#cfh'),  //要修改的面板id
            options:{       //要修改的属性
                title:'修改标题'
            }
        });
    });
[/code]



**onContextMenu   e,title,index 在右键点击一个选项卡面板的时候触发。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            onContextMenu:function (e,title,index) {
                alert('在右键点击一个选项卡面板的时候触发。');
                alert('接收右键点击按钮标题'+title);
                alert('接收右键点击按钮索引'+index);
            }
        });
    });
[/code]





**四．方法列表 Tabs 方法**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330203052508-303865754.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330203101086-1316389766.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330203229602-1714715207.png)**



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330203242430-1935991889.png)

**options   none 返回选项卡属性。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
        });
        alert($('#box').tabs('options'));  //返回选项卡属性。
    });
[/code]



**tabs   none 返回所有选项卡面板。也就是返回所有按钮对象**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
        });
        alert($('#box').tabs('tabs'));  //返回所有选项卡面板。也就是返回所有按钮对象
    });
[/code]



**resize   none 调整选项卡容器大小和布局。也就是选项卡如果因为什么原因变形了，可以重置这个选项卡**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
        });
        alert($('#box').tabs('resize'));  //也就是选项卡如果因为什么原因变形了，可以重置这个选项卡
    });
[/code]



**add
options添加一个新选项卡面板，选项参数是一个配置对象，查看选项卡面板属性的更多细节。在添加一个新选项卡面板的时候它将变成可选的。添加一个非选中状态的选项卡面板时，记得设**

**置'selected'属性为 false。 第二个参数是一个对象，以键值对方式设置新增的面板属性，详情见第五节 **选项卡面板****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
        });
        $('#box').tabs('add',{      //添加一个新选项卡面板
            id:'xmb',           //设置新增id
            title:'新按钮',      //设置新增按钮标题
            content:'新内容'     //设置新增内容
            //更多见第五节
        });
    });
[/code]



**close   which关闭一个选项卡面板，'which'参数可以是选项卡面板的标题或者索引，以指定要关闭的面板。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('close',1);  //关闭一个选项卡面板，'which'参数可以是选项卡面板的标题或者索引，以指定要关闭的面板。
    });
[/code]



**getTab   which 获取指定选项卡面板，'which'参数可以是选项卡面板的标题或者索引。 **获取指定选项卡面板对象****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        alert($('#box').tabs('getTab',1));  //which 获取指定选项卡面板，'which'参数可以是选项卡面板的标题或者索引。
    });
[/code]



**getTabIndex   tab 获取指定选项卡面板的索引。获取指定id的按钮索引**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        alert($('#box').tabs('getTabIndex','#cfh'));  //获取指定选项卡面板的索引
    });
[/code]



**getSelected   none获取选择的选项卡面板。下面的例子展示了如何获取选择的选项卡面板索引。获取以选定的选项 **卡面板对象****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        alert($('#box').tabs('getSelected'));  //获取指定选项卡面板的对象
    });
[/code]



  
**select   which 选择一个选项卡面板，'which'参数可以是选项卡面板的标题或者索引。 **选择一个选项卡面板****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('select',1);  //选择一个选项卡面板
    });
[/code]



**unselect   which 取消选择一个选项卡面板，'which'参数可以是选项卡面板的标题或者索引。取消选择的选项卡**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('unselect',0);  //取消选择的选项卡
    });
[/code]



**showHeader   none 显示选项卡的标签头。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('showHeader');  //显示选项卡的标签头。
    });
[/code]



**hideHeader   none 隐藏选项卡的标签头。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('hideHeader');  //隐藏选项卡的标签头
    });
[/code]



**exists   which 表明指定的面板是否存在，'which'参数可以是选项卡面板的标题或索引。 **指定的面板是否存在，返回布尔值****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        alert($('#box').tabs('exists',4));  //指定的面板是否存在
    });
[/code]



**update   param更新指定的选项卡面板，'param'参数包含2个属性：tab：要更新的选项卡面板。options：面板的属性。修改面板**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('update',{
            tab:$('#cfh'),  //要修改的面板id
            options:{       //要修改的属性
                title:'修改标题'
            }
        });
    });
[/code]



**enableTab   which 启用指定的选项卡面板，'which'参数可以是选项卡面板的标题或索引。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('disableTab',1);  //禁用指定的选项卡面板
        $('#box').tabs('enableTab',1);  //启用指定的选项卡面板
    });
[/code]



**disableTab   which 禁用指定的选项卡面板，'which'参数可以是选项卡面板的标题或索引。**

[code]

    $(function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400      //选项卡容器高度
        });
        $('#box').tabs('disableTab',1);  //禁用指定的选项卡面板
    });
[/code]



**scrollBy   deltaX 滚动选项卡标题指定的像素数量，负值则向右滚动，正值则向左滚动。就是网页一打开 **滚动选项卡移动多少****

****![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330221437070-214255576.png)****

[code]

    $( function () {
        $('#box').tabs({
            width: 500,      //选项卡容器宽度
            height: 400,      //选项卡容器高度
            tabWidth:200
        });
        $('#box').tabs('scrollBy',1);  //滚动选项卡标题指定的像素数量，负值则向右滚动，正值则向左滚动
    });
[/code]



**五．选项卡面板， 以下一般是在新增选项卡时使用**

**给选项卡属性一样的下面就不举例了**

**选项卡面板继承了 panel 一些属性，以下是公共属性。**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330205744102-950579192.png)

**id   string 选项卡面板的 ID 属性。默认值 null。**

**title   string 选项卡面板的标题文本。默认值空。**

**content   string 选项卡面板的内容。默认值空。**

**href   string 从 URL 加载远程数据内容填充到选项卡面板。默认值 null。**

**cache   boolean 如果为 true，在'href'属性设置了有效值的时候缓存选项卡面板。默认值 true。**

**iconCls  string 定义了一个图标的 CSS 类 ID 显示到选项卡面板标题。默认值 null。**

**width   number 选项卡面板宽度。默认值 auto。**

**height   number 选项卡面板高度。默认值 auto。**

**collapsible   boolean 如果为 true，则允许选项卡摺叠。默认值false。**



**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330223414352-258877133.png)**



**closable   boolean设置为 true 时，选项卡面板将显示一个关闭按钮，在点击的时候会关闭选项卡面板。默认为 false。**

**selected   boolean 设置为 true 时，选项卡面板会被选中。默认为 false。**

