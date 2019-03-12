---
layout: post
title: " 第一百九十九节，jQuery EasyUI，Panel(面板)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Panel(面板)组件**



**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解EasyUI中Panel(面板)组件的使用方法，这个组件不依赖于其他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <div class="easyui-panel" data-options="closable:true"title="My Panel" style="width:500px;">
    　　<p>内容区域</p>
    </div>
[/code]

**panel()将元素执行面板方法**

[code]

     //JS 加载调用
    $('#box').panel({
    　　width:500,
    　　height:150,
    　　title : '面板',
    　　closable : true,
    });
[/code]





**二．属性列表**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329185343717-1692619122.png)

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329185358826-1194221001.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329185406967-890273042.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170329185415654-534909454.png)**



**id  string 面板的 ID 值。默认为 null。设置面板的id**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            id:'pox'           //设置面板的id
        });
    });
[/code]



**title  string 面板显示的标题文本。默认为 null。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板'     //面板显示的标题
        });
    });
[/code]



**iconCls  string 设置一个 16x16 图标的 CSS 类 ID 显示在面板左上角。默认为 null。设置面板标题左边图标**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit'  //设置面板标题左边图标
        });
    });
[/code]



**width  number 设置面板宽度。默认值 auto。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150         //设置面板高度
        });
    });
[/code]



**height  number 设置面板高度。默认值 auto。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150         //设置面板高度
        });
    });
[/code]



**left  number 设置面板距离左边的位置（即 X 轴位置）。默认为null。，结合定位使用**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            left:200,           //设置面板距离左边的位置（即 X 轴位置）
            top:200             //设置面板距离顶部的位置（即 Y 轴位置）
        });
        $('#box').panel('panel').css('position','absolute'); //获取面板对象，设置定位
    });
[/code]



**top  number 设置面板距离顶部的位置（即 Y 轴位置）。默认为** _ **null。 **结合定位使用****_

[code]

     /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            left:200,           //设置面板距离左边的位置（即 X 轴位置）
            top:200             //设置面板距离顶部的位置（即 Y 轴位置）
        });
        $('#box').panel('panel').css('position','absolute'); //获取面板对象，设置定位
    });
[/code]



**cls  string 添加一个 CSS 类 ID 到面板。默认为 null。给面板添加一个class来设置css**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            cls:'pppox'         //给面板添加一个class来设置css
        });
    });
[/code]



**headerCls  string 添加一个 CSS 类 ID 到面板头部。默认为 null。给面板头部 **添加一个class来设置css****

[code]

     /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            headerCls:'pppox'         //给面板头部添加一个class来设置css
        });
    });
[/code]



**bodyCls  string 添加一个 CSS 类 ID 到面板正文部分。默认为null。给面板正文 **
**添加一个class来设置css******

[code]

     /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            bodyCls:'pppox'         //给面板正文添加一个class来设置css
        });
    });
[/code]



**style  subject 添加一个当前指定样式到面板。默认为{}。添加一个指定css样式到面板，注意如果给内置的样式有冲突可以没有效果**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            bodyCls:'pppox',         //给面板正文添加一个class来设置css
            style: {                //添加一个指定css样式到面板，注意如果给内置的样式有冲突可以没有效果
                'min-height': '250px'
            }
        });
    });
[/code]



**fit  boolean 当设置为 true 的时候面板大小将自适应父容器。默认为 false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            bodyCls:'pppox',         //给面板正文添加一个class来设置css
            fit:true                //当设置为 true 的时候面板大小将自适应父容器。默认为 false。
        });
    });
[/code]



**border  boolean 定义是否显示面板边框。默认为 true**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            border:false         //定义是否显示面板边框。默认为 true
        });
    });
[/code]



**doSize  boolean 如果设置为 true，在面板被创建的时候将重置大小和重新布局。默认为 true。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            doSize:true           //如果设置为 true，在面板被创建的时候将重置大小和重新布局。默认为 true。
        });
    });
[/code]



