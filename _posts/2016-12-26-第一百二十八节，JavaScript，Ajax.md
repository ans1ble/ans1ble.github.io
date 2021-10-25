---
layout: post
title: " 第一百二十八节，JavaScript，Ajax "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，Ajax**



**学习要点：**

**1.XMLHttpRequest**

**2.GET与POST**

**3.封装Ajax**



**2005年Jesse James Garrett发表了一篇文章，标题为：“Ajax：A new Approach to Web
Applications”。他在这篇文章里介绍了一种技术，用他的话说，就叫：Ajax，是Asynchronous JavaScript +
XML的简写。这种技术能够想服务器请求额外的数据而无须卸载页面(即刷新)，会带来更好的用户体验。一时间，席卷全球。**



**一．** **XMLHttpRequest对象**

**Ajax技术核心是XMLHttpRequest对象(
简称XHR)，这是由微软首先引入的一个特性，其他浏览器提供商后来都提供了相同的实现。在XHR出现之前，Ajax式的通信必须借助一些hack手段来实现，大多数是使用隐藏的框架或内嵌框架。**

**XHR的出现，提供了向服务器发送请求和解析服务器响应提供了流畅的接口。能够以异步方式从服务器获取更多的信息，这就意味着，用户只要触发某一事件，在不刷新网页的情况下，更新服务器最新的数据。**

**虽然Ajax中的x代表的是XML，但Ajax通信和数据格式无关，也就是说这种技术不一定使用XML。**

**IE7+、Firefox、Opera、Chrome和Safari都支持原生的XHR对象，在这些浏览器中创建XHR对象可以直接实例化XMLHttpRequest即可。**

**XMLHttpRequest()创建xhr对象**

[code]

     var xhr = new XMLHttpRequest();   //创建xhr对象
    alert(xhr);    //打印对象
[/code]

**如果是IE6及以下，那么我们必须还需要使用ActiveX对象通过MSXML库来实现。在低版本IE浏览器可能会遇到三种不同版本的XHR对象，即MSXML2.XMLHttp、MSXML2.XMLHttp.3.0、MSXML2.XMLHttp.6.0。我们可以编写一个函数。**

**兼容IE低版本创建 **xhr对象****

[code]

     var xhr = new createXHR(); //执行兼容IE低版本创建xhr对象函数
    alert(xhr); //打印xhr对象
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
[/code]



**创建了XHR对象，在使用XHR对象时，先必须调用open()方法，它接受三个参数：要发送的请求类型(get、post)、请求的URL和表示是否异步。**

**open()方法，准备发送http请求，3个参数，参数1请求类型get或post，参数2请求的url可以是动态的也可以是静态的（如：demo.php，demo.html）,参数3表示是否异步/false同步/true异步**  
 **使用方式：**  
 **XHR对象.open('get','demo.php',false)**

[code]

     var xhr = new createXHR(); //执行兼容IE低版本创建xhr对象函数
    //open()方法，准备发送http请求，3个参数，参数1请求类型get或post，参数2请求的url可以是动态的也可以是静态的（如：demo.php，demo.html）,参数3表示是否异步/false同步/true异步
    xhr.open('get','demo.html',false);  //准备发送
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
[/code]

**open()方法并不会真正发送请求，而只是启动一个请求以备发送。通过send()方法进行发送请求，send()方法接受一个参数，作为请求主体发送的数据。如果不需要则，必须填null。执行send()方法之后，请求就会发送到服务器上。**

**send()方法方法，发送http请求，1个参数，请求主体发送的数据,如果不需要则，必须填null**  
 **使用方式：**  
 **XHR对象.send(null)**

[code]

     var xhr = new createXHR(); //执行兼容IE低版本创建xhr对象函数
    //open()方法，准备发送http请求，3个参数，参数1请求类型get或post，参数2请求的url可以是动态的也可以是静态的（如：demo.php，demo.html）,参数3表示是否异步/false同步/true异步
    xhr.open('get','demo.py',false);  //准备发送
    //send()方法方法，发送http请求，1个参数，请求主体发送的数据,如果不需要则，必须填null
    xhr.send(null); //发送请求
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
[/code]



**当send()方法请求发送到服务器端，收到响应后，响应的数据会自动填充XHR对象的属性。那么一共有四个属性：**



**属性名**

|

**说明**  
  
---|---  
  
**responseText**

|

**作为响应主体被返回的文本**  
  
**responseXML**

|

