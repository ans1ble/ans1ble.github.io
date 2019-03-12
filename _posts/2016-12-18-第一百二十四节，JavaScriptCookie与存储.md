
---
layout: post
title: " 第一百二十四节，JavaScriptCookie与存储 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScriptCookie与存储**



**学习要点：**

**1.cookie**

**2.cookie局限性**

**3.其他存储**



**随着Web越来越复杂，开发者急切的需要能够本地化存储的脚本功能。这个时候，第一个出现的方案：cookie诞生了。cookie的意图是：在本地的客户端的磁盘上以很小的文件形式保存数据。**



**一．** **Cookie**

**cookie也叫HTTP
Cookie，最初是客户端与服务器端进行会话使用的。比如，会员登录，下次回访网站时无须登录了；或者是购物车，购买的商品没有及时付款，过两天发现购物车里还有之前的商品列表。**

**HTTP Cookie要求服务器对任意HTTP请求发送Set-
Cookie，因此，Cookie的处理原则上需要在服务器环境下进行。当然，现在大部分浏览器在客户端也能实现Cookie的生成和获取。(目前Chrome不可以在客户端操作，其他浏览器均可)**



**cookie的组成**

**cookie由名/值对形式的文本组成：name=value。完整格式为：**

**name=value; [expires=date]; [path=path]; [domain=somewhere.com]; [secure]**

**中括号是可选，name=value是必选。**



**向磁盘写入 **cookie****

****使用方式：****

****document.cookie = 名称****

********document.cookie = 名称 = 值********

**********完整形式：document.cookie =
'user=值;expires=失效时间;path=访问路径;domain=访问域名;secure=安全的https限制通讯';**********

********如果名称或者值有中文需要编码和解码********

[code]

    document.cookie = 'user=' + encodeURIComponent('李炎恢');     //编码方式向磁盘写入cookie
    alert(decodeURIComponent(document.cookie));                //解码方式读取写入的cookie
[/code]



**读取写入的cookie**

**使用方式：**

**document.cookie**

**如果写入有编码，读取就需要解码**

[code]

    document.cookie = 'user=' + encodeURIComponent('李炎恢');     //编码方式向磁盘写入cookie
    alert(decodeURIComponent(document.cookie));                //解码方式读取写入的cookie
[/code]



****expires=** cookie有效时间**

**每个浏览器都各自保存了 **cookie文件，设置有效时间，就是告诉浏览器这个 **cookie保存多久，******

**失效时间，如果没有声明，则为浏览器关闭后即失效。声明了失效时间，那么时间到期后方能失效。**

**设置失效时间**

**expires=失效时间（单位Mon Dec 26 2016 15:07:40 GMT+0800）**



[code]

    var date = new Date();                        //创建日期对象
    //getDate获取系统当前日期
    //setDate将日期转换成毫秒数
    date.setDate(date.getDate() + 7);
    //alert(date); 返回Mon Dec 26 2016 15:07:40 GMT+0800
    //向磁盘写入一个cookie文件，名称为user，值为林贵秀编码，有效时间expires=有效日期
    document.cookie = "user= " + encodeURIComponent('林贵秀') +";expires=" + date;
[/code]



**PS：可以通过Firefox浏览器查看和验证失效时间。如果要提前删除cookie也非常简单，只要重新创建cookie把时间设置当前时间之前即可：date.getDate()
- 1或new Date(0)。**





**********path= **cookie** 访问路径**********

**********访问路径，当设置了路径，那么只有设置的那个路径文件才可以访问cookie。**********

[code]

     var date = new Date();                        //创建日期对象
    //getDate获取系统当前日期
    //setDate将日期转换成毫秒数
    date.setDate(date.getDate() + 7);
    //alert(date); 返回Mon Dec 26 2016 15:07:40 GMT+0800
    var path = '/js/'; //表示当前工程目录下的js文件夹下
    //向磁盘写入一个cookie文件，名称为user，值为林贵秀编码，有效时间expires=有效日期
    document.cookie = "user= " + encodeURIComponent('林贵秀') +";expires=" + date + ";path=" + path;
[/code]



**domain=cookie访问域名**

**访问域名，用于限制只有设置的域名才可以访问，那么没有设置，会默认限制为创建cookie的域名**

[code]

     var date = new Date();                        //创建日期对象
    //getDate获取系统当前日期
    //setDate将日期转换成毫秒数
    date.setDate(date.getDate() + 7);
    //alert(date); 返回Mon Dec 26 2016 15:07:40 GMT+0800
    var path = '/js/'; //表示当前工程目录下的js文件夹下
    var domain = 'localhost'; //设置访问域名
    //向磁盘写入一个cookie文件，名称为user，值为林贵秀编码，有效时间expires=有效日期
    document.cookie = "user= " + encodeURIComponent('林贵秀') +";expires=" + date + ";path=" + path + ";domain=" + domain;
