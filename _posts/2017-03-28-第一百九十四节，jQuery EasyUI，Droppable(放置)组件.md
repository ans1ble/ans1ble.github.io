---
layout: post
title: " 第一百九十四节，jQuery EasyUI，Droppable(放置)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Droppable(放置)组件**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328174517576-2003664903.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Droppable(放置)组件的使用方法，所谓放置，就将一个
物体入某一个物体内触发各种效果，这个组件不依赖于其他组件。**



**一．加载方式**

[code]

     //class 加载方式
    <div id="dd"
        class="easyui-droppable"
        data-options="accept:'#box,#pox'"
        style="background:black;width:600px;height:400px;">
    </div>
[/code]

**droppable()将一个元素设置成放置元素，放置元素就是将另外指定的元素放置进来触发事件**

[code]

     //JS 加载调用
    $('#box').droppable({
    　　accept:'#box,#pox',
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328170839686-2110927475.png)**

**accept selector 默认为 null，确定哪些元素被接受，值为要接收放置的元素id**

[code]

     /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({    //将fzh元素设置成放置
            accept:'#box,#pox'   //确定哪些元素被接受，值为要接收放置的元素id
        })
    });
[/code]



**disabled boolean 默认为 false，如果为 true，则禁止放置**



[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept:'#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            disabled:true         //如果为 true，则禁止放置
        })
    });
[/code]







**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328171423076-1594943910.png)**



**注意：以下事件 e接收的事件event对象， **source接收的放置进来的元素对象****

**onDragEnter  e,source 在被拖拽元素到放置区内的时候触发，只触发一次**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDragEnter: function (e, source) {       //在被拖拽元素到放置区内的时候触发，只触发一次
                $(this).css('background', 'blue');
            }
        })
    });
[/code]



  
**onDragOver  e,source 在被拖拽元素经过放置区的时候触发**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDragEnter: function (e, source) {       //在被拖拽元素经过放置区的时候触发，触发多次
                $(this).css('background', 'blue');
            }
        })
    });
[/code]



  
**onDragLeave  e,source 在被拖拽元素离开放置区的时候触发**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDragLeave: function (e, source) {       //在被拖拽元素离开放置区的时候触发，
                $(this).css('background', 'blue');
            }
        })
    });
[/code]



  
**onDrop  e,source 在被拖拽元素放入到放置区的时候触发，也就是放下鼠标左键弹起时触发**



[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDrop: function (e, source) {       //在被拖拽元素放入到放置区的时候触发，也就是放下鼠标左键弹起时触发
                $(this).css('background', 'blue');
            }
        })
    });
[/code]









**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170328172916764-828788589.png)**



**options  none 返回属性对象**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDrop: function (e, source) {       //在被拖拽元素放入到放置区的时候触发，也就是放下鼠标左键弹起时触发
                $(this).css('background', 'blue');
            }
        });
        var p = $('#fzh').droppable('options');   //options  none 返回属性对象
        $.each(p, function (attr, value) {        //遍历属性对象
            alert(attr + ':' + value);
        });
    });
[/code]



  
**enable  none 启用放置功能**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDrop: function (e, source) {       //在被拖拽元素放入到放置区的时候触发，也就是放下鼠标左键弹起时触发
                $(this).css('background', 'blue');
            }
        });
        $('#fzh').droppable('disable');  //disable  none
        $('#fzh').droppable('enable');  //enable  none 启用放置功能
    });
[/code]



  
**disable  none 禁用放置功能**

[code]

    /**
    <div id="fzh">放置</div>
    
    <div id="box">
        <div id="pox">内容部分</div>
    </div>
     **/
    
    $(function () {
        $('#box').draggable({    //将box元素设置拖拽
    
        });
        $('#fzh').droppable({     //将fzh元素设置成放置
            accept: '#box,#pox',   //确定哪些元素被接受，值为要接收放置的元素id
            onDrop: function (e, source) {       //在被拖拽元素放入到放置区的时候触发，也就是放下鼠标左键弹起时触发
                $(this).css('background', 'blue');
            }
        });
        $('#fzh').droppable('disable');  //disable  none 禁用放置功能
    });
[/code]



**$.fn.droppable.defaults 重写默认值对象。**

[code]

    $.fn.droppable.defaults.disabled =  true;
[/code]



