---
layout: post
title: " 第一百五十二节，封装库--JavaScript，表单验证--年月日注入 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单验证--年月日注入**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170225212022882-1009815715.png)**





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

前台js

[code]

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
        function select_day() {                  //当改变年value值并失去焦点时触发
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
                    //判断润年29天
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
[/code]

首先引入封装库

