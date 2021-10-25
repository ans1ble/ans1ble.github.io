---
layout: post
title: " 第一百八十六节，jQuery，验证表单插件，Ajax 表单插件，验证和提交表单 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，验证表单插件，Ajax 表单插件，验证和提交表单**



**HTML**

[code]

     <form id="reg" method="post" action="yzh.php" title="会员注册">
        <ol class="reg_error"></ol>
        <p>
            <label for="user">帐号：</label>
            <input type="text" name="user" class="text" id="user"/>
            <span class="star">*</span>
        </p>
        <p>
            <label for="pass">密码：</label>
            <input type="text" name="pass" class="text" id="pass"/>
            <span class="star">*</span>
        </p>
        <p>
            <label for="email">邮箱：</label>
            <input type="text" name="email" class="text" id="email"/>
            <span class="star">*</span>
        </p>
        <p>
            <label>性别：</label>
            <input type="radio" name="sex" id="male" checked="checked" value="男"><label for="male">男</label></input>
            <input type="radio" name="sex" id="female" value="女"><label for="female">女</label></input>
        </p>
        <p>
            <label for="date">生日：</label>
            <input type="text" name="date" readonly="readonly" class="text" id="date"/>
        </p>
    </form>
    <div id="loading">数据交互中...</div>
[/code]

**css**

[code]

     /*注册框*/
    #reg {
        padding: 15px;
        display: none;
    }
    
    #reg p {
        margin: 10px 0;
        padding: 0;
    }
    
    #reg p label {
        font-size: 14px;
        /*color: #666;*/
    }
    
    #reg p .star {
        color: red;
    }
    
    #reg .text {
        border-radius: 4px;
        border: 1px solid #ccc;
        background: #fff;
        height: 25px;
        width: 200px;
        text-indent: 5px;
        color: #666;
    }
    #reg .reg_error{
        color: #ff171f;
        padding:0;
        margin:0 0 0 20px;
    }
    #reg .succ{
        display:inline-block;
        width:20px;
        background:url(../img/reg_succ.png) no-repeat;
    }
    
    /*ui提示信息*/
    .ui-tooltip{
        color: #ff1c24;
    }
    
    .su{
        width: 50px;
        height: 20px;
        background-color: #2cff24;
    }
    #loading {
        line-height:30px;
        font-size:14px;
        font-weight:bold;
        text-indent:40px;
        color:#666;
        padding-left:40px;
    }
[/code]

**前台js**



**closeOnEscape对话框插件属，性阻止点击键盘ESC键关闭dialog**





**beforeClose对话框插件属性，值是一个函数，关闭对话框执行函数**





**submitHandler表单验证插件属性，值是一个函数，全部验证成功执行函数，接收一个参数是表单对象**





**beforeSubmit提交ajax提交插件属性，值是一个函数，提交时执行函数**





**success提交ajax提交插件属性，值是一个函数，提交成功后执行函数**



  
**highlight表单验证插件属性，值是一个函数，当验证不合法时执行函数**



  
**unhighlight表单验证插件属性，值是一个函数，当验证合法时执行函数**



  
**showErrors表单验证插件属性，值是一个函数，当验证不合法时执行函数，可以获取不合法句柄**



