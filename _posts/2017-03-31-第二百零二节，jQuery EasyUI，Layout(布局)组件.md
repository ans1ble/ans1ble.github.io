---
layout: post
title: " 第二百零二节，jQuery EasyUI，Layout(布局)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Layout(布局)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331211440399-320094003.png)

**学习要点：**

**1.加载方式**

**2.布局属性**

**3.区域面板属性**

**4.方法列表**



**本节课重点了解 EasyUI 中 Layout(布局)组件的使用方法，这个组件依赖于 Panel（面 板）组件和
resizable(调整大小)组件。**



**一．加载方式**

**class 加载方式，这个属性一般使用 **class方法使用****

[code]

     <body id="box" class="easyui-layout">
        <div data-options="region:'north',title:'头部标题',split:true" style="height:100px;"></div>
        <div data-options="region:'south',title:'底部标题',split:true" style="height:100px;"></div>
        <div data-options="region:'east',title:'右边标题',split:true" style="width:100px;"></div>
        <div data-options="region:'west',title:'左边标题',split:true" style="width:100px;"></div>
        <div data-options="region:'center',title:'中间标题'" style="padding:5px;background:#eee;"></div>
    </body>
[/code]



**layout()将一个符合要求的元素执行布局方法**

[code]

    $( function () {
        $('#box').layout({
            //......
        });
    });
[/code]





**二．布局属性**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331185525586-1498661037.png)**

**fit   boolean如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为
false。**

[code]

    $(function () {
        $('#box').layout({
            fit:true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
    });
[/code]





**三．区域面板属性**

**一般写在html属性data-options里**

**区域面板属性定义与 panel 组件类型，下面是公共和新增的属性：**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331190101242-674049817.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331190108133-1258787713.png)**



**title string 布局面板标题文本。默认值 null。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            split:true"
            style="height:100px;">
        </div>
[/code]



**region string 定义布局面板位置，可用的值有：north(上),south(下), east(右), west(左),
center(中间)。默认值空。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            split:true"
            style="height:100px;">
        </div>
[/code]



**border boolean 为 true 时显示布局面板边框。默认值 true。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            border:false,
            "style="height:100px;">
        </div>
[/code]



**split boolean 为 true 时用户可以通过分割栏改变面板大小。默认值 false。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            split:true,
            "style="height:100px;">
        </div>
[/code]



**iconCls string 一个包含图标的 CSS 类 ID，该图标将会显示到面板标题上。默认值 null。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            iconCls:'icon-remove',
            "style="height:100px;">
        </div>
[/code]



**href string 用于读取远程站点数据的 URL 链接。默认值null。 加载数据**

[code]

        <div data-options="
            region:'north',
            title:'头部标题',
            href:'is_user.php',
            "style="height:100px;">
        </div>
[/code]



**collapsible boolean 定义是否显示折叠按钮。默认值 true。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            collapsible:false,
            "style="height:100px;">
        </div>
[/code]



**minWidth number 最小面板宽度。默认值10。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            minWidth:200,
            "style="height:100px;">
        </div>
[/code]



**minHeight number 最小面板高度。默认值10。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            minHeight:200,
            "style="height:100px;">
        </div>
[/code]



**maxWidth number 最大面板宽度。默认值10000。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            maxWidth:200,
            "style="height:100px;">
        </div>
[/code]



**maxHeight number 最大面板高度。默认值10000。**

[code]

         <div data-options="
            region:'north',
            title:'头部标题',
            maxHeight:200,
            "style="height:100px;">
        </div>
[/code]

**最终格式**

[code]

     <body id="box" >
        <div data-options="
            region:'north',
            title:'头部标题',
            maxHeight:200,
            split:true,
            "style="height:100px;">
        </div>
        <div data-options="region:'south',title:'底部标题',split:true" style="height:100px;"></div>
        <div data-options="region:'east',title:'右边标题',split:true" style="width:100px;"></div>
        <div data-options="region:'west',title:'左边标题',split:true" style="width:100px;"></div>
        <div data-options="region:'center',title:'中间标题'" style="padding:5px;background:#eee;"></div>
    </body>
[/code]





**四．方法列表，以下在js里使用**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170331193308555-1220185221.png)**

**resize   none 设置布局大小。就是如果布局出现变形，可以用这个方法重置大小和布局**

[code]

    $(function () {
        $('#box').layout({
            fit:true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        $('#box').layout('resize'); //就是如果布局出现变形，可以用这个方法重置大小和布局
    });
[/code]



**panel   region 返 回 指 定 面 板 ， 'region' 参 数 可 用 值 有 ：'north(上),south(下),
east(右), west(左),'center(中间)'。**

[code]

    $(function () {
        $('#box').layout({
            fit:true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        alert($('#box').layout('panel','east')); //返 回 指 定 面 板
    });
[/code]



**collapse   region 折 叠 指 定 面 板 。 'region' 参 数 可 用 值 有 ：north(上),south(下),
east(右), west(左)**

[code]

    $(function () {
        $('#box').layout({
            fit:true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        $('#box').layout('collapse','east'); //折 叠 指 定 面 板
    });
[/code]



**expand   region 展 开 指 定 面 板 。 'region' 参 数 可 用 值 有 ：north(上),south(下),
east(右), west(左)**

[code]

    $(function () {
        $('#box').layout({
            fit:true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        $('#box').layout('collapse','east'); //折 叠 指 定 面 板
        $('#box').layout('expand','east'); //展 开 指 定 面 板
    });
[/code]



**add   options 添加指定面板。属性参数是一个配置对象，更多细节请查看选项卡面板属性。**

[code]

    $(function () {
        $('#box').layout({
            fit: true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        $('#box').layout('remove', 'east');  //移 除 指 定 面 板
        $('#box').layout('add', {
            title: '111',     //标题
            region: 'east',   //添加右边
            maxWidth:200      //最宽200
        });
    });
[/code]



**remove   region 移 除 指 定 面 板 。 'region' 参 数 可 用 值 有 ：north(上),south(下),
east(右), west(左)**

[code]

    $(function () {
        $('#box').layout({
            fit: true    //如果设置为 true，布局组件将自适应父容易。当使用 body 标签创建布局的时候，整个页面会自动最大。默认为 false。
        });
        $('#box').layout('remove','east');  //移 除 指 定 面 板
    });
[/code]



**$.fn.layout.defaults 重写默认值对象。 参照前面的章节**



