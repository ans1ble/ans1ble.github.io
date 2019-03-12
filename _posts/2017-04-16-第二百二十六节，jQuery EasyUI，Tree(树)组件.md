---
layout: post
title: " 第二百二十六节，jQuery EasyUI，Tree(树)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Tree(树)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423121859288-1315071549.png)

**本节课重点了解 EasyUI 中 Tree(树)组件的使用方法， 这个组件依赖于 Draggable(拖 动)和 Droppable(放置)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <ul class="easyui-tree">
        <li>
            <span>系统管理</span>
            <ul>
                <li>
                    <span>主机信息</span>
                    <ul>
                        <li>版本信息</li>
                        <li>数据库信息</li>
                    </ul>
                </li>
                <li>更新信息</li>
                <li>程序信息</li>
            </ul>
        </li>
        <li>
            <span>会员管理</span>
            <ul>
                <li>新增会员</li>
                <li>审核会员</li>
            </ul>
        </li>
    </ul>
[/code]



**JS 加载方式**

**tree()将一个ul元素执行Tree(树)组件**

**树控件数据格式化： 注意：这些属性都是写在json远程数据里的**

**id ：节点 ID，对加载远程数据很重要。 **

**text：显示节点文本。(必选)**

**state ：节点状态，'open' 或 'closed'，默认：'open'。如果为'closed'的时候， 将不自动展开该节点。**

**checked ：表示该节点是否被选中。 **

**attributes : 被添加到节点的自定义属性。**

**children: 一个节点数组声明了若干节点。**



html

[code]

    <ul id="box"></ul>
[/code]

js

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
        });
    });
[/code]



**注意：这些属性都是写在 json远程数据里的**

**id ：节点 ID，对加载远程数据很重要。**

[code]

    [
      {
        "id": 1,
        "text": "系统管理",
        "iconCls": "icon-add"
      }
    ]
[/code]



**text ：显示节点文本。(必选)**

[code]

    [
      {
        "id": 1,
        "text": "系统管理",
        "iconCls": "icon-add"
      }
    ]
[/code]



**children : 一个节点数组声明了若干节点。**

[code]

    [
      {
        "id": 1,
        "text": "系统管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "主机信息",
            "children":[
              {
                "text" : "版本信息"
              },
              {
                "text" : "数据库信息"
              }
            ]
          },
          {
            "text": "更新信息"
          },
          {
            "text": "程序信息"
          }
        ]
      },
      {
        "id": 2,
        "text": "会员管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "新增会员"
          },
          {
            "text": "审核会员"
          }
        ]
      }
    ]
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416201650681-1307829968.png)

**state ：节点状态，'open' 或 'closed'，默认：'open'。如果为'closed'的时候， 将不自动展开该节点。**

[code]

    [
      {
        "id": 1,
        "text": "系统管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "主机信息",
            "state":"closed",
            "children":[
              {
                "text" : "版本信息"
              },
              {
                "text" : "数据库信息"
              }
            ]
          },
          {
            "text": "更新信息"
          },
          {
            "text": "程序信息"
          }
        ]
      },
      {
        "id": 2,
        "text": "会员管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "新增会员"
          },
          {
            "text": "审核会员"
          }
        ]
      }
    ]
[/code]



**checked ：表示该节点是否被选中。**



[code]

    [
      {
        "id": 1,
        "text": "系统管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "主机信息",
            "state":"closed",
            "children":[
              {
                "text" : "版本信息",
                "checked":true
              },
              {
                "text" : "数据库信息"
              }
            ]
          },
          {
            "text": "更新信息"
          },
          {
            "text": "程序信息"
          }
        ]
      },
      {
        "id": 2,
        "text": "会员管理",
        "iconCls": "icon-add",
        "children": [
          {
            "text": "新增会员"
          },
          {
            "text": "审核会员"
          }
        ]
      }
    ]
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417110024602-625818818.png)





**attributes : 被添加到节点的自定义属性。**

**以上属性都是写在 **json远程数据里的****





**二．属性列表**

**  属性表格的属性扩展自 Tree(数据表格)，属性表格新增的的属性如下：**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416232643743-1222587902.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416232650149-1999375182.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170416232656274-227935236.png)

**url   string 检索远程数据的 URL 地址。**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
        });
    });