[/code]

**PS：如果定义了60.com，那么在这个域名下的任何网页都可访问，如果定义了v.60.com，那么只能在这个二级域名访问该cookie，而主域名和其他子域名则不能访问。**

**PS：设置域名，必须在当前域名绑定的服务器上设置，如果在60.com服务器上随意设置其他域名，则会无法创建cookie。**



************secure ** ** ** ** **安全的https限制通讯**********************

**********************安全设置，指明必须通过安全的通信通道来传输(HTTPS)才能获取cookie。仅限加密连接**********************

[code]

     var date = new Date();                        //创建日期对象
    //getDate获取系统当前日期
    //setDate将日期转换成毫秒数
    date.setDate(date.getDate() + 7);
    //alert(date); 返回Mon Dec 26 2016 15:07:40 GMT+0800
    var path = '/js/'; //表示当前工程目录下的js文件夹下
    var domain = 'localhost'; //设置访问域名
    //向磁盘写入一个cookie文件，名称为user，值为林贵秀编码，有效时间expires=有效日期
    document.cookie = "user= " + encodeURIComponent('林贵秀') +";expires=" + date + ";path=" + path + ";domain=" + domain + ";secure";
[/code]

**PS：https安全通信链接需要单独配置。**



**JavaScript设置、读取和删除并不是特别的直观方便，我们可以封装成函数来方便调用。**

[code]

     //创建cookie
    setCookie('usr1', '林闺秀1', 1);
    setCookie('usr2', '林闺秀2', 2);
    setCookie('usr3', '林闺秀3', 3);
    
    //创建cookie，创建cookie函数
    //setCookie函数接收cookie，名称，值，失效日期(天数)，[访问路径，访问域名，安全通讯https限制]
    function setCookie(name, value, expires, path, domain, secure) {
        //将接收到的名称和值编码后，格式化成键值对
        var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
        if (typeof expires == "number" && expires > 0) {  //判断接收到的失效日期，是否是数值类型并且大于0
            var date = new Date();         //创建日期对象
            date.setDate(date.getDate() + expires);  //获取系统当前时间，加上接收到的失效时间等于总失效日期
            cookieText += '; expires=' + date;  //将失效日期累加到cookieText
        }
        if (path) {   //判断访问路径是否存在
            cookieText += '; expires=' + path;  //如果访问路径存在，将访问路径累加到cookieText
        }
        if (domain) {  //判断访问域名是否存在
            cookieText += '; domain=' + domain;  //如果访问域名存在，将访问域名累加到cookieText
        }
        if (secure) {  //判断https通讯限制是否存在
            cookieText += '; secure';  //如果https通讯限制存在，将https通讯限制累加到cookieText
        }
        document.cookie = cookieText;  //向磁盘写入cookie文件
    }
    
    //获取cookie
    alert(getCookie('usr1'));
    alert(getCookie('usr2'));
    alert(getCookie('usr3'));
    
    //获取cookie，获取cookie函数，获取cookie名称的值
    function getCookie(name) {  //接收要获取的cookie名称，
        //将接收到的cookie名称进行编码后，格式化赋值给cookieName
        var cookieName = encodeURIComponent(name) + '=';
        //用编码和格式化后的cookie名称，在document.cookie里查找它的索引位置
        var cookieStart = document.cookie.indexOf(cookieName);
        //默认cookie值为空
        var cookieValue = null;
    
        if (cookieStart > -1) {   //判断如果查找cookie名称的索引大于负一
            //从cookie名称开始搜索;的位置
            var cookieEnd = document.cookie.indexOf(';', cookieStart);
            if (cookieEnd == -1) { //判断如果从cookie名称开始搜索;的位置等于负一
                cookieEnd = document.cookie.length; //cookieEnd重新赋值等于document.cookie的长度
            }
            //截取字符串，cookie名称位置加上cookie名称长度等于截取开始位置，从cookie名称开始搜索;引号的位置为结束位置
            //将截取的字符串解码
            cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
        }
        return cookieValue;  //返回解码后的cookie名称值
    }
    
    //删除cookie
    unsetCookie('usr1');
    
    //删除cookie，删除cookie函数
    function unsetCookie(name) {  //接收要删除cookie名称
        //重新创建此cookie，cookie名称等于空，过期时间设置成过去，这样cookie就失效了
        document.cookie = name + "= ; expires=" + new Date(0);
    }
[/code]



**二．cookie** **局限性**

