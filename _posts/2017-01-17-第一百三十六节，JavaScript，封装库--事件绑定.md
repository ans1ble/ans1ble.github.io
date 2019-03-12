
---
layout: post
title: " 第一百三十六节，JavaScript，封装库--事件绑定 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，封装库--事件绑定**



**在函数库添加两个函数**

****添加事件绑定函数****

****删除 ** **事件绑定函数********



************添加事件绑定函数************

[code]

     /** addEvent()函数库函数，跨浏览器添加事件绑定,注意：传入事件名称时不要on
     * 接收3个参数
     * 参数1要绑定事件的元素对象，
     * 参数2事件名称，也就是什么事件，注意：传入事件名称时不要on
     * 参数3接收的事件执行函数
     * 注意：一个元素对象，执行了多个相同的事件函数时只执行一次，其他的会被忽略，注意是相同的事件函数
     * 说明：
     * 事件函数里的this，代表绑定事件元素对象本身
     * 事件函数里有一个可选参数e,e接收的元素event对象，传入addEvent()后跨浏览器获取到元素event对象，将元素event对象赋值给e
     * 所以事件函数里的e,代表元素event对象，前提是首先要在事件函数传参e后，再在事件函数里调用e,得到元素event对象
     * e.preventDefault()方法，在事件函数里写e.preventDefault()方法，兼容浏览器阻止事件元素对象默认行为，前提在事件函数要传参e
     * e.stopPropagation()方法，在事件函数里写e.stopPropagation()方法，阻止元素对象的父级元素事件冒泡行为，前提在事件函数要传参e
     **/
    function addEvent(obj, type, fn) {
        if (typeof obj.addEventListener != 'undefined') {
            obj.addEventListener(type, fn, false);
        } else {
            //创建一个存放事件的哈希表(散列表)
            if (!obj.events) obj.events = {};
            //第一次执行时执行
            if (!obj.events[type]) {
                //创建一个存放事件处理函数的数组
                obj.events[type] = [];
                //把第一次的事件处理函数先储存到第一个位置上
                if (obj['on' + type]) obj.events[type][0] = fn;
            } else {
                //同一个注册函数进行屏蔽，不添加到计数器中
                if (addEvent.equal(obj.events[type], fn)) return false;
            }
            //从第二次开始我们用事件计数器来存储
            obj.events[type][addEvent.ID++] = fn;
            //执行事件处理函数
            obj['on' + type] = addEvent.exec;
        }
    }
    /*-------------------------------------------------------------------------------------*/
    //为每个事件分配一个计数器
    //JS一切皆为对象，所以addEvent.ID语法正确，实际上是个全局变量
    addEvent.ID = 1;
    //执行事件处理函数
    addEvent.exec = function (event) {
        var e = event || addEvent.fixEvent(window.event);
        var es = this.events[e.type];
        for (var i in es) {
            es[i].call(this, e);
        }
    };
    //同一个注册函数进行屏蔽
    addEvent.equal = function (es, fn) {
        for (var i in es) {
            if (es[i] == fn) return true;
        }
        return false;
    };
    //把IE常用的Event对象配对到W3C中去
    addEvent.fixEvent = function (event) {
        event.preventDefault = addEvent.fixEvent.preventDefault;
        event.stopPropagation = addEvent.fixEvent.stopPropagation;
        return event;
    };
    //IE阻止默认行为
    addEvent.fixEvent.preventDefault = function () {
        this.returnValue = false;
    };
    //IE取消冒泡
    addEvent.fixEvent.stopPropagation = function () {
        this.cancelBubble = true;
    };
    /*---------------------------------------------------------------------------------------*/
[/code]



****删除 ** **事件绑定函数********

[code]

     /** removeEvent()函数库函数，跨浏览器删除事件绑定,注意：传入事件名称时不要on
     * 接收3个参数
     * 参数1接收事件绑定时的元素对象
     * 参数2接收事件绑定时的事件名称，也就是什么事件，注意：传入事件名称时不要on
     * 参数3接收事件绑定时的执行函数
     **/
    function removeEvent(obj, type, fn) {
        if (typeof obj.removeEventListener != 'undefined') {
            obj.removeEventListener(type, fn, false);
        } else {
            for (var i in obj.events[type]) {
                if (obj.events[type][i] == fn) {
                    delete obj.events[type][i];
                }
            }
        }
    }
[/code]



