---
layout: post
title: " 第二百二十三节，jQuery EasyUI，ComboBox(下拉列表框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，ComboBox(下拉列表框)组件， 可以远程加载数据的下拉列表组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415171202173-99635499.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 ComboBox(下拉列表框)组件的使用方法， 这个组件依赖于 Combo(自定义下拉框)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <select id="box" class="easyui-combobox" name="box" style="width:200px;">
        <option value="aaaa">aaaa</option>
        <option value="bbbb">bbbb</option>
        <option value="cccc">cccc</option>
        <option value="dddd">dddd</option>
        <option value="eeee">eeee</option>
    </select>
[/code]

**JS 加载方式**

[code]

     <input id="box" name="user">
[/code]

**js代码**

**combobox()将一个input元素执行，(下拉列表框)组件**



[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',
            textField: 'user',
            url: 'content.json',
        });
    });
[/code]





**二．属性列表**



**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415121842376-1136161301.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415121853330-760689466.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415121903267-540731955.png)**

**远程content.json**



[code]

    [
        {
            "user" : "蜡笔小新",
            "email" : "xiaoxin@163.com",
            "date" : "2014-10-1",
            "id":"1",
            "xb":"男"
        },
        {
            "user" : "樱桃小丸子",
            "email" : "xiaowanzi@163.com",
            "date" : "2014-10-2",
            "id":"2",
            "xb":"女"
        },
        {
            "user" : "黑崎一护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3",
            "id":"3",
            "xb":"男"
        },
        {
            "user" : "黑崎2护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3",
            "id":"4",
            "xb":"女"
        },
        {
            "user" : "黑崎3护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3",
            "id":"5",
            "xb":"男"
        },
        {
            "user" : "黑崎4护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3",
            "id":"6",
            "xb":"女"
        },
        {
            "user" : "黑崎5护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3",
            "id":"7"
            ,"xb":"男"
        }
    
    ]
[/code]



**valueField   string 基础数据值名称绑定到该下拉列表框。默认为 value。设置下拉框的
**value值，如果是远程数据设置数据库指定的字段为 ** **value值********

[code]

    $( function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    });
[/code]





**textField   string 基础数据字段名称绑定到该下拉列表框。默认值 text。 **设置下拉框的 **text**
**值，如果是远程数据设置数据库指定的字段为 **text** ** **值**********

[code]

    $( function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    });
[/code]



**groupField   string 指定分组的字段名称。默认值 null。通过数据库一个字段来分组如通过性别字段分组**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            groupField:'xb'             //通过数据库一个字段来分组如通过性别字段分组
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415133915376-599072887.png)



**groupFormatter   function(group)返回格式化后的分组标题文本，以显示分组项**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            groupField:'xb',             //通过数据库一个字段来分组如通过性别字段分组
            groupFormatter:function (group) {       //返回格式化后的分组标题文本，以显示分组项
                return '('+group+')';
            }
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415134140251-563022038.png)





**mode
string定义了当文本改变时如何读取列表数据。设置为'remote'时，下拉列表框将会从服务器加载数据。当设置为“remote”模式时，用户输入将被发送到名为'q'的
HTTP 请求参数到服务器检索新数据。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            groupField:'xb',             //通过数据库一个字段来分组如通过性别字段分组
            groupFormatter:function (group) {       //返回格式化后的分组标题文本，以显示分组项
                return '('+group+')';
            },
            mode:'remote'               //向服务器传递输入值来索引
        });
    });
[/code]



**url   string 通过 URL 加载远程列表数据。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    });
[/code]



**method   string HTTP 方法检索数据(POST / GET)。设置远程提交方式**



**data   array 数据列表加载。本地化获取数据**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            // url: 'content.json',        //URL 加载远程列表数据
            groupField:'xb',             //通过数据库一个字段来分组如通过性别字段分组
            groupFormatter:function (group) {       //返回格式化后的分组标题文本，以显示分组项
                return '('+group+')';
            },
            mode: 'remote',               //向服务器传递输入值来索引
            data: [
                {
                    "user": "蜡笔小新",
                    "email": "xiaoxin@163.com",
                    "date": "2014-10-1",
                    "id": "1",
                    "xb": "男"
                },
                {
                    "user": "樱桃小丸子",
                    "email": "xiaowanzi@163.com",
                    "date": "2014-10-2",
                    "id": "2",
                    "xb": "女"
                }
            ]
        });
    });
[/code]



**filter   function定义当'mode'设置为'local'时如何过滤本地数据，函数有 2
个参数：q：用户输入的文本。row：列表行数据。返回 true 的时候允许行显示。过滤查找， **mode不设置的情况下使用****

