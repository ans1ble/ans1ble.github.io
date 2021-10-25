---
layout: post
title: " 第一百八十七节，jQuery，知问前端--cookie 插件，注册成功后生成cookie，显示登录状态 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，知问前端--cookie 插件**



**学习要点：**

**1.使用 cookie 插件**

**2.注册直接登录**

**Cookie 是网站用来在客户端保存识别用户的一种小文件。一般来用库可以保存用户登 录信息、购物数据信息等一系列微小信息。**



**一．使用 cookie 插件**

**官方网站：http://plugins.jquery.com/cookie/**

**cookie()生成cookie文件，3个参数，参数1cookie名称，参数2cookie值，参数3是一个对象设置cookie**

**生成一个 cookie：**

[code]

    $.cookie('123','456');
[/code]



**设置 cookie**

**expires : 7, 过期时间，7 天后，设置过期时间**

  
**path : '/', 设置路径，上一层，设置路径**

  
**domain : 'www.ycku.com', 设置域名，设置域名后，cookie在指定域名下有效**

  
**secure : true, 默认为 false，需要使用安全协议 https，设置true后只有在https协议下有效**

[code]

        $.cookie('123','456' ,{
            expires:10,                     //设置cookie有效期为10天
            path : '/'                      //设置cookie路径
            // domain : 'www.jxiou.com',    //设置cookie域名，只有在当前域名下有效
            // secure : true                //设置cookie为https协议下有效
        });
[/code]



**cookie属性raw，关闭编码/解码，默认为 false默认是自动编码和解码的**

[code]

        $.cookie('123','456' ,{
            expires:10,                     //设置cookie有效期为10天
            path : '/'                      //设置cookie路径
            // domain : 'www.jxiou.com',    //设置cookie域名，只有在当前域名下有效
            // secure : true                //设置cookie为https协议下有效
        });
        $.cookie.raw = true;                //关闭编码/解码，关闭后cookie内容将以明码方式存在，建议不要关闭
[/code]



**读取 cookie 数据，参数为要读取的 **cookie名称****

[code]

        $.cookie('123','456' ,{
            expires:10,                     //设置cookie有效期为10天
            path : '/'                      //设置cookie路径
            // domain : 'www.jxiou.com',    //设置cookie域名，只有在当前域名下有效
            // secure : true                //设置cookie为https协议下有效
        });
        alert($.cookie('123'));             //读取 cookie 数据,参数为要读取的cookie名称
[/code]



**读取所有 cookie 数据，不传参数**

[code]

        $.cookie('adc','456' ,{
            expires:10,                     //设置cookie有效期为10天
            path : '/'                      //设置cookie路径
            // domain : 'www.jxiou.com',    //设置cookie域名，只有在当前域名下有效
            // secure : true                //设置cookie为https协议下有效
        });
        alert($.cookie().adc);              //读取所有 cookie 数据，不传参数
[/code]

**注意：读取所有的 cookie 是以对象键值对存放的，所以，也可以$.cookie().user 获取。**



**removeCookie()删除cookie，参数是要删除的cookie名称**

[code]

        $.cookie('adc','456' ,{
            expires:10,                     //设置cookie有效期为10天
            path : '/'                      //设置cookie路径
            // domain : 'www.jxiou.com',    //设置cookie域名，只有在当前域名下有效
            // secure : true                //设置cookie为https协议下有效
        });
        $.removeCookie('adc', {
                path: '/'
        });                     //removeCookie()删除cookie，参数是要删除的cookie名称
[/code]



**注册成功后生成cookie，显示登录状态**

**html**

[code]

     <div id="header">
        <div class="header_main">
            <h1>知问</h1>
            <div class="header_search">
                <input type="text" name="search" class="search"/>
            </div>
            <div class="header_button">
                <button id="search_button">提交</button>
            </div>
            <div class="header_member">
                <a href="javascript:void(0)" id="reg_a">注册</a>
                <a href="javascript:void(0)" id="member">用户</a>
                |
                <a href="javascript:void(0)" id="login_a">登录</a>
                <a href="javascript:void(0)" id="logout">退出</a>
            </div>
        </div>
    </div>
    
    
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

**前台js**

[code]

     //判断cookie
        var ifcookie = function () {
            if ($.cookie('user')) {                     //判断cookie存在
                $('#member, #logout').show();           //显示用户和退出
                $('#reg_a, #login_a').hide();           //隐藏注册和登录
                $('#member').html($.cookie('user'));    //改名用户为用户名称
            } else {
                $('#member, #logout').hide();           //隐藏用户和退出
                $('#reg_a, #login_a').show();           //显示注册和登录
            }
        };
        ifcookie();                                     //执行cookie判断
    
        //点击退出
        $('#logout').click(function () {
            $.removeCookie('user');                     //删除cookie
            ifcookie();                                 //执行cookie判断
        });
    
        //创建交互数据提示框
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
                                $.cookie('user', $('#user').val());                                                                //注册成功创建，cookie
                                setTimeout(function () {                                    //睡眠1秒
                                    ifcookie();                                             //执行cookie判断
                                    $('#loading').dialog('close');                          //关闭交互提示对话框
                                    $('#reg').dialog('close');                              //关闭注册对话框
                                    $('#reg').resetForm();                                  //重置表单
                                    $('#reg span.star').html('*').removeClass('succ');      //改变验证提示信息
                                }, 1000);
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



