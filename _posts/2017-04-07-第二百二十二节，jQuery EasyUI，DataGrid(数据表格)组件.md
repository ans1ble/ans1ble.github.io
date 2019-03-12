
---
layout: post
title: " 第二百二十二节，jQuery EasyUI，DataGrid(数据表格)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQuery EasyUI，DataGrid(数据表格)组件**



**学习要点：**

**1.加载方式**

**2.分页功能**



**本节课重点了解 EasyUI 中 DataGrid(数据表格)组件的使用方法， 这个组件依赖于
Panel(面板)、Resizeable(调整大小)、LinkButton(按钮)、Pageination(分页)组件。**



**一．加载方式**

**DataGrid 以表格形式展示数据，并提供了丰富的选择、排序、分组和编辑数据的功能 支持。DataGrid
的设计用于缩短开发时间，并且使开发人员不需要具备特定的知识。它是 轻量级的且功能丰富。**

**class 加载方式**

[code]

     <table class="easyui-datagrid" data-options="width:400">
        <thead>
        <tr>
            <th data-options="field:'username'">帐号</th>
            <th data-options="field:'email'">邮件</th>
            <th data-options="field:'create'">注册时间</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>蜡笔小新</td>
            <td>xiaoxin@163.com</td>
            <td>2014-10-1</td>
        </tr>
        <tr>
            <td>樱桃小丸子</td>
            <td>yingtao@163.com</td>
            <td>2014-10-2</td>
        </tr>
        <tr>
            <td>黑崎一护</td>
            <td>yihu@163.com</td>
            <td>2014-10-3</td>
        </tr>
        </tbody>
    </table>
[/code]





**JS 加载方式**

**datagrid()将table元素执行数据表格组件**

html

[code]

    <table id="box">
        <thead>
        <tr>
            <th>帐号</th>
            <th>邮件</th>
            <th>注册时间</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>蜡笔小新</td>
            <td>xiaoxin@163.com</td>
            <td>2014-10-1</td>
        </tr>
        <tr>
            <td>樱桃小丸子</td>
            <td>yingtao@163.com</td>
            <td>2014-10-2</td>
        </tr>
        <tr>
            <td>黑崎一护</td>
            <td>yihu@163.com</td>
            <td>2014-10-3</td>
        </tr>
        </tbody>
    </table>
[/code]

js

[code]

    $(function () {
        $('#box').datagrid({
            // width: 400,
            title: '用户列表',
            iconCls: 'icon-search',
            columns: [[
                {
                    field: 'username',
                    title: '帐号',
                },
                {
                    field: 'email',
                    title: '邮件',
                },
                {
                    field: 'date',
                    title: '注册时间',
                }
            ]]
        })
    });
[/code]



**二．分页和排序**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407222839035-952485800.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407222852378-2071085451.png)

**远程加载数据[重点]**

**如果是远程加载数据，html只需要写一个table标签即可**

**html**

[code]

     <table id="box"></table>
[/code]

**JSON 数据，content.json**

[code]

     [
        {
            "user" : "蜡笔小新",
            "email" : "xiaoxin@163.com",
            "date" : "2014-10-1"
        },
        {
            "user" : "樱桃小丸子",
            "email" : "xiaowanzi@163.com",
            "date" : "2014-10-2"
        },
        {
            "user" : "黑崎一护",
            "email" : "yihu@163.com",
            "date" : "2014-10-3"
        }
    ]
[/code]

**js调用**

[code]

    $( function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]]
        })
    });
[/code]



**url   string 从远程请求JSON 数据数据。默认为 null。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]]
        })
    });
[/code]



**columns   array DataGrid 列配置对象，详见列属性说明中更多细节。默认值为 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]]
        })
    });
[/code]

**远程加载数据显示到表格原理图**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407233514457-1625568645.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407233544816-427596477.png)



**pagination   boolean 设置为 true，则在 DataGrid 组件底部显示分页工具栏。默认为 false。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true         //组件底部显示分页工具栏
        })
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407234109144-1225273780.png)



**pageNumber   number 设置分页时初始化页码。默认为 null。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9]          //设置可选每页显示条数
        })
    });
[/code]



**pageSize   number ****设置分页时设置每页多少条** **。默认为10。 注意与 **pageList结合****

[code]

    $( function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9]          //设置可选每页显示条数
        })
    });
[/code]



**pageList   array设置分页时初始化条数选择大小。默认为[10,20,30,40,50]。设置可选每页显示条数，注意与
**pageSize结合****

[code]

    $( function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9]          //设置可选每页显示条数
        })
    });
[/code]



**pagePosition   string 设 置 分 页 工 具 栏 的 位 置 。 可 选 值 为 ：top,bottom,both。默认
bottom。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            pagePosition:'bottom'
        })
    });
[/code]



  
**列属性，在 columns属性 里设置的属性**  
 **title   string 列标题名称。默认 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            pagePosition:'bottom'
        })
    });
[/code]



**field   String 列字段名称。默认 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            pagePosition:'bottom'
        })
    });
[/code]



**width   number 列的宽度。没有设置则自适应。默认 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            pagePosition:'bottom'
        })
    });
[/code]





**三.排序功能**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170408182804207-1413272245.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170408182811910-906638062.png)**



**sortName   string 设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
        })
    });
[/code]



**sortOrder   string 设置列排序的顺序,ASC 和 DESC，默认是 ASC。 **这个值会发送到数据库****

[code]

    $( function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
        })
    });
[/code]



**multiSort   boolean 设置是否运行多列排序，默认为 false。一般不使用，会将所有排序的字段和排序方法传输**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sortable:true,       //则可以点击排序
                    order:'DESC'         //点击排序的方式
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            // sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            // sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
            remoteSort:false,        //设置服务器对数据进行排序。默认为 true。false不通过服务器排序
            multiSort:true          //设置是否运行多列排序，默认为 false。
        })
    });
[/code]



**remoteSort   boolean 设置服务器对数据进行排序。默认为 true。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sortable:true,       //则可以点击排序
                    order:'DESC'         //点击排序的方式
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            // sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            // sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
            remoteSort:false        //设置服务器对数据进行排序。默认为 true。false不通过服务器排序
        })
    });
[/code]



**method   string 设置请求远程数据类型，默认为 post。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            sortOrder:'DESC',        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
            method:'get'            //设置请求远程数据类型，默认为 post。
        })
    });
[/code]



**queryParams   object 设置请求远程数据发送的额外数据。默认为null。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            sortOrder:'DESC',        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
            queryParams:{           //设置请求远程数据发送的额外数据
                id:1
            }
        })
    });
[/code]



**  列属性，在 columns 里设置的属性**

