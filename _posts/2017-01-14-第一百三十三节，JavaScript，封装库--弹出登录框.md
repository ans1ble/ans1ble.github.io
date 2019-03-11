第一百三十三节，JavaScript，封装库--弹出登录框

**JavaScript，封装库--弹出登录框**

****封装库，增加了两个方法****

**yuan_su_ju_zhong()方法，将获取到的区块元素居中到页面，**  
 **chuang_kou_shi_jian()方法，浏览器窗口事件，当窗口的大小变化时触发函数**

    
    
     /** yuan_su_ju_zhong()方法，将获取到的区块元素居中到页面，
     * 注意：使用此方法时，首先要在css里将目标区块设置成(绝对定位,position: absolute;)
     **/
    feng_zhuang_ku.prototype.yuan_su_ju_zhong = function () {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            var style = window.getComputedStyle ? window.getComputedStyle(yan_su, null) : null || yan_su.currentStyle;
            var y_style = style.display;
            if (y_style === "none") {
                yan_su.style.display = "block";
            }
            var width = yan_su.offsetWidth;
            var height = yan_su.offsetHeight;
            if (y_style === "none") {
                yan_su.style.display = "none";
            }
            var top = (document.documentElement.clientHeight - height) / 2;
            var left = (document.documentElement.clientWidth - width) / 2;
            for (var ii = 0; ii < this.jie_dian.length; ii++) {
                this.jie_dian[ii].style.top = top + 'px';
                this.jie_dian[ii].style.left = left + 'px';
            }
        } else {
            alert("区块元素页面居中,只能设置一个区块元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
    
    /** chuang_kou_shi_jian()方法，浏览器窗口事件，当窗口的大小变化时触发函数
     * 接收一个参数，就是触发时要执行的函数（包含函数功能）
     **/
    feng_zhuang_ku.prototype.chuang_kou_shi_jian = function (fn) {
        window.onresize = fn;
        return this;
    };



**弹出登录框**

**![](https://images2015.cnblogs.com/blog/955761/201701/955761-20170114142859463-327394665.png)**





**html代码**

    
    
     <div id="login">
        <h2><img src="img/close.png" alt="" class="close" />网站登录</h2>
        <div class="user">帐 号：<input type="text" name="user" class="text" /></div>
        <div class="pass">密 码：<input type="password" name="pass" class="text" /></div>
        <div class="button"><input type="button" class="submit" value="" /></div>
        <div class="other">注册新用户 | 忘记密码？</div>
    </div>



**css代码**

    
    
     /*登录框*/
    #login{
        width: 350px;
        height: 250px;
        border: 1px solid #ccc;
        position:absolute;
        display: none;
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



**前台js代码**



    
    
    //弹出登录框
        //获取登录框，执行将登录框居中方法，执行浏览器窗口事件方法
        $().huo_qu_id('login').yuan_su_ju_zhong().chuang_kou_shi_jian(function () {
            //获取登录框，执行将登录框居中方法
            $().huo_qu_id('login').yuan_su_ju_zhong();
        });
        //获取登录元素节点，执行点击事件方法
        $().huo_qu_class('deng_lu').on_click(function () {
            //获取登录框，改变css
            $().huo_qu_id('login').css('display','block');
        });
        //获取登录框里的关闭元素，执行点击事件方法
        $().huo_qu_class('close').on_click(function () {
            //获取登录框，改变css
            $().huo_qu_id('login').css('display','none')
        });



