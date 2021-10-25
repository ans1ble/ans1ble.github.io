---
layout: post
title: " 第二百一十二节，jQuery EasyUI，Combo(自定义下拉框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Combo(自定义下拉框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404202726378-793173216.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Combo(自定义下拉框)组件的使用方法， 这个组件依赖于 ValidateBox(验证框)组件**



**一．加载方式**

**自定义下拉框不能通过标签的方式进行创建。**

[code]

     <input id="box">
[/code]

**JS 加载调用**

**combo()将元素执行自定义下拉框方法**

[code]

    $( function () {
        $('#box').combo({
            required: true,
            multiple: true,
        });
    });
[/code]



**如果要实现自定义下来选择(图片、文本、按钮均可)，需要配合一些代码。**

**列：**

**html**

[code]

     <!--下拉组件框-->
    <input id="box"> 
    <!--下拉区块-->
    <div id="food">
        <div style="color:#99BBE8;background:#fafafa;padding:5px;">
            请选择一个食物
        </div>
        <div style="padding:10px">
            <input type="radio" name="food" value="01"><span>煎饼果子</span><br/>
            <input type="radio" name="food" value="02"><span>牛腩米线</span><br/>
            <input type="radio" name="food" value="03"><span>水果沙拉</span><br/>
            <input type="radio" name="food" value="04"><span>蛋黄派</span><br/>
            <input type="radio" name="food" value="05"><span>其他</span>
        </div>
    </div>
[/code]

**js**

[code]

    $( function () {
        $('#box').combo({
            required: true,    //不能为空
            multiple: false     //是否支持多选
        });
        $('#food').appendTo($('#box').combo('panel'));  //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();    //获取到选择的value值
            var s = $(this).next('span').text(); //获取span里的内容
            //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');
        })
    });
[/code]





**二．属性列表**

**Combo 属性，扩展自 ValidateBox **(验证框)** 属性,所以验证方面的参照 **ValidateBox
**(验证框)章节即可******

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404180523394-830614484.png)

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404180530441-2042155733.png)**

**width   number 组件的宽度。默认值 auto。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**height   number 组件的高度。默认值22。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**panelWidth   number 下拉面板宽度。默认值 null。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            panelWidth:300,
            panelHeight:100
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**panelHeight   number 下拉面板高度。默认值200。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            panelWidth:300,
            panelHeight:100
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**multiple   boolean 定义是否支持多选。默认值 false。,没什么用**



**selectOnNavigation   boolean 定义是否允许使用键盘导航来选择项目。默认值 true。 **没什么用****



**separator   string 在多选的时候使用何种分隔符进行分割。默认值’,’。 ** **没什么用******



**editable   boolean 定义用户是否可以直接输入文本到字段中。默认值 true。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            editable:false      //定义用户是否可以直接输入文本到字段中。默认值 true。
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**disabled   boolean 设置启用/禁用字段。默认值 false。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            disabled:true     //设置启用/禁用字段。默认值 false。
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**readonly   boolean 设置该字段为读写/只读模式。默认值false。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            readonly:false     //设置该字段为读写/只读模式。默认值false。
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**hasDownArrow   boolean 定义是否显示向下箭头按钮。默认值true。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            hasDownArrow:false     //定义是否显示向下箭头按钮。默认值true。
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**value   string 字段的默认值。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            value:2    //字段的默认值。
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**delay   number最后一次输入事件与执行搜索之间的延迟间隔（执行自动完成功能的延迟间隔）默认值200。可以输入的时候输入后多少时间自动下拉**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            delay:2000    //可以输入的时候输入后多少时间自动下拉
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**keyHandler   object 在用户按下键的时候调用一个函数。后面会讲到**



**PS：这里有些属性无法在单独组件使用中体现它的效果，需要配合整个表单或服务器 支持。在后面的课程中设计到综合使用的时候再去了解。  
**





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404192454191-1705347647.png)**



**onShowPanel   none 当下拉面板显示的时候触发。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            onShowPanel:function () {
                alert('当下拉面板显示的时候触发');
            }
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**onHidePanel   none 当下拉面板隐藏的时候触发。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            onHidePanel:function () {
                alert('当下拉面板隐藏的时候触发');
            }
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]



**onChange   newValue, oldValue 当字段值改变的时候触发。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30,
            onChange:function (newValue, oldValue) {
                alert('当字段值改变的时候触发');
                //newValue接收当前改变的值，oldValue改变前的值
                alert(newValue + '|' + oldValue);
            }
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        })
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404193347347-1511603941.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404193354660-373176713.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404193403191-2117403609.png)**



**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        alert($('#box').combo('options'));  //返回属性对象
    });
[/code]



**panel   none 返回下拉面板对象。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        alert($('#box').combo('panel'));  //返回下拉面板对象
    });
[/code]



**textbox   none 返回文本框对象。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        alert($('#box').combo('textbox'));  //返回文本框对象
    });
[/code]



**destroy   none 销毁该组件。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('destroy');  //销毁该组件
    });
[/code]



**resize   width 调整组件宽度。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('resize','100');  //调整组件宽度
    });
[/code]



**showPanel   none 显示下拉面板。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('showPanel');  //显示下拉面板
    });
[/code]



**hidePanel   none 隐藏下拉面板。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('hidePanel');  //隐藏下拉面板
    });
[/code]



**disable   none 禁用组件。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('disable');  //禁用组件
    });
[/code]



**enable   none 启用组件。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('enable');  //启用组件
    });
[/code]



**readonly   mode 启用/禁用只读模式。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $('#box').combo('readonly',true);  //启用/禁用只读模式。
    });
[/code]



**validate   none 验证输入的值是否有效。返回验证结果对象**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).click(function () {
            alert($('#box').combo('validate'));
        });
    });
[/code]



**isValid   none 返回验证结果。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).click(function () {
            alert($('#box').combo('isValid'));
        });
    });
[/code]



**clear   none 清除控件的值。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).click(function () {
            $('#box').combo('clear');
        });
    });
[/code]



**reset   none 重置控件的值。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).dblclick(function () {
            $('#box').combo('reset');
        });
    });
[/code]



**getText   none 获取输入的文本。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).dblclick(function () {
            alert($('#box').combo('getText'));
        });
    });
[/code]



**setText   text 设置输入的文本。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
    });
[/code]



**getValues   none 获取组件值的数组。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).dblclick(function () {
            alert($('#box').combo('getValues'));
        });
    });
[/code]



**setValues   values 设置组件值的数组。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).dblclick(function () {
            alert($('#box').combo('setValues',[52]));
        });
    });
[/code]





**getValue   none 获取组件的值。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
        $(document).dblclick(function () {
            alert($('#box').combo('getValue'));
        });
    });
[/code]



**setValue   value 设置组件的值。**

[code]

    $(function () {
        $('#box').combo({
            width:400,
            height:30
        });
        $('#food').appendTo($('#box').combo('panel'));                               //将下拉区块添加到下拉框里
        $('#food input').click(function () {
            var v = $(this).val();                                                   //获取到选择的value值
            var s = $(this).next('span').text();                                     //获取span里的内容
            $('#box').combo('setValue', v).combo('setText', s).combo('hidePanel');   //将value值添加到组件value里，将span里的内容添加是组件输入框，最后关闭下拉面板
        });
    });
[/code]





**我们可以使用$.fn.combo.defaults 重写默认值对象。 见前面**