**如果响应主体内容类型是"text/xml"或"application/xml"，则返回包含响应数据的XML DOM文档**  
  
**status**

|

**响应的HTTP状态**  
  
**statusText**

|

**HTTP状态的说明**  
  
**接受响应之后，第一步检查status属性，以确定响应已经成功返回。一般以HTTP状态代码为200作为成功的标志。除了成功的状态代码，还有一些别的：**

**HTTP状态码**

|

**状态字符串**

|

**说明**  
  
---|---|---  
  
**200**

|

**OK**

|

**服务器成功返回了页面**  
  
**400**

|

**Bad Request**

|

**语法错误导致服务器不识别**  
  
**401**

|

**Unauthorized**

|

**请求需要用户认证**  
  
**404**

|

**Not found**

|

**指定的URL在服务器上找不到**  
  
**500**

|

**Internal Server Error**

|

**服务器遇到意外错误，无法完成请求**  
  
**503**

|

**ServiceUnavailable**

|

**由于服务器过载或维护导致无法完成请求**  
  
**responseText属性，作为响应主体被返回的文本**

[code]

     var xhr = new createXHR(); //执行兼容IE低版本创建xhr对象函数
    //open()方法，准备发送http请求，3个参数，参数1请求类型get或post，参数2请求的url可以是动态的也可以是静态的（如：demo.php，demo.html）,参数3表示是否异步/false同步/true异步
    xhr.open('get','demo.html',false);  //准备发送
    //send()方法方法，发送http请求，1个参数，请求主体发送的数据,如果不需要则，必须填null
    xhr.send(null); //发送请求
    //responseText属性，作为响应主体被返回的文本
    alert(xhr.responseText);
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
[/code]

**其他属性见上表，同理**



**动态获取请求数据，结合点击事件**

[code]

    addEvent(document, 'click',  function () {  //执行添加事件函数，添加一个点击事件，点击页面时激发函数
        var xhr = new createXHR();  //执行兼容IE低版本创建xhr对象函数
        xhr.open('get', 'demo.html', false);    //设置了同步，准备请求
        xhr.send(null);  //发送请求
        if (xhr.status == 200) {                    //如果返回成功了，判断状态码是否等于200
            alert(xhr.responseText);                //调出服务器返回的数据
        } else {
            alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
        }
    });
    
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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



****open()方法** 异步调用【常用】**

**同步调用固然简单，但使用异步调用才是我们真正常用的手段。
使用异步调用的时候，需要触发readystatechange事件，然后检测readyState属性即可。这个属性有五个值：**

**readyState属性**

**值**

|

**状态**

|

**说明**  
  
---|---|---  
  
**0**

|

**未初始化**

|

**尚未调用open()方法**  
  
**1**

|

**启动**

|

**已经调用open()方法，但尚未调用send()方法**  
  
**2**

|

**发送**

|

**已经调用send()方法，但尚未接受响应**  
  
**3**

|

**接受**

|

**已经接受到部分响应数据**  
  
**4**

|

**完成**

|

**已经接受到全部响应数据，而且可以使用**  
  
**异步调用**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('get', 'demo.html', true); //open()方法异步调用,准备请求
        xhr.send(null);  //发送请求
        xhr.onreadystatechange = function () {  //当请求时执行函数
            if (xhr.readyState == 4) {  //判断已经接受到全部响应数据，而且可以使用
                if (xhr.status == 200) {  //判断状态码为200
                    alert(xhr.responseText); //获取请求页面内容
                } else {
                    //否则打印错误
                    alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
                }
            }
        };
    });
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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

**PS：使用abort()方法可以取消异步请求，放在send()方法之前会报错。放在responseText之前会得到一个空值。**



**注意如果请求的url是动态页面，获取页面数据时，不是实时的解决方式**

[code]

    xhr.open('get', 'demo.php?rand=' + Math.random(),  true);
[/code]



**二．** **GET** **与POST**

**在提供服务器请求的过程中，有两种方式，分别是：GET和POST。在Ajax使用的过程中，GET的使用频率要比POST高。**

**在web程序上，GET一般是URL提交请求，比如：demo.php?name=lee &age=100**  
 **POST一般是表单提交，比如： <form method="post">...**

**在了解这两种请求方式前，我们先了解一下HTTP头部信息，包含服务器返回的响应头信息和客户端发送出去的请求头信息。我们可以获取响应头信息或者设置请求头信息。我们可以在Firefox浏览器的firebug查看这些信息。**

**两种头信息**

