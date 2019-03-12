---
layout: post
title: " 第一百五十一节，封装库--JavaScript，表单验证--密码确认验证--回答验证--电子邮件验证加自动补全 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单验证--密码确认验证--回答验证--电子邮件验证加自动补全**



**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170225051712257-905181334.png)**



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
                <dd style="padding:0 0 0 320px;">还可以输入200字</dd>
                <dd style="padding:0 0 0 80px;"><input type="button" class="submit"/></dd>
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
[/code]

前台js

[code]

    //密码确认
        $('form').hq_form_name('notpass').yuan_su_shi_jian('focus', function () {          //获取密码确认框，添加聚集光标事件
            $('#reg .info_notpass').xian_shi();                                            //聚集光标时显示提示
            $('#reg .error_notpass').yin_cang();
            $('#reg .succ_notpass').yin_cang();
        }).yuan_su_shi_jian('blur', function () {
            var mima = trim($('form').hq_form_name('pass').hq_value());
            var qrmima = trim($(this).hq_value());
            if (qrmima == '') {
                $('#reg .info_notpass').yin_cang();
            } else if (qrmima == mima) {
                $('#reg .info_notpass').yin_cang();
                $('#reg .error_notpass').yin_cang();
                $('#reg .succ_notpass').xian_shi();
            }else {
                $('#reg .info_notpass').yin_cang();
                $('#reg .error_notpass').xian_shi();
                $('#reg .succ_notpass').yin_cang();
            }
        });
    
         //回答
        $('form').hq_form_name('ans').yuan_su_shi_jian('focus', function () {          //获取回答框，添加聚集光标事件
            $('#reg .info_ans').xian_shi();                                            //聚集光标时显示提示
            $('#reg .error_ans').yin_cang();
            $('#reg .succ_ans').yin_cang();
        }).yuan_su_shi_jian('blur', function () {
            var huida = trim($(this).hq_value());
            if (huida == '') {
                $('#reg .info_ans').yin_cang();
            } else if (huida.length >= 2 && huida.length <= 32) {
                $('#reg .info_ans').yin_cang();
                $('#reg .error_ans').yin_cang();
                $('#reg .succ_ans').xian_shi();
            } else {
                $('#reg .info_ans').yin_cang();
                $('#reg .error_ans').xian_shi();
                $('#reg .succ_ans').yin_cang();
            }
        });
    
        //电子邮件
        $('form').hq_form_name('email').yuan_su_shi_jian('focus', function () {          //获取电子邮件框，添加聚集光标事件
            $('#reg .info_email').xian_shi();                                            //聚集光标时显示提示
            $('#reg .error_email').yin_cang();
            $('#reg .succ_email').yin_cang();
            if(trim($('form').hq_form_name('email').hq_value()).indexOf('@') == -1){
                $('#reg .all_email').xian_shi();
            }
        }).yuan_su_shi_jian('blur', function () {
            $('#reg .all_email').yin_cang();
            var email = trim($(this).hq_value());
            if (email == '') {
                $('#reg .info_email').yin_cang();
            } else if (/^[a-zA-Z0-9_\-\.]+@[a-zA-Z0-9_\-]+(\.[a-zA-Z]{2,4}){1,2}$/.test(email)) {
                $('#reg .info_email').yin_cang();
                $('#reg .error_email').yin_cang();
                $('#reg .succ_email').xian_shi();
            } else {
                $('#reg .info_email').yin_cang();
                $('#reg .error_email').xian_shi();
                $('#reg .succ_email').yin_cang();
            }
        });
        //电子邮件自动补全界面
        $('#reg .all_email li').shu_biao_yi_ru_yi_chu(function () {
            $(this).c_css('background','#e5edf2');
            $(this).c_css('color','#369');
        },function () {
            $(this).c_css('background','none');
            $(this).c_css('color','#666');
        });
        //自动补全键入
        $('form').hq_form_name('email').yuan_su_shi_jian('keyup', function (event) {
            var value = trim($(this).hq_value());
            if (value.indexOf('@') == -1) {               //在没遇到@时补全，如果遇到停止补全
                $('#reg .all_email span').wen_ben(value);
            } else {
                $('#reg .all_email').yin_cang();
            }
            var length = $('#reg .all_email li').jd_length();
            if (event.keyCode == 40) {       //上键选择补全
                if (this.jishuqi == undefined || this.jishuqi >= length - 1) {    //计数器
                    this.jishuqi = 0;
                } else {
                    this.jishuqi++;
                }
                $('#reg .all_email li').c_css('background', 'none');
                $('#reg .all_email li').c_css('color', '#666666');
                $('#reg .all_email li').guo_lv_jie_dian(this.jishuqi).c_css('background', '#e5edf2');
                $('#reg .all_email li').guo_lv_jie_dian(this.jishuqi).c_css('color', '#369');
            }
            if (event.keyCode == 38) {       //下键选择补全
                if (this.jishuqi == undefined || this.jishuqi <= 0) {    //计数器
                    this.jishuqi = length - 1;
                } else {
                    this.jishuqi--;
                }
                $('#reg .all_email li').c_css('background', 'none');
                $('#reg .all_email li').c_css('color', '#666666');
                $('#reg .all_email li').guo_lv_jie_dian(this.jishuqi).c_css('background', '#e5edf2');
                $('#reg .all_email li').guo_lv_jie_dian(this.jishuqi).c_css('color', '#369');
            }
            if (event.keyCode == 13){       //按下回车键
                $(this).hq_value($('#reg .all_email li').guo_lv_jie_dian(this.jishuqi).wen_ben_guo_lv());
                $('#reg .all_email').yin_cang();
                this.jishuqi = undefined;  //初始化
            }
        });
        //点击补全
        $('#reg .all_email li').yuan_su_shi_jian('mousedown',function () {
            $('form').hq_form_name('email').hq_value($(this).wen_ben_guo_lv());
        });
[/code]

首先引入封装库