[/code]



**method   string 检索数据的 HTTP 方法。（POST / GET）**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST'           //检索数据的 HTTP 方法
        });
    });
[/code]



**animate   boolean 定义节点在展开或折叠的时候是否显示动画效果。**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true            //定义节点在展开或折叠的时候是否显示动画效果
        });
    });
[/code]



**checkbox   boolean 定义是否在每一个借点之前都显示复选框。**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true            //定义是否在每一个借点之前都显示复选框
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417103111227-304430407.png)

**cascadeCheck   boolean 定义是否层叠选中状态。也就是选择时不关联上级目录**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            cascadeCheck:false      //定义是否层叠选中状态。也就是选择时不关联上级目录
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417103654790-304862669.png)

**onlyLeafCheck   boolean 定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            onlyLeafCheck:true,     //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417104146477-412201875.png)



**lines   boolean 定义是否显示树控件上的虚线。**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            onlyLeafCheck:true,     //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            lines:true              //定义是否显示树控件上的虚线。
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417104419587-1649424771.png)



**dnd   boolean 定义是否启用拖拽功能。也就是支持拖拽改变层级关系**

[code]

    $(function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            onlyLeafCheck:true,     //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            lines:true,              //定义是否显示树控件上的虚线。
            dnd:true                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
    });
[/code]



**data   array 节点数据加载。本地加载节点数据**

