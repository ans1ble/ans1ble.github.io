---
layout: post
title: " 第一百七十八节，jQuery-UI，知问前端--对话框 UI "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery-UI，知问前端--对话框 UI**



**学习要点：**

**1.开启多个 dialog**

**2.修改 dialog 样式**

**3.dialog()方法的属性**

**4.dialog()方法的事件**

**5.dialog 中使用 on()**

****dialog()方法，将指定区块实现对话框功能****



****一．开启多个****

****dialog 我们可以同时打开多个 dialog，只要设置不同的 id 即可实现。****

[code]

    $('#reg' ).dialog();
    $('#login').dialog();
[/code]



**二．修改 dialog 样式**

**在弹出的 dialog 对话框中，在火狐浏览器中打开 Firebug 或者右击- >查看元素。这样， 我们可以看看 dialog
的样式，根据样式进行修改。我们为了和网站主题符合，对 dialog 的标 题背景进行修改。**

[code]

    //无须修改 ui 里的 CSS，直接用 style.css 替代掉
    .ui-widget-header {
    　　background:url(../img/ui_header_bg.png);
    }
[/code]

**注意：其他修改方案类似。**



**三．dialog()方法的属性**

**对话框方法有两种形式：1.dialog(options)，options 是以对象键值对的形式传参，每个
键值对表示一个选项；2.dialog('action', param)，action 是操作对话框方法的字符串，param 则是 options
的某个选项。**

****dialog()方法，接收一个对象，对象以键值对方式，设置对话框的各种参数****

****![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312141519748-644758843.png)****

**dialog 外观选项**

**title 字符串 对话框的标题，可以直接设置在 DOM 元素上**

  
**buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数**

**html**



[code]

    <div id="header">
        <div class="header_main">
            <h1>知问</h1>
            <div class="header_search">
                <input type="text" name="search" class="search"/>
            </div>
            <div class="header_button">
                <input type="button" value="查询" id="search_button"/>
            </div>
            <div class="header_member">
                <a href="###" id="reg_a">注册</a> |
                <a href="javascript:void(0)" id="login_a">登录</a>
            </div>
        </div>
    </div>
    
    <div id="reg">
        表单区
    </div>
[/code]

[code]

    $('#reg_a').click(function () {
            $('#reg').dialog({
                'title': '会员注册',        //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons':{
                    '提交':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    },
                    '重置':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    }
                }
            });
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312150745717-2126303728.png)

**dialog 页面位置选项**

  
****position 字符串，** 设置一个对话框窗口的坐标位置，**

**默认为 center。其他设置值为：left top、top right、bottom left、right
bottom（四个角）、top、bottom（顶部或底部，宽度居中）、left 或 right（左边或右边，高度居中）、center（默认值）**

[code]

    $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册',        //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons':{
                    '提交':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    },
                    '重置':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    }
                },
                'position':'center'         //position 字符串，设置一个对话框窗口的坐标位置，
            });
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312151601623-1108866337.png)

**dialog 大小选项**



**width 默认300/数值 对话框的宽度。默认为 300，单位是像素。**

  
**height **默认** auto/数值 对话框的高度。默认为 auto，单位是像素。**

  
**minWidth **默认** 150/数值 对话框的最小宽度。默认 150，单位是像素。**

  
**minHeight **默认** 150/数值 对话框的最小高度。默认 150，单位是像素。**

  
**maxWidth **默认** auto/数值 对话框的最大宽度。默认 auto，单位是像素。**

  
**maxHeight **默认** auto/数值 对话框的最大高度。默认 auto，单位是像素。**

[code]

    $('#reg_a').click(function () {
            $('#reg').dialog({
                'title': '会员注册',        //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons':{
                    '提交':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    },
                    '重置':function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
                        
                    }
                },
                'position':'center',        //position 字符串，设置一个对话框窗口的坐标位置，
                'width': 400,               //width 默认300/数值 对话框的宽度。默认为 300，单位是像素。
                'height':300                //height 默认auto/数值 对话框的高度。默认为 auto，单位是像素。
            });
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312153205842-1853774049.png)

