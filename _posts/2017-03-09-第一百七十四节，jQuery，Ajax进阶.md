---
layout: post
title: " 第一百七十四节，jQuery，Ajax进阶 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，Ajax进阶**



**学习要点：**

**1.加载请求**

**2.错误处理**

**3.请求全局事件**

**4.JSON 和 JSONP**

**5.jqXHR 对象**



**在 Ajax 课程中，我们了解了最基本的异步处理方式。本章，我们将了解一下 Ajax 的 一些全局请求事件、跨域处理和其他一些问题。**



**一．加载请求**

**在 Ajax 异步发送请求时，遇到网速较慢的情况，就会出现请求时间较长的问题。而超
过一定时间的请求，用户就会变得不再耐烦而关闭页面。而如果在请求期间能给用户一些提
示，比如：正在努力加载中...，那么相同的请求时间会让用户体验更加的好一些。**

**jQuery 提供了两个全局事件，.ajaxStart()和.ajaxStop()。这两个全局事件，只要用户触发 了
Ajax，请求开始时（未完成其他请求）激活.ajaxStart()，请求结束时（所有请求都结束了） 激活.ajaxStop()。**

**ajaxStart()方法，请求开始时（未完成其他请求）激活.ajaxStart()，在document上使用，参数是匿名函数，可以在函数里做请求时的提示和操作**

  
**ajaxStop()方法，请求结束时（所有请求都结束了）激活.ajaxStop()，在document上使用，参数是匿名函数，可以在函数里做请求结束的提示和操作**

[code]

         //ajax请求
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'http://www.test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                }
            });
        });
    
        //监测ajax请求
        $(document).ajaxStart(function () {  //未完成请求时
            $('span').show();  //显示正在请求，请稍等
        }).ajaxStop(function () {  //请求结束时
            $('span').hide();  //隐藏请求提示元素
        });
[/code]



**如果请求时间太长，可以设置超时**

[code]

         //ajax请求
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'http://www.test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                },
                timeout : 500  //如果请求时间太长，可以设置超时
            });
        });
    
        //监测ajax请求
        $(document).ajaxStart(function () {  //未完成请求时
            $('span').show();  //显示正在请求，请稍等
        }).ajaxStop(function () {  //请求结束时
            $('span').hide();  //隐藏请求提示元素
        });
[/code]



**如果某个 ajax 不想触发全局事件，可以设置取消**

[code]

         //ajax请求
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'http://www.test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                },
                global : false  //如果某个 ajax 不想触发全局事件，可以设置取消
            });
        });
    
        //监测ajax请求
        //global : false了就不会触发这两个事件了，这里就不起作用了
        $(document).ajaxStart(function () {  //未完成请求时
            $('span').show();  //显示正在请求，请稍等
        }).ajaxStop(function () {  //请求结束时
            $('span').hide();  //隐藏请求提示元素
        });
[/code]



**二．错误处理**

**Ajax 异步提交时，不可能所有情况都是成功完成的，也有因为代码异步文件错误、网
络错误导致提交失败的。这时，我们应该把错误报告出来，提醒用户重新提交或提示开发者 进行修补。**

**  在之前高层封装中是没有回调错误处理的，比如$.get()、$.post()和.load()。所以，早期
的方法通过全局.ajaxError()事件方法来返回错误信息。而在 jQuery1.5 之后，可以通过连缀
处理使用局部.error()方法即可。而对于$.ajax()方法，不但可以用这两种方法，还有自己的属 性方法 error : function ()
{}。**



**$.ajax()使用属性提示错误,error : function () {}。**

[code]

         //ajax请求
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                },
                error: function (xhr, errorText, errorStatus) {  //如果发生错误，返回错误信息
                    alert(xhr.statusText + ':' + xhr.status);
                }
            });
        });
[/code]



**error()方法提示错误**

******fail() ** **.方法将取代 **error()，请求失败时调用的回调函数，接收三个形式参数xhr, status,
info************



**$.post()使用连缀.error()方法提示错误，连缀方法将被.fail()取代**

[code]

        $('form input[type=button]').click( function () {
            $.post('ttttest.php').error(function (xhr, status, info) {  //如果出现错误打印错误信息
                alert(xhr.status + ':' + xhr.statusText);
            });
        });
[/code]



**ajaxError()全局事件提示错误,在document上使用，参数是一个匿名函数，函数接收4个形式参数，event对象, xhr通讯对象,
settings, infoError**