**sortable   boolean 设置为 true，则可以点击排序。默认 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sortable:true,       //则可以点击排序
                    order:'DESC'         //点击排序的方式
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            // sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            // sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
        })
    });
[/code]



**order   string 点击排序的默认，ASC 或 DESC，默认 undefined。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sortable:true,       //则可以点击排序
                    order:'DESC'         //点击排序的方式
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            // sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            // sortOrder:'DESC'        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
        })
    });
[/code]



**sorter   Function 自定义排序，接受 a,b 两个值。注意自定义排序remoteSort要设置为false**



[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            sortName:'date',        //设置哪些列可以进行排序。默认为 null。值为field的值也就是可以排序的字段，这个值会发送到数据库
            sortOrder:'DESC',        //设置列排序的顺序,ASC 和 DESC，默认是 ASC。这个值会发送到数据库
            queryParams:{           //设置请求远程数据发送的额外数据
                id:1
            },
            remoteSort:false        //设置服务器对数据进行排序。默认为 true。false则不通过服务器排序
        })
    });
[/code]



**四、样式设置**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170411184250688-1728127115.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170411184304751-772387796.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170411184317282-2008204790.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170411184331641-484240148.png)

**striped   boolean 是否显示斑马线效果。默认为 false。也就是隔一行显示一个淡灰色背景**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            striped:true            //是否显示斑马线效果。默认为 false。也就是隔一行显示一个淡灰色背景
        })
    });
[/code]



**nowrap   boolean 是否在一行显示所有数据。默认为 true。也就是文字受到挤压是否换行**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            nowrap:false            //是否在一行显示所有数据。默认为 true。
        })
    });
[/code]



**fitColumns   boolean 是否自动展开或收缩，以达到自适应。默认为 false。也就是是否自适应面板**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            fitColumns:true            //也就是是否自适应面板
        })
    });
[/code]



**data   array,object 手工数据加载。默认为 null。前提是要阻止掉服务器加载**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            // url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            data:[{
                user:'手工用户',
                email:'手工邮件',
                date:'2014-12-8'
            }]
        })
    });
[/code]



**loadMsg   string 从远程加载数据显示的提示信息。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            loadMsg:'数据加载中'
        })
    });
[/code]



**rownumbers   boolean 设置 true，显示一个行号。默认为 false。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            rownumbers:true         //显示一个行号。默认为 false。
        })
    });
[/code]



**singleSelect   boolean 设置 true，只能选定一行。默认为 false。也就是点击后改变背景颜色只能选定一行**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            singleSelect:true         //只能选定一行。默认为 false。
        })
    });
[/code]



**showHeader   boolean 是否显示行头，默认为 true。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            showHeader:false         //是否显示行头，默认为 true。
        })
    });
[/code]



**showFooter   boolean 是否显示行尾，默认为 false。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            showFooter:true         //是否显示行尾，默认为 false。
        })
    });
[/code]



**scrollbarSize   number 滚动条所占的宽度或高度。默认为18。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            scrollbarSize:30         //滚动条所占的宽度或高度。默认为18。
        })
    });
[/code]



**rowStyler   function 带两个参数，index 索引，row 对象，可以通过 return 返回选定行的样式。可以修改指定行的样式**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    // width: 200,
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            rowStyler:function (index,row) {    //row接收整个数据对象
                if (row.user == '樱桃小丸子'){
                    //这里返回的也可以是CSS的class名称
                    alert(index);
                    return 'background-color:orange';
                }
            }
        })
    });
[/code]



  
**列属性，在 columns 里设置的属性**

**align   string 对齐列数据。有 left,center,right 三种。默认为 undefined。设置标题和内容对齐方式**



[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    align:'center'
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]









**halign   string 对齐标题。有 left,center,right 三种。默认为undefined。只设置标题对齐方式**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    halign:'center'     //只设置标题对齐方式
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**resizable   boolean 设置 true，则允许改变大小。是否允许改变大小**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    resizable:false     //是否允许改变大小
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**fixed   boolean 设置 true，则阻止自适应。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    fixed:true     //设置 true，则阻止自适应。
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**hidden   boolean 设置 true，则隐藏列。**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    hidden:true     //设置 true，则隐藏列。
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    sorter:function (a,b) {
                        alert(a+b);     //ad得到第一个日期，b得到第二个日期，以此循环，可以量上一个日期和下一个日期做判断来排序
                    }
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**formatter   function 单元格格式化函数，接受三个参数：value 值,row对象,index 索引。设置数据**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    formatter:function (value,row,index) {
                        //value得到数据内容,row得到整个表格数据对象,index索引
                        return '('+value+')';
                    }
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**styler   function 单元格样式设定，接受三个参数：value 值,row对象,index 索引。设置单元格**

[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    styler:function (value,row,index) {
                        //value得到数据内容,row得到整个表格数据对象,index索引
                        if (value == '蜡笔小新'){
                            return 'background-color:orange';
                        }
                    }
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
        })
    });
[/code]



**五，自适应填充表格布满**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412142259830-2034307786.png)**



[code]

    $(function () {
        $('#box').datagrid({
            width: 400,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width:100
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                    width:100
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    width:100
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            fitColumns:true,         //设置表格自适应
            scrollbarSize:0          //滚动条所占的宽度或高度。默认为18。
        })
    });
[/code]





**六，查询功能**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412164121798-398946774.png)**

**toolbar   Array,selector顶部工具栏的 DataGrid 面板。可能的值：1) 一 个 数 组 ， 每 个 工 具 属 性 都
和linkbutton 一样。2) 选择器指定的工具栏。 **toolbar属性:** 将指定区块添加成数据表格工具栏**  
  

**load
param加载和显示第一页的所有行。如果指定了'param'，它将取代'queryParams'属性。通常可以通过传递一些参数执行一次查询，通过调用这个方法从服务器加载新数据**。
**load方法：提交查询数据**

html

[code]

    <table id="box"></table>
    <div id="tb">
        <div>
            <a id="tianjia" href="#">添加</a>
            <a id="xiougai" href="#">修改</a>
            <a id="shanchu" href="#">删除</a>
        </div>
        <div id="gjl2">
            查询帐号：<input class="textbox" type="text" name="user">
            创建时间从：<input class="shj1" type="text" name="date_from">
            到：<input class="shj2" type="text" name="date_to">
            <a class="chx" href="#">查询</a>
        </div>
    </div>
[/code]

css

[code]

    #tb{
        padding:5px;
    }
    #gjl2{
        padding: 5px;
    }
    
    .textbox {
        height: 20px;
        margin: 0;
        padding: 0 2px;
        box-sizing: content-box;
    }
    .chx{
        margin: 0 0 0 20px;
    }
