---
layout: post
title: " 第一百七十九节，jQuery-UI，知问前端--按钮 UI-图标 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery-UI，知问前端--按钮 UI**



**学习要点：**

**1.使用 button 按钮**

**2.修改 button 样式**

**3.button()方法的属性**

**4.button('action', param)**

**5.单选、复选按钮**

**按钮（button），可以给生硬的原生按钮或者文本提供更多丰富多彩的外观。它不单单 可以设置按钮或文本，还可以设置单选按钮和多选按钮。**



**一．使用 button 按钮**

**使用 button 按钮 UI 的时候，不一定必须是 input 按钮形式，普通的文本也可以设置成 button 按钮。**

[code]

    $('#search_button').button();
[/code]



**二．修改 button 样式**

**在弹出的 button 对话框中，在火狐浏览器中打开 Firebug 或者右击- >查看元素。这样， 我们可以看看 button
的样式，根据样式进行修改。我们为了和网站主题符合，对 dialog 的 标题背景进行修改。**

[code]

    //无须修改 ui 里的 CSS，直接用 style.css 替代掉
    .ui-state-default, .ui-widget-content .ui-state-default, .ui-widget-header .ui-state-default {
    background:url(../img/ui_header_bg.png);
    }
    .ui-state-active, .ui-widget-content .ui-state-active, .ui-widget-header .ui-state-active {
    background:url(../img/ui_white.png);
    }
[/code]

**注意：其他修改方案类似。**



**三．button()方法的属性**

**按钮方法有两种形式：1.button(options)，options 是以对象键值对的形式传参，每个键
值对表示一个选项；2.button('action', param)，action 是操作对话框方法的字符串，param 则 是 options
的某个选项。**

**button()方法,将一个按钮元素，执行按钮效果，参数接收一个对象，以键值对方式设置各种参数**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313143942807-1446788265.png)

  **jQuery-UI，图标**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313160240291-755075625.jpg)

**disabled false/布尔值 默认为 false，设置为 true 时，按钮是非激活的。**



**label 无/字符串 对应按钮上的文字。如果没有，HTML 内容将被作为按钮的文字。**



**icons 无/字符串对应按钮上的图标。在按钮文字前面和后面都可以放置一个图标，通过对象键值对的方式完成：**  
 **{**  
 **primary : 'ui-icon-search',**  
 **secondary : 'ui-icon-search'**  
 **}**



**text true/布尔值 当时设置为 false 时，不会显示文字，但必须指定一个图标。**



[code]

        $('#search_button').button({
            //disabled:true,        //disabled false/布尔值 默认为 false，设置为 true 时，按钮是非激活的。
            label:'搜索',            //label 无/字符串 对应按钮上的文字。如果没有，HTML 内容将被作为按钮的文字。
            icons:{                 //icons 无/字符串对应按钮上的图标。在按钮文字前面和后面都可以放置一个图标，通过对象键值对的方式完成
                primary : 'ui-icon-search',    //按钮文字前图标
                secondary : 'ui-icon-search'   //按钮文字后图标
            },
            text:false                         //隐藏按钮文字
        });
[/code]





**button 的事件方法create**

**注意：对于 button 的事件方法，只有一个：create，当创建 button 时调用。**

[code]

        $('#search_button' ).button({
            create:function () {   //当创建 button 时调用
                alert('创建');
            }
        });
[/code]



**四．button('action', param)**

**button('action', param)方法能设置和获取按钮。action 表示指定操作的方式。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313151206463-278501044.png)**





**button('disable') jQuery 对象 禁用按钮**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        $('#search_button').button('disable');     //button('disable') jQuery 对象 禁用按钮
[/code]



  
**button('enable') jQuery 对象 启用按钮**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        $('#search_button').button('disable');     //button('disable') jQuery 对象 禁用按钮
        $('#search_button').button('enable');     //button('enable') jQuery 对象 启用按钮
[/code]



  
**button('destroy') jQuery 对象 删除按钮，直接阻断了 button。**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        $('#search_button').button('destroy');   //button('destroy') jQuery 对象 删除按钮，直接阻断了 button。
[/code]



  
**button('refresh') jQuery 对象 更新按钮布局。**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        $('#search_button').button('refresh');   //button('refresh') jQuery 对象 更新按钮布局。
[/code]



  
**button('widget') jQuery 对象 获取按钮的 jQuery 对象**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        alert($('#search_button').button('widget'));   //button('widget') jQuery 对象 获取按钮的 jQuery 对象
[/code]



  
**button('option', param) 一般值 获取 options 属性的值，第二个参数是要获取的属性，**

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        alert($('#search_button').button('option', 'label'));   //button('option', param) 一般值 获取 options 属性的值
[/code]



  
**button('option', param, value) jQuery 对象 设置 options 属性的值，
**第二个参数是要设置的属性，第三个参数是要设置的值****

[code]

        $('#search_button' ).button({
            label:'搜索'
        });
        $('#search_button').button('option', 'label','搜索一下');   //button('option', param, value) jQuery 对象 设置 options 属性的值，第二个参数是要设置的属性，第三个参数是要设置的值
[/code]



**五．单选框、复选框**

**button 按钮不但可以设置普通的按钮，对于单选框、复选框同样有效。**

****单选框****

**html**

[code]

     <div id="reg">
        <input type="radio" name="sex" value="male" id="male"><label for="male">男</label></input>
        <input type="radio" name="sex" value="female" id="female"><label for="female">女</label></input>
    </div>
[/code]

[code]

    //jQuery 单选框
    $('#reg input[type=radio]').button();
    //jQuery 单选框改
    $('#reg').buttonset();
[/code]

**复选框**

**html**

[code]

     <div id="reg">
        <input type="checkbox" name="color" value="red" id="red"><label for="red">红</label></input>
        <input type="checkbox" name="color" value="green" id="green"><label for="green">绿</label></input>
        <input type="checkbox" name="color" value="yellow" id="yellow"><label for="yellow">黄</label></input>
        <input type="checkbox" name="color" value="orange" id="orange"><label for="orange">橙</label></input>
    </div>
[/code]

[code]

            //复选框
            $('#reg input[type=checkbox]').button();
            //复选框改
            $('#reg').buttonset();
[/code]

**  buttonset()将一个元素下的所有按钮，单选框，复选框，执行按钮化ui**