**noheader  boolean 如果设置为 true。将不会创建面板标题。默认为false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            noheader:true         //如果设置为 true。将不会创建面板标题。默认为false。
        });
    });
[/code]



**content  string 面板主体内容。默认为 null。，设置面板主体内容**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            content :'这是修改后的主体内容'         //设置面板主体内容
        });
    });
[/code]



**collapsible  boolean 定义是否显示可折叠按钮。默认为 false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true         //定义是否显示可折叠按钮。默认为 false。
        });
    });
[/code]



**minimizable  boolean 定义是否显示最小化按钮。默认为 false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            minimizable :true     //定义是否显示最小化按钮。默认为 false。
        });
    });
[/code]



**maximizable  boolean 定义是否显示最大化按钮。默认为 false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            maximizable :true     //定义是否显示最大化按钮。默认为 false。
        });
    });
[/code]



**closable  boolean 定义是否显示关闭按钮。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            closable :true     //定义是否显示关闭按钮。
        });
    });
[/code]



**tools   array,selector自定义工具菜单，可用值：(1)数 组 ， 每 个 元 素 都 包 含 ’iconCls’
和’handler’属性。(2)指向工具菜单的选择器。默认为[]。**

**自定义根据按钮接收一个数组，数组里接收对象，以键值对的方式设置 **iconCls图标，和
**handler点击后的操作，要设置多个图标数组里就接收多个对象******

[code]

     /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            closable :true,     //定义是否显示关闭按钮。
            tools:[{            //自定义工具菜单
                iconCls:'icon-edit',    //iconCls图标
                handler:function () {
                    alert('点击后的操作');    //handler点击后的操作
                }
            }]
        });
    });
[/code]



**collapsed  boolean 定义是否在初始化的时候折叠面板。默认值为false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            collapsed :true     //定义是否在初始化的时候折叠面板。默认值为false。
        });
    });
[/code]



**minimized  boolean 定义是否在初始化的时候最小化面板。默认值为false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            minimized :true     //定义是否在初始化的时候最小化面板。默认值为false。
        });
    });
[/code]



**maximized  boolean 定义是否在初始化的时候最大化面板。默认值为false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            maximized :true     //定义是否在初始化的时候最大化面板。默认值为false。
        });
    });
[/code]



**closed  boolean 定义是否在初始化的时候关闭面板。默认为false。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            closed :true     //定义是否在初始化的时候关闭面板。默认为false。
        });
    });
[/code]



**href  string 从 URL 读取远程数据并且显示到面板。默认为null。，值为要加载的文件地址采用的 **ajax加载****

[code]

     /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/'     //URL 读取远程数据并且显示到面板。默认为null。
        });
    });
[/code]



**cache  boolean 如果为 true，在超链接载入时缓存面板内容。默认为 true。，也就是缓存远程数据**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            cache:true          //如果为 true，在超链接载入时缓存面板内容。默认为 true。，也就是缓存远程数据
        });
    });
[/code]



**loadingMessage   string 在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。设置远程加载时的内容**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中'     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
        });
    });
[/code]



**extractor   function 定义如何从 ajax
应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板，data接收远程数据**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330160243727-240911721.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330160253945-1780327288.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330160300336-2022996343.png)**



**onBeforeLoad  none 在加载远程数据之前触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeLoad:function () {
                alert('在加载远程数据之前触发。');
            }
        });
    });
[/code]



**onLoad  none 在加载远程数据时触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onLoad:function () {
                alert('在加载远程数据时触发。');
            }
        });
    });
[/code]



**onBeforeOpen  none在打开面板之前触发，返回 false 可以取消打开操作。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeOpen:function () {
                alert('在打开面板之前触发，返回 false 可以取消打开操作。');
                // return false;  //返回false时，打开之后操作将取消
            },
            onOpen:function () {
                alert('在打开面板之后触发。');
            }
        });
    });
[/code]



**onOpen  none 在打开面板之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeOpen:function () {
                alert('在打开面板之前触发，返回 false 可以取消打开操作。');
                // return false;  //返回false时，打开之后操作将取消
            },
            onOpen:function () {
                alert('在打开面板之后触发。');
            }
        });
    });
