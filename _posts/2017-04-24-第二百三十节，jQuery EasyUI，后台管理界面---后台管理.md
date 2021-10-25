---
layout: post
title: " 第二百三十节，jQuery EasyUI，后台管理界面---后台管理 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，后台管理界面---后台管理**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424150555897-1869038083.png)**





**一，admin.php，后台管理界面**

[code]

    <? php
        session_start();
        if (!isset($_SESSION['admin'])) {     //判断用户登录成功时创建的SESSION是否存在
            header('location:login.php');     //如果不存在，跳转到登录页面
        }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
    <title>jQuery Easy UI</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="easyui/themes/default/easyui.css" />
    <link rel="stylesheet" type="text/css" href="easyui/themes/icon.css" />
    <link rel="stylesheet" type="text/css" href="css/admin.css" />
    </head>
    <body class="easyui-layout">
    
    <div data-options="region:'north',title:'header',split:true,noheader:true" style="height:60px;background:#666;">
        <div class="logo">后台管理</div>
        <div class="logout">您好，<?php echo $_SESSION['admin']?> | <a href="logout.php">退出</a></div>
    </div>   
    <div data-options="region:'south',title:'footer',split:true,noheader:true" style="height:35px;line-height:30px;text-align:center;">
        &copy;2009-2015 瓢城 Web 俱乐部. Powered by PHP and EasyUI.
    </div>    
    <div data-options="region:'west',title:'导航',split:true,iconCls:'icon-world'" style="width:180px;padding:10px;">
        <ul id="nav"></ul>
    </div>   
    <div data-options="region:'center'" style="overflow:hidden;">
        <div id="tabs">
            <div title="起始页" iconCls="icon-house" style="padding:0 10px;display:block;">
                欢迎来到后台管理系统！
            </div>
        </div>
    </div> 
    
    
    <script type="text/javascript" src="easyui/jquery.min.js"></script>
    <script type="text/javascript" src="easyui/jquery.easyui.min.js"></script>
    <script type="text/javascript" src="easyui/locale/easyui-lang-zh_CN.js" ></script>
    <script type="text/javascript" src="js/admin.js"></script>
    </body>
    </html>
[/code]



**二，logout.php点击退出**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424151113225-317401748.png)**

[code]

    <? php
        session_start();
        session_destroy();                  //清除创建的session
        header('location:login.php');       //跳转到登录页面
    ?>
[/code]



**三，admin.js加载导航**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424161245256-201922817.png)**

**数据库表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424160851584-1606715514.png)**





**admin.js**

[code]

    $( function () {
        
        $('#nav').tree({                                            //将导航元素执行树形结构方法
            url : 'nav.php',                                        //远程加载树形结构数据
            lines : true,                                            //显示结构虚线
            onLoadSuccess : function (node, data) {                    //在数据加载成功后触发
                if (data) {                                            //data接收的所有目录信息对象，判断目录节点是否存在
                    $(data).each(function (index, value) {            //遍历所有目录
                        if (this.state == 'closed') {                //判断如果目录对象里的state等于closed,说明此目录有子目录
                            $('#nav').tree('expandAll');            //展开所有节点
                        }
                    });
                }
            },
            onClick : function (node) {                                //当用户点击一个目录时
                if (node.url) {                                        //判断当前对象的url是否存在，也就是在数据库里的url连接地址
                    if ($('#tabs').tabs('exists', node.text)) {        //判断当前目录名称的选项卡是否打开
                        $('#tabs').tabs('select', node.text);        //如果打开的则选择在当前选项卡上
                    } else {                                        //如果当然选项卡没有打开
                        $('#tabs').tabs('add', {                    //添加一个新选项卡面板
                            title : node.text,                        //标题为当前目录的名称
                            iconCls : node.iconCls,                    //图标为当前目录的图标
                            closable : true,                        //显示关闭按钮
                            href : node.url + '.php',                //读取远程数据并显示到面板
                        });
                    }
                }
            }
        });
        
        $('#tabs').tabs({            //将布局的id为tabs，也就是内容区块执行选项卡组件
            fit : true,                //铺满容器，
            border : false,            //不显示选项卡容器边框
        });
        
    });
[/code]

**nav.php，导航数据页**