[/code]

js

[code]

    $(function () {
        //将table标签执行数据表格组件方法
        $('#box').datagrid({
            width: 800,                 //设置宽度
            url : 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width:100
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                    width:100
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    width:100
                }
            ]],
            pagination:true,         //组件底部显示分页工具栏
            pageNumber:1,             //设置分页时初始化页码
            pageSize:3,               //设置分页时设置每页多少条
            pageList:[3,6,9],          //设置可选每页显示条数
            fitColumns:true,         //设置表格自适应
            scrollbarSize:0,          //滚动条所占的宽度或高度。默认为18。
            toolbar:'#tb'           //引入id为tb的区块工具栏
        });
        //数据表格工具栏1
        $('#tianjia').linkbutton({  //将工具栏里的添加执行按钮方法
            iconCls:'icon-add',     //设置图标
            plain:true              //按钮扁平化
        });
        $('#xiougai').linkbutton({  //将工具栏里的修改执行按钮方法
            iconCls:'icon-edit',    //设置图标
            plain:true              //按钮扁平化
        });
        $('#shanchu').linkbutton({  //将工具栏里的删除执行按钮方法
            iconCls:'icon-remove',  //设置图标
            plain:true              //按钮扁平化
        });
        //数据表格工具栏2
        $('.shj1').datebox();   //查询日期输入框
        $('.shj2').datebox();   //查询日期输入框
        $('.chx').linkbutton({  //查询按钮
            iconCls:"icon-search"
        });
        //查询功能
        $('.chx').click(function () {   //点击查询后执行obj对象里的search方法
            obj.search();
        });
        var obj = {                     //obj对象
            search: function () {
                $('#box').datagrid('load',{                         //执行数据表格的load方法提交数据
                    user : $.trim($('input[name="user"]').val()),   //获取查询用户
                    date_from : $('input[name="date_from"]').val(), //获取查询起始时间
                    date_to : $('input[name="date_to"]').val(),     //获取查询结束时间
                });
            }
        };
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412165203658-908950572.png)



**七，新增功能**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412193313455-720095412.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412193334736-766747240.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412193346845-2102922774.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170412193357548-592089206.png)



**DataGrid 属性，扩展自 Panel 面板**  
 **editors   object 定义在编辑行的时候使用的编辑器。**

  
**列属性，在 columns 里设置的属性**  
 **editor   string,object指明编辑类型。当字符串指明编辑类型的时候，对象包含两个属性：type ： 字 符 串 ， 可 使 用 的
类 型 有
：text,textarea,checkbox,numberbox,validatebox,datebox,combobox,combotree。options：对象，object，该编辑器属性对应于编辑类型。**

  
**Editor(编辑器)**  
 **init   container, options 初始化编辑器并返回目标对象。**  
 **destroy   target 如果有必要销毁编辑器。**  
 **getValue   target 从编辑器中获取值。**  
 **setValue   target , value 向编辑器中写入值。**  
 **resize   target , width 如果有必要调整编辑器的大小。**

  
**DataGrid 方法**  
 **appendRow   row 追加一个新行。新行将被添加到最后的位置。**



[code]

                $('#box').datagrid('appendRow',{
                    user:'林贵秀',
                    email:'729088188@qq.com',
                    date:'2017-4-12'
                });
[/code]



**insertRow   row插入一个新行，参数包括一下属性：index：要插入的行索引，如果该索引值未定义，则追加新行。row：行数据。**

**beginEdit   index 开始编辑行。**  
 **endEdit   index 结束编辑行。**

**rejectChanges   none回 滚 所 有 从 创 建 或 上 一 次 调 用acceptChanges 函数后更改的数据。**

  
**DataGrid 事件**  
 **onAfterEdit
rowIndex,rowData,changes在用户完成编辑一行的时候触发，参数包括：rowIndex：编辑行的索引，索引从 0
开始。rowData：对应于完成编辑的行的记录。changes：更改后的字段(键)/值对。**



[code]

    $(function () {
        //将数据表格的列属性，在 columns 里设置的属性editor扩展一个type属性值datetimebox也就是日期输入框带时分秒
        $.extend($.fn.datagrid.defaults.editors, {
            datetimebox: {
                init: function (container, options) {
                    var input = $('<input type="text">').appendTo(container);
                    options.editable = false;
                    input.datetimebox(options);
                    return input;
                },
                getValue: function (target) {
                    return $(target).datetimebox('getValue');
                },
                setValue: function (target, value) {
                    $(target).datetimebox('setValue', value);
                },
                resize: function (target, width) {
                    $(target).datetimebox('resize', width);
                },
                destroy: function (target) {
                    $(target).datetimebox('destroy');
                },
            }
        });
        //将table标签执行数据表格组件方法
        $('#box').datagrid({
            width: 800,                 //设置宽度
            url: 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true
                        }
                    }
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true,
                            validType: 'email'
                        }
                    }
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'datetimebox',
                        options: {
                            required: true,
                        }
                    }
                }
            ]],
            pagination: true,         //组件底部显示分页工具栏
            pageNumber: 1,             //设置分页时初始化页码
            pageSize: 3,               //设置分页时设置每页多少条
            pageList: [3, 6, 9],          //设置可选每页显示条数
            fitColumns: true,         //设置表格自适应
            scrollbarSize: 0,          //滚动条所占的宽度或高度。默认为18。
            toolbar: '#tb',           //引入id为tb的区块工具栏
            //      第五步
            onAfterEdit : function (rowIndex, rowData, changes) {       //在用户完成编辑一行的时候触发
                $('#baoc,#qxiao').hide();
                obj.panduan = false;
                $.each(rowData, function (attr, value){
                    //在这里就可以通过Ajax向数据库添加数据，rowData接收的添加数据的对象
                    alert(attr + ':' + value);
                });
            }
        });
        //数据表格工具栏1
        $('#tianjia').linkbutton({  //将工具栏里的添加执行按钮方法
            iconCls: 'icon-add',     //设置图标
            plain: true              //按钮扁平化
        });
        $('#xiougai').linkbutton({  //将工具栏里的修改执行按钮方法
            iconCls: 'icon-edit',    //设置图标
            plain: true              //按钮扁平化
        });
        $('#shanchu').linkbutton({  //将工具栏里的删除执行按钮方法
            iconCls: 'icon-remove',  //设置图标
            plain: true              //按钮扁平化
        });
        $('#baoc').linkbutton({     //将工具栏里的保存执行按钮方法
            iconCls: 'icon-save',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        $('#qxiao').linkbutton({     //将工具栏里的取消执行按钮方法
            iconCls: 'icon-redo',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        //数据表格工具栏2
        $('.shj1').datebox();   //查询日期输入框
        $('.shj2').datebox();   //查询日期输入框
        $('.chx').linkbutton({  //查询按钮
            iconCls: "icon-search"
        });
        //查询功能
        $('.chx').click(function () {       //点击查询后执行obj对象里的search方法
            obj.search();
        });
        //添加        第一步
        $('#tianjia').click(function () {   //点击添加按钮执行obj对象里的tianjia方法
            obj.tianjia();
        });
        //保存        第三步
        $('#baoc').click(function () {      //点击保存按钮执行obj对象里的baoc方法
            obj.baoc();
        });
        //取消        第六步
        $('#qxiao').click(function () {      //点击取消按钮执行obj对象里的qxiao方法
            obj.qxiao();
        });
        var obj = {                     //obj对象
            panduan: false,
            //查询
            search: function () {
                if (!this.panduan) {
                    $('#box').datagrid('load', {                         //执行数据表格的load方法提交数据
                        user: $.trim($('input[name="user"]').val()),   //获取查询用户
                        date_from: $('input[name="date_from"]').val(), //获取查询起始时间
                        date_to: $('input[name="date_to"]').val(),     //获取查询结束时间
                    });
                }
            },
            //添加        第二步
            tianjia: function () {
                $('#baoc,#qxiao').show();
                if (!this.panduan) {
                    $('#box').datagrid('insertRow', {        //向数据表格插入一行
                        index: 0,                            //插入位置第0个索引，也就是第一条
                        row: {}
                    });
                    $('#box').datagrid('beginEdit', 0);     //开始编辑
                    this.panduan = true;                    //调整为true防止重复添加
                }
            },
            //保存  第四步
            baoc: function () {
                $('#box').datagrid('endEdit', 0);           //结束编辑
            },
            //取消   第七步
            qxiao: function () {
                $('#baoc,#qxiao').hide();                    //隐藏保存取消按钮
                this.panduan = false;
                $('#box').datagrid('rejectChanges');        //回 滚 所 有 从 创 建 或 上 一 次 调 用acceptChanges 函数后更改的数据。
            }
        };
    });
[/code]





**八，修改删除功能**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170413104239392-1068313230.png)**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170413104248580-640723737.png)