[/code]



**onBeforeClose  none在关闭面板之前触发，返回 false 可以取消关闭操作。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeClose:function () {
                alert('在关闭面板之前触发，返回 false 可以取消关闭操作。');
                return false;
            },
            onClose:function () {
                alert('在面板关闭之后触发。');
            }
        });
    });
[/code]



**onClose  none 在面板关闭之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeClose:function () {
                alert('在关闭面板之前触发，返回 false 可以取消关闭操作。');
                return false;
            },
            onClose:function () {
                alert('在面板关闭之后触发。');
            }
        });
    });
[/code]



**onBeforeDestroy  none在面板销毁之前触发，返回 false 可以取消销毁操作。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeDestroy:function () {
                alert('在面板销毁之前触发，返回 false 可以取消销毁操作。');
                return false;
            },
            onDestroy:function () {
                alert('在面板销毁之后触发。');
            }
        });
    });
[/code]



**onDestroy  none 在面板销毁之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeDestroy:function () {
                alert('在面板销毁之前触发，返回 false 可以取消销毁操作。');
                return false;
            },
            onDestroy:function () {
                alert('在面板销毁之后触发。');
            }
        });
    });
[/code]



**onBeforeCollapse  none在面板折叠之前触发，返回 false 可以终止折叠操作。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeCollapse:function () {
                alert('在面板折叠之前触发，返回 false 可以终止折叠操作。');
                // return false;
            },
            onCollapse:function () {
                alert('在面板折叠之后触发。');
            }
        });
    });
[/code]



**onCollapse  none 在面板折叠之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeCollapse:function () {
                alert('在面板折叠之前触发，返回 false 可以终止折叠操作。');
                // return false;
            },
            onCollapse:function () {
                alert('在面板折叠之后触发。');
            }
        });
    });
[/code]



**onBeforeExpand  none在面板展开之前触发，返回 false 可以终止展开操作。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeExpand:function () {
                alert('在面板展开之前触发，返回 false 可以终止展开操作。');
                // return false;
            },
            onExpand:function () {
                alert('在面板展开之后触发。');
            }
        });
    });
[/code]



**onExpand  none 在面板展开之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onBeforeExpand:function () {
                alert('在面板展开之前触发，返回 false 可以终止展开操作。');
                // return false;
            },
            onExpand:function () {
                alert('在面板展开之后触发。');
            }
        });
    });
[/code]



**onResize   width,height在面板改变大小之后触发。width：新的宽度。height：新的高度。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onResize:function (width,height) {
                alert('在面板改变大小之后触发。' +width+ '：新的宽度。' +height+ '：新的高度。');
            }
        });
    });
[/code]



**onMove   left,top在面板移动之后触发。left：新的左边距位置。top：新的上边距位置。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onMove:function (left,top) {
                alert('在面板移动之后触发。' +left+ '：新左边位置。' +top+ '：新头部位置。');
            }
        });
    });
[/code]



**onMaximize   none 在窗口最大化之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onMaximize:function () {
                alert('在窗口最大化之后触发。');
            }
        });
    });
[/code]



**onRestore  none 在窗口恢复到原始大小以后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onRestore:function () {
                alert('在窗口恢复到原始大小以后触发。');
            }
        });
    });
[/code]



**onMinimize  none 在窗口最小化之后触发。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            },
            onMinimize:function () {
                alert('在窗口最小化之后触发。');
            }
        });
    });
[/code]





**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330165441133-950422462.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330165450524-72982471.png)**



**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170330165459836-49629037.png)**

**options  none 返回属性对象。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        alert($('#box').panel('options'));   //返回属性对象。
    });
[/code]



**panel  none 返回面板对象。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        alert($('#box').panel('panel'));   //返回面板对象。
    });
[/code]



**header  none 返回面板头对象。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        alert($('#box').panel('header'));   //返回面板头对象。
    });
