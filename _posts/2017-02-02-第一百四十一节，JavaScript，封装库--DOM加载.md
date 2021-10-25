---
layout: post
title: " 第一百四十一节，JavaScript，封装库--DOM加载 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--DOM加载**

****DOM加载，跨浏览器封装 **DOM加载，当网页文档结构加载完毕后执行函数，不等待图片音频视频等文件加载完毕******

[code]

     /** dom_jia_zai()函数，DOM页面加载函数，等待页面结构加载完毕后就执行函数，不需要等待页面音频视频等文件加载完毕，提高加载速度
     * 参数是页面结构加载完毕后要执行的函数
     * 一般前写前台js文件时，使用此方法加载DOM页面后执行代码，提高速度
     **/
    function dom_jia_zai(fn){
        var isReady = false;
        var timer = null;
        function doReady(fn) {
            if(timer) clearInterval(timer);
            if (isReady) return;
            isReady = true;
            fn();
        }
        if ((sys.opera && sys.opera < 9) || (sys.firefox && sys.firefox < 3) || (sys.webkit && sys.webkit < 525)){
            timer = setInterval(function () {
                if (document && document.getElementById && document.getElementsByTagName && document.body) {
                    doReady();
                }
            }, 1);
        }else if(document.addEventListener){
            addEvent(document, 'DOMContentLoaded', function () {                  //页面结构树加载完毕后执行函数，不会等待音频视频等文件加载完毕
                fn();
                removeEvent(document, 'DOMContentLoaded', arguments.callee);
            });
        }else if(sys.ie && sys.ie < 9){
            var timer = null;
            timer = setInterval(function () {
                try {
                    document.documentElement.doScroll('left');
                    doReady();
                } catch (e) {}
            },1);
        }
    }
[/code]



**前台js 代码**

[code]

    dom_jia_zai( function () {
    alert('111');
    
    });
[/code]



