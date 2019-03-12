
---
layout: post
title: " 第一百八十九节，jQueryUI，折叠菜单 UI "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQueryUI，折叠菜单 UI**



**学习要点：**

**1.使用 accordion**

**2.修改 accordion 样式**

**3.accordion()方法的属性**

**4.accordion()方法的事件**

**5.accordion 中使用 on**



**折叠菜单（accordion），和选项卡一样也是一种在同一个页面上切换不同内容的功能
UI。它和选项卡的使用几乎没有什么太大区别，只是显示的效果有所差异罢了。**



**一．使用 accordion**

**使用 accordion 比较简单，但需要按照指定的规范即可。**

**HTML 部分**

[code]

     <div id="accordion">
        <h1>菜单 1</h1>
        <div>内容 1</div>
        <h1>菜单 2</h1>
        <div>内容 2</div>
        <h1>菜单 3</h1>
        <div>内容 3</div>
    </div>
[/code]

**jQuery 部分**

**accordion()方法，让符合要求的区块执行折叠菜单方法**

[code]

    $('#accordion').accordion();
[/code]



**二．修改 accordion 样式**

**在显示的 accordion 折叠菜单中，在火狐浏览器中打开 Firebug 或者右击- >查看元素。这 样，我们可以看看 accordion
的样式，根据样式进行修改。我们为了和网站主题符合，对 accordion 的标题背景进行修改。**

[code]

    //无须修改 ui 里的 CSS，直接用 style.css 替代掉
    .ui-widget-header {
        background:url(../img/ui_header_bg.png);
    }
[/code]



**三．accordion()方法的属性**

**选项卡方法有两种形式：1.accordion(options)，options 是以对象键值对的形式传参，每
个键值对表示一个选项；2.accordion('action', param)，action 是操作选项卡方法的字符串， param 则是 options
的某个选项。**

**accordion 外观选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325224604611-1052294972.png)**

**collapsible false/布尔值 当设置为 true 是，允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容。**

[code]

        $('#accordion' ).accordion({
            collapsible:true        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
        });
[/code]



  
**disabled 无/布尔值 默认为 false，设置为 true 则禁用折叠菜单。禁止后菜单无法折叠**

[code]

        $('#accordion' ).accordion({
            collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            disabled:true            //禁止后菜单无法折叠
        });
[/code]



  
**event click/字符串 触发 accordion 的事件类型，默认为 click。可以设置 mouseover
等其他鼠标事件。设置什么事件触发折叠**

[code]

        $('#accordion' ).accordion({
            collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            // disabled:true,            //禁止后菜单无法折叠
            event:'mouseover'       //设置什么事件触发折叠
        });
[/code]



  
**active 数组和布尔值如果是数组，初始化时默认显示哪个 tab，默认值为 0。如果是布尔值，那么默认是否折叠。条件必须是 collapsible
值为 true。**

[code]

        $('#accordion' ).accordion({
            collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            // disabled:true,            //禁止后菜单无法折叠
            event:'mouseover',       //设置什么事件触发折叠
            active:true
        });
[/code]





**heightStyle content/字符串默认为 auto，即自动根据最高的那个为基准，fill 则是填充一定的可用高度，content
则是根据内容伸展高度。**

[code]

        $('#accordion').accordion({
            // collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            // disabled:true,            //禁止后菜单无法折叠
            // event:'mouseover',       //设置什么事件触发折叠
            // active:true,
            heightStyle:'content'       //折叠高度设置
        });
[/code]



  
**header h1/字符串 设置折叠菜单的标题标签。**

[code]

        $('#accordion' ).accordion({
            // collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            // disabled:true,            //禁止后菜单无法折叠
            // event:'mouseover',       //设置什么事件触发折叠
            // active:true,
            // heightStyle:'content'       //折叠高度设置
            header:'h3'                 //设置折叠菜单的标题标签,如设置成h3,在html里也要对应
        });
[/code]





**icons 默认图标 设置想要的图标。**

[code]

        $('#accordion' ).accordion({
            // collapsible:true,        //允许菜单折叠对应的内容。默认值为 false，不会关闭对应内容
            // disabled:true,            //禁止后菜单无法折叠
            // event:'mouseover',       //设置什么事件触发折叠
            // active:true,
            // heightStyle:'content'       //折叠高度设置
            // header:'h3'                 //设置折叠菜单的标题标签,如设置成h3,在html里也要对应
            icons: {
                "header": "ui-icon-plus",           //折叠时图标
                "activeHeader": "ui-icon-minus"     //设置展开时图标
            }
        });
[/code]





**三．accordion()方法的事件**

**除了属性设置外，accordion()方法也提供了大量的事件。这些事件可以给各种不同状态 时提供回调函数。**



**accordion 事件选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325232126424-2061167249.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325232133783-729353700.png)**

