---
layout: post
title: " 第一百八十五节，jQuery，Ajax 表单插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，Ajax 表单插件**



**学习要点：**

**1.核心方法**

**2.option 参数**

**3.工具方法**

**传统的表单提交，需要多次跳转页面，极大的消耗资源也缺乏良好的用户体验。而这款 form.js 表单的 Ajax 提交插件将解决这个问题。**



**一．核心方法**

**官方网站：http://malsup.com/jquery/form/**

**form.js 插件有两个核心方法：ajaxForm()和 ajaxSubmit()，它们集合了从控制表单元素 到决定如何管理提交进行的功能。**

****ajaxForm()方法，传统方式提交，在form元素上使用****

****传统方式提交，也就是采用的 <input type="submit" value="提交" />****

****注意：使用 ajaxForm()方法，会直接实现 ajax 提交。自动阻止了默认行为不会跳转页面，而它提交的 默认页面是 form 控件的
action 属性的值。提交的方式是 method 属性的值。****

[code]

        $('#reg').ajaxForm( function () {  //success : fucntion () {}就是这里的function
            alert('提交');                
        });
[/code]



****ajaxSubmit()方法，表单不是传统方式提交，使用了js的   **Submit()方法，提交******

[code]

        $('#reg').submit( function () {     //不会阻止默认行为，会跳转
            $(this).ajaxSubmit(function () {
                alert('提交');
            });
            return false;   //阻止默认行为
        });
[/code]



**注意：ajaxForm()方法，是针对 form 直接提交的，所以阻止了默认行为。而 ajaxSubmit() 方法，由于是针对
submit()方法的，所以需要手动阻止默认行为。而使用了 validate.js 验证 插件，那么 ajaxSubmit()比较适合我们。**



******二．option 参数******

******option 参数是一个以键值对传递的对象，可以通过这个对象，设置各种 Ajax 提交的功 能。******

[code]

        $('#reg').submit( function () {      //不会阻止默认行为，会跳转
            $(this).ajaxSubmit({
                url: 'test.php',            //设置提交的 url，可覆盖 action 属性
                target: '#box',             //服务器返回的内容存放在#box 里
                type: 'POST',               //GET,POST
                dataType: null,             //xml,json,script，默认为 null
                clearForm: true,            //成功提交后，清空表单
                resetForm: true,            //成功提交后，重置表单
                data: {                     //增加额外的数据提交
                    aaa: 'bbb',
                    ccc: 'ddd'
                },
                beforeSubmit: function (formData, jqForm, options) {    //提交前的验证
                    alert(formData[0].name);                    //得到传递表单元素的 name
                    alert(formData[0].value);                   //得到传递表单元素的 value
                    alert(jqForm);                              //得到 form 的 jquery 对象
                    alert(options);                             //得到目前 options 设置的属性
                    alert('正在提交中！！！');
                    return true;
                },
                success: function (responseText, statusText) {  //提交成功后的操作
                    alert(responseText + statusText);           //成功后回调
                },
                error: function (event, errorText, errorType) { //错误时调用  //提交失败的操作
                    alert(errorText + errorType);
                }
            });
            return false;   //阻止默认行为
        });
[/code]



**三．工具方法**

**form.js 除了提供两个核心方法之外，还提供了一些常用的工具方法。这些方法主要是 在提交前或后对数据或表单进行处理的。**

******formSerialize()表单序列化，内置了的，这里还是需要了解一下******

[code]

     //表单序列化
    alert($('#reg').formSerialize());
[/code]



**fieldSerialize()序列化某一个字段**

[code]

     //序列化某一个字段
    alert($('#reg #user').fieldSerialize());
[/code]



**fieldValue()得到某个字段的 value 值**

[code]

     //得到某个字段的 value 值
    alert($('#reg #user').fieldValue());
[/code]



**resetForm()重置表单**

[code]

     //重置表单
    $('#reg').resetForm()
[/code]



**clearFields()清空某个字段**

[code]

     //清空某个字段
    $('#reg #user').clearFields();
[/code]



