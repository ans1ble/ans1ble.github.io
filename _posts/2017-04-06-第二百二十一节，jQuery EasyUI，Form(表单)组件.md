---
layout: post
title: " 第二百二十一节，jQuery EasyUI，Form(表单)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Form(表单)组件**



**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Form(表单)组件的使用方法，这个组件不依赖于任何组件**



**一．加载方式**

**表单组件只能在 JS 区域设置，首先定义一张表单。**



[code]

    <form id="box" method="post">
        <div>
            <label>用户名:</label>
            <input type="text" name="name"/>
        </div>
        <div>
            <label>邮　箱:</label>
            <input type="text" name="email"/>
        </div>
        <input type="submit">
    </form>
[/code]



**JS 加载调用**

**form()将form表单元素执行表单组件方法**

[code]

    $( function () {
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]



**解析 JSON 数据**

远程返回代码

[code]

    //JSON类型
    {
        "name" : "bnbbs",
        "email" : "bnbbs@163.com"
    }
[/code]

js代码

[code]

            //读取JSON里面的email值
            success: function (data) {
                var data = eval('(' + data + ')');  //将字符串转换成JSON类型
                if (data.email) {
                    alert(data.email);      //读取JSON里面的email值
                }
            }
[/code]



**自动提交，只有在form()方法里，第一个参数写上'submit'就会自动提交**

[code]

    $( function () {
        $('#box').form('submit',{
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407161306863-1003159600.png)**

**url   string 提交表单动作的 URL 地址。默认值 null。**

[code]

    $(function () {
        $('#box').form('submit',{
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407161517363-1170379255.png)**

**onSubmit   param 在提交之前触发，返回 false 可以终止提交。**

[code]

    $(function () {
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]



**success   data 在表单提交成功以后触发。**

[code]

    $(function () {
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]



**注意：以下3个事件要结合load方法使用，也就是一般要在获取数据填充到表单时使用**

**onBeforeLoad   param在请求加载数据之前触发。返回 false 可以停止该动作。【 **不推荐** 】**

[code]

    $(function () {
        $('#box').form({
            onBeforeLoad: function (param) {
                alert('在请求之前');
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            onLoadSuccess: function (data) {
                alert('在请求完成之后');
                alert(data);
            },
            onLoadError: function (param) {
                alert('在请求出错后');
            }
        });
        $('#box').form('load','uer.php');   //获取数据
    });
[/code]



**onLoadSuccess   data 在表单数据加载完成后触发。 **【 **不推荐** 】****

[code]

    $(function () {
        $('#box').form({
            onBeforeLoad: function (param) {
                alert('在请求之前');
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            onLoadSuccess: function (data) {
                alert('在请求完成之后');
                alert(data);
            },
            onLoadError: function (param) {
                alert('在请求出错后');
            }
        });
        $('#box').form('load','uer.php');   //获取数据
    });
[/code]



**onLoadError   none 在表单数据加载出现错误的时候触发。**



[code]

    $(function () {
        $('#box').form({
            onBeforeLoad: function (param) {
                alert('在请求之前');
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            onLoadSuccess: function (data) {
                alert('在请求完成之后');
                alert(data);
            },
            onLoadError: function (param) {
                alert('在请求出错后');
            }
        });
        $('#box').form('load','uer.php');   //获取数据
    });
[/code]







**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170407180916550-852135670.png)**

**submit   options 执行自动提交操作，该选项参数是一个对象。**

[code]

    $(function () {
        $('#box').form('submit',{
           url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            },
        });
    });
[/code]



**load   data 读取记录填充到表单中。**

[code]

    $(function () {
        $('#box').form({
           url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            },
        });
        $('#box').form('load', {    //将对象里的数据填充到对应的输入框
            name: 'bnbbs',          //将值填充到name为name的输入框
            email: 'bnbbs@163.com', //将值填充到name为email的输入框
        });
        //当然也可以将远程JSON数据填充到输入框如,xxx.php里是JSON数据
        // $('#box').form('load','xxx.php');
    });
[/code]



**clear   none 清除表单数据。**

[code]

    $(function () {
        $('#box').form({
           url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            },
        });
        $('#box').form('clear');
    });
[/code]



**reset   none 重置表单数据。**

[code]

    $(function () {
        $('#box').form({
           url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            },
        });
        $('#box').form('reset');
    });
[/code]



**validate   none做表单字段验证，当所有字段都有效的时候 返 回 true 。 该 方 法 使
用validatebox(验证框)插件。【重点】**

[code]

    $(function () {
        $('input[name=name]').validatebox({  //验证表单
            required: true,  //不能为空
        });
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                return $(this).form('validate');   //当所有字段都有效的时候 返 回 true ，返回false不能提交表单
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
    });
[/code]



**enableValidation   none 启用验证。**

[code]

    $(function () {
        $('input[name=name]').validatebox({  //验证表单
            required: true,  //不能为空
        });
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                return $(this).form('validate');   //当所有字段都有效的时候 返 回 true ，返回false不能提交表单
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
        $('#box').form('enableValidation');
    });
[/code]



**disableValidation   none 禁用验证。**

[code]

    $(function () {
        $('input[name=name]').validatebox({  //验证表单
            required: true,  //不能为空
        });
        $('#box').form({
            url: 'user.php',
            onSubmit: function (param) {    //在提交前触发
                return $(this).form('validate');   //当所有字段都有效的时候 返 回 true ，返回false不能提交表单
                param.code = '320902';      //接收的参数可以自定义，额外发送数据，以定义名称=值
            },
            success: function (data) {      //发送后触发，
                alert(data);                //接收响应内容
            }
        });
        $('#box').form('disableValidation');
    });
[/code]





**使用$.fn.form.defaults 重写默认值对象。**