[code]

    $('#loading').dialog({                  //数据交互提示框，执行对话框方法
            autoOpen : false,                   //创建对话框关闭
            modal : true,                       //遮罩
            closeOnEscape : false,              //阻止点击键盘ESC键关闭dialog
            resizable : false,                  //阻止调整对话框大小
            draggable : false,                  //阻止对话框可以移动
            width : 230,
            height : 50
        }).parent().parent().find('.ui-widget-header').hide();  //找到对话框标题隐藏
        //注册框
        $('#reg_a').on('click',function () {                    //将注册框，执行对话框方法
            $('#reg').dialog({
                autoOpen : true,
                modal : true,
                resizable : false,
                width : 320,
                height : 360,
                buttons : {                                     //注册对话框创建按钮
                    '提交' : function () {
                        $(this).submit();                       //执行提交方法
                    }
                },
                closeText : '关闭对话框',
                beforeClose:function (e,ui) {                   //将要关闭，执行回调函数
                    $('#reg').resetForm();                                //Ajax 表单插件方法，重置表单
                    $('#reg span.star').html('*').removeClass('succ');    //改变提示信息
                    $('#reg ol').html('');                                //将提示信息去掉
                    $('#reg input').css('border', '1px solid #ccc');      //改变出错边框颜色
                }
            }).buttonset().validate({                                           //验证表单
                submitHandler: function (form) {                                //全部验证成功准备提交
                    $(form).ajaxSubmit({                                        //Ajax 表单插件方法，提交
                        url: 'add.php',                                         //提交页面
                        type: 'POST',                                           //提交方式
                        beforeSubmit: function (formData, jqForm, options) {    //提交时
                            $('#loading').dialog('open');                       //打开交互对话框
                            $('#reg').dialog('widget').find('button').eq(1).button('disable');                                  //将注册对话框的提交按钮禁止
                            $('#loading').css('background', 'url(img/743.gif) no-repeat 20px center').html('数据交互中...');     //载入交互对话框图片
                        },
                        success: function (responseText, statusText) {                                                             //提交后
                            if (responseText) {                                                                                    //判断提交成功返回值
                                $('#reg').dialog('widget').find('button').eq(1).button('enable');                                  //取消阻止注册提交按钮
                                $('#loading').css('background', 'url(img/chg.png) no-repeat 20px center').html('数据新增成功...');  //载入提交成功图片
                                setTimeout(function () {                                    //睡眠1秒
                                    $('#loading').dialog('close');                          //关闭交互提示对话框
                                    $('#reg').dialog('close');                              //关闭注册对话框
                                    $('#reg').resetForm();                                  //重置表单
                                    $('#reg span.star').html('*').removeClass('succ');      //改变验证提示信息
                                }, 10000);
                            }
                        }
                    });
                },
                highlight: function (element, errorClass) {                             //如果出错，错误框边框改变颜色
                    $(element).css('border', '1px solid #630');
                    $(element).parent().find('span').html('*').removeClass('succ');     //改变验证提示信息
                },
                unhighlight: function (element, errorClass) {                           //如果正确取消边框改变颜色
                    $(element).css('border', '1px solid #ccc');
                    $(element).parent().find('span').html('&nbsp;').addClass('succ');   //显示正确图片
                },
                showErrors: function (errorMap, errorList) {                            //获取出错句柄
                    var errors = this.numberOfInvalids();
                    if (errors > 0) {                                                   //判断出错句柄个数来改变对话框的高度
                        $('#reg').dialog('option', 'height', errors * 20 + 360);        //注册对话框自动根据错误数量来改变高度
                    } else {
                        $('#reg').dialog('option', 'height', 360);                      //没有错误还原高度
                    }
                    this.defaultShowErrors();
                },
                errorLabelContainer: 'ol.reg_error',                                    //有错误时，将所有表单错误信息统一放到class为ol.reg_error的元素里
                wrapper: 'li',                                                          //将每个错误信息放入一个li标签
                rules : {                                                               //表单验证规则
                    user : {                                                            //验证用户名
                        required:true,                                                  //不能为空
                        rangelength:[2,10]                                              //不得小于2位大于10位
                    },
                    pass:{                                                              //验证密码
                        required:true,                                                  //不能为空
                        rangelength:[6,20]                                              //不得小于6位大于20位
                    },
                    email:{                                                             //验证邮箱
                        required:true,                                                  //不能为空
                        email:true                                                      //必须是邮箱格式
                    }
                },
                messages : {                                                            //错误提示
                    user : {
                        required:'用户名不能为空！',
                        rangelength:jQuery.format('用户名不得小于{0}位，大于{1}位')
                    },
                    pass:{
                        required:'密码不能为空',
                        rangelength:jQuery.format('密码不得小于{0}位，大于{1}位')
                    },
                    email:{
                        required:'邮箱不能为空',
                        email:'请输入正确的邮箱格式'
                    }
                }
            });
    
    
            //邮箱执行自动补全
            $('#email').autocomplete({
                autoFocus: true,
                delay: 0,
                source: function (request, response) {
                    var hosts = ['qq.com', '163.com', '263.com', 'gmail.com', 'hotmail.com'], //起始
                        term = request.term,        //获取输入值
                        ix = term.indexOf('@'),     //@
                        name = term,                //用户名
                        host = '',                  //域名
                        result = [];                //结果
                    //结果第一条是自己输入
                    result.push(term);
                    if (ix > -1) { //如果有@的时候
                        name = term.slice(0, ix);       //得到用户名
                        host = term.slice(ix + 1);      //得到域名
                    }
                    if (name) {
                        //得到找到的域名
                        var findedHosts = (host ? $.grep(hosts, function (value, index) {
                                return value.indexOf(host) > -1;
                            }) : hosts),
                            //最终列表的邮箱
                            findedResults = $.map(findedHosts, function (value, index) {
                                return name + '@' + value;
                            });
                        //增加一个自我输入
                        result = result.concat(findedResults);
                    }
                    response(result);
                }
            });
    
            //将生日执行日历ui
            $('#date').datepicker({
                showOtherMonths:true,
                changeYear:true,
                changeMonth:true,
                yearSuffix:''
            });
        });
[/code]

**提交PHP文件**

[code]

    <? php
        header('Content-Type:text/html; charset=utf-8');
        
        define('DB_HOST', 'localhost');
        define('DB_USER', 'root');
        define('DB_PWD', '279819');
        define('DB_NAME', 'zhiwen');
        
        $conn = @mysql_connect(DB_HOST, DB_USER, DB_PWD) or die('数据库链接失败：'.mysql_error());
        
        @mysql_select_db(DB_NAME) or die('数据库错误：'.mysql_error());
        
        @mysql_query('SET NAMES UTF8') or die('字符集错误：'.mysql_error());
        sleep(3);
        require 'config.php';
        
        $query = "INSERT INTO user (user, pass, email, sex, birthday, date) 
                VALUES ('{$_POST['user']}', sha1('{$_POST['pass']}'), '{$_POST['email']}', '{$_POST['sex']}', '{$_POST['birthday']}', NOW())";
        
        mysql_query($query) or die('新增失败！'.mysql_error());
        
        echo mysql_affected_rows();
        
        mysql_close();
    ?>
[/code]



