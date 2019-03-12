---
layout: post
title: " 第一百九十三节，jQuery EasyUI，Draggable(拖动)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Draggable(拖动)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328155318951-1572022338.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Draggable(拖动)组件的使用方法，这个组件不依赖于其 他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <div id="box" class="easyui-draggable" style="width:400px;height:200px;background:red;">
    　　内容部分
    </div>
[/code]

[code]

    //JS 加载调用
    $('#box').draggable();
[/code]



**draggable()将一个元素实行拖拽方法，接收一个对象，对象里是属性**



**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170327173330514-1933390576.png)**



**revert false/boolean 设置为 true，则拖动停止时返回起始位置， **拖动停止时返回起始位置****

[code]

    $( function () {
        $('#box').draggable({
            revert:'true'         //拖动停止时返回起始位置
        });
    });
[/code]



**cursor move/string 拖动时的 CSS 指针样式， **拖动时的 CSS 鼠标指针样式****

[code]

    $( function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            cursor:'move'            //拖动时的 CSS 鼠标指针样式
        });
    });
[/code]



**Proxy null/string、function当使用'clone'，则克隆一个替代元素拖动。如果指定一个函数，则自定义替代元素。**
**克隆元素拖动**



[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            // edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
            // axis:'h'                    //设置拖动为垂直'v'，还是水平'h'
            proxy: function (source) {
                var p = $('<div style="border:1px solid #ccc; width:400px; height:200px;"></div>');
                p.html($(source).html()).appendTo('body');
                return p;
            }
        });
    });
[/code]





[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            // edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
            // axis:'h'                    //设置拖动为垂直'v'，还是水平'h'
            Proxy:'clone',      //克隆元素拖动
            deltaX:20,          //拖动时鼠标在元素的x位置
            deltaY:20           //拖动时鼠标在元素的y位置
            //以上3个一搬配合使用
        });
    });
[/code]



**deltaX null/number 被拖动的元素对应于当前光标位置 x  ，拖动时鼠标在元素的x位置**

[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            // edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
            // axis:'h'                    //设置拖动为垂直'v'，还是水平'h'
            Proxy:'clone',      //克隆元素拖动
            deltaX:20,          //拖动时鼠标在元素的x位置
            deltaY:20           //拖动时鼠标在元素的y位置
            //以上3个一搬配合使用
        });
    });
[/code]



**deltaY null/number 被拖动的元素对应于当前光标位置 y， **拖动时鼠标在元素的y位置****

[code]

    $( function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            // edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
            // axis:'h'                    //设置拖动为垂直'v'，还是水平'h'
            Proxy:'clone',      //克隆元素拖动
            deltaX:20,          //拖动时鼠标在元素的x位置
            deltaY:20           //拖动时鼠标在元素的y位置
            //以上3个一搬配合使用
        });
    });
[/code]



**handle null/selector 开始拖动的句柄， 就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id**

[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            handle:'#pox'            //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
        });
    });
[/code]



**disabled false/boolean 设置为 true，则停止拖动， 禁止拖动**

[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            disabled:true            //禁止拖动
        });
    });
[/code]



**edge 0/number 可以在其中拖动的容器的宽度，
设置可拖动区域在区块里的宽度，相当于css的外边距，如设置20，则区块上下左右20px的范围不可以拖动**

[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
        });
    });
[/code]



**axis null/string 设置拖动为垂直'v'，还是水平'h'， **设置拖动为垂直'v'，还是水平'h'****



[code]

    $(function () {
        $('#box').draggable({
            // revert:'true'         //拖动停止时返回起始位置
            // handle:'#pox'         //就是设置拖动元素里指定的元素才可以拖动，值为可拖动元素的id
            // disabled:true            //禁止拖动
            // edge:20                  //设置可拖动区域在区块里的宽度，相当于css的外边距
            axis:'h'                    //设置拖动为垂直'v'，还是水平'h'
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328144830529-607585665.png)**



**onBeforeDrag e 拖动之前触发，返回 false 将取消拖动**

[code]

    $( function () {
        $('#box').draggable({
            onBeforeDrag:function (e) {      // 拖动之前触发，返回 false 将取消拖动
                alert('拖动之前触发');
                return false;
            }
        });
    });
[/code]



**onStartDrag e 拖动开始时触发**

[code]

    $( function () {
        $('#box').draggable({
            onStartDrag: function (e) {
                alert('拖动开始时触发');
            }
        });
    });
[/code]



**onDrag e 拖动过程中触发，不能拖动时返回 false**

[code]

    $( function () {
        $('#box').draggable({
            onDrag: function (e) {
                alert('拖动过程中触发，不能拖动时返回 false');
            }
        });
    });
[/code]



**onStopDrag e 拖动停止时触发**

[code]

    $( function () {
        $('#box').draggable({
            onStopDrag: function (e) {
                alert('拖动停止时触发');
            }
        });
    });
[/code]





**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328150137779-2117609347.png)**

**options  none 返回属性对象**

[code]

    $(function () {
        $('#box').draggable({
            revert:'true'         //拖动停止时返回起始位置
        });
        // $('#box').draggable('disable');     //disable  none 禁止拖动
        // $('#box').draggable('enable');      //enable  none 允许拖动
        alert($('#box').draggable('options'));  //返回属性对象
    });
[/code]



  
**proxy  none 如果代理属性被设置则返回该拖动代理元素**

[code]

    $(function () {
        $('#box').draggable({
            onStartDrag: function (e) {
                alert($('#box').draggable('proxy'));
            }
        });
    });
[/code]



  
**enable  none 允许拖动**

[code]

    $(function () {
        $('#box').draggable({
    
        });
        $('#box').draggable('disable');     //disable  none 禁止拖动
        $('#box').draggable('enable');      //enable  none 允许拖动
    });
[/code]



**disable  none 禁止拖动**

[code]

    $(function () {
        $('#box').draggable({
    
        });
        $('#box').draggable('disable');     //disable  none 禁止拖动
        $('#box').draggable('enable');      //enable  none 允许拖动
    });
[/code]



**$.fn.draggable.defaults 重写默认值对象**

**PS：我们可以使用$.fn.draggable.defaults 重写默认值对象。**

[code]

    $( function () {
        $.fn.draggable.defaults.cursor = 'text';   //重写默认值对象,重写后以后的拖动都是这个默认鼠标指针
        
        $('#box').draggable({
    
        });
    });
[/code]