**create 当创建一个折叠菜单时激活此事件。**  
 **该方法有两个参数(event, ui)，ui 参数有两个子属性 header 和 panel，得到当前标题和内容选项的对象。**

[code]

        $('#accordion').accordion({
            create: function (event, ui) {    //当创建一个折叠菜单时激活此事件。
                alert($(ui.header.get()).html()); //的到当前展开的菜单标题对象
                alert($(ui.panel.get()).html());  //的到当前展开的菜单内容对象
            }
        });
[/code]



  
**activate 当切换一个折叠菜单时，启动此事件。**  
 **该方法有两个参数(event, ui)，ui 参数有四个子属性
newHeader、newPanel、oldHeader，oldPanel。分别得到的时候新 header 对象、**  
 **新内容对象、旧 header 对象和旧内容对象。**

[code]

        $('#accordion' ).accordion({
            activate: function (event, ui) {    //当切换一个折叠菜单时，启动此事件
                alert($(ui.oldHeader.get()).html()); //获取上一个展开菜单的标题对象
                alert($(ui.oldPanel.get()).html());  //获取上一个展开菜单的内容对象
                alert($(ui.newHeader.get()).html()); //获取当前要展开的标题对象
                alert($(ui.newPanel.get()).html());  //获取当前要展开的内容对象
            }
        });
[/code]



**beforeActivate 当切换一个折叠菜单之前，启动此事件。**  
 **该方法有两个参数 (event, ui)，ui 参数 有四 个子属 性
newHeader、newPanel、oldHeader，oldPanel。分别得到的时候新 header对象、新内容对象、旧 header
对象和旧内容对象。**

[code]

        $('#accordion').accordion({
            beforeActivate: function (event, ui) {    //当切换一个折叠菜单之前，启动此事件
                alert($(ui.oldHeader.get()).html()); //获取上一个展开菜单的标题对象
                alert($(ui.oldPanel.get()).html());  //获取上一个展开菜单的内容对象
                alert($(ui.newHeader.get()).html()); //获取当前要展开的标题对象
                alert($(ui.newPanel.get()).html());  //获取当前要展开的内容对象
            }
        });
[/code]





**accordion('action', param)方法**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325233730111-1212821695.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325233739580-1100827488.png)**

**accordion('disable') jQuery 对象 禁用折叠菜单**

[code]

        $('#accordion' ).accordion({
    
        });
        $('#accordion').accordion('disable');       //禁用折叠菜单
[/code]



**accordion('enable') jQuery 对象 启用折叠菜单**

[code]

        $('#accordion' ).accordion({
    
        });
        $('#accordion').accordion('enable');       //启用折叠菜单
[/code]



**accordion('widget') jQuery 对象 获取折叠菜单的 jQuery 对象**

[code]

        $('#accordion' ).accordion({
    
        });
        alert($('#accordion').accordion('widget'));       //获取折叠菜单的 jQuery 对象
[/code]



**accordion('destroy') jQuery 对象 删 除 折 叠 菜 单 ， 直 接 阻 断 了accordion。**

[code]

        $('#accordion' ).accordion({
    
        });
        $('#accordion').accordion('destroy');       //直 接 阻 断 了accordion。
[/code]



**accordion('refresh') jQuery 对象 更新折叠菜单，比如高度。**

[code]

        $('#accordion' ).accordion({
    
        });
        $('#accordion').accordion('refresh');       //更新折叠菜单，比如高度
[/code]



**accordion('option', param) 一般值 获取 options 属性的值**

[code]

        $('#accordion' ).accordion({
            event:'mouseover'       //设置什么事件触发折叠
        });
        alert($('#accordion').accordion('option', 'event'));       //获取accordion属性的值
[/code]



**accordion('option', param,value)jQuery 对象 设置 options 属性的值**

[code]

        $('#accordion' ).accordion({
            event:'mouseover'       //设置什么事件触发折叠
        });
        $('#accordion').accordion('option', 'event','mouseover');       //设置accordion属性的值
[/code]





**五．accordion 中使用 on()**

**在 accordion 的事件中，提供了使用 on()方法处理的事件方法。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170325235853190-1323694272.png)**

**accordionactivate 折叠菜单切换时触发**

[code]

        $('#accordion' ).accordion({
            event: 'mouseover'       //设置什么事件触发折叠
        });
        //菜单切换时触发
        $('#accordion').on('accordionactivate', function () {
            alert('菜单切换时触发！');
        });
[/code]



**accordionbeforeactivate折叠菜单切换前触发**

[code]

        $('#accordion' ).accordion({
            event: 'mouseover'       //设置什么事件触发折叠
        });
        //菜单切换前触发
        $('#accordion').on('accordionbeforeactivate ', function () {
            alert('菜单切换前触发！');
        });
[/code]



