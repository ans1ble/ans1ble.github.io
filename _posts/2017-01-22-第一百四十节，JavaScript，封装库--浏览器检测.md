---
layout: post
title: " 第一百四十节，JavaScript，封装库--浏览器检测 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--浏览器检测**

**在函数库编写一个，浏览器检测对象**

[code]

     /** sys浏览器检测对象，对象下有两个属性，liu_lan_qi属性和xi_tong属性
     * liu_lan_qi属性，检测浏览器名称和版本号，如：alert(sys.liu_lan_qi);
     * xi_tong属性，检测浏览器运行环境，如：alert(sys.xi_tong);
     **/
    (function () {                       //闭包，自我执行
        window.sys = {};                  //全局变量对象，保存浏览器信息
        var ua = navigator.userAgent.toLowerCase();           //获取浏览器信息，并转化成小写
        var s = [];                                           //浏览器信息数组
        /**判断IE浏览器**/
        if ((/msie ([\d.]+)/).test(ua)) {                      //IE10以下判断字段为：msie x版本号
            s = ua.match(/msie ([\d.]+)/);                    //如果有获取到msie x版本号返回数组
            sys.liu_lan_qi = '浏览器为IE：' + s[1];            //向sys对象添加liu_lan_qi属性，属性值等于获取到的数组第二个元素
        } else if ((/trident/).test(ua)) {                      //ie10以上判断字段为：trident
            s = ua.match(/rv:([\d.]+)/);                      //如果有获取到trident字段返回数组
            sys.liu_lan_qi = '浏览器为IE：' + s[1];
        }
        /**判断火狐浏览器**/
        if ((/firefox\/([\d.]+)/).test(ua)) {                  //火狐判断字段为：firefox
            s = ua.match(/firefox\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为firefox：' + s[1];
        }
        /**判断谷歌浏览器**/
        if ((/chrome\/([\d.]+)/).test(ua)) {                    //谷歌判断字段为：chrome
            s = ua.match(/chrome\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为chrome：' + s[1];
        }
        /**判断Opera浏览器**/
        if ((/opera\/.*version\/([\d.]+)/).test(ua)) {         //谷歌判断字段为：opera 与 version
            s = ua.match(/opera\/.*version\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为Opera：' + s[1];
        }
        /**判断Opera浏览器**/
        if ((/version\/([\d.]+).*safari/).test(ua)) {         //谷歌判断字段为：version 与 safari
            s = ua.match(/version\/([\d.]+).*safari/);
            sys.liu_lan_qi = '浏览器为Opera：' + s[1];
        }
        /**判断系统**/
        if (Boolean(navigator.platform)) {
            sys.xi_tong = '环境系统为：' + navigator.platform;
        } else {
            alert("无法检测到环境系统")
        }
    })();
[/code]



**前台js代码**

[code]

        alert(sys.liu_lan_qi);
        alert(sys.xi_tong);
[/code]