**响应头信息：服务器返回的信息，客户端可以获取，但不可以设置**  
 **请求头信息：客户端发送的信息，客户端可以设置，但不可以获取**

**获取响应头信息**

**getAllResponseHeaders()方法，获取整个响应头信息**  
 **使用方式**  
 **xhr对象.getAllResponseHeaders()**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('get', 'demo.html', true); //open()方法异步调用,准备请求
        xhr.send(null);  //发送请求
        xhr.onreadystatechange = function () {  //当请求时执行函数
            if (xhr.readyState == 4) {  //判断已经接受到全部响应数据，而且可以使用
                if (xhr.status == 200) {  //判断状态码为200
                    
                    alert(xhr.getAllResponseHeaders()); //getAllResponseHeaders()方法，获取整个响应头信息
                    
                } else {
                    //否则打印错误
                    alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
                }
            }
        };
    });
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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



**getResponseHeader()方法，获取单个响应头信息,参数是要获取头信息的名称**  
 **使用方式**  
 **xhr对象.getResponseHeader('要获取头信息的名称')**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('get', 'demo.html', true); //open()方法异步调用,准备请求
        xhr.send(null);  //发送请求
        xhr.onreadystatechange = function () {  //当请求时执行函数
            if (xhr.readyState == 4) {  //判断已经接受到全部响应数据，而且可以使用
                if (xhr.status == 200) {  //判断状态码为200
    
                    alert(xhr.getResponseHeader('Content-Type')); //getResponseHeader()方法，获取单个响应头信息,参数是要获取头信息的名称
    
                } else {
                    //否则打印错误
                    alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
                }
            }
        };
    });
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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



**设置单个请求头信息**

**setRequestHeader()方法，设置单个请求头信息,两个参数，要设置的头信息名称和值**  
 **使用方式**  
 **xhr对象.setRequestHeader('头信息名称','值')**

**注意：放在open方法之后，send方法之前**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('get', 'demo.html', true); //open()方法异步调用,准备请求
    
        //setRequestHeader()方法，设置单个请求头信息,两个参数，要设置的头信息名称和值
        xhr.setRequestHeader('MyHeader', 'Lee');        //放在open方法之后，send方法之前
        
        xhr.send(null);  //发送请求
        xhr.onreadystatechange = function () {  //当请求时执行函数
            if (xhr.readyState == 4) {  //判断已经接受到全部响应数据，而且可以使用
                if (xhr.status == 200) {  //判断状态码为200
                    //alert(xhr.getAllResponseHeaders()); //获取整个响应头信息
                } else {
                    //否则打印错误
                    alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
                }
            }
        };
    });
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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

**PS：我们只可以获取服务器返回回来响应头信息，无法获取向服务器提交的请求头信息，自然自定义的请求头，在JavaScript端是无法获取到的。**





**GET请求**

**GET请求是最常见的请求类型，最常用于向服务器查询某些信息。必要时，可以将查询字符串参数追加到URL的末尾，以便提交给服务器。**

[code]

    xhr.open('get', 'demo.php?rand=' + Math.random() + '&name=Koo',  true);
[/code]

**通过URL的末尾提交数据，可以通过动态页面获取提交的数据**



**通过URL后的问号给服务器传递键值对数据，服务器接收到返回响应数据。特殊字符传参产生的问题可以使用encodeURIComponent()进行编码处理，中文字符的返回及传参，可以将页面保存和设置为utf-8格式即可。**

[code]

     var url = 'demo.php?rand=' + Math.random();
    url = addURLParam(url,'name','lguix');
    url = addURLParam(url,'aeg',100);
    
    //一个通用的URL提交函数
    function addURLParam(url, name, value) {
        url += (url.indexOf('?') == -1 ? '?' : '&');            //判断的url是否有已有参数
        url += encodeURIComponent(name) + '=' + encodeURIComponent(value);
        alert(url);
        return url;
    }
[/code]

**PS：当没有encodeURIComponent()方法时，在一些特殊字符比如“ &”，会出现错误导致无法获取。**



**POST请求**

**POST请求可以包含非常多的数据，我们在使用表单提交的时候，很多就是使用的POST传输方式。**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('post', 'demo.php', true); //open()方法异步调用,准备请求
[/code]

