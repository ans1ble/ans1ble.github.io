---
layout: post
title: " 第一百八十节，jQuery-UI，知问前端--消息提示 UI "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery-UI，知问前端-- **消息提示 UI****



**学习要点：**

**1.HTML 部分**

**2.CSS 部分**

**3.jQuery 部分**

**通过前面已学的 jQuery UI 部件，我们来创建一个注册表单。**

**html**

[code]

     <div id="reg" title="会员注册">
        <p>
            <label for="user">帐号：</label>
            <input type="text" name="user" class="text" id="user" title="请输入帐号，不小于2 位！"/>
            <span class="star">*</span>
        </p>
        <p>
            <label for="pass">密码：</label>
            <input type="text" name="pass" class="text" id="pass" title="请输入密码，不小于6 位！"/>
            <span class="star">*</span>
        </p>
        <p>
            <label for="email">邮箱：</label>
            <input type="text" name="email" class="text" id="email" title="请输入电子邮件！"/>
            <span class="star">*</span>
        </p>
        <p>
            <label>性别：</label>
            <input type="radio" name="sex" id="male" checked="checked"><label for="male">男</label></input>
            <input type="radio" name="sex" id="female"><label for="female">女</label></input>
        </p>
        <p>
            <label for="date">生日：</label>
            <input type="text" name="date" readonly="readonly" class="text" id="date"/>
        </p>
    </div>
[/code]

**css**

[code]

     /*注册框*/
    #reg {
        padding: 15px;
    }
    
    #reg p {
        margin: 10px 0;
        padding: 0;
    }
    
    #reg p label {
        font-size: 14px;
        color: #666;
    }
    
    #reg p .star {
        color: red;
    }
    
    #reg .text {
        border-radius: 4px;
        border: 1px solid #ccc;
        background: #fff;
        height: 25px;
        width: 200px;
        text-indent: 5px;
        color: #666;
    }
[/code]

**js**

[code]

     //注册框
        $('#reg_a').on('click',function () {   //将注册框，执行对话框方法
            $('#reg').dialog({
                autoOpen : true,
                modal : true,
                resizable : false,
                width : 320,
                height : 340,
                buttons : {
                    '提交' : function () {
                        
                    }
                }
            });
            $('#reg').buttonset();      //将单选框，执行按钮方法
        });
[/code]



**消息提示 UI**

**工具提示（tooltip），是一个非常实用的 UI。它彻底扩展了 HTML 中的 title 属性，让
提示更加丰富，更加可控制，全面提升了用户体验。**

**tooltip()方法，将元素，有title属性的执行提示信息方法，提示信息为title值，鼠标移入提示，鼠标移出消失，接收一个对象**



**一．调用 tooltip()方法**

**在调用 tooltip()方法之前，首先需要针对元素设置相应 title 属性。**

[code]

     <input type="text" name="user" class="text" id="user" title="请输入帐号，不小于 2 位！" />
[/code]

[code]

    $('#user').tooltip();
[/code]



**二．修改 tooltip()样式**

**在弹出的 tooltip 提示框后，在火狐浏览器中打开 Firebug 或者右击- >查看元素。这样， 我们可以看看 tooltip
的样式，根据样式进行修改。**

**可以在自定义css里修改，比如颜色**

[code]

    .ui-tooltip {
        color: #ff1c24;
    }
[/code]

**注意：其他修改方案类似。**



**三．tooltip()方法的属性**

**对话框方法有两种形式：1.tooltip(options)，options 是以对象键值对的形式传参，每个
键值对表示一个选项；2.tooltip('action', param)，action 是操作对话框方法的字符串，param 则是 options
的某个选项。**

**tooltip 外观选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313174900291-503199455.png)**

**disabled false/布尔值 设置为 true，将禁止显示工具提示。**

[code]

            $('#reg input[title]' ).tooltip({
                disabled : true              //将禁止显示工具提示
            });
[/code]



  
**content 无/字符串 设置 title 内容。建议还是在htnl里设置 **title****

[code]

            $('#reg input[title]' ).tooltip({
                // disabled : true              //将禁止显示工具提示
                content : '提示信息'             //content 无/字符串 设置 title 内容。建议还是在htnl里设置title
            });
[/code]



  
**items 无/字符串 设置选择器以限定范围。，也就是选择器，限定指定元素下的 ** **title才启用消息提示******

[code]

            $('[title]').tooltip({           //选择了所有的title
                //限定了只有input，的title才启用提示
                items : 'input'             //items 无/字符串 设置选择器以限定范围。，也就是选择器，限定指定元素下的title才启用消息提示
            });
[/code]



  
**tooltipClass 无/字符串 引入 class 形式的 CSS 样式。以 **class形式引入样式，也就是在
**tooltipClass属性里设置一个css选择器名称，然后用这个名称到css写样式******

[code]

            $('#reg input[title]' ).tooltip({
                tooltipClass : 'anl'  //tooltipClass 无/字符串 引入 class 形式的 CSS 样式。以class形式引入样式，也就是在tooltipClass属性里设置一个css选择器名称，然后用这个名称到css写样式
            });
[/code]

css

[code]

    .anl{
        background-color: #23ff2e;
        color: #ff1c24;
    }
[/code]



**tooltip 页面位置选项**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313183040745-187972013.png)