[code]

    $(function () {
        $('#box').tree({
            // url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            onlyLeafCheck:true,     //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            lines:true,              //定义是否显示树控件上的虚线。
            dnd:true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            data: [{                 //节点数据加载。本地加载节点数据
                "text": "本地数据",
                "children": [
                    {
                        "text": "子目录"
                    }
                ]
            }]
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417110917946-2126954654.png)



**formatter   function(node) 定义如何渲染节点的文本。格式化目录文本， **node返回节点对象****

[code]

    $( function () {
        $('#box').tree({
            url: 'content.json',    //远程加载数据
            method:'POST',           //检索数据的 HTTP 方法
            animate:true,            //定义节点在展开或折叠的时候是否显示动画效果
            checkbox:true,            //定义是否在每一个借点之前都显示复选框
            onlyLeafCheck:true,     //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            lines:true,              //定义是否显示树控件上的虚线。
            dnd:true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            formatter:function (node) {     //定义如何渲染节点的文本。格式化目录文本，node返回节点对象
                return '['+node.text+']';
            }
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170417111519306-790056416.png)



**loader   function(param,success,error)定义如何从远程服务器加载数据。返回false
可以忽略本操作。该函数具备以下参数：param：发送到远程服务器的参数对象。success(data)：当检索数据成功的时候调用的回调函数。error()：当检索数据失败的时候调用的回调函数。**



**loadFilter
function(data,parent)返回过滤过的数据进行展示。返回数据是标准树格式。该函数具备以下参数：data：加载的原始数据。parent:
DOM 对象，代表父节点。**





**三，异步加载， 也就是远程数据库动态加载目录**

**如果想从数据库里获取导航内容，那么就必须实现一张父类子类的无限极数据库分类表。主要字段 有**

**id(编号) 、自动编号，记录每一条目录的id号**

**text(名称) 、记录每一条目录的名称**

**state(状态) 、记录每一条目录是否有子目录，closed表示有子目录，open表示无子目录**

**tid(类别) 。记录每一条目录的父级目录id，也就是所属目录的id号，一级目录用0表示**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418082141477-1879043635.png)**



**第一步，显示所有一级目录**

**首次打开页面，时传递数据库tid为0，获取到所有tid为0的数据，也就是获取所有一级目录**

html

[code]

    <ul id="box"></ul>
[/code]

js

[code]

    $(function () {
        
        $('#box').tree({
            url : 'tree.php',    //远程加目录载数据
            lines : true,        //定义是否显示树控件上的虚线。
        });
    
    });
[/code]

tree.php

[code]

    <?php
        //sleep(3);
        require 'config.php';
        
        //$q = $_POST['q'] ? $_POST['q'] : '';
        
        $tid = 0;       //首次打开页面，时传递数据库tid为0，获取到所有tid为0的数据
        
    //    if (isset($_POST['id'])) {
    //        $tid = $_POST['id'];
    //    }
        
        $query = mysql_query("SELECT id,text,state FROM think_nav WHERE tid='$tid'") or die('SQL 错误！');
    
        
        $json = '';
        
        while (!!$row = mysql_fetch_array($query, MYSQL_ASSOC)) {
            $json .= json_encode($row).',';
        }
    
        $json = substr($json, 0, -1);
        echo '['.$json.']';
        //将获取到的数据转换为json格式
        //[{"id":"1","text":"\u7cfb\u7edf\u7ba1\u7406","state":"closed"},{"id":"2","text":"\u4f1a\u5458\u7ba1\u7406","state":"closed"},{"id":"3","text":"\u4e3b\u673a\u4fe1\u606f","state":"closed"}]
        mysql_close();
    ?>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418091150477-1104148982.png)



**  第二步，动态获取子目录**

**当用户点击父级目录是，会自动将父级目录的id传递到远程地址， 获取数据库tid为这个父级id的数据，也就是这个父级目录的子目录**

tree.php

[code]

    <?php
        //sleep(3);
        require 'config.php';
        
        //$q = $_POST['q'] ? $_POST['q'] : '';
        
        $tid = 0;       //首次打开页面，时传递数据库tid为0，获取到所有tid为0的数据
        
        if (isset($_POST['id'])) {          //判断如果，用户点击父级目录时有传递id
            $tid = $_POST['id'];            //将传递的id赋值给tid
        }
        
        $query = mysql_query("SELECT id,text,state FROM think_nav WHERE tid='$tid'") or die('SQL 错误！');
    
        
        $json = '';
        
        while (!!$row = mysql_fetch_array($query, MYSQL_ASSOC)) {
            $json .= json_encode($row).',';
        }
    
        $json = substr($json, 0, -1);
        echo '['.$json.']';
        //获取到tid为接收到的父亲id的数据转换为json格式
        //[{"id":"6","text":"\u66f4\u65b0\u4fe1\u606f","state":"open"},{"id":"7","text":"\u7a0b\u5e8f\u4fe1\u606f","state":"open"}]
        mysql_close();
    ?>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418094437852-627678155.png)

**注意：这个过程是动态获取子目录的**





**第三步，展开所有的目录**

html

[code]

    <ul id="box"></ul>
[/code]

js

[code]

    $(function () {
    
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            onLoadSuccess: function (node, data) {   //当加载完毕后执行
                //data接收返回的目录对象
                if (data) {        //判断返回的目录对象如果有值
                    $(data).each(function (index, value) {        //遍历所有的目录对象
                        if (this.state == 'closed') {            //判断如果目录对象里的state等于closed,说明此目录有子目录
                            $('#box').tree('expandAll');        //展开所有子目录
                        }
                    })
                }
            }
        });
    
    });
[/code]

tree.php

[code]

    <?php
        //sleep(3);
        require 'config.php';
        
        //$q = $_POST['q'] ? $_POST['q'] : '';
        
        $tid = 0;       //首次打开页面，时传递数据库tid为0，获取到所有tid为0的数据
        
        if (isset($_POST['id'])) {          //判断如果，用户点击父级目录时有传递id
            $tid = $_POST['id'];            //将传递的id赋值给tid
        }
        
        $query = mysql_query("SELECT id,text,state FROM think_nav WHERE tid='$tid'") or die('SQL 错误！');
    
        
        $json = '';
        
        while (!!$row = mysql_fetch_array($query, MYSQL_ASSOC)) {
            $json .= json_encode($row).',';
        }
    
        $json = substr($json, 0, -1);
        echo '['.$json.']';
        //获取到tid为接收到的父亲id的数据转换为json格式
        mysql_close();
    ?>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418103553274-238752965.png)



**四，事件列表**

**很多事件的回调函数都包含 'node'参数对象，其具备如下属性：**

**id：绑定节点的标识值。**

**text：显示的节点文本。**

**iconCls：显示的节点图标 CSS 类 ID。**

**checked：该节点是否被选中。**

**state：节点状态，'open' 或 'closed'。**

**attributes：绑定该节点的自定义属性。**

**target：目标 DOM 对象。**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110745290-1973006754.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110803884-791461664.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110811446-1423954213.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110822352-2026007232.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110835806-601087564.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170418110845102-354718636.png)**