**$.post()使用全局.ajaxError()事件提示错误**

[code]

         //ajax请求
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                }
            });
        });
    
        //ajaxError()全局事件提示错误,在document上使用，参数是一个匿名函数，函数接收4个形式参数，event对象, xhr通讯对象, settings, infoError
        $(document).ajaxError(function (event, xhr, settings, infoError) {
            alert(xhr.status + ':' + xhr.statusText);
            alert(settings + ':' + infoError);
        });
[/code]



**三．请求全局事件**

**jQuery 对于 Ajax 操作提供了很多全局事件方法，.ajaxStart()、.ajaxStop()、.ajaxError()
等事件方法。他们都属于请求时触发的全局事件，除了这些，还有一些其他全局事件：**

**注意：全局事件方法是所有 Ajax 请求都会触发到，并且只能绑定在 document 上。而局 部方法，则针对某个 Ajax。
对于一些全局事件方法的参数，大部分为对象，而这些对象有哪些属性或方法能调用， 可以通过遍历方法得到。**



**ajaxSuccess()，对应一个局部方法：.success()，请求成功完成时执行。请求成功时执行**

[code]

         //$.post()使用全局事件方法.ajaxSuccess()
        $('form input[type=button]').click(function () {
            $.post('test.php', $('form').serialize(), function (response, status, xhr) {
                $('#box').html(response);
            });
        });
        //使用全局事件方法.ajaxSuccess()
        $(document).ajaxSuccess(function (event, xhr, settings) {
            alert(xhr.responseText);
        });
[/code]

****success() **Ajax局部方法， **请求成功完成时执行。请求成功时执行********

**************done().方法将取代 **success()，请求成功后调用的回调函数，接收三个形式参数response, status,
xhr【推荐】****************

[code]

         //$.post()使用局部方法.success()
        $('form input[type=button]').click(function () {
            $.post('test.php', $('form').serialize(), function (response, status, xhr) {
                $('#box').html(response);
            }).success(function (response, status, xhr) {   //success()Ajax局部方法，请求成功完成时执行。请求成功时执行
                alert(response);
            });
        });
[/code]





**ajaxComplete()，对应一个局部方法：.complete()，请求完成后注册一个回调函数。请求完成无论成功失败都执行**

[code]

        $('form input[type=button]').click( function () {
            $.post('test.php', $('form').serialize(), function (response, status, xhr) {
                alert('成功');
            });
        });
        //$.post()请求完成的全局方法.ajaxComplete()
        $(document).ajaxComplete(function (event, xhr, settings) {
            alert('完成');
        });
[/code]

****complete() ** ** **Ajax局部方法， **请求完成无论成功失败都执行************

****************always() ** **.方法将取代
**complete()，请求完成后调用的回调函数，接收三个形式参数response, status,
xhr【推荐】**********************

[code]

         //$.post()请求完成的局部方法.complete()
        $('form input[type=button]').click(function () {
            $.post('test.php', $('form').serialize(), function (response, status, xhr) {
                alert('成功');
            }).complete(function (xhr, status) {  //complete()Ajax局部方法，请求完成无论成功失败都执行
                alert('完成');
            });
        });
[/code]



**ajaxSend()，没有对应的局部方法，只有属性 beforeSend，请求发送之前要绑定的函数。请求之前执行**

[code]

        $('form input[type=button]').click( function () {
            $.post('test.php', $('form').serialize(), function (response, status, xhr) {
                alert('成功');
            });
        });
        //$.post()请求发送之前的全局方法.ajaxSend()
        $(document).ajaxSend(function (event, xhr, settings) {
            alert('发送请求之前');
        });
[/code]

**beforeSend， ** ** ** ** **Ajax局部 **属性， **请求之前执行****************

[code]

         //$.ajax()方法，可以直接通过属性设置即可。
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'test.php',
                data: $('form').serialize(),
                success: function (response, status, xhr) {
                    $('#box').html(response);
                },
                complete: function (xhr, status) {
                    alert('完成' + ' - ' + xhr.responseText + ' - ' + status);
                },
                beforeSend: function (xhr, settings) {   //beforeSend，Ajax局部属性，请求之前执行
                    alert('请求之前' + ' - ' + xhr.readyState + ' - ' + settings.url);
                }
            });
    
        });
[/code]