**cookie虽然在持久保存客户端用户数据提供了方便，分担了服务器存储的负担。但是还有很多局限性的。**

**第一： 每个特定的域名下最多生成20个cookie（根据不同的浏览器有所区别）。**

**1.IE6或更低版本最多20个cookie**

**2.IE7和之后的版本最多可以50个cookie。IE7最初也只能20个，之后因被升级不定后增加了。**

**3.Firefox最多50个cookie**

**4.Opera最多30个cookie**

**5.Safari和Chrome没有做硬性限制。**

** **

**PS：为了更好的兼容性，所以按照最低的要求来，也就是 最多不得超过20个cookie。当超过指定的
cookie时，浏览器会清理掉早期的cookie。IE和Opera会清理近期最少使用的cookie，Firefox会随机清理cookie。**

** **

**第二： cookie的最大大约为4096字节(4k)，为了更好的兼容性，一般不能超过4095字节即可。**

** **

**第三： cookie存储在客户端的文本文件，所以特别重要和敏感的数据是不建议保存在cookie的。比如银行卡号，用户密码等。**





**三．** **其他存储**

****userData储存 **IE提供的一种存储其实属于css，非IE不支持，【及不推荐使用】IE10以上也不支持，为了将移除******

**IE提供了一种存储可以持久化用户数据，叫做userData，从IE5.0就开始支持。每个数据最多128K，每个域名下最多1M。这个持久化数据存放在缓存中，如果缓存没有清理，那么会一直存在。**

[code]

     //首先要在html页面写上cssstyle="behavior:url(#default#userData)"
    //<div style="behavior:url(#default#userData)" id="box"></div>
    
    addEvent(window, 'load', function () {    //创建事件，等待页面加载完毕后激发函数
        //通过id获取到标签元素，
        var box = document.getElementById('box');
        //给元素添加一个属性名称和值，如果属性名称和值有中文需要编码
        box.setAttribute('name', encodeURIComponent('林贵秀'));
        //保存文件，里面写名称，相当于cookie名称
        box.save('bookinfo');
    
        //box.removeAttribute('name');            //删除userDate
        //box.save('bookinfo');
    
        box.load('bookinfo'); //相当于加载cookie名称，里面接收名称
        //解码打印出元素的属性值
        alert(decodeURIComponent(box.getAttribute('name')));
    });
    
    //跨浏览器添加事件，添加事件兼容
    function addEvent(obj, type, fn) {     //添加事件函数，接收3个参数，1事件对象，2事件名称，3事件函数
        //判断浏览器如果支持w3c
        if (obj.addEventListener) {
            //就用w3c的addEventListener方法添加对象，将事件名称和事件函数传入添加事件
            obj.addEventListener(type, fn, false);
        } else if (obj.attachEvent) {   //判断如果浏览器是IE9以下，就用IE的方法attachEvent添加事件
            //将事件名称和事件函数传入创建对象
            obj.attachEvent('on' + type, fn);
        }
    }
[/code]



**Web存储**

**在比较高版本的浏览器，JavaScript提供了sessionStorage和globalStorage。在HTML5中提供了localStorage来取代globalStorage。而浏览器最低版本为：IE8+、Firefox3.5+、Chrome
4+和Opera10.5+。**

**PS：由于这三个对浏览器版本要求较高，我们就只简单的在Firefox了解一下，有兴趣的可以通过关键字搜索查询。**

**sessionStorage数据 **Web存储****

[code]

     //通过方法存储和获取
    sessionStorage.setItem('name', '李炎恢');  //存储数据
    alert(sessionStorage.getItem('name')); //获取存储数据
    
    //通过属性存储和获取
    sessionStorage.book = '李炎恢';  //存储数据
    alert(sessionStorage.book);  //获取存储数据
    
    //删除存储
    sessionStorage.removeItem('name');
[/code]



**由于localStorage代替了globalStorage，所以在Firefox、Opera和Chrome目前的最新版本已不支持。**

****localStorage **数据 **Web存储********

[code]

     //通过方法存储和获取
    localStorage.setItem('name', '李炎恢');  //储存数据
    alert(localStorage.getItem('name'));  //读取储存数据
    　　
    //通过属性存储和获取
    localStorage.book = '李炎恢';  //储存数据
    alert(localStorage.book);   //读取储存数据
    　　
    //删除存储
    localStorage.removeItem('name');
[/code]

**PS：这三个对象都是永久保存的，保存在缓存里，只有手工删除或者清理浏览器缓存方可失效。在容量上也有一些限制，主要看浏览器的差异，Firefox3+、IE8+、Opera为5M，，Chrome和Safari为2.5M。**