**onClick   node 在用户点击一个节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick:function (node) {                    //点击目录后触发
                $.each(node, function (attr, value){    //遍历出目录对象
                    alert(attr + '：' + value);            //打印出对象里的数据
                });
            }
        });
    });
[/code]



**onDblClick   node 在用户双击一个节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDblClick:function (node) {                //双击目录后触发
                $.each(node, function (attr, value){    //遍历出目录对象
                    alert(attr + '：' + value);            //打印出对象里的数据
                });
            }
        });
    });
[/code]



**onBeforeLoad   node,param在请求加载远程数据之前触发，返回false 可以取消加载操作。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeLoad:function (node,param) {        //在请求加载远程数据之前触发，返回false 可以取消加载操作。
                alert(node);    //接收的目录信息对象
                alert(param);    //接收的目录id对象
                // return false;
            }
        });
    });
[/code]



**onLoadSuccess   node, data 在数据加载成功以后触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onLoadSuccess:function (node, data) {        //在数据加载成功以后触发
                alert(node);    //接收的当前目录信息对象
                alert(data);    //接收的所有目录信息对象
            }
        });
    });
[/code]



**onLoadError   arguments在数据加载失败的时候触发，arguments参数和 jQuery
的$.ajax()函数里面的'error'回调函数的参数相同。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree1.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onLoadError:function (arguments) {        //在数据加载失败的时候触发
                // alert(arguments);    //接收错误信息对象
                // $.each(arguments, function (attr, value){
                //     alert(attr+value)
                // });
                alert(arguments.status);  //打印错误信息代码
            }
        });
    });
[/code]



**onBeforeExpand   node 在节点展开之前触发，返回 false 可以取消展开操作。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeExpand:function (node) {        //在节点展开之前触发，返回 false 可以取消展开操作
                alert(node);    //接收展开目录信息对象
                // return false;
            }
        });
    });
[/code]



**onExpand   node 在节点展开的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onExpand:function (node) {        //在节点展开的时候触发
                alert(node);    //接收展开目录信息对象
                // return false;
            }
        });
    });
[/code]



**onBeforeCollapse   node 在节点折叠之前触发，返回 false 可以取消折叠操作。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeCollapse:function (node) {        //在节点折叠之前触发，返回 false 可以取消折叠操作
                alert(node);    //接收折叠目录信息对象
                // return false;
            }
        });
    });
[/code]



**onCollapse   node 在节点折叠的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onCollapse:function (node) {        //在节点折叠的时候触发
                alert(node);    //接收折叠目录信息对象
            }
        });
    });
[/code]



**onBeforeCheck   node,checked在用户点击勾选复选框之前触发，返回false 可以取消选择动作。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeCheck:function (node,checked) {        //在用户点击勾选复选框之前触发，返回false 可以取消选择动作
                alert(node);    //接收勾选目录信息对象
                alert(checked); //接收勾选状态，布尔值
            }
        });
    });
[/code]



**onCheck   node,checked 在用户点击勾选复选框的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onCheck:function (node,checked) {        //在用户点击勾选复选框的时候触发
                alert(node);    //接收勾选目录信息对象
                alert(checked); //接收勾选状态，布尔值
            }
        });
    });
[/code]



**onBeforeSelect   node 在用户选择一个节点之前触发，返回false 可以取消选择动作。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeSelect:function (node) {        //在用户选择一个节点之前触发，返回false 可以取消选择动作。
                alert(node);    //接收选择目录信息对象
            }
        });
    });
[/code]



**onSelect   node 在用户选择节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onSelect:function (node) {        //在用户选择节点的时候触发
                alert(node);    //接收选择目录信息对象
            }
        });
    });
[/code]



**onContextMenu   e, node 在右键点击节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onContextMenu:function (node) {        //在右键点击节点的时候触发
                alert(node);    //接收点击目录信息对象
                //可以制作右击弹出菜单
            }
        });
    });
[/code]



**onBeforeDrag   node 在开始拖动节点之前触发，返回 false 可以拒绝拖动。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeDrag:function (node) {        //在开始拖动节点之前触发，返回 false 可以拒绝拖动
                alert(node);    //接收拖动目录信息对象
            }
        });
    });
