---
layout: post
title: " 第一百五十节，封装库--JavaScript，表单验证--密码验证 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单验证--密码验证**



**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170223212030632-2085623356.png)**



![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170223212047007-755974833.png)

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
[/code]

前台js

[code]

    //验证密码
        $('form').hq_form_name('pass').yuan_su_shi_jian('focus', function () {          //获取密码框，添加聚集光标事件
            $('#reg .info_pass').xian_shi();                                            //聚集光标时显示提示
            $('#reg .error_pass').yin_cang();
            $('#reg .succ_pass').yin_cang();
        }).yuan_su_shi_jian('blur', function () {                                       //光标离开事件
            if (trim($(this).hq_value()) == '') {
                $('#reg .info_pass').yin_cang();
            } else {
                if (qiang_yanzh(this)) {
                    $('#reg .succ_pass').xian_shi();
                    $('#reg .info_pass').yin_cang();
                    $('#reg .error_pass').yin_cang();
                } else {
                    $('#reg .succ_pass').yin_cang();
                    $('#reg .info_pass').yin_cang();
                    $('#reg .error_pass').xian_shi();
                }
            }
        });
        //密码强度验证
        $('form').hq_form_name('pass').yuan_su_shi_jian('keyup',function () {           //按下键盘键放开时事件
            qiang_yanzh(this);
        });
        function qiang_yanzh(_this) {
            var neirong = trim($(_this).hq_value());                                     //获取输入的字符
            var chuang = neirong.length;                                                //获取输入的字符长度
            var fuza = 0;                                                               //计数器，同级密码的复杂性
            var flag = false;                                                          //统计用户输入是否合法
            //第一个必须条件验证6至20位之间
            if (chuang >= 6 && chuang <= 20){
                $('#reg .info_pass .q1').wen_ben('●').c_css('color','#008000');
            }else {
                $('#reg .info_pass .q1').wen_ben('○').c_css('color','#666');
            }
            //第二个必须条件大小写字母、数字和非空格字符，任意一个即可满足
            if (chuang > 0 && !/\s/.test(neirong)) {
                $('#reg .info_pass .q2').wen_ben('●').c_css('color', '#008000');
            } else {
                $('#reg .info_pass .q2').wen_ben('○').c_css('color', '#666');
            }
            //第三个必须条件大、小写字母、数字、非空字符，2种以上
            if (/[0-9]/.test(neirong)){         //判断是否输入了数字
                fuza ++;
            }
            if (/[a-z]/.test(neirong)){         //判断是否输入了小写字母
                fuza ++;
            }
            if (/[A-Z]/.test(neirong)){         //判断是否输入了大写字母
                fuza ++;
            }
            if (/[^0-9a-zA-Z]/.test(neirong)){  //判断是否输入了特殊字符
                fuza ++;
            }
    
            if (fuza >= 2){
               $('#reg .info_pass .q3').wen_ben('●').c_css('color', '#008000');
            }else {
                $('#reg .info_pass .q3').wen_ben('○').c_css('color', '#666');
            }
            //安全级别判断
            //判断等级务必从高数值到低数值判断。防止高数值无法判断
            if (chuang >= 10 && fuza >= 3) {
                $('#reg .info_pass .s1').c_css('color', '#008000');
                $('#reg .info_pass .s2').c_css('color', '#008000');
                $('#reg .info_pass .s3').c_css('color', '#008000');
                $('#reg .info_pass .s4').c_css('color', '#008000').wen_ben('高');
            }else if(chuang >= 8 && fuza >= 2){
                $('#reg .info_pass .s1').c_css('color', '#FF6600');
                $('#reg .info_pass .s2').c_css('color', '#FF6600');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').c_css('color', '#FF6600').wen_ben('中');
            }else if(chuang >= 1 && fuza >= 1){
                $('#reg .info_pass .s1').c_css('color', '#800000');
                $('#reg .info_pass .s2').c_css('color', '#ccc');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').c_css('color', '#800000').wen_ben('低');
            }else {
                $('#reg .info_pass .s1').c_css('color', '#ccc');
                $('#reg .info_pass .s2').c_css('color', '#ccc');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').wen_ben('');
            }
            if (chuang >= 6 && chuang <= 20 && !/\s/.test(neirong) && fuza >= 2) flag = true;
            return flag;
        }
[/code]

首先要引入函数库和封装库