**position 对象 使用对象的键值对赋值，有两个属性：my 和 at表示坐标。my 是以目标点左下角为基准，at 以my 为基准。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    // my : 'left top',  //设置提示框相当对于元素出现的横坐标，设置提示框相当对于元素出现的竖坐标
                    my : 'left center',
                    at : 'right+5 center'
                }
            });
[/code]



**tooltip 视觉选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313190123651-2113999586.png)**

**show false/布尔值 显示对话框时，默认采用淡入效果。**

  
**hide false 布尔值 关闭对话框时，默认采用淡出效果。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                show : false,   //关闭淡入
                hide : false    //关闭淡出
            });
[/code]

**注意：设置 true 后，默认为淡入淡出，如果想使用别的特效，可以使用以下表格中的字 符串参数。**

**show 和 hide 可选特效**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313190629495-1595358445.png)**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313190642338-1205783167.png)

**blind 工具提示从顶部显示或消失**

  
**bounce 工具提示断断续续地显示或消失，垂直运动**

  
**clip 工具提示从中心垂直地显示或消失**

  
**slide 工具提示从左边显示或消失**

  
**drop 工具提示从左边显示或消失，有透明度变化**

  
**fold 工具提示从左上角显示或消失**

  
**highlight 工具提示显示或消失，伴随着透明度和背景色的变化**

  
**puff 工具提示从中心开始缩放。显示时“收缩”，消失时“生长”**

  
**scale 工具提示从中心开始缩放。显示时“生长”，消失时“收缩”**

  
**pulsate 工具提示以闪烁形式显示或消失**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                show : 'scale',   //scale 工具提示从中心开始缩放。显示时“生长”，消失时“收缩”
                hide : 'scale'
            });
[/code]



**tooltip 行为选项**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313191326666-1754886944.png)

**track false/布尔值 设置为 true，能跟随鼠标移动。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                track : true   //能跟随鼠标移动
            });
[/code]



**四．tooltip()方法的事件**

**除了属性设置外，tooltip()方法也提供了大量的事件。这些事件可以给各种不同状态时 提供回调函数。这些回调函数中的 this 值等于对话框内容的
div 对象，不是整个对话框的 div。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313192257713-266166639.png)**

**create当工具提示被创建时会调用 create 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                create : function () {    //create当工具提示被创建时会调用
                    alert('创建时');
                }
            });
[/code]



**open当工具提示被显示时，会调用 open 方法，该方法有两个参数(event, ui)。此事件中的 ui 有一个参数
tooltip，返回是工具提示的 jQuery 对象。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                open : function () {    //open当工具提示被显示时
                    alert('被显示时');
                }
            });
[/code]



**close当工具提示关闭时，会调用 close 方法。关闭的工具提示可以用
tooltip('open')重新打开。该方法有两个参数(event,ui)。此事件中的 ui 有一个参数 tooltip，返回是工具提示的 jQuery
对象。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                },
                close : function () {    //close当工具提示关闭时
                    alert('关闭时');
                }
            });
[/code]



**tooltip('action', param)方法**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313193021073-1305881789.png)**

**tooltip('open') jQuery 对象 打开工具提示**

[code]

     $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('open');   //tooltip('open') jQuery 对象 打开工具提示
[/code]



  
**tooltip('close') jQuery 对象 关闭工具提示**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('close');   //tooltip('close') jQuery 对象 关闭工具提示
[/code]



  
**tooltip('disable') jQuery 对象 禁用工具提示**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('disable');   //tooltip('disable') jQuery 对象 禁用工具提示
[/code]



  
**tooltip('enable') jQuery 对象 启用工具提示**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('enable');   //tooltip('enable') jQuery 对象 启用工具提示
[/code]



  
**tooltip('destroy') jQuery 对象 删除工具提示，直接阻断了 tooltip。**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('destroy');   //tooltip('destroy') jQuery 对象 删除工具提示，直接阻断了 tooltip。
[/code]



  
**tooltip('widget') jQuery 对象 获取工具提示的 jQuery 对象**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('widget');   //tooltip('widget') jQuery 对象 获取工具提示的 jQuery 对象
[/code]



  
**tooltip('option', param) 一般值 获取 options 属性的值，第二个参数是要获取的属性名称**

[code]

            $('#reg input[title]' ).tooltip({
                position : {
                    my : 'left top'
                }
            });
            alert($('#reg input[title]').tooltip('option', 'position'));   //tooltip('option', param) 一般值 获取 options 属性的值，第二个参数是要获取的属性名称
[/code]



  
**tooltip('option', param, value) jQuery 对象 设置 options 属性的值，
**第二个参数是要设置的属性名称，第三个参数是要设置的属性值****

[code]

            $('#reg input[title]' ).tooltip({
                content : '改变文字',
                position : {
                    my : 'left top'
                }
            });
            $('#reg input[title]').tooltip('option', 'content','提示');   //tooltip('option', param, value) jQuery 对象 设置 options 属性的值，第二个参数是要设置的属性名称，第三个参数是要设置的属性值
[/code]



**五．tooltip()中使用 on()**

**在 tooltip 的事件中，提供了使用 on()方法处理的事件方法。**

**on()方法触发的对话框事件**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313194507916-2147161154.png)**

**tooltipopen  显示时触发**

[code]

            $('#reg').on('tooltipopen',function () {
                alert('显示时触发');
            });
[/code]



  
**tooltipclose 每一次移动时触发**



[code]

            $('#reg').on('tooltipclose',function () {
                alert('每一次移动时触发');
            });
[/code]