**列属性，在 columns 里设置的属性**  
 **checkbox   boolean 如果为 true，则显示复选框。该复选框列固定宽度。将一列表格变成多选框**



**DataGrid 方法**  
 **getSelections   none返回所有被选中的行数组对象，当没有记录被选中的时候将返回一个空数组。**

  
**getRowIndex   row 获取到当前行的索引。**

  
**unselectRow   index 取消指定选择的行。**



**DataGrid 事件**  
 **onDblClickRow   rowIndex,rowData在用户双击一行的时候触发，参数包括：rowIndex：点击的行的索引值，该索引值从
0开始。rowData：对应于点击行的记录。**



[code]

    $(function () {
        //将数据表格的列属性，在 columns 里设置的属性editor扩展一个type属性值datetimebox也就是日期输入框带时分秒
        $.extend($.fn.datagrid.defaults.editors, {
            datetimebox: {
                init: function (container, options) {
                    var input = $('<input type="text">').appendTo(container);
                    options.editable = false;
                    input.datetimebox(options);
                    return input;
                },
                getValue: function (target) {
                    return $(target).datetimebox('getValue');
                },
                setValue: function (target, value) {
                    $(target).datetimebox('setValue', value);
                },
                resize: function (target, width) {
                    $(target).datetimebox('resize', width);
                },
                destroy: function (target) {
                    $(target).datetimebox('destroy');
                },
            }
        });
        //将table标签执行数据表格组件方法
        $('#box').datagrid({
            width: 800,                 //设置宽度
            url: 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    //第三步，设置id表格列
                    field : 'id',
                    title : '编号',
                    width : 100,
                    checkbox : true,    //将id列变成多选框
                },
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true
                        }
                    }
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true,
                            validType: 'email'
                        }
                    }
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'datetimebox',
                        options: {
                            required: true,
                        }
                    }
                }
            ]],
            pagination: true,         //组件底部显示分页工具栏
            pageNumber: 1,             //设置分页时初始化页码
            pageSize: 3,               //设置分页时设置每页多少条
            pageList: [3, 6, 9],          //设置可选每页显示条数
            fitColumns: true,         //设置表格自适应
            scrollbarSize: 0,          //滚动条所占的宽度或高度。默认为18。
            toolbar: '#tb',           //引入id为tb的区块工具栏
            // singleSelect : true,      //只允许选择一行
            //编辑完保存执行
            onAfterEdit : function (rowIndex, rowData, changes) {       //在用户完成编辑一行的时候触发
                $('#baoc,#qxiao').hide();
                obj.panduan = undefined;
                $.each(rowData, function (attr, value){
                    //在这里就可以通过Ajax向数据库添加数据，rowData接收的添加数据的对象
                    alert(attr + ':' + value);
                });
            },
            //双击一行触发        第一步双击修改
            onDblClickRow: function (rowIndex, rowData) {
                if (obj.panduan != undefined){
                    $('#box').datagrid('endEdit', obj.panduan);     //结束编辑
                }
                if (obj.panduan == undefined) {
                    $('#baoc,#qxiao').show();                      //显示保存和取消按钮
                    $('#box').datagrid('beginEdit', rowIndex);     //获取双击的行索引开始编辑
                    obj.panduan = rowIndex;
                }
            }
        });
        //数据表格工具栏1
        $('#tianjia').linkbutton({  //将工具栏里的添加执行按钮方法
            iconCls: 'icon-add',     //设置图标
            plain: true              //按钮扁平化
        });
        $('#xiougai').linkbutton({  //将工具栏里的修改执行按钮方法
            iconCls: 'icon-edit',    //设置图标
            plain: true              //按钮扁平化
        });
        $('#shanchu').linkbutton({  //将工具栏里的删除执行按钮方法
            iconCls: 'icon-remove',  //设置图标
            plain: true              //按钮扁平化
        });
        $('#baoc').linkbutton({     //将工具栏里的保存执行按钮方法
            iconCls: 'icon-save',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        $('#qxiao').linkbutton({     //将工具栏里的取消执行按钮方法
            iconCls: 'icon-redo',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        //数据表格工具栏2
        $('.shj1').datebox();   //查询日期输入框
        $('.shj2').datebox();   //查询日期输入框
        $('.chx').linkbutton({  //查询按钮
            iconCls: "icon-search"
        });
        //查询功能
        $('.chx').click(function () {       //点击查询后执行obj对象里的search方法
            obj.search();
        });
        //添加
        $('#tianjia').click(function () {   //点击添加按钮执行obj对象里的tianjia方法
            obj.tianjia();
        });
        //保存
        $('#baoc').click(function () {      //点击保存按钮执行obj对象里的baoc方法
            obj.baoc();
        });
        //取消
        $('#qxiao').click(function () {      //点击取消按钮执行obj对象里的qxiao方法
            obj.qxiao();
        });
        //修改
        $('#xiougai').click(function () {      //点击修改按钮执行obj对象里的xiougai方法
            obj.xiougai();
        });
        $('#shanchu').click(function () {      //点击删除按钮执行obj对象里的shanchu方法
            obj.shanchu();
        });
        var obj = {                     //obj对象
            panduan: undefined,
            //查询
            search: function () {
                if (this.panduan == undefined) {
                    $('#box').datagrid('load', {                         //执行数据表格的load方法提交数据
                        user: $.trim($('input[name="user"]').val()),   //获取查询用户
                        date_from: $('input[name="date_from"]').val(), //获取查询起始时间
                        date_to: $('input[name="date_to"]').val(),     //获取查询结束时间
                    });
                }
            },
            //添加
            tianjia: function () {
                $('#baoc,#qxiao').show();
                if (this.panduan == undefined) {
                    $('#box').datagrid('insertRow', {        //向数据表格插入一行
                        index: 0,                            //插入位置第0个索引，也就是第一条
                        row: {}
                    });
                    $('#box').datagrid('beginEdit', 0);     //开始编辑
                    this.panduan = 0;                    //调整为true防止重复添加
                }
            },
            //保存
            baoc: function () {
                $('#box').datagrid('endEdit', this.panduan);           //结束编辑
            },
            //取消
            qxiao: function () {
                $('#baoc,#qxiao').hide();                    //隐藏保存取消按钮
                this.panduan = undefined;
                $('#box').datagrid('rejectChanges');        //回 滚 所 有 从 创 建 或 上 一 次 调 用acceptChanges 函数后更改的数据。
            },
            //修改        第二步选择一行点击修改按钮修改
            xiougai:function () {
                var rows = $('#box').datagrid('getSelections');     //返回所有被选中的行数组对象，当没有记录被选中的时候将返回一个空数组。
                if (rows.length == 1) {
                    if (this.panduan != undefined) {
                        $('#box').datagrid('endEdit', this.panduan);     //结束编辑
                    }
                    if (this.panduan == undefined) {
                        var index = $('#box').datagrid('getRowIndex', rows[0]);     //获取到当前行的索引
                        $('#baoc,#qxiao').show();                                   //显示保存和取消按钮
                        $('#box').datagrid('beginEdit', index);                  //获取双击的行索引开始编辑
                        this.panduan = index;
                        $('#box').datagrid('unselectRow', index);                //取消指定选择的行
                    }
                }else {
                    $.messager.alert('警告', '请选择一行修改！', 'warning');
                }
            },
            //第四步       删除
            shanchu:function () {
                var rows = $('#box').datagrid('getSelections');     //返回所有被选中的行数组对象，当没有记录被选中的时候将返回一个空数组。
                if (rows.length > 0){
                    $.messager.confirm('确定操作', '您正在要删除所选的记录吗？', function (flag) {
                        if (flag) {             //如果用户点击了确定
                            var ids = [];
                            for (var i = 0; i < rows.length; i ++) {    //循环出数组对象
                                ids.push(rows[i].id);                   //将对象里的id添加到数组
                            }
                            //在这里可以将要删除的id发送到数据库
                            alert(ids.join(','));
                        }
                    });
                }else {
                    $.messager.alert('提示', '请选择要删除的记录！', 'info');
                }
            }
        };
    });
[/code]





**九，添加，修改，删除，后台交互**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170413232734845-870974544.png)**



**load   param 加载和显示第一页的所有行，即刷新当前页。**

**loading   none 显示载入状态。**

**loaded   none 隐藏载入状态。**

**unselectAll   none 取消所有当前页中的所有行。**

**getChanges
type从上一次的提交获取改变的所有行。类型参数指明用哪些类型改变的行，可以使用的值有：inserted,deleted,updated
等。当类型参数未配置的时候返回所有改变的行。获取那种类型执行的数据**



[code]

    $(function () {
        //将数据表格的列属性，在 columns 里设置的属性editor扩展一个type属性值datetimebox也就是日期输入框带时分秒
        $.extend($.fn.datagrid.defaults.editors, {
            datetimebox: {
                init: function (container, options) {
                    var input = $('<input type="text">').appendTo(container);
                    options.editable = false;
                    input.datetimebox(options);
                    return input;
                },
                getValue: function (target) {
                    return $(target).datetimebox('getValue');
                },
                setValue: function (target, value) {
                    $(target).datetimebox('setValue', value);
                },
                resize: function (target, width) {
                    $(target).datetimebox('resize', width);
                },
                destroy: function (target) {
                    $(target).datetimebox('destroy');
                },
            }
        });
        //将table标签执行数据表格组件方法
        $('#box').datagrid({
            width: 800,                 //设置宽度
            url: 'content.json',       //远程加载数据地址
            title: '用户列表',           //面板属性，添加标题
            iconCls: 'icon-search',     //添加图标
            columns: [[                 //设置要显示表格数据
                {
                    //第三步，设置id表格列
                    field : 'id',
                    title : '编号',
                    width : 100,
                    checkbox : true,    //将id列变成多选框
                },
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true
                        }
                    }
                },
                {
                    field: 'email',     //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '邮件',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true,
                            validType: 'email'
                        }
                    }
                },
                {
                    field: 'date',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '注册时间',   //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'datetimebox',
                        options: {
                            required: true,
                        }
                    }
                }
            ]],
            pagination: true,         //组件底部显示分页工具栏
            pageNumber: 1,             //设置分页时初始化页码
            pageSize: 3,               //设置分页时设置每页多少条
            pageList: [3, 6, 9],          //设置可选每页显示条数
            fitColumns: true,         //设置表格自适应
            scrollbarSize: 0,          //滚动条所占的宽度或高度。默认为18。
            toolbar: '#tb',           //引入id为tb的区块工具栏
            // singleSelect : true,      //只允许选择一行
            //编辑完保存执行
            onAfterEdit : function (rowIndex, rowData, changes) {       //在用户完成编辑一行的时候触发
                $('#baoc,#qxiao').hide();
                //添加数据和修改数据后台交互
                var inserted = $('#box').datagrid('getChanges', 'inserted');    //获取添加数据
                var updated = $('#box').datagrid('getChanges', 'updated');      //获取修改数据
                var url = '';
                var info = '';
                //新增用户
                if (inserted.length > 0) {
                    url = 'add.php';
                    info = '新增';
                }
                //修改用户
                if (updated.length > 0) {
                    url = 'update.php';
                    info = '修改';
                }
                $.ajax({
                    type : 'POST',
                    url : url,
                    data : {
                        row : rowData                       //将数据对象发送到服务器
                    },
                    beforeSend : function () {              //提交前触发
                        $('#box').datagrid('loading');      //显示载入状态
                    },
                    success : function (data) {             //提交后触发
                        if (data) {                         //data接收数据库响应条数
                            $('#box').datagrid('loaded');   //隐藏载入状态
                            $('#box').datagrid('load');     //刷新当前页面
                            $('#box').datagrid('unselectAll');  //取消所有行选择
                            $.messager.show({                   //成功后提示信息
                                title : '提示',
                                msg : data + '个用户被' + info + '成功！'
                            });
                            obj.panduan = undefined;            //将obj对象里的panduan设置为undefined
                        }
                    }
                });
            },
            //双击一行触发        第一步双击修改
            onDblClickRow: function (rowIndex, rowData) {
                if (obj.panduan != undefined){
                    $('#box').datagrid('endEdit', obj.panduan);     //结束编辑
                }
                if (obj.panduan == undefined) {
                    $('#baoc,#qxiao').show();                      //显示保存和取消按钮
                    $('#box').datagrid('beginEdit', rowIndex);     //获取双击的行索引开始编辑
                    obj.panduan = rowIndex;
                }
            }
        });
        //数据表格工具栏1
        $('#tianjia').linkbutton({  //将工具栏里的添加执行按钮方法
            iconCls: 'icon-add',     //设置图标
            plain: true              //按钮扁平化
        });
        $('#xiougai').linkbutton({  //将工具栏里的修改执行按钮方法
            iconCls: 'icon-edit',    //设置图标
            plain: true              //按钮扁平化
        });
        $('#shanchu').linkbutton({  //将工具栏里的删除执行按钮方法
            iconCls: 'icon-remove',  //设置图标
            plain: true              //按钮扁平化
        });
        $('#baoc').linkbutton({     //将工具栏里的保存执行按钮方法
            iconCls: 'icon-save',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        $('#qxiao').linkbutton({     //将工具栏里的取消执行按钮方法
            iconCls: 'icon-redo',    //设置图标
            plain: true              //按钮扁平化
        }).css('display', 'none');
        //数据表格工具栏2
        $('.shj1').datebox();   //查询日期输入框
        $('.shj2').datebox();   //查询日期输入框
        $('.chx').linkbutton({  //查询按钮
            iconCls: "icon-search"
        });
        //查询功能
        $('.chx').click(function () {       //点击查询后执行obj对象里的search方法
            obj.search();
        });
        //添加
        $('#tianjia').click(function () {   //点击添加按钮执行obj对象里的tianjia方法
            obj.tianjia();
        });
        //保存
        $('#baoc').click(function () {      //点击保存按钮执行obj对象里的baoc方法
            obj.baoc();
        });
        //取消
        $('#qxiao').click(function () {      //点击取消按钮执行obj对象里的qxiao方法
            obj.qxiao();
        });
        //修改
        $('#xiougai').click(function () {      //点击修改按钮执行obj对象里的xiougai方法
            obj.xiougai();
        });
        $('#shanchu').click(function () {      //点击删除按钮执行obj对象里的shanchu方法
            obj.shanchu();
        });
        var obj = {                     //obj对象
            panduan: undefined,
            //查询
            search: function () {
                if (this.panduan == undefined) {
                    $('#box').datagrid('load', {                         //执行数据表格的load方法提交数据
                        user: $.trim($('input[name="user"]').val()),   //获取查询用户
                        date_from: $('input[name="date_from"]').val(), //获取查询起始时间
                        date_to: $('input[name="date_to"]').val(),     //获取查询结束时间
                    });
                }
            },
            //添加
            tianjia: function () {
                $('#baoc,#qxiao').show();
                if (this.panduan == undefined) {
                    $('#box').datagrid('insertRow', {        //向数据表格插入一行
                        index: 0,                            //插入位置第0个索引，也就是第一条
                        row: {}
                    });
                    $('#box').datagrid('beginEdit', 0);     //开始编辑
                    this.panduan = 0;                    //调整为true防止重复添加
                }
            },
            //保存
            baoc: function () {
                $('#box').datagrid('endEdit', this.panduan);           //结束编辑
            },
            //取消
            qxiao: function () {
                $('#baoc,#qxiao').hide();                    //隐藏保存取消按钮
                this.panduan = undefined;
                $('#box').datagrid('rejectChanges');        //回 滚 所 有 从 创 建 或 上 一 次 调 用acceptChanges 函数后更改的数据。
            },
            //修改        第二步选择一行点击修改按钮修改
            xiougai:function () {
                var rows = $('#box').datagrid('getSelections');     //返回所有被选中的行数组对象，当没有记录被选中的时候将返回一个空数组。
                if (rows.length == 1) {
                    if (this.panduan != undefined) {
                        $('#box').datagrid('endEdit', this.panduan);     //结束编辑
                    }
                    if (this.panduan == undefined) {
                        var index = $('#box').datagrid('getRowIndex', rows[0]);     //获取到当前行的索引
                        $('#baoc,#qxiao').show();                                   //显示保存和取消按钮
                        $('#box').datagrid('beginEdit', index);                  //获取双击的行索引开始编辑
                        this.panduan = index;
                        $('#box').datagrid('unselectRow', index);                //取消指定选择的行
                    }
                }else {
                    $.messager.alert('警告', '请选择一行修改！', 'warning');
                }
            },
            //第四步       删除
            shanchu:function () {
                var rows = $('#box').datagrid('getSelections');     //返回所有被选中的行数组对象，当没有记录被选中的时候将返回一个空数组。
                if (rows.length > 0){
                    $.messager.confirm('确定操作', '您正在要删除所选的记录吗？', function (flag) {
                        if (flag) {             //如果用户点击了确定
                            var ids = [];
                            for (var i = 0; i < rows.length; i ++) {    //循环出数组对象
                                ids.push(rows[i].id);                   //将对象里的id添加到数组
                            }
                            //在这里可以将要删除的id发送到数据库
                            // alert(ids.join(','));
                            //删除后台交互
                            $.ajax({
                                type : 'POST',
                                url : 'delete.php',
                                data : {
                                    ids : ids.join(','),
                                },
                                beforeSend : function () {          //提交之前触发
                                    $('#box').datagrid('loading');  //显示载入状态
                                },
                                success : function (data) {         //提交之后触发，data接收数据库删除影响条数
                                    if (data) {
                                        $('#box').datagrid('loaded');           //隐藏载入状态
                                        $('#box').datagrid('load');             //刷新当前页
                                        $('#box').datagrid('unselectAll');      //取消所有选择行
                                        $.messager.show({                       //提示框
                                            title : '提示',
                                            msg : data + '个用户被删除成功！',    //提示删除信息
                                        });
                                    }
                                },
                            });
                        }
                    });
                }else {
                    $.messager.alert('提示', '请选择要删除的记录！', 'info');
                }
            }
        };
    });