[code]

    $( function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            groupFormatter: function (group) {       //返回格式化后的分组标题文本，以显示分组项
                return '(' + group + ')';
            },
            filter: function (q, row) {
                var opts = $(this).combobox('options');
                return row[opts.textField].indexOf(q) >= 0;
            },
        });
    });
[/code]



**formatter   function 定义如何渲染行。该函数接受 1 个参数：row。格式化下拉选项**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            groupFormatter: function (group) {       //返回格式化后的分组标题文本，以显示分组项
                return '(' + group + ')';
            },
            formatter: function (row) {     //格式化下拉选项
                var opts = $(this).combobox('options');
                return '[' + row[opts.textField] + ']';
            }
        });
    });
[/code]



**loader   function(param,success,error)定义了如何从远程服务器加载数据。返回false
可以忽略该动作。该函数具备如下参数：param：传递到远程服务器的参数对象。success(data)：在检索数据成功的时候调用该回调函数。error()：在检索数据失败的时候调用该回调函数。**



**loadFilter function(data) 返回过滤后的数据并显示。**





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415144111001-628785782.png)**

**onBeforeLoad   param在请求加载数据之前触发，返回 false 取消该加载动作。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onBeforeLoad:function () {  //在请求加载数据之前触发，返回 false 取消该加载动作。
                alert('在请求加载数据之前触发');
            }
        });
    });
[/code]



  
**onLoadSuccess   none 在加载远程数据成功的时候触发。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onLoadSuccess:function () {  //在加载远程数据成功的时候触发
                alert('在加载远程数据成功的时候触发');
            }
        });
    });
[/code]



  
**onLoadError   none 在加载远程数据失败的时候触发。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content2.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onLoadError:function () {  //在加载远程数据失败的时候触发
                alert('在加载远程数据失败的时候触发');
            }
        });
    });
[/code]



  
**onSelect   record 在用户选择列表项的时候触发。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onSelect:function () {  //在用户选择列表项的时候触发
                alert('在用户选择列表项的时候触发');
            }
        });
    });
[/code]



  
**onUnselect   record 在用户取消选择列表项的时候触发。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onUnselect:function () {  //在用户取消选择列表项的时候触发
                alert('在用户取消选择列表项的时候触发');
            }
        });
    
        $('#ann').click(abc);                       //点击按钮后
        function abc() {
            $('#box').combobox('unselect', 1);      //取消选择列表
        }
    
    });
[/code]





**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415161126908-1464541237.png)**



**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
        var shux = $('#box').combobox('options');       //返回属性对象
        $.each(shux, function (attr, value) { //遍历 JavaScript 原生态的对象数组
            alert(attr + ':' + value);
        });
    });
[/code]



**getData   none 返回加载数据。**

  
**loadData   data 读取本地列表数据。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            // url: 'content.json',        //URL 加载远程列表数据
        });
    
        $('#box').combobox('loadData',[{    //读取本地列表数据。
            "user" : "蜡笔小新",
            "email" : "xiaoxin@163.com",
            "date" : "2014-10-1",
            "id":"1",
            "xb":"男"
        }]);
    
    });
[/code]



  
**reload   url 请求远程列表数据。通过'url'参数重写原始URL 值。**

  
**setValues   values 设置下拉列表框值数组。 **设置下拉列表框 **values值，数组方式也就是设置多个值******

  
**setValue   value 设置下拉列表框的值。 **

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    
        $('#box').combobox('setValue','555');   //设置下拉列表框的值
    
    });
[/code]



  
**clear   none 清除下拉列表框的值。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    
        $('#box').combobox('clear');   //清除下拉列表框的值
    
    });
[/code]



  
**select   value 选择指定项。**

[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
        });
    
        $('#box').combobox('select',2);   //选择指定项
    
    });
[/code]



  
**unselect   value 取消选择指定项。**



[code]

    $(function () {
        $('#box').combobox({
            valueField: 'id',           //设置下拉框的value值，如果是远程数据设置数据库指定的字段为value值
            textField: 'user',          //设置下拉框的text值，如果是远程数据设置数据库指定的字段为text值
            url: 'content.json',        //URL 加载远程列表数据
            // groupField: 'xb',             //通过数据库一个字段来分组如通过性别字段分组
            onUnselect:function () {  //在用户取消选择列表项的时候触发
                alert('在用户取消选择列表项的时候触发');
            }
        });
    
        $('#ann').click(abc);                       //点击按钮后
        function abc() {
            $('#box').combobox('unselect', 1);      //取消选择列表
        }
    
    });
[/code]



