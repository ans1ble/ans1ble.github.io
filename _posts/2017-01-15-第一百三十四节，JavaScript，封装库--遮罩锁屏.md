第一百三十四节，JavaScript，封装库--遮罩锁屏

**JavaScript，封装库--遮罩锁屏**

**封装库新增1个方法**

    
    
     /** zhe_zhao_suo_ping()方法，将一个区块元素设置成遮罩锁屏区块
     * 注意：一般需要在css文件将元素设置成隐藏
     **/
    feng_zhuang_ku.prototype.zhe_zhao_suo_ping = function () {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            var chang_w = getInner().width;  //getInner()函数库函数，跨浏览器获取浏览器视窗大小
            var chang_h = getInner().height;
            yan_su.style.width = chang_w + 'px';
            yan_su.style.height = chang_h + 'px';
            yan_su.style.position = 'absolute';
            yan_su.style.top = '0';
            yan_su.style.left = '0';
        } else {
            alert("遮罩锁屏区块,只能设置一个区块元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };



**遮罩锁屏**

**![](https://images2015.cnblogs.com/blog/955761/201701/955761-20170115001620744-988774354.png)**





**html代码**



    
    
    <div id="suo_ping"></div>





**css代码**

    
    
     /*遮罩锁屏区块*/
    #suo_ping{
        z-index: 9998; /*注意：如果遮罩层上面有元素，它的层级要大于9998*/
        background: #000;
        filter: alpha(opacity=50);
        opacity: 0.5;
        display: none;
    }





**前台js代码**

    
    
     //弹出登录框加遮罩锁屏
        //获取登录框，执行将登录框居中方法，执行浏览器窗口事件方法
        $().huo_qu_id('login').yuan_su_ju_zhong().chuang_kou_shi_jian(function () {
            //获取登录框，执行将登录框居中方法
            $().huo_qu_id('login').yuan_su_ju_zhong();
            //获取遮罩锁屏元素，执行遮罩锁屏方法
            $().huo_qu_id('suo_ping').zhe_zhao_suo_ping();
        });
        //获取登录元素节点，执行点击事件方法
        $().huo_qu_class('deng_lu').on_click(function () {
            //获取登录框，改变css
            $().huo_qu_id('login').xian_shi();
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



