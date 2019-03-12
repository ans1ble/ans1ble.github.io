
---
layout: post
title: " 第二百二十九节，jQuery EasyUI，后台管理界面---后台登录 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**jQuery EasyUI，后台管理界面---后台登录**



**登录原理图**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424142458397-1822692468.png)



**一，login.php，登录界面**

[code]

    <!DOCTYPE html>
    <html>
    <head>
    <title>jQuery Easy UI</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="easyui/themes/default/easyui.css" />
    <link rel="stylesheet" type="text/css" href="easyui/themes/icon.css" />
    <link rel="stylesheet" type="text/css" href="css/login.css" />
    </head>
    <body>
    
    
    <div id="login">
        <p>管理员帐号：<input type="text" id="manager"  class="textbox"></p>
        <p>管理员密码：<input type="password" id="password" class="textbox"></p>
    </div>
    
    <div id="btn">
        <a href="#" class="easyui-linkbutton">登录</a>
    </div>
    
    
    <script type="text/javascript" src="easyui/jquery.min.js"></script>
    <script type="text/javascript" src="easyui/jquery.easyui.min.js"></script>
    <script type="text/javascript" src="easyui/locale/easyui-lang-zh_CN.js" ></script>
    <script type="text/javascript" src="js/index.js"></script>
    </body>
    </html>
[/code]



**二，index.js，设置登录界面样式，和验证登录信息，提交数据**

[code]

    $( function () {
        
        //登录界面
        $('#login').dialog({                //登录对话框
            title : '登录后台',
            width : 300,
            height : 180,
            modal : true,                    //遮罩锁屏
            iconCls : 'icon-login',            //图标
            buttons : '#btn',                //将登录按钮加载到对话框里
        });
        
        //管理员帐号验证
        $('#manager').validatebox({
            required : true,                                //账号不能为空
            missingMessage : '请输入管理员帐号',                //提示信息
            invalidMessage : '管理员帐号不得为空',            //错误信息
        });
        
        //管理员密码验证
        $('#password').validatebox({
            required : true,                                //密码不能为空
            validType : 'length[6,30]',                        //长度6到30位之间
            missingMessage : '请输入管理员密码',                //提示信息
            invalidMessage : '管理员密码不得为空',            //错误信息
        });
        
        //加载时判断验证
        if (!$('#manager').validatebox('isValid')) {                   //判断账号是否合法
            $('#manager').focus();                                       //如果不合法将光标定位到输入框
        } else if (!$('#password').validatebox('isValid')) {           //判断密码是否合法
            $('#password').focus();                                       //如果不合法将光标定位动输入框
        }
        
        
        //单击登录
        $('#btn a').click(function () {
            if (!$('#manager').validatebox('isValid')) {                //判断账号是否合法
                $('#manager').focus();                                    //如果不合法将光标定位到输入框
            } else if (!$('#password').validatebox('isValid')) {        //判断密码是否合法
                $('#password').focus();                                    //如果不合法将光标定位动输入框
            } else {                                                    //如果账号和密码都合法
                $.ajax({                                                //执行ajax提交数据库
                    url : 'checklogin.php',                                //提交页面
                    type : 'post',                                        //提交方式
                    data : {                                            //提交数据
                        manager : $('#manager').val(),                    //获取账号输入框值提交
                        password : $('#password').val(),                //获取密码输入框值提交
                    },
                    beforeSend : function () {                            //提交时事件
                        $.messager.progress({                            //创建窗口信息，进度条方式
                            text : '正在登录中...',                        //提示内容
                        });
                    },
                    success : function (data, response, status) {        //提交后事件
                        $.messager.progress('close');                    //关闭进度条方式的窗口信息
                        
                        if (data > 0) {                                    //判断如果checklogin.php返回大于0，表示登录成功
                            location.href = 'admin.php';                //跳转到后台页面
                        } else {
                            $.messager.alert('登录失败！', '用户名或密码错误！', 'warning', function () {        //窗口信息提示登录失败
                                $('#password').select();    //选中密码框文本
                            });
                        }
                    }
                });
            }
        });
        
    });
[/code]



**三，checklogin.php，接收提交的用户数据，数据库查找**

[code]

    <? php
        session_start();
        require 'config.php';                       //引入数据库配置文件
        
        $manager = $_POST['manager'];               //接收户名
        $password = sha1($_POST['password']);       //接收密码
        
        $query = mysql_query("SELECT id FROM easyui_admin WHERE manager='$manager' AND password='$password' LIMIT 1") or die('SQL 错误！');
        
        if (!!mysql_fetch_array($query, MYSQL_ASSOC)) {         //判断数据库里的用户名和密码与用户输入的匹配到
            $_SESSION['admin'] = $manager;                      //创建SESSION
            echo 1;                                             //返回1
        } else {
            echo 0;                                             //返回0
        }
        
        
    ?>
[/code]



**四，数据库表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424143453553-751411414.png)**







**五，admin.php，登录成功后界面**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170424143653444-1403800592.png)**

