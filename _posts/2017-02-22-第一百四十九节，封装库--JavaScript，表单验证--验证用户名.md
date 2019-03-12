---
layout: post
title: " 第一百四十九节，封装库--JavaScript，表单验证--验证用户名 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单验证--验证用户名**



注册验证功能，顾名思义就是验证表单中每个字段的合法性，如果全部合法才可以提交表单。



**效果图**

**聚集光标时**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170222201253960-652813145.png)**



信息不合法是

![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170222201440538-1919500100.png)

信息合法时

![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170222201542226-1775919141.png)



html

[code]

    <div id="reg">
        <h2 class="tuo"><img src="img/close.png" alt="" class="close" />会员注册</h2>
        <form name="reg">
            <dl>
                <dd>用 户 名： <input type="text" name="user" class="text"/>
                    <span class="info info_user">请输入用户名，4~20位，由字母、数字和下划线组成！</span>
                    <span class="error error_user">输入不合法，请重新输入！</span>
                    <span class="succ succ_user">可用</span>
                </dd>
                <dd>密　　码： <input type="password" name="pass" class="text"/></dd>
                <dd>密码确认： <input type="password" name="notpass" class="text"/></dd>
                <dd><span style="vertical-align:-2px">提　　问：</span> <select name="ques">
                    <option value="0">- - - - 请选择 - - - -</option>
                    <option value="1">- - 您最喜欢吃的菜</option>
                    <option value="2">- - 您的狗狗的名字</option>
                    <option value="3">- - 您的出生地</option>
                    <option value="4">- - 您最喜欢的明星</option>
                </select></dd>
                <dd>回　　答： <input type="text" name="ans" class="text"/></dd>
                <dd>电子邮件： <input type="text" name="email" class="text"/></dd>
                <dd class="birthday"><span style="vertical-align:-2px">生　　日：</span> <select name="year">
                    <option value="0">- 请选择 -</option>
                </select> 年
                    <select name="month">
                        <option value="0">- 请选择 -</option>
                    </select> 月
                    <select name="day">
                        <option value="0">- 请选择 -</option>
                    </select> 日
                </dd>
                <dd style="height:105px;"><span style="vertical-align:85px">备　　注：</span> <textarea name="ps"></textarea>
                </dd>
                <dd style="padding:0 0 0 320px;">还可以输入200字</dd>
                <dd style="padding:0 0 0 80px;"><input type="button" class="submit"/></dd>
            </dl>
        </form>
    </div>
[/code]

css

[code]

    /*注册*/
    #reg {
        width:600px;
        height:550px;
        border:1px solid #ccc;
        position:absolute;
        display:none;
        z-index:9999;
        background:#fff;
    }
    #reg h2 {
        height:40px;
        line-height:40px;
        text-align:center;
        font-size:14px;
        letter-spacing:1px;
        color:#666;
        background:url(img/login_header.png) repeat-x;
        margin:0;
        padding:0;
        border-bottom:1px solid #ccc;
        margin:0 0 20px 0;
        cursor:move;
    }
    #reg h2 img {
        float:right;
        position:relative;
        top:14px;
        right:8px;
        cursor:pointer;
    }
    #reg dl {
        font-size:14px;
        color:#666;
        margin:20px;
        padding:0 0 0 10px;
    }
    #reg dl dd {
        height:30px;
        padding:5px 0;
    }
    #reg dl dd input.text, #reg dl dd select {
        width:200px;
        height:25px;
        border:1px solid #ccc;
        background:#fff;
        font-size:14px;
        color:#666;
    }
    #reg dl dd select {
        width:202px;
    }
    #reg dl dd.birthday select {
        width:100px;
    }
    #reg dl dd textarea {
        width:360px;
        height:100px;
        background:#fff;
        border:1px solid #ccc;
    }
    #reg dl dd input.submit {
        width:143px;
        height:33px;
        background:url(img/reg.png) no-repeat;
        border:none;
        cursor:pointer;
    }
    
    /*注册提示*/
    /*用户名提示*/
    #reg dl dd span.info, #reg dl dd span.error, #reg dl dd span.succ {
        display:block;
        font-size:12px;
        color:#333;
        width:165px;
        height:32px;
        line-height:32px;
        padding:0 0 0 35px;
        position:absolute;
        letter-spacing:1px;
        display:none;
    }
    #reg dl dd span.info {
        background:url(img/reg_info.png) no-repeat;
    }
    #reg dl dd span.error {
        background:url(img/reg_error.png) no-repeat;
    }
    #reg dl dd span.succ {
        height:14px;
        line-height:14px;
        background:url(img/reg_succ.png) no-repeat;
        padding:0 0 0 20px;
        color:green;
    }
    /*输入*/
    #reg dl dd span.info_user {
        height:43px;
        line-height:18px;
        padding-top:7px;
        background:url(img/reg_info2.png) no-repeat;
        top:60px;
        left:310px;
        /*display:block;*/
    }
    /*错误*/
    #reg dl dd span.error_user {
        top:60px;
        left:310px;
        /*display:block;*/
    }
    /*可用*/
    #reg dl dd span.succ_user {
        top:70px;
        left:315px;
        /*display:block;*/
    }
[/code]

前台js

[code]

    // 表单验证
        //验证用户名
        $('form').hq_form_name('user').yuan_su_shi_jian('focus', function () {                 //给用户名设置聚集光标事件
            $('#reg .info_user').xian_shi();                                                    //当聚集光标时显示输入提示
            $('#reg .error_user').yin_cang();
            $('#reg .succ_user').yin_cang();
        }).yuan_su_shi_jian('blur', function () {                                              //给用户名设置光标离开事件
    
            if (trim($(this).hq_value()) == ''){                                               //当光标离开时判断，输入框是否为空
                $('#reg .info_user').yin_cang();                                                //如果输入框为空，隐藏输入提示
                $('#reg .error_user').xian_shi();
            }else if (!/[a-zA-Z0-9_]{4,20}/.test(trim($(this).hq_value()))){                   //如果输入的信息不符合提示要求
                $('#reg .error_user').xian_shi();                                               //显示错误提示
                $('#reg .info_user').yin_cang();
                $('#reg .succ_user').yin_cang();
            }else{
                $('#reg .succ_user').xian_shi();
                $('#reg .info_user').yin_cang();
                $('#reg .error_user').yin_cang();
            }
    
        });
[/code]

首先引入函数库和封装库

