---
layout: post
title: " 第二百二十八节，jQuery EasyUI，TreeGrid(树形表格)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，TreeGrid(树形表格)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423232247726-1094217643.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 TreeGrid(树形表格)组件的使用方法， 这个组件依赖于 DataGrid(数据表格)组件。**



**一．加载方式**

**建立一个 JSON 文件**

[code]

     [
      {
        "id": 1,
        "name": "系统管理",
        "date": "2015-05-10",
        "children": [
          {
            "id": 2,
            "name": "主机信息",
            "date": "2015-05-11"
          }
        ]
      },
      {
        "id": 3,
        "name": "会员管理",
        "date": "2015-05-10",
        "children": [
          {
            "id": 4,
            "name": "认证审核",
            "date": "2015-05-11"
          }
        ]
      }
    ]
[/code]

**class 加载方式**

[code]

     <table class="easyui-treegrid" style="width:380px;height:150px"
           data-options="url:'property.json',idField:'id',treeField:'name'">
        <thead>
        <tr>
            <th data-options="field:'name',width:180">菜单名称</th>
            <th data-options="field:'date',width:180">创建时间</th>
        </tr>
        </thead>
    </table>
[/code]



**JS 加载方式**

**treegrid()将一个table元素执行TreeGrid(树形表格)组件**

[code]

     <table id="box" style="width:380px;height:150px;"></table>
[/code]

[code]

    $(function () {
        $('#box').treegrid({
            url: 'property.json',
            idField: 'id',            //定义关键字段来标识树节点。也就是数据的id
            treeField: 'name',        //定义树形显示字段
            columns: [[                //定义表格头名称
                {
                    title: '菜单名称',
                    field: 'name',
                    width: 180,
                },
                {
                    title: '创建时间',
                    field: 'date',
                    width: 180,
                }
            ]],
        });
    });
[/code]



**二．属性列表**

**树形表格扩展自 datagrid(数据表格)，树形表格新增的属性如下：**

****方法和 DataGrid 一致，不在重复！略。****

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423225416679-1924231422.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423225423304-711527959.png)**

**idField   string 定义关键字段来标识树节点。（必须的）**



**treeField   string 定义树节点字段。（必须的）**



**animate   boolean 定义在节点展开或折叠的时候是否显示动画效果。**



**loader   function(param,success,error)定义以何种方式从远程服务器读取数据。返回false
可以忽略该动作。该函数具有一下参数：param：传递到远程服务器的参数对象。success(data)：当检索数据成功的时候调用的回调函数。error()：当检索数据失败的时候调用的回调函数。**



**loadFilter   function(data,parentId) 返回过滤后的数据进行展示。**

**方法和 DataGrid 一致，不在重复！略。  
**





**三．事件列表**

**树形表格的事件扩展自 datagrid(数据表格)，树形表格新增的时间如下：**

****  事件和 DataGrid 基本一致，代码演示忽略。****

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423225938163-1617930205.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423225949522-1535747628.png)

**onClickRow   row 在用户点击节点的时候触发。**



**onDblClickRow   row 在用户双击节点的时候触发。**



**onClickCell   field,row 在用户点击单元格的时候触发。**



**onDblClickCell   field,row 在用户双击单元格的时候触发。**



**onBeforeLoad   row, param在请求数据加载之前触发，返回 false可以取消加载动作。**



**onLoadSuccess   row, data 数据加载完成之后触发。**



**onLoadError   arguments数据加载失败的时候触发，参数和jQuery 的$.ajax()函数的'error'回调函数一样。**



**onBeforeExpand   row在节点展开之前触发，返回 false 可以取消展开节点的动作。**



**onExpand   row 在节点被展开的时候触发。**



**onBeforeCollapse   row在节点折叠之前触发，返回 false 可以取消折叠节点的动作。**



**onCollapse   row 在节点被折叠的时候触发。**



**onContextMenu   e, row 在右键点击节点的时候触发。**



**onBeforeEdit   row 在用户开始编辑节点的时候触发。**



**onAfterEdit   row,changes 在用户完成编辑的时候触发。**



**onCancelEdit   row 在用户取消编辑节点的时候触发。**



**  事件和 DataGrid 基本一致，代码演示忽略。**





**四．方法列表**

**很多方法都使用'id'命名参数，而'id'参数代表树节点的值。**

**方法和 DataGrid 一致，代码演示忽略。**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423230932163-858902126.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423230938757-2016191579.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423230945429-8798344.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423230952007-748455361.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423231024491-329319884.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170423231033116-1760662345.png)**

**options   none 返回树形表格的属性。**



**resize   options设置树形表格大小，options 包含 2 个属性：width：树形表格的新宽度。height：树形表格的新高度。**



**fixRowHeight   id 修正指定的行高。**



**load   param 读取并显示首页内容。**



**loadData   data 读取树形表格数据。**



**reload   id重新加载树形表格数据。如果'id'属性有值，将重新载入指定树形行，否则重新载入所有行。**



**reloadFooter   footer 重新载入页脚数据。**



**getData   none 获取载入数据。**



**getFooterRows   none 获取页脚数据。**



**getRoot   none 获取根节点，返回节点对象。**



**getRoots   none 获取所有根节点，返回节点数组。**



**getParent   id 获取父节点。**



**getChildren   id 获取子节点。**



**getSelected   none获取选择的节点并返回它，如果没有节点被选中则返回 null。**



**getSelections   none 获取所有选择的节点。**



**getLevel   id 获取指定节点等级。**



**find   id 查找指定节点并返回节点数据。**



**select   id 选择一个节点。**



**unselect   id 反选一个节点。**



**selectAll   none 选择所有节点。**



**unselectAll   none 反选所有节点。**



**collapse   id 折叠一个节点。**



**expand   id 展开一个节点。**



**collapseAll   id 折叠所有节点。**



**expandAll   id 展开所有节点。**



**expandTo   id 打开从根节点到指定节点之间的所有节点。**



**toggle   id 节点展开/折叠状态触发器。**



**append   param追加节点到一个父节点，'param'参数包含如下属性：parent：父节点
ID，如果未指定则追加到根节点。data：数组，节点数据。**



**insert   param插入一个新节点到指定节点。'param'参数包含一下参数：before：插入指定节点 ID 值之前。after：插入指定节点
ID 值之后。data：新节点数据。**



**remove   id 移除一个节点和他的所有子节点。**



**pop   id 弹出并返回节点数据以及它的子节点之后删除。**



**refresh   id 刷新指定节点。**



**update   param更新指定节点。'param'参数包含以下属性：id：要更新的节点的 ID。row：新的行数据。**



**beginEdit   id 开始编辑一个节点。**



**endEdit   id 结束编辑一个节点。**



**cancelEdit   id 取消编辑一个节点。**



**getEditors   id获取指定行编辑器。每个编辑器都包含以下属性：actions：编辑器执行的动作。target：目标编辑器的 jQuery
对象。field：字段名称。type：编辑器类型。**



**getEditor   param获取指定编辑器，'param'参数包含 2 个属性：id：行节点 ID。field：字段名称。**



**  方法和 DataGrid 一致，代码演示忽略。**