**dialog 视觉选项**

  
**show 默认false/布尔值 显示对话框时，默认采用淡入效果。**

  
**hide 默认false 布尔值 关闭对话框时，默认采用淡出效果。**

[code]

    $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册',         //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons': {
                    '提交': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    },
                    '重置': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    }
                },
                'position': 'center',        //position 字符串，设置一个对话框窗口的坐标位置，
                'width': 400,                //width 默认300/数值 对话框的宽度。默认为 300，单位是像素。
                'height': 300,               //height 默认auto/数值 对话框的高度。默认为 auto，单位是像素。
                'show':true,                 //show 默认false/布尔值 显示对话框时，默认采用淡入效果。
                'hide':true                  //hide 默认false 布尔值 关闭对话框时，默认采用淡出效果。
    
            });
        });
[/code]



**注意：设置 true 后，默认为淡入淡出，如果想使用别的特效，可以使用以下表格中的字 符串参数。**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312154018623-1010813566.png)

**show 和 hide 可选特效**

  
**blind 对话框从顶部显示或消失**

  
**bounce 对话框断断续续地显示或消失，垂直运动**

  
**clip 对话框从中心垂直地显示或消失**

  
**slide 对话框从左边显示或消失**

  
**drop 对话框从左边显示或消失，有透明度变化**

  
**fold 对话框从左上角显示或消失**

  
**highlight 对话框显示或消失，伴随着透明度和背景色的变化**

  
**puff 对话框从中心开始缩放。显示时“收缩”，消失时“生长”**

  
**scale 对话框从中心开始缩放。显示时“生长”，消失时“收缩”**

  
**pulsate 对话框以闪烁形式显示或消失**

[code]

    $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册',         //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons': {
                    '提交': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    },
                    '重置': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    }
                },
                'position': 'center',        //position 字符串，设置一个对话框窗口的坐标位置，
                'width': 400,                //width 默认300/数值 对话框的宽度。默认为 300，单位是像素。
                'height': 300,               //height 默认auto/数值 对话框的高度。默认为 auto，单位是像素。
                'show':'puff',               //puff 对话框从中心开始缩放。显示时“收缩”，消失时“生长”
                'hide':'puff'                //puff 对话框从中心开始缩放。显示时“收缩”，消失时“生长”
    
            });
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312154937139-850314170.png)



**dialog 行为选项**



**autoOpen 默认true/布尔值 默认为 true，调用 dialog()方法时就会打开对话框；如果为
false，对话框不可见，但对话框已创建，可以通过 dialog('open')才能可见。**



**draggable 默认true/布尔值 默认为 true，可以移动对话框，false 无法移动。**



**resizable 默认True/布尔值 默认为 true，可以调整对话框大小，false 无法调整**



**modal 默认false/布尔值 默认为 false，对话框外可操作，true 对话框会遮罩一层灰纱，无法操作。**



**closeText 默认英文/字符串 设置关闭按钮的 title 文字**

[code]

    $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册',         //title 字符串 对话框的标题，可以直接设置在 DOM 元素上
                'buttons': {
                    '提交': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    },
                    '重置': function () {    //buttons 对象 以对象键值对方式，给 dialog 添加按钮。键是按钮的名称，值是用户点击后调用的回调函数
    
                    }
                },
                'position': 'center',        //position 字符串，设置一个对话框窗口的坐标位置，
                'width': 400,                //width 默认300/数值 对话框的宽度。默认为 300，单位是像素。
                'height': 300,               //height 默认auto/数值 对话框的高度。默认为 auto，单位是像素。
                'show':'puff',               //puff 对话框从中心开始缩放。显示时“收缩”，消失时“生长”
                'hide':'puff',               //puff 对话框从中心开始缩放。显示时“收缩”，消失时“生长”
                'draggable': false,          //draggable 默认true/布尔值 默认为 true，可以移动对话框，false 无法移动。
                'resizable': false,          //resizable 默认True/布尔值 默认为 true，可以调整对话框大小，false 无法调整
                'modal':true,                //modal 默认false/布尔值 默认为 false，对话框外可操作，true 对话框会遮罩一层灰纱，无法操作。
                'closeText':'关闭窗口'       //closeText 默认英文/字符串 设置关闭按钮的 title 文字
    
            });
    
        });
