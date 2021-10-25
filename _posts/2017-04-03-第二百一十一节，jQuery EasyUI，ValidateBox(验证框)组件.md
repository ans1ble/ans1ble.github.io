---
layout: post
title: " 第二百一十一节，jQuery EasyUI，ValidateBox(验证框)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，ValidateBox(验证框)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404162834128-1956281540.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.方法列表**

**4.自定义验证**



**本节课重点了解 EasyUI 中 ValidateBox(验证框)组件的使用方法，这个组件依赖于 Tooltip(提示框)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <input id="email" class="easyui-validatebox"
    data-options="required:true,validType:'email'" />
[/code]



**validatebox将一个输入框执行验证框方法**



**JS 加载调用**

[code]

    $( function () {
        $('#email').validatebox({
            required: true,
            validType: 'email'
        });
    });
[/code]





**二．属性列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403211654816-568023490.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403211702175-1080602324.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403211746285-397546010.png)

**required boolean 定义为必填字段。默认为 false。不能为空**

[code]

    /**
    <input id="email" />
     **/
    
    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            validType: 'email'
        });
    });
[/code]



**validType string,array 定义字段验证类型，比如：email、url、length[0,100]
、remote['url','paramname']。默认值为：null。**

 电子邮件验证

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: 'email'   //必须为电子邮件类型
        });
    });
[/code]

网址验证，还必须包含http

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: 'url'   //网址验证，还必须包含http
        });
    });
[/code]

字符串验证位数

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: 'length[5,10]'   //字符串验证位数
        });
    });
[/code]

远程服务器验证

[code]

    /**
    <input name="par" id="email" />
     **/
    
    $(function () {
        $('#email').validatebox({
            // required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: 'remote["user.php","par"]'  //远程服务器验证,第一个参数是远程文件，第二个参数数输入框name值
            //远程返回true通过，返回false不通过
        });
    });
[/code]

组合形式，用数组方式包含

[code]

    /**
    <input name="par" id="email" />
     **/
    
    $(function () {
        $('#email').validatebox({
            // required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"]  //组合形式,邮件格式5值10位
        });
    });
[/code]





**delay number 延迟到最后验证输入值。默认值200。 验证反应时间**

[code]

    $(function () {
        $('#email').validatebox({
            // required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            delay:1000  //验证反应时间
        });
    });
[/code]



**missingMessage string 当文本框未填写时出现的提示信息。默认值：This field is required。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            delay:1000,  //验证反应时间
            missingMessage:'请输入电子邮件'    //当文本框未填写时出现的提示信息
        });
    });
[/code]



**invalidMessage string 当文本框的内容被验证为无效时出现的提示。默认值 null。**

[code]

    $( function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
    });
[/code]



**tipPosition string 定义当文本框内容无效的时候提示消息显 示 的 位 置 ， 有 效 的 值 有
：'left','right'。默认值 right。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件',
            tipPosition:'right'
        });
    });
[/code]



**deltaX number 提示框在水平方向平移。默认值0。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件',
            tipPosition:'right',
            deltaX:50
        });
    });
[/code]



**novalidate boolean 为 true 时关闭验证功能。默认值 false。**



[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件',
            tipPosition:'right',
            deltaX:50,
            novalidate:true     //true 时关闭验证功能。默认值 false。
        });
    });
[/code]







**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403222528816-1004714103.png)**

**options   none 返回属性列表。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        alert($('#email').validatebox('options'));  //返回属性对象
    });
[/code]



**destroy   none 移除并销毁组件。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        $('#email').validatebox('destroy');  //移除并销毁组件
    });
[/code]



**validate   none 验证文本框的内容是否有效。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        alert($('#email').validatebox('validate'));  //验证文本框的内容是否有效
    });
[/code]



**isValid   none调用 validate 方法并且返回验证结果，true 或者 false。一般用这个**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        alert($('#email').validatebox('isValid'));  //验证文本框的内容是否有效
    });
[/code]



**enableValidation   none 启用验证。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        $('#email').validatebox('disableValidation');  //禁用验证
        $('#email').validatebox('enableValidation');  //启用验证
    });
[/code]



**disableValidation   none 禁用验证。**

[code]

    $(function () {
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType: ["email","length[5,10]"],  //组合形式,邮件格式5值10位
            missingMessage:'请输入电子邮件',    //当文本框未填写时出现的提示信息
            invalidMessage:'请输入5至10位正确的电子邮件'
        });
        $('#email').validatebox('disableValidation');  //禁用验证
        $('#email').validatebox('enableValidation');  //启用验证
    });
[/code]





**我们可以使用$.fn.validatebox.defaults 重写默认值对象。**





**四．自定义验证**

**我们可以使用重写默认规则的方式来创建一个新的规则。**

**新增一个规则**

[code]

    $( function () {
        //新增一个验证规则
        $.extend($.fn.validatebox.defaults.rules, {
            minLength: {    //自定义名称
                validator: function (value, param) {
                    //value接收的输入字符, param接收的使用自定义时传进来的位数
                    return value.length >= param[0];
                },
                message: '请长度不小于{0}的字符'
            }
        });
    
        $('#email').validatebox({
            required: true,      // 定义为必填字段。默认为 false。不能为空
            //定义字段验证类型
            validType : 'minLength[5]'
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403225512269-1699057726.png)