[/code]





**十，其他功能**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414112225736-1908544551.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414112240923-1545405633.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414112253283-1694507738.png)

**DataGrid 属性**  
 **fitColumns   boolean 收缩列的大小，以适应网络的宽度，防止水平滚动。默认值为 false。设置表格自适应**



**frozenColumns   array同列属性，但是这些列将会被冻结在左侧。默认值为 undefined。冻结列要配合
**fitColumns使用，参数将要冻结的列写入 **frozenColumns属性******

[code]

    　　　　 fitColumns:  false,         //设置表格自适应
            frozenColumns:[[
                {
                    //第三步，设置id表格列
                    field : 'id',
                    title : '编号',
                    width : 100,
                    checkbox : true,    //将id列变成多选框
                },
                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true
                        }
                    }
                }
            ]],
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414120443783-109656343.png)





**DataGrid 列属性**  
 **formatter   function 单元格格式化函数，带三个参数：value,rowData,rowIndex。**

[code]

                {
                    field: 'user',      //field，对应远程JSON 数据里的对象属性，也就是数据库字段
                    title: '帐号',      //title，定义数据的标题
                    width: 100,
                    editor: {
                        type: 'validatebox',
                        options: {
                            required: true
                        }
                    },
                    formatter:function (value,rowData,rowIndex) {
                        return '('+value+')';
                    }
                },
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414121305001-939342780.png)