[/code]



**四．dialog()方法的事件**

**除了属性设置外，dialog()方法也提供了大量的事件。这些事件可以给各种不同状态时 提供回调函数。这些回调函数中的 this 值等于对话框内容的
div 对象，不是整个对话框的 div。**



**focus()当对话框被激活时（首次显示以及每次在上面点击）会调用 focus 方法，该方法有两个参数(event, ui)。此事件中的 ui
参数为空。**



[code]

        $('#reg_a').click(function () {
            $('#reg').dialog({
                focus:function (e,ui) {    //得到焦点，执行回调函数
                    alert('获取焦点');
                }
            });
        });
[/code]





**create()当对话框被创建时会调用 create 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                create:function (e,ui) {    //创建焦点，执行回调函数
                    alert('创建焦点');
                }
            });
        });
[/code]



**open()当对话框被显示时（首次显示或调用 dialog('open')方法）会调用 open 方法，该方法有两个参数(event,
ui)。此事件中的 ui 参数为空。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                open:function (e,ui) {    //显示，执行回调函数
                    alert('显示');
                }
            });
        });
[/code]



**beforeClose()当 对 话 框 将 要 关 闭 时 （ 当 单 击 关 闭 按 钮 或 调 用dialog('close')方法），会调用
beforeclose 方法。如果该函数返回 false，对话框将不会被关闭,关闭的对话框可以用
dialog('open')重新打开。该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                beforeClose:function (e,ui) {    //将要关闭，执行回调函数
                    alert('将要关闭');
                }
            });
        });
[/code]

[code]

        $('#reg_a').click(function () {
            $('#reg').dialog({
                beforeClose:function (e,ui) {    //将要关闭，执行回调函数
                    alert('将要关闭');
                    return false;               //返回false，对话框不关闭，只执行回调函数
                }
            });
        });
[/code]



**close()当 对 话 框 将 要 关 闭 时 （ 当 单 击 关 闭 按 钮 或 调 用dialog('close')方法），会调用 close
方法。关闭的对话框可以用 dialog('open')重新打开。该方法有两个参数(event,ui)。此事件中的 ui 参数为空。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                close:function (e,ui) {    //关闭，执行回调函数
                    alert('关闭');
                }
            });
        });
[/code]



**drag()当对话框移动时，每次移动一点均会调用 drag 方法。该方法有两个参数。该方法有两个参数(event, ui)。此事件中的 ui
有两个属性对象：**  
 **1.position，得到当前移动的坐标，有两个子属性：top 和left。得到对话框与头部和左边的位置**  
 **2.offset，得到当前移动的坐标，有两个子属性：top 和 left。得到对话框与页面开始头部和左边的位置**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                drag:function (e,ui) {                   //每次移动，执行回调函数
                    alert('头部：' + ui.position.top);    //得到对话框与头部的位置
                    alert('左边：' + ui.position.left);   //得到对话框与左边的位置
                }
            });
        });
[/code]

[code]

        $('#reg_a').click(function () {
            $('#reg').dialog({
                drag:function (e,ui) {                   //每次移动，执行回调函数
                    alert('头部：' + ui.offset.top);    //得到对话框与页面开始头部的位置
                    alert('左边：' + ui.offset.left);   //得到对话框与页面开始左边的位置
                }
            });
        });
[/code]



