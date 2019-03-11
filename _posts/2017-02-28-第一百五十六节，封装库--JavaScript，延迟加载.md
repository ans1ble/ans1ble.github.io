第一百五十六节，封装库--JavaScript，延迟加载

**封装库--JavaScript，延迟加载**



**延迟加载的好处，就是在浏览器视窗外的图片，不加载，拖动鼠标到浏览器视窗内后加载，用户不看的图片就不用加载，可以减少服务器大量流量**

**将图片的src地址用一张统一的图片，这样初始化都加载这张图片，减少流量**

**将图片正真的连接地址用另外的属性赋值**

**当用户视窗高度加上滚动条高度，大于等于，图片头部与浏览器头部的距离时，将正真的连接地址，改变到src，**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170228133206282-1253409321.png)**



html

    
    
    <!--延迟加载-->
        <div id="photo">
            <dl>
                <dt><img xsrc="img/p1.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p2.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p3.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p4.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
    
            <dl>
                <dt><img xsrc="img/p5.jpg" src="img/wait_load.jpg" class="wait_load" alt="" /></dt>
                <dd>延迟加载图片</dd>
            </dl>
        </div>

css

    
    
    /*延迟加载*/
    #photo {
        width:900px;
        float:left;
    }
    #photo dl {
        width:225px;
        height:270px;
        float:left;
        margin:5px 0 15px 0;
    }
    #photo dl dt {
        width:200px;
        height:250px;
        margin:0 auto;
    }
    #photo dl dd {
        height:25px;
        line-height:25px;
        text-align:center;
    }

前台js

    
    
    //延迟加载
        var wait_load = $('.wait_load');                      //获取所有的图片节点
        wait_load.shzh_tou_ming_du(0);                        //将所有图片设置成透明
        $(window).yuan_su_shi_jian('scroll',_wait_load);
        $(window).yuan_su_shi_jian('resize',_wait_load);
        function _wait_load() {
            setTimeout(function () {                          //延迟100毫秒
                for (var i = 0; i < wait_load.jd_length(); i++) {                        //根据图片的长度来循环
                    var _this = wait_load.hq_jd(i);                                      //获取到每次循环对应的图片对象
                    if(getInner().height + gun_dong_tiao_wei_zhi().top >= ju_li_liu_lan_qi_tou(_this)) {      //判断视窗高度加上滚动条的高度，大于等于，元素头部到浏览器头部距离时
                        $(_this).qh_shu_xing_zhi('src', $(_this).qh_shu_xing_zhi('xsrc')).yi_dong_tou_ming({  //每次循环对应的图片改变src并显示出来
                            attr: 'o',
                            target: 100,
                            t: 30,
                            step: 10
                        });
                    }
                }
            }, 100);
        }



首先要引入封装库