**DataGrid 事件**  
 **onHeaderContextMenu   e, field 在鼠标右击 DataGrid 表格头的时候触发。**

[code]

            pagination: true,         //组件底部显示分页工具栏
            pageNumber: 1,             //设置分页时初始化页码
            pageSize: 3,               //设置分页时设置每页多少条
            pageList: [3, 6, 9],          //设置可选每页显示条数
            fitColumns: true,         //设置表格自适应
            scrollbarSize: 0,          //滚动条所占的宽度或高度。默认为18。
            toolbar: '#tb',           //引入id为tb的区块工具栏
            onHeaderContextMenu:function (e, field) {       //在鼠标右击表格头的时候触发
                e.preventDefault();
                alert(field);          //接收列字段名称
            },
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414122257376-1523960952.png)



**onRowContextMenu   e,rowIndex,rowData在鼠标右击一行记录的时候触发。**

**html**

**右键菜单**



[code]

    <div id="menu" class="easyui-menu" style="width:120px;display:none;">
        <div onclick="" iconCls="icon-add">增加</div>
        <div onclick="" iconCls="icon-remove">删除</div>
        <div onclick="" iconCls="icon-edit">修改</div>
    </div>
[/code]



**js**





[code]

            pagination: true,         //组件底部显示分页工具栏
            pageNumber: 1,             //设置分页时初始化页码
            pageSize: 3,               //设置分页时设置每页多少条
            pageList: [3, 6, 9],          //设置可选每页显示条数
            fitColumns: true,         //设置表格自适应
            scrollbarSize: 0,          //滚动条所占的宽度或高度。默认为18。
            toolbar: '#tb',           //引入id为tb的区块工具栏
            onRowContextMenu: function (e, rowIndex, rowData) {       //在鼠标右击一行记录的时候触发
                e.preventDefault();
                $('#menu').menu('show', {   //显示菜单方法
                    left: e.pageX,
                    top: e.pageY,
                });
            },
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414123142423-1814269207.png)