**  注意：在 jQuery1.5 版本以后，使用.success()、.error()和.complete()连缀的方法，可以
用.done()、.fail()和.always()取代。**



**四．JSON 和 JSONP**

**如果在同一个域下，$.ajax()方法只要设置 dataType 属性即可加载 JSON 文件。而在非 同域下，可以使用
JSONP，但也是有条件的。**

**ajax()同一个域下加载 JSON 文件**

[code]

        $('form input[type=button]').click( function () {
            $.ajax({
                type: 'POST',
                url: 'test.json',
                dataType: 'json',
                success: function (response, status, xhr) {
                    alert(response[0].url);
                }
            });
    
        });
[/code]



**如果想跨域操作文件的话，我们就必须使用 JSONP。JSONP(JSON with Padding)是一个 非官方的协议，它允许在服务器端集成
Script tags 返回至客户端，通过 javascript callback 的 形式实现跨域访问（这仅仅是 JSONP 简单的实现形式）。**

**跨域的 PHP 端文件**

[code]

    <? php
        $arr = array('a'=>1,'b'=>2,'c'=>3,'d'=>4,'e'=>5);
        $result = json_encode($arr);
        $callback = $_GET['callback'];  //这里是通讯契约
        echo $callback."($result)";
    ?>
[/code]

**$.getJSON()方法跨域获取 JSON**

[code]

        $.getJSON('http://www.li.cc/test.php?callback=?',  function (response) {  //必须传递契约
            console.log(response);
        });
[/code]

**ajax()方法跨域获取 JSON**

[code]

        $.ajax({
            url:  'http://www.li.cc/test.php?callback=?',
            dataType: 'json',  //必须指定类型
            success: function (response, status, xhr) {
                console.log(response);
                alert(response.a);
            }
        });
[/code]

**注意：跨域获取必须传递契约**



**JSONP，数据类型dataType: 'jsonp'，这种类型不需要传递契约【重点】**

[code]

         //跨域获取 JSON
        $('form input[type=button]').click(function () {
            $.ajax({
                type: 'POST',
                url: 'http://www.li.cc/test.php',
                dataType: 'jsonp',   //JSONP，数据类型dataType: 'jsonp'，这种类型不需要传递契约
                success: function (response, status, xhr) {
                    alert(response);
                }
            });
    
        });
[/code]



**五．jqXHR 对象【推荐】**

**在之前，我们使用了局部方法：.success()、.complete()和.error()。这三个局部方法并不 是 XMLHttpRequest
对象调用的，而是$.ajax()之类的全局方法返回的对象调用的。这个对象， 就是 jqXHR 对象，它是原生对象 XHR 的一个超集。**

**jqXHR就是$.ajax()返回的本身对象**

[code]

        $('form input[type=button]').click( function () {
            var jqXHR = $.ajax({
                type: 'POST',
                url: 'test.php',
                data: $('form').serialize() //表单序列化
            });
            //此时的jqXHR就是ajax的返回对象,后面还可以连缀
            jqXHR.done(function (response, status, xhr) {
                alert(response + '1')
            }).done(function (response, status, xhr) {
                alert(response + '2')
            });
    
        });
[/code]



**注意：如果使用 jqXHR 对象的话，那么建议用.done()、.always()和.fail()代
替.success()、.complete()和.error()。以为在未来版本中，很可能将这三种方法废弃取消 。**

****done().方法将取代 **success()，请求成功后调用的回调函数，接收三个形式参数response, status, xhr******

****always() ** **.方法将取代 **complete()，请求完成后调用的回调函数，接收三个形式参数response, status,
xhr**********

****fail() ** **.方法将取代 **error()，请求失败时调用的回调函数，接收三个形式参数xhr, status,
info**********



**使用 jqXHR 的连缀方式比$.ajax()的属性方式有三大好处： 1.可连缀操作，可读性大大提高； 2.可以多次执行同一个回调函数；
3.为多个操作指定回调函数；**



**多个操作指定回调函数**

**when()全局方法，可以接收多个jqXHR对象处理，参数是要处理的，jqXHR对象，在方法的匿名函数里接收处理**

[code]

         var jqXHR = $.ajax('test.php');
        var jqXHR2 = $.ajax('test2.php');
        $.when(jqXHR, jqXHR2).done(function (r1, r2) {
            alert(r1[0]);
            alert(r2[0]);
        });
[/code]



