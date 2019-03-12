---
layout: post
title: " 第一百三十五节，JavaScript，封装库--拖拽 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--拖拽**

****封装库新增1个 **拖拽** 方法****



[code]

    /** tuo_zhuai()方法，将一个弹窗元素实现拖拽功能
     * 注意：一般需要在css文件将元素里的某一个区块光标设置成提示可以拖拽，如：cursor: move;
     * 无参
     **/
    feng_zhuang_ku.prototype.tuo_zhuai = function () {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            yan_su.onmousedown = function (e) {
               // preDef(e);  //preDef()函数库函数，阻止事件默认行为,
                var e1 = getEvent(e);  //getEvent()函数库函数，跨浏览器获取事件对象,事件event对象,
                var diffx = e1.clientX - yan_su.offsetLeft;
                var diffy = e1.clientY - yan_su.offsetTop;
                if(typeof yan_su.setCapture != 'undefined'){
                    yan_su.setCapture();
                }
                document.onmousemove = function (e) {
                    var e2 = getEvent(e);
                    var left = e2.clientX - diffx;
                    var top = e2.clientY - diffy;
                    if (left < 0){
                        left = 0;
                    }else if(left > getInner().width - yan_su.offsetWidth){
                        left = getInner().width - yan_su.offsetWidth;
                    }
                    if (top < 0){
                        top = 0;
                    }else if(top > getInner().height - yan_su.offsetHeight){
                        top = getInner().height - yan_su.offsetHeight;
                    }
                    yan_su.style.left = left + 'px';
                    yan_su.style.top = top + 'px';
                };
                document.onmouseup = function () {
                    document.onmousemove = null;
                    document.onmouseup = null;
                    if (typeof yan_su.releaseCapture != 'undefined') {
                        yan_su.releaseCapture();
                    }
                };
            };
        } else {
            alert("将一个弹窗元素实现拖拽功能,只能设置一个弹窗元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
[/code]



**HTML代码**

[code]

     <div id="login">
        <h2><img src="img/close.png" alt="" class="close" />网站登录</h2>
        <div class="user">帐 号：<input type="text" name="user" class="text" /></div>
        <div class="pass">密 码：<input type="password" name="pass" class="text" /></div>
        <div class="button"><input type="button" class="submit" value="" /></div>
        <div class="other">注册新用户 | 忘记密码？</div>
    </div>
[/code]



**css代码**



[code]

    /*登录框*/
    #login{
        width: 350px;
        height: 250px;
        border: 1px solid #ccc;
        position:absolute;
        display: none;
        z-index: 9999;
        background-color: #fff;
    }
    #login h2{
        background: rgba(0, 0, 0, 0) url("img/login_header.png") repeat-x scroll 0 0;
        border-bottom: 1px solid #ccc;
        color: #666;
        font-size: 14px;
        height: 40px;
        line-height : 40px;
        text-align: center;
        letter-spacing: 1px;
        margin: 0 0 20px;
        cursor: move;
    }
    #login h2 img{
        cursor: pointer;
        float: right;
        position: relative;
        right: 8px;
        top: 14px;
    }
    #login div.user, #login div.pass {
        color: #666;
        font-size: 14px;
        padding: 5px 0;
        text-align: center;
    }
    #login input.text {
        background: #fff none repeat scroll 0 0;
        border: 1px solid #ccc;
        font-size: 14px;
        height: 25px;
        width: 200px;
    }
    #login .button {
        padding: 20px 0;
        text-align: center;
    }
    #login input.submit {
        background: rgba(0, 0, 0, 0) url("img/login_button.png") no-repeat scroll 0 0;
        border: medium none;
        cursor: pointer;
        height: 30px;
        width: 107px;
    }
    #login .other {
        color: #666;
        padding: 15px 10px;
        text-align: right;
    }
    /*遮罩锁屏区块*/
    #suo_ping{
        z-index: 9998; /*注意：如果遮罩层上面有元素，它的层级要大于9998*/
        background: #000;
        filter: alpha(opacity=50);
        opacity: 0.5;
        display: none;
    }
[/code]



**前台js代码**

[code]

     //前台调用代码
    window.onload = function (){
        //获取到个人中心元素节点，执行鼠标移入移出方法
        $().huo_qu_class('ge_ren_zhong_xin','tou').shu_biao_yi_ru_yi_chu(function () {
            //当鼠标移入时，改变个人中心背景图片
            $(this).css('background', 'url(img/arrow2.png) no-repeat right center');
            //当鼠标移入时，将ul元素执行显示方法
            $().huo_qu_name('ul').xian_shi();
        }, function () {
            //当鼠标移出时，改变个人中心背景图片
            $(this).css('background', 'url(img/arrow.png) no-repeat right center');
            //当鼠标移出时，将ul元素执行隐藏方法
            $().huo_qu_name('ul').yin_cang();
        });
    
        //弹出登录框加遮罩锁屏
        //获取登录框，执行将登录框居中方法，执行浏览器窗口事件方法
        $().huo_qu_id('login').yuan_su_ju_zhong().chuang_kou_shi_jian(function () {
            //获取登录框，执行将登录框居中方法
            $().huo_qu_id('login');
            //获取遮罩锁屏元素，执行遮罩锁屏方法
            $().huo_qu_id('suo_ping').zhe_zhao_suo_ping();
        });
        //获取登录元素节点，执行点击事件方法
        $().huo_qu_class('deng_lu').on_click(function () {
            //获取登录框，改变css
            $().huo_qu_id('login').xian_shi().yuan_su_ju_zhong();
            //获取遮罩锁屏元素，执行显示方法，执行遮罩锁屏方法
            $().huo_qu_id('suo_ping').xian_shi().zhe_zhao_suo_ping();
        });
        //获取登录框里的关闭元素，执行点击事件方法
        $().huo_qu_class('close').on_click(function () {
            //获取登录框，改变css
            $().huo_qu_id('login').yin_cang();
            //获取遮罩锁屏元素，执行隐藏方法
            $().huo_qu_id('suo_ping').yin_cang();
        });
    
        //拖拽
        $().huo_qu_id('login').tuo_zhuai();
    
    
    };
[/code]