[/code]



**onStartDrag   node 在开始拖动节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onStartDrag:function (node) {        //在开始拖动节点的时候触发
                alert(node);    //接收拖动目录信息对象
            }
        });
    });
[/code]



**onStopDrag   node 在停止拖动节点的时候触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onStopDrag:function (node) {        //在停止拖动节点的时候触发
                alert(node);    //接收拖动目录信息对象
            }
        });
    });
[/code]



**onDragEnter   target,source在拖动一个节点进入到某个目标节点并释放的时候触发，返回 false
可以拒绝拖动。target：释放的目标节点元素。source：开始拖动的源节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDragEnter:function (target,source) {        //在拖动一个节点进入到某个目标节点并释放的时候触发，返回 false 可以拒绝拖动
                alert(target);    //target：释放的目标节点元素
                alert(source);    //source：开始拖动的源节点对象
            }
        });
    });
[/code]



**onDragOver   target,source在拖动一个节点经过某个目标节点并释放的时候触发，返回 false
可以拒绝拖动。target：释放的目标节点元素。source：开始拖动的源节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDragOver:function (target,source) {        //在拖动一个节点经过某个目标节点并释放的时候触发，返回 false 可以拒绝拖动
                alert(target);    //target：释放的目标节点元素
                alert(source);    //source：开始拖动的源节点对象
            }
        });
    });
[/code]



**onDragLeave   target,source在拖动一个节点离开某个目标节点并释放的时候触发，返回 false
可以拒绝拖动。target：释放的目标节点元素。source：开始拖动的源节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDragLeave:function (target,source) {        //在拖动一个节点离开某个目标节点并释放的时候触发，返回 false 可以拒绝拖动
                alert(target);    //target：释放的目标节点元素
                alert(source);    //source：开始拖动的源节点对象
            }
        });
    });
[/code]



**onBeforeDrop   target,source,point在拖动一个节点放置之前触发，返回 false
可以拒绝拖动。target：释放的目标节点元素。source：开始拖动的源节点。point：表示哪一种拖动操作，可用值有：'append','top' 或
'bottom'。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onBeforeDrop:function (target,source,point) {        //在拖动一个节点放置之前触发，返回 false 可以拒绝拖动
                alert(target);    //target：释放的目标节点元素
                alert(source);    //source：开始拖动的源节点对象
                alert(point);    //point：表示哪一种拖动操作，可用值有：'append','top' 或 'bottom'。
            }
        });
    });
[/code]



**onDrop   target,source,point当节点位置被拖动放置时触发。target：DOM
对象，需要被拖动动的目标节点。source：源节点。point：表示哪一种拖动操作，可用值有：'append','top' 或 'bottom'。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDrop:function (target,source,point) {        //当节点位置被拖动放置时触发
                alert(target);    //target：释放的目标节点元素
                alert(source);    //source：开始拖动的源节点对象
                alert(point);    //point：表示哪一种拖动操作，可用值有：'append','top' 或 'bottom'。
            }
        });
    });
[/code]



**onBeforeEdit   node 在编辑节点之前触发。**



**onAfterEdit   node 在编辑节点之后触发。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd: true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDblClick: function (node) {                    //双击一个节点时
                $('#box').tree('beginEdit', node.target);    //开始编辑一个节点
            },
            onAfterEdit: function (node) {                        //在编辑节点之后触发
                alert('执行服务器端');
                alert(node);
            }
        });
    });
[/code]



**onCancelEdit   node 在取消编辑操作的时候触发**。





**五，方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170420124750056-438534068.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170420124801977-890929308.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170420124807477-1515099253.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170420124816493-1020932573.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170420124822196-632830230.png)

**options   none 返回树控件属性。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
        alert($('#box').tree('options'));        //返回树控件属性
    });
[/code]



**loadData   data 读取树控件数据。也就是读取一个本地数据替换原来的数据**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
    
        //点击一个按钮
        $('#anl').click(function () {
            $('#box').tree('loadData', [
                {
                    text: '加载'
                }
            ]);
        });
    });
[/code]



**getNode   target 获取指定节点对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick : function (node) {
                alert($('#box').tree('getNode', node.target)); //获取指定节点对象
            }
        });
    });
