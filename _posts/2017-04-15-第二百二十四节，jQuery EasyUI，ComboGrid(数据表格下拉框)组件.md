---
layout: post
title: " 第二百二十四节，jQuery EasyUI，ComboGrid(数据表格下拉框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，ComboGrid(数据表格下拉框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416105135192-1467828306.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**



**本节课重点了解 EasyUI 中 ComboGrid(数据表格下拉框)组件的使用方法， 这个组件 依赖于 Combo(自定义下拉框)和
DataGrid(数据表格)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <select id="box" class="easyui-combogrid" name="dept"
            style="width:250px;"
            data-options="
                panelWidth:450,
                value:'请选择一个值',
                idField:'id',
                textField:'user',
                url:'content.json',
                columns:[[
                    {field:'user',title:'帐号',width:120},
                    {field:'email',title:'邮箱',width:120},
                    {field:'date',title:'创建时间',width:120},
                ]]
    "></select>
[/code]

**JS 加载方式**

[code]

     <input id="box" name="user" value="请选择一个用户">
[/code]

**js**

****combogrid()将一个input元素执行数据表格下拉框组件****

[code]

    $( function () {
        $('#box').combogrid({
            panelWidth: 600,
            idField: 'id',
            textField: 'user',
            url: 'content.json',
            columns: [[
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]





**二．属性列表**

**注意： **Combo(自定义下拉框)组件，用 ** **自定义下拉框的属性，方法，事件  **** DataGrid(数据表格)组件用 **
**数据表格的属性，方法，事件********

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415213649876-2007613122.png)**

**loadMsg   string 在数据表格加载远程数据的时候显示消息。默认值为 null。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]



**idField   string ID 字段名称。默认值为 null。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]



**textField   string 要显示在文本框中的文本字段。默认值为null。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]



**mode
string定义在文本改变的时候如何读取数据网格数据。设置为'remote'，数据表格将从远程服务器加载数据。当设置'emote'模式的时候，用户输入将会发送到名为'q'的
http 请求参数，向服务器检索新的数据。默认值为 local。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            mode:'remote',
            // filter: function (q, row) {
            //     var opts = $(this).combogrid('options');
            //     return row[opts.textField].indexOf(q) >= 0;
            // },
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]



**filter   function(q, row)定义在'mode'设置为'local'的时候如何选择本地数据，返回 true 时则选择该行。**



[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            // mode:'remote',
            filter: function (q, row) {
                var opts = $(this).combogrid('options');
                return row[opts.textField].indexOf(q) >= 0;
            },
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
    });
[/code]







**三，事件**

**PS：数据表格下拉框事件完全扩展自 combo(自定义下拉框)和 datagrid(数据表格)。**





**四，方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416102608270-1839202388.png)**

**options   none 返回属性对象。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
        alert($('#box').combogrid('options'));      //返回属性对象
    });
[/code]



  
**grid   none 返回数据表格对象。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
        var dxang = $('#box').combogrid('grid');      //返回数据表格对象
        $.each(dxang, function (attr, value) {        //遍历 JavaScript 原生态的对象数组
            alert(attr + ':' + value);
        });
    });
[/code]



  
**setValues   values 设置组件值数组。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
        $('#box').combogrid('setValues',[1,2,3]);      //设置组件值数组
    });
[/code]



  
**setValue   value 设置组件值。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
        $('#box').combogrid('setValue',2222);      //设置组件值
    });
[/code]



  
**clear   none 清除组件的值。**

[code]

    $(function () {
        $('#box').combogrid({
            panelWidth: 600,            //数据表格宽度
            idField: 'id',              //设置value值，一般设置数据库字段
            textField: 'user',          //显示在文本框中的文本字段
            url: 'content.json',        //远程加载数据地址
            loadMsg:'数据加载中',
            columns: [[                 //表格数据字段
                {
                    field: 'id',
                    title: '编号',
                    width: 120,
                },
                {
                    field: 'user',
                    title: '帐号',
                    width: 120,
                },
                {
                    field: 'email',
                    title: '邮箱',
                    width: 120,
                },
                {
                    field: 'date',
                    title: '创建时间',
                    width: 120,
                }
            ]]
        });
        $('#box').combogrid('clear');      //清除组件的值
    });
[/code]



