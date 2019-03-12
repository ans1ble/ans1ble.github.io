
---
layout: post
title: " 第一百五十三节，封装库--JavaScript，表单验证--备注字数验证 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**封装库--JavaScript，表单验证--备注字数验证**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170226142944554-1862059965.png)**



![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170226142956210-29094436.png)



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
                <dd>密　　码： <input type="password" name="pass" class="text"/>
                    <span class="info info_pass">
                        <p>安全级别：<strong class="s s1">■</strong><strong class="s s2">■</strong><strong
                                class="s s3">■</strong> <strong class="s s4" style="font-weight:normal;"></strong></p>
                        <p><strong class="q1" style="font-weight:normal;">○</strong> 6-20 个字符</p>
                        <p><strong class="q2" style="font-weight:normal;">○</strong> 只能包含大小写字母、数字和非空格字符</p>
                        <p><strong class="q3" style="font-weight:normal;">○</strong> 大、小写字母、数字、非空字符，2种以上</p>
                    </span>
                    <span class="error error_pass">输入不合法，请重新输入！</span>
                    <span class="succ succ_pass">可用</span>
                </dd>
                <dd>密码确认： <input type="password" name="notpass" class="text"/>
                    <span class="info info_notpass">请再一次输入密码！</span>
                    <span class="error error_notpass">密码不一致，请重新输入！</span>
                    <span class="succ succ_notpass">可用</span>
                </dd>
                <dd><span style="vertical-align:-2px">提　　问：</span> <select name="ques">
                    <option value="0">- - - - 请选择 - - - -</option>
                    <option value="1">- - 您最喜欢吃的菜</option>
                    <option value="2">- - 您的狗狗的名字</option>
                    <option value="3">- - 您的出生地</option>
                    <option value="4">- - 您最喜欢的明星</option>
                </select></dd>
                <dd>回　　答： <input type="text" name="ans" class="text"/>
                    <span class="info info_ans">请输入回答，2~32位！</span>
                    <span class="error error_ans">回答不合法，请重新输入！</span>
                    <span class="succ succ_ans">可用</span>
                </dd>
                <dd>电子邮件： <input type="text" name="email" class="text" autocomplete="off"/>
                    <span class="info info_email">请输入电子邮件！</span>
                    <span class="error error_email">邮件不合法，请重新输入！</span>
                    <span class="succ succ_email">可用</span>
                    <ul class="all_email">
                        <li><span></span>@qq.com</li>
                        <li><span></span>@163.com</li>
                        <li><span></span>@sohu.com</li>
                        <li><span></span>@sina.com.cn</li>
                        <li><span></span>@gmail.com</li>
                    </ul>
                </dd>
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
                <dd class="tsh1">还可以输入<strong class="unm">10</strong>字</dd>
                <dd class="tsh2">已超过<strong class="unm2"></strong>字,<span>清尾</span></dd>
                <dd><input type="button" class="submit"/></dd>
            </dl>
        </form>
    </div>
[/code]

css

[code]

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
    
    /*密码验证*/
    #reg dl dd span.info_pass {
        width:244px;
        height:102px;
        padding:4px 0 0 16px;
        background:url(img/reg_info3.png) no-repeat;
        top:60px;
        left:310px;
        /*display:block;*/
        letter-spacing:0;
    }
    #reg dl dd span.info_pass p {
        height:25px;
        line-height:25px;
        color:#666;
    }
    #reg dl dd span.info_pass p strong.s {
        color:#ccc;
    }
    #reg dl dd span.error_pass {
        top:43px;
        left:295px;
    }
    #reg dl dd span.succ_pass {
        top:52px;
        left:295px;
    }
    /*错误*/
    #reg dl dd span.error_pass {
        top:110px;
        left:310px;
        /*display:block;*/
    }
    /*可用*/
    #reg dl dd span.succ_pass {
        top:110px;
        left:315px;
        /*display:block;*/
    }
    #reg .info_pass strong{
        font-size: 25px;
    }
    
    /*密码确认*/
    #reg dl dd span.info_notpass{
        height:43px;
        line-height:18px;
        padding-top:7px;
        background:url(img/reg_info2.png) no-repeat;
        top:140px;
        left:310px;
        /*display:block;*/
    }
    /*错误*/
    #reg dl dd span.error_notpass {
        top:140px;
        left:310px;
        /*display:block;*/
    }
    /*可用*/
    #reg dl dd span.succ_notpass {
        top:150px;
        left:315px;
        /*display:block;*/
    }
    
    /*回答*/
    #reg dl dd span.info_ans{
        height:43px;
        line-height:18px;
        padding-top:7px;
        background:url(img/reg_info2.png) no-repeat;
        top:220px;
        left:310px;
        /*display:block;*/
    }
    /*错误*/
    #reg dl dd span.error_ans {
        top:220px;
        left:310px;
        /*display:block;*/
    }
    /*可用*/
    #reg dl dd span.succ_ans {
        top:220px;
        left:315px;
        /*display:block;*/
    }
    
    /*电子邮件*/
    #reg dl dd span.info_email{
        height:43px;
        line-height:18px;
        padding-top:7px;
        background:url(img/reg_info2.png) no-repeat;
        top:255px;
        left:310px;
        /*display:block;*/
    }
    /*错误*/
    #reg dl dd span.error_email {
        top:255px;
        left:310px;
        /*display:block;*/
    }
    /*可用*/
    #reg dl dd span.succ_email {
        top:275px;
        left:315px;
        /*display:block;*/
    }
    #reg dl dd ul.all_email {
        width:180px;
        height:130px;
        background:#fff;
        padding:5px 10px;
        position:absolute;
        top:292px;
        left:104px;
        border:1px solid #ccc;
        display:none;
    }
    #reg dl dd ul.all_email li {
        height:25px;
        line-height:25px;
        border-bottom:1px solid #e5edf2;
        padding:0 5px;
        cursor:pointer;
    }
    
    /*备注提示*/
    #reg dl dd.tsh1{
        padding:0 0 0 320px;
        display: block;
    }
    
    #reg dl dd.tsh2{
        padding:0 0 0 320px;
        display: none;
    }
    #reg dl dd.tsh2 span{
        color: #1227ff;
        cursor:pointer;
    }
    
    /*提交*/
    #reg dl dd input.submit{
        margin-left:150px;
        background-color: #19ff1d;
    }
[/code]

前台js

[code]

    //备注
        var zong = 10;     //总输入字数
        $('form').hq_form_name('ps').yuan_su_shi_jian('keyup', function () {
            beizhu(zong);
        }).yuan_su_shi_jian('paste',function () {    //鼠标粘贴检测
            setTimeout(function () {
               beizhu(zong);
            },50);
        });
        //清尾
        $('#reg .tsh2 span').on_click(function () {
            $('form').hq_form_name('ps').hq_value($('form').hq_form_name('ps').hq_value().substring(0,zong));
            beizhu(zong);
        });
    
        function beizhu(zong) {
            var num = zong - $('form').hq_form_name('ps').hq_value().length;    //得到还可以输入
            if (num >= 0) {
                $('#reg .tsh1').c_css('display', 'block');
                $('#reg .tsh2').c_css('display', 'none');
                $('#reg .tsh1 .unm').wen_ben(num);
            } else if (num < 0) {
                var chang = ($('form').hq_form_name('ps').hq_value().length) - zong;  //得到超出多少
                $('#reg .tsh1').c_css('display', 'none');
                $('#reg .tsh2').c_css('display', 'block');
                $('#reg .tsh2 .unm2').wen_ben(chang).c_css('color', '#FF3724');
            }
        }
[/code]

必须先引入封装库

