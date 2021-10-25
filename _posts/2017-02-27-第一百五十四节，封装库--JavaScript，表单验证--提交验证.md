---
layout: post
title: " 第一百五十四节，封装库--JavaScript，表单验证--提交验证 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单验证--提交验证**

**将表单的所有必填项，做一个判断函数，填写正确时返回布尔值**

**最后在提交时，判断每一项是否正确，全部正确才可以 提交**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170227104216923-858494342.png)**



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
                <dd><input type="button" class="submit" name="sub"/></dd>
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

    // 表单验证
        $('form').sh_jd().reset();
        //验证用户名
        $('form').hq_form_name('user').yuan_su_shi_jian('focus', function () {                 //给用户名设置聚集光标事件
            $('#reg .info_user').xian_shi();                                                    //当聚集光标时显示输入提示
            $('#reg .error_user').yin_cang();
            $('#reg .succ_user').yin_cang();
        }).yuan_su_shi_jian('blur', function () {                                              //给用户名设置光标离开事件
    
            if (trim($(this).hq_value()) == ''){                                               //当光标离开时判断，输入框是否为空
                $('#reg .info_user').yin_cang();                                                //如果输入框为空，隐藏输入提示
            }else if (!pd_user()){                   //如果输入的信息不符合提示要求
                $('#reg .error_user').xian_shi();                                               //显示错误提示
                $('#reg .info_user').yin_cang();
                $('#reg .succ_user').yin_cang();
            }else{
                $('#reg .succ_user').xian_shi();
                $('#reg .info_user').yin_cang();
                $('#reg .error_user').yin_cang();
            }
        });
        function pd_user() { //最终判断
            if (/[a-zA-Z0-9_]{4,20}/.test(trim($('form').hq_form_name('user').hq_value())))return true;
        }
    
    
        //验证密码
        $('form').hq_form_name('pass').yuan_su_shi_jian('focus', function () {          //获取密码框，添加聚集光标事件
            $('#reg .info_pass').xian_shi();                                            //聚集光标时显示提示
            $('#reg .error_pass').yin_cang();
            $('#reg .succ_pass').yin_cang();
        }).yuan_su_shi_jian('blur', function () {                                       //光标离开事件
            if (trim($(this).hq_value()) == '') {
                $('#reg .info_pass').yin_cang();
            } else {
                if (qiang_yanzh()) {
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
            qiang_yanzh();
        });
        function qiang_yanzh() {
            var neirong = trim($('form').hq_form_name('pass').hq_value());                                     //获取输入的字符
            var chuang = neirong.length;                                                //获取输入的字符长度
            var fuza = 0;                                                               //计数器，同级密码的复杂性
            //第一个必须条件验证6至20位之间
            if (chuang >= 6 && chuang <= 20) {
                $('#reg .info_pass .q1').wen_ben('●').c_css('color', '#008000');
            } else {
                $('#reg .info_pass .q1').wen_ben('○').c_css('color', '#666');
            }
            //第二个必须条件大小写字母、数字和非空格字符，任意一个即可满足
            if (chuang > 0 && !/\s/.test(neirong)) {
                $('#reg .info_pass .q2').wen_ben('●').c_css('color', '#008000');
            } else {
                $('#reg .info_pass .q2').wen_ben('○').c_css('color', '#666');
            }
            //第三个必须条件大、小写字母、数字、非空字符，2种以上
            if (/[0-9]/.test(neirong)) {         //判断是否输入了数字
                fuza++;
            }
            if (/[a-z]/.test(neirong)) {         //判断是否输入了小写字母
                fuza++;
            }
            if (/[A-Z]/.test(neirong)) {         //判断是否输入了大写字母
                fuza++;
            }
            if (/[^0-9a-zA-Z]/.test(neirong)) {  //判断是否输入了特殊字符
                fuza++;
            }
    
            if (fuza >= 2) {
                $('#reg .info_pass .q3').wen_ben('●').c_css('color', '#008000');
            } else {
                $('#reg .info_pass .q3').wen_ben('○').c_css('color', '#666');
            }
            //安全级别判断
            //判断等级务必从高数值到低数值判断。防止高数值无法判断
            if (chuang >= 10 && fuza >= 3) {
                $('#reg .info_pass .s1').c_css('color', '#008000');
                $('#reg .info_pass .s2').c_css('color', '#008000');
                $('#reg .info_pass .s3').c_css('color', '#008000');
                $('#reg .info_pass .s4').c_css('color', '#008000').wen_ben('高');
            } else if (chuang >= 8 && fuza >= 2) {
                $('#reg .info_pass .s1').c_css('color', '#FF6600');
                $('#reg .info_pass .s2').c_css('color', '#FF6600');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').c_css('color', '#FF6600').wen_ben('中');
            } else if (chuang >= 1 && fuza >= 1) {
                $('#reg .info_pass .s1').c_css('color', '#800000');
                $('#reg .info_pass .s2').c_css('color', '#ccc');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').c_css('color', '#800000').wen_ben('低');
            } else {
                $('#reg .info_pass .s1').c_css('color', '#ccc');
                $('#reg .info_pass .s2').c_css('color', '#ccc');
                $('#reg .info_pass .s3').c_css('color', '#ccc');
                $('#reg .info_pass .s4').wen_ben('');
            }
            if (chuang >= 6 && chuang <= 20 && !/\s/.test(neirong) && fuza >= 2){
                return true;
            }else {
                return false;
            }
        }
    
    
    
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
        function qr_mim() {
            if (trim($('form').hq_form_name('pass').hq_value()) == trim($('form').hq_form_name('notpass').hq_value())){
                return true;
            }
        }
    
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
        function qr_huoda() {
            if (trim($('form').hq_form_name('ans').hq_value()).length >= 2 && trim($('form').hq_form_name('ans').hq_value()).length <= 32){
                return true;
            }
    
        }
    
    
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
        function qr_email() {
            var lshi = trim($('form').hq_form_name('email').hq_value());
            if (/^[a-zA-Z0-9_\-\.]+@[a-zA-Z0-9_\-]+(\.[a-zA-Z]{2,4}){1,2}$/.test(lshi)){
                return true;
            }
        }
    
    
        //年月日
        var nian = $('form').hq_form_name('year');
        var yuen = $('form').hq_form_name('month');
        var ri = $('form').hq_form_name('day');
        //根据月份判断天数
        var yuen30 = [4,6,9,11];           //30天的月份
        var yuen31 = [1,3,5,7,8,10,12];    //31天的月份
    
        //注入年
        for(var i = 1950; i <= 2017; i++){
            nian.sh_jd().add(new Option(i,i),undefined);
        }
    
        //注入月
        for (var i = 1; i <= 12; i++){
            yuen.sh_jd().add(new Option(i,i),undefined);
        }
    
        //判断注入日
        //当改变年月value值并失去焦点时触发
        nian.yuan_su_shi_jian('change', select_day);
        yuen.yuan_su_shi_jian('change', select_day);
        function select_day() {
            if (nian.hq_value() != 0 && yuen.hq_value() != 0) {      //判断当年月的值都不等于0时
                //清理之前的注入
                ri.sh_jd().options.length = 1;
                var chu_ri = 0;                                         //初始化日
                //注入31天
                if (pd_shuzu(yuen31, parseInt(yuen.hq_value()))) {      //判断当月属于31天时
                    chu_ri = 31;
                    //注入30
                } else if (pd_shuzu(yuen30, parseInt(yuen.hq_value()))) {
                    chu_ri = 30;
                } else {
                    //判断润年29天1
                    if ((parseInt(nian.hq_value()) % 4 == 0 && parseInt(nian.hq_value()) % 100 != 0) || parseInt(nian.hq_value()) % 400 == 0) {
                        chu_ri = 29;
                    } else {
                        //注入28天
                        chu_ri = 28;
                    }
                }
                for (var i = 1; i <= chu_ri; i++) {
                    ri.sh_jd().add(new Option(i, i), undefined);
                }
    
            } else {    //如果年为0时清理注入
                ri.sh_jd().options.length = 1;
            }
    
        }
    
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
    
        //提交判断
        $('form').hq_form_name('sub').on_click(function () {
            var flag = true;
            if (!pd_user()) {        //判断用户名
                flag = false;
                $('#reg .error_user').xian_shi();
            }
            if (!qiang_yanzh()) {    //判断密码
                flag = false;
                $('#reg .error_pass').xian_shi();
            }
            if (!qr_mim()){          //判断确认密码
                flag = false;
                $('#reg .error_notpass').xian_shi();
            }
            if (!qr_huoda()){        //判断回答
                flag = false;
                $('#reg .error_ans').xian_shi();
            }
            if (!qr_email()){        //判断电子邮件
                flag = false;
                $('#reg .error_email').xian_shi();
            }
    
            if (flag) {
                $('form').sh_jd().submit(); //执行提交
            }
    
        });
[/code]



