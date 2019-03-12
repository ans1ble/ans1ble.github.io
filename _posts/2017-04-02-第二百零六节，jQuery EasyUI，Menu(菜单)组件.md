---
layout: post
title: " 第二百零六节，jQuery EasyUI，Menu(菜单)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Menu(菜单)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402205120602-100283526.png)

**学习要点：**

**1.加载方式**

**2.菜单项属性**

**3.菜单属性**

**4.菜单事件**

**5.菜单方法**



**本节课重点了解 EasyUI 中 Menu(菜单)组件的使用方法，这个组件不依赖于任何其他 组件。**





**一．加载方式**

**菜单组件通常用于快捷菜单，在加载方式上，通过 class 或 JS 进行设置为菜单组件。 然后，再通过 JS 事件部分再响应。**

**class 加载方式，**

[code]

     <div id="box" class="easyui-menu" style="width:120px;">
        <div>新建</div>
        <div>
            <span>打开</span>
            <div style="width:150px;">
                <div>Word</div>
                <div>Excel</div>
                <div>PowerPoint</div>
            </div>
        </div>
        <div data-options="iconCls:'icon-save'">保存</div>
        <div class="menu-sep"></div>
        <div>退出</div>
    </div>
[/code]

**注意必须结合js使用，因为默认class 加载方式，是隐藏的，而且默认是浏览器系统菜单**

**js**

[code]

    $( function () {
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            })
        })
    });
[/code]



**menu()方法，将元素执行鼠标左键自定义菜单方法**

**JS 加载方式**

[code]

    $( function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            })
        })
    });
[/code]



**二．菜单项属性， 菜单主体属性**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402190523945-1950242588.png)**

**在 data-options 设置，只有两个有效，这些属性一般用于 **class 加载方式的每一项，或者使用方法增加时设置****

[code]

     <div data-options="
    　　iconCls :'icon-save',
    　　disabled : true,
    ">保存</div>
[/code]

**PS：其他的参数会菜单方法中设置菜单项时有效**





**三．菜单属性**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402190941633-750484486.png)**

**菜单属性，有些设置在 data-options 有效**

**zIndex   number 菜单 z-index 样式，增加它的值。默认值110000。 设置菜单的层级关系**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100   //设置菜单的层级关系
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**left   number 菜单的左边距位置。默认值0。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            left:100,
            top:100
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                // left: e.pageX,  //菜单位置
                // top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**top   number 菜单的上边距位置。默认值0。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            left:100,
            top:100
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                // left: e.pageX,  //菜单位置
                // top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**minWidth   number 菜单的最小宽度。默认值120。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            left:100,
            top:100,
            minWidth:400    //菜单的最小宽度。默认值120。
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                // left: e.pageX,  //菜单位置
                // top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**hideOnUnhover   boolean 当设置为 true 时，在鼠标离开菜单的时候将自动隐藏菜单。默认值 true。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            minWidth:400,    //菜单的最小宽度。默认值120。
            hideOnUnhover:false  //当设置为 true 时，在鼠标离开菜单的时候将自动隐藏菜单。默认值 true。
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
    });
[/code]





**四．菜单事件**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402192231086-1469260261.png)**



**onShow   none 在菜单显示之后触发。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            onShow:function () {
                alert('在菜单显示之后触发。');
            }
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**onHide   none 在菜单隐藏之后触发。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            onHide:function () {
                alert('在菜单隐藏之后触发');
            }
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
    });
[/code]



**onClick   item 在菜单项被点击的时候触发。**

[code]

    $(function () {
        $('#box').menu({
            zIndex:100,   //设置菜单的层级关系
            onClick:function (item) {
                alert('在菜单项被点击的时候触发');
                alert(item); //接收点击的对象
            }
        });
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
    });
[/code]





**五．菜单方法**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402192443649-248795766.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402192451774-968073172.png)**



**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170402192457539-480039242.png)**



**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').menu({
    
        });
        alert($('#box').menu('options'));   //返回属性对象
    });
[/code]



**show   pos显示菜单到指定的位置。'pos'参数有2个属性：**  
 **left：新的左边距位置。**  
 **top：新的上边距位置。**



[code]

    $(function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            })
        });
    });
[/code]



**hide   none 隐藏菜单。**

[code]

    $(function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
            $('#box').menu('hide');      //隐藏菜单。
        });
    
    });
[/code]



**destroy   none 销毁菜单。**

[code]

    $(function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
            $('#box').menu('destroy');      //销毁菜单
        });
    });
[/code]



**getItem   itemEl 获取指定的菜单项。得到的是一个菜单项的 DOM 元素。值为指定菜单项的id**

[code]

    $(function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
            alert($('#box').menu('getItem','#df'));      //得到的是一个菜单项的 DOM 元素。值为指定菜单项的id
        });
    });
[/code]



**setText   param设置指定菜单项的文本。'param'参数包含2个属性：**  
 **target：DOM 对象，要设置值的菜单项。**  
 **text: 字符串，要设置的新文本值。**

[code]

    $( function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
            $('#box').menu('setText', {
                target: '#df',
                text: '修改'
            });
        });
    });
[/code]



**setIcon   param设置指定菜单项图标。'param'参数包含2个属性：**  
 **target：DOM 对象，要设置的菜单项。**  
 **iconCls：新的图标 CSS 类 ID。**

[code]

    $( function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
            $('#box').menu('setIcon', {
                target: '#df',
                iconCls : 'icon-add'
            });
        });
    });
[/code]



**findItem   text 查 找 的 指 定 菜 单 项 ， 返 回 的 对 象 和getItem 方法是一样的。**

[code]

    $(function () {
        $('#box').menu({
    
        });
        $(document).on('contextmenu',function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show',{   //执行自定义鼠标左键菜单
                left:e.pageX,  //菜单位置
                top:e.pageY    //菜单位置
            });
        alert($('#box').menu('findItem','新建'));
        });
    });
[/code]



**appendItem
options追加新的菜单项，'options'参数代表新菜单项属性。默认情况下添加的项在菜单项的顶部。追加一个子菜单项，'parent'属性应该设置指定的父项元素，并且该父项元素必须是已经定义在页面上的。**

[code]

    $(function () {
        $('#box').menu({});
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
        $('#box').menu('appendItem', {
            text: '新增',
            iconCls: 'icon-add',
            onclick: function () {
                alert('新增');
            }
        });
    });
[/code]

追加一个子菜单项

[code]

    $(function () {
        $('#box').menu({});
        $(document).on('contextmenu', function (e) {   //设置鼠标左键方法
            e.preventDefault();  //阻止默认行为，阻止掉浏览器系统菜单
            $('#box').menu('show', {   //执行自定义鼠标左键菜单
                left: e.pageX,  //菜单位置
                top: e.pageY    //菜单位置
            });
        });
        $('#box').menu('appendItem', {
            parent: $('#box').menu('findItem', '打开').target,
            text: '新增',
            iconCls: 'icon-add',
            onclick: function () {
                alert('新增');
            },
        });
    });
[/code]





**removeItem   itemEl 移除指定的菜单项。值为目标id**

[code]

    $('#box').menu('removeItem', '#new');
[/code]



**enableItem   itemEl 启用菜单项。 **值为目标id****

[code]

    $('#box').menu('disableItem', '#new');
[/code]



**disableItem   itemEl 禁用菜单项。 **值为目标id****



[code]

    $('#box').menu('enableItem', '#new');
[/code]



**  $.fn.menu.defaults 重写默认值对象。见前面**