[code]

    <? php
        require 'config.php';
        
        $id = isset($_POST['id']) ? $_POST['id'] : 0;       //判断是否有传递id,如果有id值为id,如果没有id值为0
        //将$id值到数据库去查找nid字段
        $query = mysql_query("SELECT id,text,state,iconCls,url FROM easyui_nav WHERE nid='$id'") or die('SQL 错误！');
    
        
        $json = '';
        
        while (!!$row = mysql_fetch_array($query, MYSQL_ASSOC)) {
            $json .= json_encode($row).',';
        }
    
        $json = substr($json, 0, -1);
        echo '['.$json.']';
        mysql_close();
    ?>
[/code]



**四，点击对应的导航，远程对应的页面获取数据库信息显示到对应的选项卡**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170426180629631-843218735.png)**



**导航js**

[code]

    $( function () {
        
        $('#nav').tree({                                            //将导航元素执行树形结构方法
            url : 'nav.php',                                        //远程加载树形结构数据
            lines : true,                                            //显示结构虚线
            onLoadSuccess : function (node, data) {                    //在数据加载成功后触发
                if (data) {                                            //data接收的所有目录信息对象，判断目录节点是否存在
                    $(data).each(function (index, value) {            //遍历所有目录
                        if (this.state == 'closed') {                //判断如果目录对象里的state等于closed,说明此目录有子目录
                            $('#nav').tree('expandAll');            //展开所有节点
                        }
                    });
                }
            },
            onClick : function (node) {                                //当用户点击一个目录时
                if (node.url) {                                        //判断当前对象的url是否存在，也就是在数据库里的url连接地址
                    if ($('#tabs').tabs('exists', node.text)) {        //判断当前目录名称的选项卡是否打开
                        $('#tabs').tabs('select', node.text);        //如果打开的则选择在当前选项卡上
                    } else {                                        //如果当然选项卡没有打开
                        $('#tabs').tabs('add', {                    //添加一个新选项卡面板
                            title : node.text,                        //标题为当前目录的名称
                            iconCls : node.iconCls,                    //图标为当前目录的图标
                            closable : true,                        //显示关闭按钮
                            href : node.url + '.php',                //读取远程数据并显示到面板
                        });
                    }
                }
            }
        });
        
        $('#tabs').tabs({            //将布局的id为tabs，也就是内容区块执行选项卡组件
            fit : true,                //铺满容器，
            border : false,            //不显示选项卡容器边框
        });
        
    });
[/code]



**  选项卡操作**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170426181237787-1271533367.png)

**HTML**

[code]

     <?php
        session_start();
        if (!isset($_SESSION['admin'])) {
            header('location:login.php');
        }
    ?>
    
    <table id="manager"></table>
    
    <div id="manager_tool" style="padding:5px;">
        <div style="margin-bottom:5px;">
            <a href="#" class="easyui-linkbutton" iconCls="icon-add-new" plain="true" onclick="manager_tool.add();">添加</a>
            <a href="#" class="easyui-linkbutton" iconCls="icon-edit-new" plain="true" onclick="manager_tool.edit();">修改</a>
            <a href="#" class="easyui-linkbutton" iconCls="icon-delete-new" plain="true" onclick="manager_tool.remove();">删除</a>
            <a href="#" class="easyui-linkbutton" iconCls="icon-reload" plain="true"  onclick="manager_tool.reload();">刷新</a>
            <a href="#" class="easyui-linkbutton" iconCls="icon-redo" plain="true" onclick="manager_tool.redo();">取消选择</a>        
        </div>
        <div style="padding:0 0 0 7px;color:#333;">
            查询帐号：<input type="text" class="textbox" name="user" style="width:110px">
            创建时间从：<input type="text" name="date_from" class="easyui-datebox" editable="false" style="width:110px">
            到：<input type="text" name="date_to" class="easyui-datebox" editable="false" style="width:110px">
            <a href="#" class="easyui-linkbutton" iconCls="icon-search" onclick="obj.search();">查询</a>
        </div>
    </div>
    
    
    <form id="manager_add" style="margin:0;padding:5px 0 0 25px;color:#333;">
        <p>管理帐号：<input type="text" name="manager" class="textbox" style="width:200px;"></p>
        <p>管理密码：<input type="password" name="password" class="textbox" style="width:200px;"></p>
        <p>分配权限：<input id="auth" class="textbox" name="auth" style="width:205px;"></p>
    </form>
    
    
    <form id="manager_edit" style="margin:0;padding:5px 0 0 25px;color:#333;">
        <input type="hidden" name="id" class="textbox" style="width:200px;">
        <p>管理帐号：<input type="text" name="manager_edit" disabled="true" class="textbox" style="width:200px;"></p>
        <p>管理密码：<input type="password" name="password_edit" class="textbox" style="width:200px;"></p>
        <p>分配权限：<input id="auth_edit" class="textbox" name="auth_edit" style="width:205px;"></p>
    </form>
    
    
    
    <script type="text/javascript" src="js/manager.js"></script>
