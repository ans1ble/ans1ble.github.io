---
layout: post
title: " 第一百九十五节，jQuery EasyUI，Resizable(调整大小)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Resizable(调整大小)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328192941717-1149338696.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Resizeable(调整大小)组件的使用方法，调整大小就是可
以对元素可以拖着调整大小，这个组件不依赖于其他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <div id="rr" class="easyui-resizable"
    　　data-options="maxWidth:800,maxHeight:600"
    　　style="width:100px;height:100px;border:1px solid #ccc;">
    </div>
[/code]

[code]

    //JS 加载调用
    $('#box').resizable({
    　　maxWidth:800,
    　　maxHeight:600,
    });
[/code]

**resizable()将制定元素执行调整大小方法**





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328182844514-1864257551.png)**

**disabled  boolean 默认为 false，设置为 true 则禁用调整**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            disabled:true        //设置为 true 则禁用调整
        });
    });
[/code]



**handles  string默认为 n,e,s,w,ne,se,sw,nw,all，声明调整的方位，** **n 表示北（** ** **上**
）、e 表示东（右）、s 表示南（下）、w 表示西（左）、还有 ne（上右角）、se（下右角）、sw（下左角）、nw（上左角） 和 all（所有）**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            handles:'n'        //n 表示北（上）,只有上方可以调整大小
        });
    });
[/code]



**minWidth  number 默认 10，调整大小时最小宽度**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            minWidth:200,         //调整大小时最小宽度
            minHeight:200         //调整大小时最小高度
        });
    });
[/code]



**minHeight  number 默认 10，调整大小时最小高度**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            minWidth:200,         //调整大小时最小宽度
            minHeight:200         //调整大小时最小高度
        });
    });
[/code]



**maxWidth  number 默认 10000，调整大小时最大宽度**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            maxWidth:200,         //调整大小时最大宽度
            maxHeight:200         //调整大小时最大高度
        });
    });
[/code]



**maxHeight  number 默认 10000，调整大小时最大高度**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            maxWidth:200,         //调整大小时最大宽度
            maxHeight:200         //调整大小时最大高度
        });
    });
[/code]



**edge  number 默认 5，边框边缘触发大小，也就是元素边缘多大像素范围显示拖拉指针**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            maxWidth:200,         //调整大小时最大宽度
            maxHeight:200,         //调整大小时最大高度
            edge:20             //也就是元素边缘多大像素范围显示拖拉指针
        });
    });
[/code]





**三．事件列表**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328190230264-1449341762.png)

**onStartResize e 在开始改变大小的时候触发**



[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onStartResize:function (e) {
                alert('在开始改变大小的时候触发');
            }
        });
    });
[/code]







**onResize e在调整大小期间触发。 当返回 false 的时候，拖动时不会实际改变 DOM 元素大小。鼠标左键弹起时改变大小**



[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onResize:function (e) {
                alert('在调整大小期间触发。当返回 false 的时候，拖动时不会实际改变 DOM 元素大小。鼠标左键弹起时改变大小');
                return false;
            }
        });
    });
[/code]







**onStopResize e 在停止改变大小的时候触发， **鼠标左键弹起时触发****



[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onStopResize:function (e) {
                alert('在停止改变大小的时候触发,鼠标左键弹起时触发');
            }
        });
    });
[/code]







**四．方法列表**



****![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328192120389-1885694168.png)****

**options  none 返回属性对象**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onStopResize:function (e) {
                alert('在停止改变大小的时候触发,鼠标左键弹起时触发');
            }
        });
        alert($('#box').resizable('options'));   //返回属性对象,可以遍历出里面的属性
    });
[/code]



**enable  none 启用调整功能**

[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onStopResize:function (e) {
                alert('在停止改变大小的时候触发,鼠标左键弹起时触发');
            }
        });
        $('#box').resizable('disable');   //禁用调整功能
        $('#box').resizable('enable');   //启用调整功能
    });
[/code]



**disable  none 禁用调整功能**



[code]

    /**
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').resizable({    //将box元素执行调整大小方法
            onStopResize:function (e) {
                alert('在停止改变大小的时候触发,鼠标左键弹起时触发');
            }
        });
        $('#box').resizable('disable');   //禁用调整功能
        $('#box').resizable('enable');   //启用调整功能
    });
[/code]





**$.fn.resizable.defaults 重写默认值对象。**





[code]

    $.fn.resizable.defaults.disabled = true;
[/code]