**dragStart()当开始移动对话框时，会调用 dragStart 方法。该方法有两个参数(event, ui)。此事件中的 ui
有两个属性对象：**  
 **1.position，得到当前移动的坐标，有两个子属性：top 和left。 **得到对话框与头部和左边的位置****  
 **2.offset，得到当前移动的坐标，有两个子属性：top 和 left。 **得到对话框与页面开始头部和左边的位置****

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                dragStart:function (e,ui) {             //开始移动对话框时，执行回调函数
                    alert('头部：' + ui.offset.top);    //得到对话框与页面开始头部的位置
                    alert('左边：' + ui.offset.left);   //得到对话框与页面开始左边的位置
    
                    alert('头部：' + ui.position.top);    //得到对话框与头部的位置
                    alert('左边：' + ui.position.left);   //得到对话框与左边的位置
                }
            });
        });
[/code]



**dragStop()当开始移动对话框时，会调用 dragStop 方法。该方法有两个参数(event, ui)。此事件中的 ui 有两个属性对象：**  
 **1.position，得到当前移动的坐标，有两个子属性：top 和 **left。 **得到对话框与头部和左边的位置******  
 **2.offset，得到当前移动的坐标，有两个子属性：top 和 left。 **得到对话框与页面开始头部和左边的位置****

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                dragStop:function (e,ui) {             //开始移动对话框时，执行回调函数
                    alert('头部：' + ui.offset.top);    //得到对话框与页面开始头部的位置
                    alert('左边：' + ui.offset.left);   //得到对话框与页面开始左边的位置
    
                    alert('头部：' + ui.position.top);    //得到对话框与头部的位置
                    alert('左边：' + ui.position.left);   //得到对话框与左边的位置
                }
            });
        });
[/code]



**resize()当对话框拉升大小的时候，每一次拖拉都会调用 resize方法。该方法有两个参数(event, ui)。此事件中的 ui
有四个属性对象：**  
 **1.size，得到对话框的大小，有两个子属性：width 和height。**  
 **2.position，得到对话框的坐标，有两个子属性：top 和 left。**  
 **3.originalSize，得到对话框原始的大小，有两个子属性：width 和 height。**  
 **4.originalPosition，得到对话框原始的坐标，有两个子属性：top 和 left。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                resize:function (e,ui) {               //当对话框拉升大小的时候，执行回调函数
                    alert('大小：' + ui.size.width + '|' + ui.size.height);    //得到对话框的大小
    
                    alert('头部和左边：' + ui.position.width + '|' + ui.position.height);    //得到对话框与头部和左边的位置
    
                    alert('原始大小：' + ui.originalSize.width + '|' + ui.originalSize.height);    //得到对话框原始大小
    
                    alert('原始大小：' + ui.originalPosition.width + '|' + ui.originalPosition.height);    //得到对话框原始头部和左边的位置
                }
            });
        });
[/code]



**resizeStart()当开始拖拉对话框时，会调用 resizeStart 方法。该方法有两个参数(event, ui)。此事件中的 ui
有四个属性对象：**  
 **1.size，得到对话框的大小，有两个子属性：width 和height。**  
 **2.position，得到对话框的坐标，有两个子属性：top 和 left。**  
 **3.originalSize，得到对话框原始的大小，有两个子属性：width 和 height。**  
 **4.originalPosition，得到对话框原始的坐标，有两个子属性：top 和 left。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                resizeStart:function (e,ui) {               //当开始拖拉对话框时，执行回调函数
                    alert('大小：' + ui.size.width + '|' + ui.size.height);    //得到对话框的大小
    
                    alert('头部和左边：' + ui.position.width + '|' + ui.position.height);    //得到对话框与头部和左边的位置
    
                    alert('原始大小：' + ui.originalSize.width + '|' + ui.originalSize.height);    //得到对话框原始大小
    
                    alert('原始大小：' + ui.originalPosition.width + '|' + ui.originalPosition.height);    //得到对话框原始头部和左边的位置
                }
            });
        });
