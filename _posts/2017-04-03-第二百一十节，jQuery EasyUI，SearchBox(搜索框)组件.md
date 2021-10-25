---
layout: post
title: " 第二百一十节，jQuery EasyUI，SearchBox(搜索框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，SearchBox(搜索框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403200919191-1937162080.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 SearchBox(搜索框)组件的使用方法， 这个组件依赖于 MenuButton(按钮)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <!--搜索框-->
    <input id="ss" class="easyui-searchbox" style="width:300px" data-options="menu:'#box'"></input>
    <!--频道按钮-->
    <div id="box" style="width:120px">
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        <div data-options="name:'sports'">建材</div>
    </div>
[/code]



**searchbox()将符合规则的元素执行搜索框方法**



**js加载**

[code]

     /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            searcher: function (value, name) {
                alert(value + ',' + name);
            },
            menu: '#box',
            prompt: '请输入内容',
        });
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403185617785-779577177.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403185628363-491486869.png)

**width   number 组件宽度。默认为 auto。**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',
            prompt: '请输入内容'
        });
    });
[/code]



**height  number 组件高度。默认为22。**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',
            prompt: '请输入内容'
        });
    });
[/code]



**prompt   string 在输入框中显示提示消息。**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',
            prompt: '请输入内容'
        });
    });
[/code]



**value   string 输入的值。默认 **value值****

[code]

     /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',
            // prompt: '请输入内容',
            value:55555
        });
    });
[/code]



  
**menu   selector搜索类型菜单。每个菜单项都具备一下属性：绑定频道id**

**name：搜索类型名称。**

**selected：自定义默认选中的搜索类型**

**名称。 默认值为 null。**

[code]

     /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
        });
    });
[/code]



**searcher   Function(value,name)在用户按下搜索按钮或回车键的时候调用 searcher 函数。默认值为 null。**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
    });
[/code]



**disabled   boolean 是否禁用搜索框。默认为 false。**



[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            disabled:true,
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
    });
[/code]





**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403193015050-731605587.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403193038222-271423471.png)

**options   none 返回属性对象。**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        //设置图标和name
        <div data-options="name:'all',iconCls:'icon-ok'">体育</div>
        //设置图标和name
        <div data-options="name:'al2',iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            disabled:true,
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('options'));   //返回属性对象
    });
[/code]



**menu   none 返回搜索类型菜单对象。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            disabled:true,
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('menu'));   //返回属性对象
    });
[/code]

**设置频道图标**



[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        var m = $('#ss').searchbox('menu');
        m.menu('setIcon', {
            target : m.menu('findItem', '建材').target,
            iconCls : 'icon-save'
        });
    });
[/code]









**textbox   none 返回文本框对象。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            disabled:true,
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('textbox'));   //返回文本框对象
    });
[/code]



**getValue   none 返回当前搜索值。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('getValue'));   //返回当前搜索值
    });
[/code]



**setValue   value 设置一个新的搜索值。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('setValue','88888'));   //设置一个新的搜索值。
    });
[/code]



**getName   none 返回当前搜索类型名。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        alert($('#ss').searchbox('getName'));   //返回当前搜索类型名。
    });
[/code]



**selectName   name 选择当前搜索类型名。指定搜素类型，值为name**

[code]

    /**
    <!--搜索框-->
    <input id="ss">
    <!--频道按钮-->
    <div id="box">
        <div name="all" data-options="iconCls:'icon-ok'">体育</div>
        <div name="ghj" data-options="iconCls:'icon-ok'">建材</div>
    </div>
     **/
    
    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('selectName','ghj');     //指定搜素类型，值为name
    });
[/code]



**destroy   none 销毁该控件。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('destroy');     //销毁该控件
    });
[/code]



**resize   width 重置组件宽度。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('resize',200);     //重置组件宽度
    });
[/code]



**disable   none 禁用组件。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('disable');     //禁用组件
    });
[/code]



**enable   none 启用组件。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('enable');     //启用组件
    });
[/code]



**clear   none 清理搜索框内容。**

[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('clear');     //清理搜索框内容
    });
[/code]



**reset   none 重置搜索框内容。**



[code]

    $(function () {
        $('#ss').searchbox({
            width:800,
            height:40,
            menu: '#box',   //绑定频道id
            prompt: '请输入内容',
            searcher:function (value,name) {
                alert('用户按下搜索按钮或回车键的时候触发');
                alert('接收当前值：' + value + '|' + '接收当前频道：' + name);
            }
        });
        $('#ss').searchbox('reset');     //重置搜索框内容
    });
[/code]







**我们可以使用$.fn.searchbox.defaults 重写默认值对象。见前面章节**