[/code]



**getData   target 获取指定节点数据，包含它的子节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick : function (node) {
                alert($('#box').tree('getData', node.target)); //获取指定节点数据，包含它的子节点。
            }
        });
    });
[/code]



**reload   target 重新载入树控件数据。也就是重新加载一下数据相当于刷新**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
        //点击一个按钮
        $('#anl').click(function () {
            $('#box').tree('reload');    //重新载入树控件数据。也就是重新加载一下数据相当于刷新
        });
    });
[/code]



**getRoot   none 获取根节点，返回节点对象。也就是获取一级目录**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
        //点击一个按钮
        $('#anl').click(function () {
            alert($('#box').tree('getRoot'));    //获取根节点，返回节点对象。
        });
    });
[/code]



**getRoots   none 获取所有根节点，返回节点数组。也就是获取所有一级目录**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
        });
        //点击一个按钮
        $('#anl').click(function () {
            alert($('#box').tree('getRoots'));    //获取所有根节点，返回节点数组。也就是获取所有一级目录
        });
    });
[/code]



**getParent   target 获取父节点，'target'参数代表节点的 DOM对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick : function (node) {
                alert($('#box').tree('getParent', node.target)); //获取父节点，'target'参数代表节点的 DOM对象。
            }
        });
        //点击一个按钮
        // $('#anl').click(function () {
         //    alert($('#box').tree('getRoots'));    //获取所有根节点，返回节点数组。也就是获取所有一级目录
        // });
    });
[/code]



**getChildren   target 获取所有子节点，'target'参数代表节点的DOM 对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick : function (node) {
                alert($('#box').tree('getChildren', node.target));     //获取所有子节点，'target'参数代表节点的DOM 对象
            }
        });
        //点击一个按钮
        // $('#anl').click(function () {
         //    alert($('#box').tree('getRoots'));    //获取所有根节点，返回节点数组。也就是获取所有一级目录
        // });
    });
[/code]



**getChecked
state获取所有选中的节点。'state'可用值有：'checked获取勾选的','unchecked获取没勾选的','indeterminate获取未知状态的'。如果'state'第二个参数未指定，将返回'checked'节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('getChildren', node.target));     //获取所有子节点，'target'参数代表节点的DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            alert($('#box').tree('getChecked','unchecked'));    //获取勾选或者未勾选的节点对象
        });
    });
[/code]



**getSelected   none获取选择节点并返回它，如果未选择则返回null。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('getChildren', node.target));     //获取所有子节点，'target'参数代表节点的DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            alert($('#box').tree('getSelected'));    //获取选择节点并返回它，如果未选择则返回null
        });
    });
[/code]



**isLeaf   target 判断指定的节点是否是叶子节点，target 参数是一个节点 DOM 对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onClick : function (node) {
                alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            }
        });
        //点击一个按钮
        // $('#anl').click(function () {
         //    alert($('#box').tree('getSelected'));    //获取选择节点并返回它，如果未选择则返回null
        // });
    });
[/code]



**find   id 查找指定节点并返回节点对象。通过id查找指定节点**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('select',node.target);    //选择一个节点，'target'参数表示节点的 DOM对象
        });
    });
[/code]



**select   target 选择一个节点，'target'参数表示节点的 DOM对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('select',node.target);    //选择一个节点，'target'参数表示节点的 DOM对象
        });
    });
[/code]



**check   target 选中指定节点。勾选一个节点**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',7);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('check',node.target);    //选中指定节点。勾选一个节点
        });
    });
[/code]



**uncheck   target 取消选中指定节点。取消勾选一个节点**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',7);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('uncheck',node.target);    //取消选中指定节点。取消勾选一个节点
        });
    });
[/code]



**collapse   target 折叠一个节点，'target'参数表示节点的 DOM对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('collapse',node.target);    //折叠一个节点
        });
    });
[/code]





**expand   target展开一个节点，'target'参数表示节点的 DOM对象。在节点关闭或没有子节点的时候，节点ID
的值(名为'id'的参数)将会发送给服务器请求子节点的数据。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('expand',node.target);    //展开一个节点，'target'参数表示节点的 DOM对象。在节点关闭或没有子节点的时候，节点ID 的值(名为'id'的参数)将会发送给服务器请求子节点的数据。
        });
    });
