---
layout: post
title: " 第一百五十八节，封装库--JavaScript，ajax说明 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，ajax说明**

****封装库** ajax()方法，ajax通讯方法，跨页面向动态页面发送或获取数据**

[code]

    /** ajax()方法，ajax通讯方法，跨页面向动态页面发送或获取数据
     *  参数是一个对象{}，如下
     *  $().ajax({
                method:'post',                  【method】属性，通讯模式，post为post模式，get为get模式
                url:'hj.php',                   【url】属性，发送数据或请求数据的url地址
                data:{                          【data】属性，是发送内容，是一个对象，里面是键值对形式的发送数据对象
                    'name':'lee',
                    'age':100
                },
                success:function (text) {       【success】属性，是一个回调函数，函数参数是text，会接收到发送或者获取到的数据
                    alert(text);
                },
                async:true                      【async】属性，请求方式，true异步方式，false同步方式
            });
     **/
    feng_zhuang_ku.prototype.ajax = function (obj) {
        //创建XHR对象
        var xhr = (function () {
            if (typeof XMLHttpRequest != 'undefined') {           //判断是否可以直接创建XHR对象，w3c
                return new XMLHttpRequest();                      //如果可以就直接创建XHR对象
            } else if (typeof ActiveXObject != 'undefined') {     //判断IE低版本的3种模式是否支持
                var version = [
                    'MSXML2.XMLHttp.6.0',
                    'MSXML2.XMLHttp.3.0',
                    'MSXML2.XMLHttp'
                ];
                for (var i = 0; version.length; i++) {
                    try {
                        return new ActiveXObject(version[i]);
                    } catch (e) {
                        //跳过
                    }
                }
            } else {
                throw new Error('您的系统或浏览器不支持XHR对象！');   //如果都不支持报错
            }
        })();  //自我执行闭包里的函数,创建XHR对象
    
        //接收对象url地址
        obj.url = obj.url + '?rand=' + Math.random();                 //组合对象传进来的通讯url地址
    
        //接收对象传来的内容，进行名值对编码
        obj.data = (function (data) {
            var arr = [];
            for (var i in data) {
                arr.push(encodeURIComponent(i) + '=' + encodeURIComponent(data[i]));
            }
            return arr.join('&');  //将数组格式化分隔符后返回
        })(obj.data);  //自我执行闭包里的函数
    
        //判断请求方式来
        if (obj.method === 'get') obj.url += obj.url.indexOf('?') == -1 ? '?' + obj.data : '&' + obj.data;
    
        //判断发送模式如果是异步
        if (obj.async === true) {
            //添加一个加载事件
            xhr.onreadystatechange = function () {
                //判断已经接受到全部响应数据，而且可以使用
                if (xhr.readyState == 4) {
                    callback();
                }
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
        function callback() {
            if (xhr.status == 200) {
                obj.success(xhr.responseText);            //回调传递参数
            } else {
                alert('获取数据错误！错误代号：' + xhr.status + '，错误信息：' + xhr.statusText);
            }
        }
        return this;
    };
[/code]

前台js

[code]

    //调用ajax
        $(document).on_click(function () {
            $().ajax({
                method:'post',
                url:'hj.php',
                data:{
                    'name':'lee',
                    'age':100
                },
                success:function (text) {
                    alert(text);
                },
                async:true
            });
        });
[/code]

通讯数据url地址hj.php

[code]

    <?php
      echo 'www.jxiou.com';
      print_r($_POST);
    ?>
[/code]

最终回调显示

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170302220215235-348005853.png)

