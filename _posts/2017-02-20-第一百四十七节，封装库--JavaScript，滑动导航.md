第一百四十七节，封装库--JavaScript，滑动导航

**JavaScript，封装库--滑动导航**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201702/955761-20170220184023210-724527109.png)**



html

    
    
    <!--滑动导航-->
    <div id="nav">
        <ul class="about">
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
        <ul class="black">
            <li>首页</li>
            <li>博文列表</li>
            <li>精彩相册</li>
            <li>动感音乐</li>
            <li>关于我</li>
        </ul>
        <div class="nav_bg">
            <ul class="white">
                <li>首页</li>
                <li>博文列表</li>
                <li>精彩相册</li>
                <li>动感音乐</li>
                <li>关于我</li>
            </ul>
        </div>
    </div>



css

    
    
    /*滑动导航*/
    #nav {
        width:465px;
        height:52px;
        background:url(img/nav_bg.png) no-repeat;
        margin:50px auto 0 auto;
        position:relative;
    }
    #nav ul {
        position:absolute;
    }
    #nav ul li {
        width:85px;
        height:52px;
        line-height:52px;
        text-align:center;
        font-weight:bold;
        float:left;
    }
    #nav ul.black {
        left:20px;
        color:#333;
        z-index:1;
    }
    #nav ul.white {
        width:425px;
        color:#fff;
        z-index:3;
        left:0;
    }
    #nav ul.about {
        z-index:4;
        left:20px;
        cursor:pointer;
        background:red;
        filter:alpha(opacity=0);
        opacity:0;
    }
    #nav div.nav_bg {
        width:85px;
        height:52px;
        background:url(img/nav_over.png) no-repeat 0 11px;
        position:absolute;
        left:20px;
        top:0px;
        z-index:2;
        overflow:hidden;
    }



前台js

    
    
    //滑动导航
        $('#nav .about li').shu_biao_yi_ru_yi_chu(function () {
            var target = $(this).sh_jd().offsetLeft;
            $('#nav .nav_bg').yi_dong_tou_ming({
                attr : 'x',
                target : target + 20,
                t : 30,
                step : 10,
                fn : function () {
                    $('#nav .white').yi_dong_tou_ming({
                        attr : 'x',
                        target : -target
                    });
                }
            });
        }, function () {
            $('#nav .nav_bg').yi_dong_tou_ming({
                attr : 'x',
                target : 20,
                t : 30,
                step : 10,
                fn : function () {
                    $('#nav .white').yi_dong_tou_ming({
                        attr : 'x',
                        target : 0
                    });
                }
            });
        });



首先引入js函数库文件，和封装库文件