**十一，剩下的方法和事件**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414191931205-460025747.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414191938611-393196174.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414191947189-591870826.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414192002501-1564285366.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414192011720-928892236.png)

**onLoadSuccess   data 在数据加载成功的时候触发。**

**onLoadError   none 在载入远程数据产生错误的时候触发。**

**onBeforeLoad   param在载入请求数据数据之前触发，如果返回false 可终止载入数据操作。**

**onClickRow   rowIndex,rowData在用户点击一行的时候触发，参数包括：rowIndex：点击的行的索引值，该索引值从 0
开始。rowData：对应于点击行的记录。**

**onDblClickRow   rowIndex,rowData在用户双击一行的时候触发，参数包括：rowIndex：点击的行的索引值，该索引值从 0
开始。rowData：对应于点击行的记录。**

**onClickCell   rowIndex,field,value在用户点击一个单元格的时候触发。**

**onDblClickCell   rowIndex,field,value在用户双击一个单元格的时候触发。**

**onSortColumn   sort,order在用户排序一列的时候触发，参数包括：sort：排序列字段名称。order：排序列的顺序(ASC 或
DESC)**

**onResizeColumn   field,width 在用户调整列大小的时候触发。**

**onSelect   rowIndex,rowData在用户选择一行的时候触发，参数包括：rowIndex：选择的行的索引值，索引从
0开始。rowData：对应于所选行的记录**

**onUnselect   rowIndex,rowData在用户取消选择一行的时候触发，参数包括：rowIndex：选择的行的索引值，索引从
0开始。rowData：对应于取消选择行的记录。**

**onSelectAll   rows 在用户选择所有行的时候触发。**

**onUnselectAll   rows 在用户取消选择所有行的时候触发。**

**onCheck   rowIndex,rowData在用户勾选一行的时候触发，参数包括：rowIndex：选中的行索引，索引从 0
开始。rowData：对应于所选行的记录。**

**onUncheck   rowIndex,rowData在用户取消勾选一行的时候触发，参数包括：rowIndex：选中的行索引，索引从 0
开始。rowData：对应于取消勾选行的记录。**

**onCheckAll   rows 在用户勾选所有行的时候触发。**

**onUncheckAll   rows 在用户取消勾选所有行的时候触发。**

**onBeforeEdit   rowIndex,rowData在用户开始编辑一行的时候触发，参数包括：rowIndex：编辑行的索引，索引从 0
开始。rowData：对应于编辑行的记录。**

**onAfterEdit
rowIndex,rowData,changes在用户完成编辑一行的时候触发，参数包括：rowIndex：编辑行的索引，索引从 0
开始。rowData：对应于完成编辑的行的记录。changes：更改后的字段(键)/值对。**