[/code]



**collapseAll   target 折叠所有节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            // var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('collapseAll');    //折叠所有节点。
        });
    });
[/code]



**expandAll   target 展开所有节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            // var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('expandAll');    //展开所有节点。
        });
    });
[/code]



**expandTo   target 打开从根节点到指定节点之间的所有节点。**



**scrollTo   target 滚动到指定节点。**



**append   param追加若干子节点到一个父节点，param 参数有2 个属性：parent：DOM
对象，将要被追加子节点的父节点，如果未指定，子节点将被追加至根节点。data：数组，节点数据。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('isLeaf', node.target));     //判断指定的节点是否是叶子节点
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('append',{        //追加若干子节点到一个父节点，param 参数有2 个属性：parent：DOM 对象，将要被追加子节点的父节点，如果未指定，子节点将被追加至根节点。data：数组，节点数据。
                parent:node.target,            //要插入的父节点
                data:[{                        //要插入的节点
                    text:'添加节点1'
                }]
            });
        });
    });
[/code]



**toggle   target 打开或关闭节点的触发器，也就是展开关闭来回切换器，target 参数是一个节点 DOM 对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',1);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('toggle',node.target);    //打开或关闭节点的触发器，也就是展开关闭来回切换器，target 参数是一个节点 DOM 对象。
        });
    });
[/code]



**insert   param在一个指定节点之前或之后插入节点，'param'参数包含如下属性：before：DOM
对象，在某个节点之前插入。after：DOM 对象，在某个节点之后插入。data：对象，节点数据。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('insert',{                //在一个指定节点之前或之后插入节点
                before:node.target,
                data:[
                    {
                        text:'插入节点'
                    }
                ]
            });
        });
    });
[/code]



**remove   target 移除一个节点和它的子节点，'target'参数是该节点的 DOM 对象。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('remove',node.target);    //移除一个节点和它的子节点
        });
    });
[/code]



**pop   target移除一个节点和它的子节点，该方法跟remove 方法一样，不同的是它将返回被移除的节点数据。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            alert($('#box').tree('pop',node.target));    //移除一个节点和它的子节点，该方法跟remove 方法一样，不同的是它将返回被移除的节点数据。
        });
    });
[/code]



**update   param修改指定节点。'param'参数包含以下属性：target(DOM
对象，将被更新的目标节点)，id，text，iconCls，checked 等。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('update',{
                target:node.target,                    //要修改的目标
                text:'修改'                            //修改名称
            });
        });
    });
[/code]



**enableDnd   none 启用拖拽功能。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            // var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('enableDnd');            //启用拖拽功能
        });
    });
[/code]



**disableDnd   none 禁用拖拽功能。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd : true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            // onClick : function (node) {
            //     alert($('#box').tree('toggle', node.target));     //打开或关闭节点的触发器，target 参数是一个节点 DOM 对象
            // }
        });
        //点击一个按钮
        $('#anl').click(function () {
            // var node = $('#box').tree('find',2);    //查找指定节点并返回节点对象。通过id查找指定节点
            $('#box').tree('disableDnd');            //禁用拖拽功能
        });
    });
[/code]



**beginEdit   target 开始编辑一个节点。**

[code]

    $(function () {
        $('#box').tree({
            url: 'tree.php',    //远程加目录载数据
            lines: true,        //定义是否显示树控件上的虚线。
            animate : true,        //在展开或者折叠时显示动画效果
            checkbox : true,    //定义节点显示复选框
            cascadeCheck : false,    //定义是否层叠选中状态。也就是选择时不关联上级目录
            onlyLeafCheck : true,    //定义是否只在末级节点之前显示复选框。也就是只有最底层目录才显示复选框
            dnd: true,                //定义是否启用拖拽功能。也就是支持拖拽改变层级关系
            onDblClick: function (node) {                    //双击一个节点时
                $('#box').tree('beginEdit', node.target);    //开始编辑一个节点
            },
            onAfterEdit: function (node) {                        //在编辑节点之后触发
                alert('执行服务器端');
                alert(node);
            }
        });
    });
[/code]



**endEdit   target 结束编辑一个节点。**



**cancelEdit   target 取消编辑一个节点。**