[/code]

**js**

[code]

    $( function () {
        
        $('#manager').datagrid({                            //执行数据表格组件
            url : 'manager_data.php',                        //获取远程数据
            fit : true,                                        //面板大小自适应父容器
            fitColumns : true,                                //表格自适应面板
            striped : true,                                    //是否显示斑马效果
            rownumbers : true,                                //显示行号
            border : false,                                    //是否显示边框
            pagination : true,                                //是否显示分页
            pageSize : 20,                                    //每页显示多少条数据
            pageList : [10, 20, 30, 40, 50],                //可选每页显示多少条数据
            pageNumber : 1,                                    //起始页
            sortName : 'date',                                //默认以什么字段排序
            sortOrder : 'desc',                                //排序方式
            toolbar : '#manager_tool',                        //加载增删改查工具栏区块
            columns : [[                                    //表格数据
                {
                    field : 'id',                            //数据库id字段
                    title : '自动编号',                        //标题
                    width : 100,
                    checkbox : true,                        //自动编号
                },
                {
                    field : 'manager',                        //数据库管理员字段
                    title : '管理员帐号',
                    width : 100,
                },
                {
                    field : 'auth',                            //数据库权限字段
                    title : '拥有权限',
                    width : 100,
                },
                {
                    field : 'date',                            //数据库日期字段
                    title : '创建日期',
                    width : 100,
                },
            ]],
        });
    
        //新增
        $('#manager_add').dialog({                                                    //执行对话框组件
            width : 350,
            title : '新增管理',
            modal : true,                                                            //遮罩
            closed : true,                                                            //可以关闭窗口
            iconCls : 'icon-user-add',                                                //图标
            buttons : [{                                                            //创建按钮
                text : '提交',                                                        //提交按钮
                iconCls : 'icon-add-new',                                            //图标
                handler : function () {                                                //点击提交按钮后触发
                    if ($('#manager_add').form('validate')) {                        //判断验证表单是否全部合法
                        $.ajax({                                                    //执行ajax提交
                            url : 'addManager.php',
                            type : 'post',
                            data : {                                                //提交数据
                                manager : $('input[name="manager"]').val(),            //获取用户名值
                                password : $('input[name="password"]').val(),        //获取密码值
                                auth : $('#auth').combotree('getText'),                //权限文本
                            },
                            beforeSend : function () {                                //提交时
                                $.messager.progress({                                //进度条信息框
                                    text : '正在新增中...',
                                });
                            },
                            success : function (data, response, status) {            //提交成功后
                                $.messager.progress('close');                        //关闭进度条信息框
                                
                                if (data > 0) {                                        //判断返回添加成功
                                    $.messager.show({                                //消息框
                                        title : '提示',
                                        msg : '新增管理成功',
                                    });
                                    $('#manager_add').dialog('close').form('reset');                        //关闭对话框，重置表单
                                    $('#manager').datagrid('reload');                                        //重新加载树形表格数据
                                } else {
                                    $.messager.alert('新增失败！', '未知错误导致失败，请重试！', 'warning');    //添加失败提示信息
                                }
                            }
                        });
                    }
                },
            },{
                text : '取消',                                                                                //取消按钮
                iconCls : 'icon-redo',
                handler : function () {                                                                        //点击取消按钮后执行函数
                    $('#manager_add').dialog('close').form('reset');                                        //关闭对话框，重置表单
                },
            }],
        });
    
        //修改
        $('#manager_edit').dialog({                                                            //修改对话框
            width : 350,
            title : '修改管理',
            modal : true,                                                                    //遮罩锁屏
            closed : true,                                                                    //可以关闭窗口
            iconCls : 'icon-user-add',                                                        //图标
            buttons : [{                                                                    //设置提交按钮
                text : '提交',
                iconCls : 'icon-edit-new',                                                    //按钮图标
                handler : function () {                                                        //点击提交后执行函数
                    if ($('#manager_edit').form('validate')) {                                //判断表单的数据是否合法
                        $.ajax({                                                            //ajax提交数据
                            url : 'updateManager.php',
                            type : 'post',
                            data : {                                                        //提交数据
                                id : $('input[name="id"]').val(),                            //获取用户名
                                password : $('input[name="password_edit"]').val(),            //获取密码
                                auth : $('#auth_edit').combotree('getText'),                //获取权限文本
                            },
                            beforeSend : function () {                                        //提交时
                                $.messager.progress({                                        //进度条信息框
                                    text : '正在修改中...',
                                });
                            },
                            success : function (data, response, status) {                    //提交后
                                $.messager.progress('close');                                //关闭进度条信息框
                                
                                if (data > 0) {                                                //判断修改是否成功
                                    $.messager.show({                                        //消息框
                                        title : '提示',
                                        msg : '修改管理成功',
                                    });
                                    $('#manager_edit').dialog('close').form('reset');        //关闭对话框，重置表单
                                    $('#manager').datagrid('reload');                        //重新加载数据表格
                                } else {
                                    $.messager.alert('修改失败！', '未知错误或没有任何修改，请重试！', 'warning');    //修改失败提示
                                }
                            }
                        });
                    }
                },
            },{
                text : '取消',                                                                //取消按钮
                iconCls : 'icon-redo',
                handler : function () {                                                        //点击取消按钮执行函数
                    $('#manager_edit').dialog('close').form('reset');                        //关闭对话框，重置表单
                },
            }],
        });
        
        //管理帐号验证
        $('input[name="manager"]').validatebox({
            required : true,
            validType : 'length[2,20]',
            missingMessage : '请输入管理名称',
            invalidMessage : '管理名称在 2-20 位',
        });
        
        //管理密码验证
        $('input[name="password"]').validatebox({
            required : true,
            validType : 'length[6,30]',
            missingMessage : '请输入管理密码',
            invalidMessage : '管理密码在 6-30 位',
        });
        
        //修改管理密码验证
        $('input[name="password_edit"]').validatebox({
            //required : true,
            validType : 'length[6,30]',
            missingMessage : '请输入管理密码',
            invalidMessage : '管理密码在 6-30 位',
        });
        
        //分配权限验证
        $('#auth').combotree({                                    //树形下拉框
            url : 'nav.php',
            required : true,                                    //不能为空
            lines : true,                                        //显示虚线
            multiple : true,                                    //支持多选
            checkbox : true,                                    //显示复选框
            onlyLeafCheck : true,                                //只有底层目录才显示复选框
            onLoadSuccess : function (node, data) {                //在数据加载成功后触发
                var _this = this;
                if (data) {                                        //判断目录对象是否存在
                    $(data).each(function (index, value) {        //遍历出目录对象
                        if (this.state == 'closed') {            //判断如果有子目录
                            $(_this).tree('expandAll');            //展开所有目录
                        }
                    });
                }
            },
        });
        
        //增删改查执行对象
        manager_tool = {
            //刷新
            reload : function () {                                        //点击刷新执行方法
                $('#manager').datagrid('reload');                        //重载数据表格
            },
            //取消全选
            redo : function () {                                        //点击取消全选
                $('#manager').datagrid('unselectAll');                    //取消全选
            },
            //添加
            add : function () {                                            //点击添加按钮执行
                $('#manager_add').dialog('open');                        //打开添加对话框
                $('input[name="manager"]').focus();                        //将光标定位到表单
            },
            //删除
            remove : function () {                                        //点击删除按钮执行
                var rows = $('#manager').datagrid('getSelections');        //获取数据表格所有选中对象
                if (rows.length > 0) {                                    //判断选中对象长度大于0
                    $.messager.confirm('确定操作', '您正在要删除所选的记录吗？', function (flag) {            //执行消息提示框，确认或者取消
                        if (flag) {                                                            //点击确认
                            var ids = [];
                            for (var i = 0; i < rows.length; i ++) {                        //循环出选中对象
                                ids.push(rows[i].id);                                        //将选中对象追加到数组
                            }
                            //console.log(ids.join(','));
                            $.ajax({                                                        //ajax提交
                                type : 'POST',
                                url : 'deleteManager.php',
                                data : {
                                    ids : ids.join(','),                                    //数组格式化分隔符
                                },
                                beforeSend : function () {                                    //提交中执行函数
                                    $('#manager').datagrid('loading');                        //显示载入状态
                                },
                                success : function (data) {                                    //提交成功后
                                    if (data) {                                                //判断是否删除了数据
                                        $('#manager').datagrid('loaded');                    //隐藏载入状态
                                        $('#manager').datagrid('load');                        //重新加载数据表格
                                        $('#manager').datagrid('unselectAll');                //取消所有选中的行
                                        $.messager.show({                                    //删除消息提示
                                            title : '提示',
                                            msg : data + '个管理被删除成功！',
                                        });
                                    }
                                },
                            });
                        }
                    });
                } else {                                                                    //如果没有选中任何行
                    $.messager.alert('提示', '请选择要删除的记录！', 'info');                    //提示信息
                }
            },
            //修改
            edit : function () {                                                            //点击修改执行
                var rows = $('#manager').datagrid('getSelections');                            //获取选中数组
                if (rows.length > 1) {                                                        //数组长度大于1
                    $.messager.alert('警告操作！', '编辑记录只能选定一条数据！', 'warning');    //提示只能选中一条
                } else if (rows.length == 1) {                                                //判断如果只选择了一条
                    $.ajax({                                                                //ajax
                        url : 'getManager.php',
                        type : 'post',
                        data : {
                            id : rows[0].id,                                                //将要修改的id发送
                        },
                        beforeSend : function () {                                            //提交时执行
                            $.messager.progress({                                            //提示信息
                                text : '正在获取中...',
                            });
                        },
                        success : function (data, response, status) {                        //提交成功后
                            $.messager.progress('close');                                    //关闭提示信息
                            
                            if (data) {                                                        //判断如果获取成功
                                
                                var obj = $.parseJSON(data);                                //将JSON转换成js格式
                                var auth = obj[0].auth.split(',');                            //获取要修改数据的权限，格式化分隔符
                                
                                $('#manager_edit').form('load', {                            //读取数据填充到表单
                                    id : obj[0].id,                                            //将id填充到name为id输入框
                                    manager_edit : obj[0].manager,                            //将用户名填充到name为manager_edit输入框
                                    //auth_edit : obj[0].auth,
                                }).dialog('open');                                            //打开对话框
                                
                                //分配权限
                                $('#auth_edit').combotree({                                    //树形下拉框
                                    url : 'nav.php',                                        //获取树形目录
                                    required : true,                                        //不能为空
                                    lines : true,                                            //显示虚线
                                    multiple : true,                                        //支持多选
                                    checkbox : true,                                        //显示复选框
                                    onlyLeafCheck : true,                                    //只有底层目录显示复选框
                                    onLoadSuccess : function (node, data) {                    //数据加载成功后触发
                                        var _this = this;
                                        if (data) {                                            //判断获取到树形数据
                                            $(data).each(function (index, value) {            //遍历目录
                                                if ($.inArray(value.text, auth) != -1) {    //查找遍历到的权限名称在数组里的下标，是否等于-1
                                                    $(_this).tree('check', value.target);    //勾选指定节点，说明是已有权限
                                                }
                                                if (this.state == 'closed') {                //判断如果有子目录
                                                    $(_this).tree('expandAll');                //展开所有目录
                                                }
                                            });
                                        }
                                    },
                                });
                                
                            } else {                                                                    //判断如果获取失败
                                $.messager.alert('获取失败！', '未知错误导致失败，请重试！', 'warning');    //提示失败信息
                            }
                        }
                    });
                } else if (rows.length == 0) {                                                            //如果一条没选中
                    $.messager.alert('警告操作！', '编辑记录至少选定一条数据！', 'warning');                //提示选择信息
                }
            },
        };
        
        
        
    });
[/code]

**parseJSON()将JSON格式转换成js原生格式**