[/code]



**resizeStop()当结束拖拉对话框时，会调用 resizeStart 方法。该方法有两个参数(event, ui)。此事件中的 ui
有四个属性对象：**  
 **1.size，得到对话框的大小，有两个子属性：width 和height。**  
 **2.position，得到对话框的坐标，有两个子属性：top 和 left。**  
 **3.originalSize，得到对话框原始的大小，有两个子属性：width 和 height。**  
 **4.originalPosition，得到对话框原始的坐标，有两个子属性：top 和 left。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                resizeStop:function (e,ui) {               //当结束拖拉对话框时，执行回调函数
                    alert('大小：' + ui.size.width + '|' + ui.size.height);    //得到对话框的大小
    
                    alert('头部和左边：' + ui.position.width + '|' + ui.position.height);    //得到对话框与头部和左边的位置
    
                    alert('原始大小：' + ui.originalSize.width + '|' + ui.originalSize.height);    //得到对话框原始大小
    
                    alert('原始大小：' + ui.originalPosition.width + '|' + ui.originalPosition.height);    //得到对话框原始头部和左边的位置
                }
            });
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312174756154-470399315.png)

**dialog('open') jQuery 对象 打开对话框**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                autoOpen:false   //隐藏对话框
            });
            $('#reg').dialog('open');  //dialog('open') jQuery 对象 打开对话框
        });
[/code]

  
**dialog('close') jQuery 对象 关闭对话框**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
    
            });
            $('#reg').dialog('close');  //dialog('close') jQuery 对象 关闭对话框
        });
[/code]



**dialog('destroy') jQuery 对象 删除对话框，直接阻断了 dialog。**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            $('#reg').dialog('destroy');  //dialog('destroy') jQuery 对象 删除对话框，直接阻断了 dialog。
        });
[/code]



**dialog('isOpen') 布尔值 判断对话框是否打开状态**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            alert($('#reg').dialog('isOpen'));  //dialog('isOpen') 布尔值 判断对话框是否打开状态
        });
[/code]



**dialog('widget') jQuery 对象 获取对话框的 jQuery 对象**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            alert($('#reg').dialog('widget'));  //dialog('widget') jQuery 对象 获取对话框的 jQuery 对象
            //也就是返回的对话框整个对象
        });
[/code]

  
**dialog('option', param) 一般值 获取 options 属性的值，也可以获取其他属性值，第二个参数是要获取的属性**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            alert($('#reg').dialog('option', 'title'));  //dialog('option', param) 一般值 获取 options 属性的值
        });
[/code]



**dialog('option', param, value) jQuery 对象 设置 options 属性的值，
**也可以设置其他属性值，参数2属性，参数3属性值****

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            $('#reg').dialog('option', 'title','表单会员注册');  //dialog('option', param, value) jQuery 对象 设置 options 属性的值，也可以设置其他属性值，参数2属性，参数3属性值
        });
[/code]



**五．dialog 中使用 on()事件**

**在 dialog 的事件中，提供了使用 on()方法处理的事件方法。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170312182911451-1188129927.png)**



**dialogfocus 得到焦点时触发**

  
**dialogopen 显示时触发**

  
**dialogbeforeclose 将要关闭时触发**

  
**dialogclose 关闭时触发**

  
**dialogdrag 每一次移动时触发**

  
**dialogdragstart 开始移动时触发**

  
**dialogdragstop 移动结束后触发**

  
**dialogresize 每次调整大小时触发**

  
**dialogresizestart 开始调整大小时触发**

  
**dialogresizestop 结束调整大小时触发**

[code]

        $('#reg_a').click( function () {
            $('#reg').dialog({
                'title': '会员注册'
            });
            $('#reg').on('dialogclose', function () {  //dialogclose 关闭时触发
                alert('关闭');
            });
        });
[/code]

**其他同理**





** **

** **