**onCancelEdit   rowIndex,rowData在用户取消编辑一行的时候触发，参数包括：rowIndex：编辑行的索引，索引从 0
开始。rowData：对应于编辑行的记录。**



[code]

            //部分事件
            onClickRow: function (rowIndex, rowData) {
                alert('单击一行时触发！');
            },
            onClickCell: function (rowIndex, field, value) {
                alert('单击一个单元格时触发！');
            },
            onUnselect: function (rowIndex, rowData) {
                alert('取消选定一行时触发！');
            },
            onCheck: function (rowIndex, rowData) {
                alert('勾选一行时触发！');
            },
            onCancelEdit: function (rowIndex, rowData) {
                alert('取消编辑一行时触发！');
            },
            onSortColumn: function (sort, order) {
                alert('排序时触发！')
            },
[/code]





**DataGrid 方法**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210213173-156276129.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210244408-1169459781.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210254001-374162068.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210304892-137708620.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210314642-2002980727.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210327033-2026217893.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210339751-885263675.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210349533-1772748430.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170414210358033-424975024.png)**

**options   none 返回属性对象。**

**getPager   none 返回页面对象。**

**getPanel   none 返回面板对象。**

**getColumnFields   frozen返回列字段。如果设置了 frozen 属性为true，将返回固定列的字段名。var opts
=$('#dg').datagrid('getColumnFields'); // 获取解冻列var opts
=$('#dg').datagrid('getColumnFields', true); // 获取冻结列**

**getColumnOption   field 返回指定列属性。**

**resize   param 做调整和布局。**

**load   param
加载和显示第一页的所有行。如果指定了'param'，它将取代'queryParams'属性。通常可以通过传递一些参数执行一次查询，通过调用这个方法从服务器加载新数据。**

**reload   param重载行。等同于'load'方法，但是它将保持在当前页。**

**reloadFooter   footer 重载页脚行。**

**loading   none 显示载入状态。**

**loaded   none 隐藏载入状态。**

**fitColumns   none使列自动展开/收缩到合适的 DataGrid宽度。**

**fixColumnSize   field 固定列大小。如果'field'参数未配置，所有列大小将都是固定的。**

**fixRowHeight   index 固定指定列高度。如果'index'参数未配置，所有行高度都是固定的。**

**freezeRow   index 冻结指定行，当 DataGrid 表格向下滚动的时候始终保持被冻结的行显示在顶部。**

**autoSizeColumn   field 自动调整列宽度以适应内容。**

**loadData   data 加载本地数据，旧的行将被移除。**

**getData   none 返回加载完毕后的数据。**

**getRows   none 返回当前页的所有行。**

**getFooterRows   none 返回页脚行。**

**getRowIndex   row返回指定行的索引号，该行的参数可以是一行记录或一个 ID 字段值。**

**getChecked   none 在复选框呗选中的时候返回所有行。**

**getSelected   none返回第一个被选中的行或如果没有选中的行则返回 null。**

**getSelections   none返回所有被选中的行，当没有记录被选中的时候将返回一个空数组。**

**clearSelections   none 清除所有选择的行。**

**clearChecked   none 清除所有勾选的行。**

**scrollTo   index 滚动到指定的行。**

**highlightRow   index 高亮一行。**

**selectAll   none 选择当前页中所有的行。**

**unselectAll   none 取消选择所有当前页中所有的行。**

**selectRow   index 选择一行，行索引从 0 开始。**

**selectRecord   idValue 通过 ID 值参数选择一行。**

**unselectRow   index 取消选择一行。**

**checkAll   none 勾选当前页中的所有行。**

**uncheckAll   none 取消勾选当前页中的所有行。**

**checkRow   index 勾选一行，行索引从 0 开始。**

**uncheckRow   index 取消勾选一行，行索引从 0 开始。**

**beginEdit   index 开始编辑行。**

**endEdit   index 结束编辑行。**

**cancelEdit   index 取消编辑行。**

**getEditors
index获取指定行的编辑器。每个编辑器都有以下属性：actions：编辑器可以执行的动作，同编辑器定义。target：目标编辑器的 jQuery
对象。**  
 **field：字段名称。type：编辑器类型，比如：'text','combobox','datebox'等。**

**getEditor   options获取指定编辑器，options 包含 2 个属性：index：行索引。field：字段名称。**

**refreshRow   index 刷新行。**

**validateRow   index 验证指定的行，当验证有效的时候返回true。**

**updateRow   param更新指定行，参数包含下列属性：index：执行更新操作的行索引。row：更新行的新数据。**

**appendRow   row追加一个新行。新行将被添加到最后的位置。**

**insertRow   param插入一个新行，参数包括一下属性：index：要插入的行索引，如果该索引值未定义，则追加新行。row：行数据。**

**deleteRow   index 删除行。**

**getChanges
type从上一次的提交获取改变的所有行。类型参数指明用哪些类型改变的行，可以使用的值有：inserted,deleted,updated等。当类型参数未配置的时候返回所有改变的行。**

**acceptChanges   none提交所有从加载或者上一次调用acceptChanges 函数后更改的数据。**

**rejectChanges   none回滚所有从创建或者上一次调用acceptChanges 函数后更改的数据。**

**mergeCells   options合并单元格，options
包含以下属性：index：行索引。field：字段名称。rowspan：合并的行数。colspan：合并的列数。**

**showColumn   field 显示指定的列。**

**hideColumn   field 隐藏指定的列。**



[code]

        //部分方法
        $('#box').datagrid('deleteRow', 0);
        $('#box').datagrid('checkAll');
        $('#box').datagrid('highlightRow', 0);
        $('#box').datagrid('mergeCells', {
            index: 0,
            field: 'user',
            rowspan: 2,
        });
        $('#box').datagrid('mergeCells', {
            index: 0,
            field: 'user',
            colspan: 2,
        });
[/code]





**目录**

**二．分页和排序**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095538236-26758007.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095546173-1309457197.png)**

****三.排序功能****



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095700751-1517799809.png)

**四、样式设置**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095837970-1947791047.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095850814-1102246166.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415095858220-1512438632.png)

**六，查询功能**

**DataGrid 属性，扩展自 Panel 面板**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100025564-1332184664.png)**

****七，新增功能****

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100212689-1834596779.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100221376-578980547.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100230798-249993708.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100238564-493366653.png)

**八，修改删除功能**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100400189-880827703.png)**



**九，添加，修改，删除，后台交互**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100454830-686633669.png)**

****十，其他功能****



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170415100603236-479885997.png)



**十一，剩下的方法和事件，见十一**