**而发送POST请求的数据，不会跟在URL的尾巴上，而是通过send()方法向服务器提交数据。**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    addEvent(document, 'click', function () {  //执行添加事件函数，添加一个点击事件，点击页面后执行函数
        var xhr = new createXHR();  //执行创建XHR对象函数，创建XHR对象
        xhr.open('post', 'demo.php', true); //open()方法异步调用,准备请求
        xhr.send('name=Lee&age=100'); //发送
[/code]

**一般来说，向服务器发送POST请求由于解析机制的原因，需要进行特别的处理。因为POST请求和Web表单提交是不同的，需要使用XHR来模仿表单提交。**

**修改响应头信息来模拟**

[code]

    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
[/code]

**PS：从性能上来讲POST请求比GET请求消耗更多一些，用相同数据比较，GET最多比POST快两倍。**



**上一节课的JSON也可以使用Ajax来回调访问。**

[code]

     var url = 'demo.json?rand=' + Math.random();
    var box = JSON.parse(xhr.responseText);
[/code]



**三．** **封装Ajax**

**因为Ajax使用起来比较麻烦，主要就是参数问题，比如到底使用GET还是POST；到底是使用同步还是异步等等，我们需要封装一个Ajax函数，来方便我们调用。**



[code]

    //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    
    //封装ajax
    function ajax(obj) {  //接收数据对象
        var xhr = new createXHR();  //执行创建xhr对象函数
        //数据对象里的url加上?rand=，在加上Math.random()
        obj.url = obj.url + '?rand=' + Math.random();
        //数据对象里的data键和值对象，执行名值对编码函数
        obj.data = params(obj.data); //接收名值对编码后并且格式化分隔符后的数组
        //判断发送方式是否是get，url里的？索引位置是否是负一。如果不是执行后面
        if (obj.method === 'get') obj.url = obj.url.indexOf('?') == -1 ? obj.url + '?' + obj.data : obj.url + '&' + obj.data;
        //判断发送模式如果是异步
        if (obj.async === true) {
            //添加一个加载事件
            xhr.onreadystatechange = function () {
                //判断已经接受到全部响应数据，而且可以使用
                if (xhr.readyState == 4) callback(); //执行callback()函数
            };
        }
        xhr.open(obj.method, obj.url, obj.async);
        if (obj.method === 'post') {
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(obj.data);
        } else {
            xhr.send(null);
        }
        if (obj.async === false) {
            callback();
        }
        function callback() { //callback()函数
            if (xhr.status == 200) {  //判断状态码如果是200
                //将获取到的页面内容，传入回调函数
                obj.success(xhr.responseText);            //回调
            } else {
                alert('数据返回失败！状态代码：' + xhr.status + '状态信息：' + xhr.statusText);
            }
        }
    }
    
    //调用ajax
    addEvent(document, 'click', function () {        //IE6需要重写addEvent
        ajax({  //数据对象
            method: 'get',     //执行ajax封装函数，将一个对象传入封装函数
            url: 'demo.html',   //请求url
            data: {
                'name': 'Lee',  //url键值
                'age': 100     //url键值
            },
            success: function (text) {  //接收回调函数
                alert(text);  //打印回调返回的内容
            },
            async: true  //true异步调用
        });
    });
    
    //名值对编码
    function params(data) {  //接收数据对象里的data键和值对象
        var arr = []; //创建数组
        for (var i in data) { //循环数据对象里的data键和值对象
            //将每次循环的对象名称 = 加上 对应名称的值，添加到arr数组
            arr.push(encodeURIComponent(i) + '=' + encodeURIComponent(data[i]));
        }
        return arr.join('&');  //将数组格式化分隔符后返回
    }
    
    
    //兼容IE低版本创建xhr对象,函数
    function createXHR() {
        if (typeof XMLHttpRequest != 'undefined') {   //判断XMLHttpRequest创建xhr对象是否支持，
            return new XMLHttpRequest();  //如果支持，创建xhr对象返回
        } else if (typeof ActiveXObject != 'undefined') { //如果不支持，判断IE低版本的3种模式是否支持
            var versions = [  //数组，3种模式
                'MSXML2.XMLHttp.6.0',
                'MSXML2.XMLHttp.3.0',
                'MSXML2.XMLHttp'
            ];
            for (var i = 0; i < versions.length; i++) {   //循环3种模式
                try {
                    return new ActiveXObject(version[i]);  //尝试每次循环的IE模式执行返回
                } catch (e) {
                    //跳过
                }
            }
        } else {  //如果上面两种都不能创建xhr对象
            //创建错误对象，抛出错误
            throw new Error('您的浏览器不支持XHR对象！');
        }
    }
    
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

**PS：封装Ajax并不是一开始就形成以上的形态，需要经过多次变化而成。**