[/code]



**body  none 返回面板主体对象。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        alert($('#box').panel('body'));   //返回面板主体对象。
    });
[/code]



**setTitle  title 设置面板头的标题文本。**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        alert($('#box').panel('setTitle','设置标题'));   //设置面板头的标题文本。
    });
[/code]



**open  forceOpen 在'forceOpen'参数设置为 true
的时候，打开面板时将跳过'onBeforeOpen'回调函数。跳过在打开面板之后触发**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        $('#box').panel('open', true);   //参数设置为 true 的时候，打开面板时将跳过'onBeforeOpen'回调函数
    });
[/code]



**close  forceClose 在'forceClose'参数设置为 true
的时候，关闭面板时将跳过'onBeforeClose'回调函数。，跳过关闭之前触发**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        $('#box').panel('close', true);   //参数设置为 true 的时候，关闭面板时将跳过'onBeforeClose'回调函数
    });
[/code]



**destroy  forceDestroy在'forceDestroy'参数设置为 true
的时候，销毁面板时将跳过'onBeforeDestory'回调函数。跳过销毁之前触发**

[code]

    /**
    <div id="box">内容部分</div>
     **/
    
    $(function () {
        $('#box').panel({
            title: '面板',     //面板显示的标题
            width:500,          //设置面板宽度
            height:150,         //设置面板高度
            iconCls:'icon-edit',  //设置面板标题左边图标
            collapsible :true,         //定义是否显示可折叠按钮。默认为 false。
            minimizable :true,     //定义是否显示最小化按钮。默认为 false。
            maximizable :true,     //定义是否显示最大化按钮。默认为 false。
            closable :true,     //定义是否显示关闭按钮。
            href :'is_user.php/',     //URL 读取远程数据并且显示到面板。默认为null。
            loadingMessage:'数据加载中',     //在加载远程数据的时候在面板内显示一条信息。默认值为 loading...。
            extractor:function (data) {         //定义如何从 ajax 应答数据中提取内容，返回提取数据。也就是将远程返回数据进行处理后返回给面板
                return data.substring(0,2);  //加收外部数据，截取后返回
            }
        });
        $('#box').panel('destroy', true);   //参数设置为 true 的时候，销毁面板时将跳过'onBeforeDestory'回调函数
    });
[/code]





**refresh  href 刷新面板来装载远程数据。如果'href'属性有了新配置，它将重写旧的'href'属性。**

[code]

    //刷新当前内容
    $('#box').panel('refresh');
[/code]



[code]

    //刷新指定载入内容
    $('#box').panel('refresh', 'content.php');
[/code]





**resize
options设置面板大小和布局。参数对象包含下列属性：width：新的面板宽度。height：新的面板高度。left：新的面板左边距位置。top：新的面板上边距位置。**

[code]

        $('#box').panel('resize', {         //设置面板大小和布局
            width : 100,
            height : 100,
            left : 100,
            top : 100
        });
[/code]



**move  options 移动面板到一个新位置。参数对象包含下列属性：left：新的左边距位置。top：新的上边距位置。**

[code]

        $('#box').panel('move', {         //设置移动的坐标
            left : 100,
            top : 100
        });
[/code]



**maximize  none 最大化面板到容器大小。**

[code]

     $('#box').panel('maximize');    //最大化面板到容器大小。
[/code]



**minimize  none 最小化面板。**

[code]

        $('#box').panel('minimize');    //最小化面板。
[/code]



**restore  none 恢复最大化面板回到原来的大小和位置。**

[code]

        $('#box').panel('restore');    //恢复最大化面板回到原来的大小和位置。
[/code]



**collapse  animate 折叠面板主题。**

[code]

        $('#box').panel('collapse');    //折叠面板主题。
[/code]



**expand  animate 展开面板主体。**

[code]

        $('#box').panel('expand');    //展开面板主体。
[/code]



**$.fn.panel.defaults 重写默认值对象。**

[code]

    $.fn.panel.defaults.border =  false;
[/code]



