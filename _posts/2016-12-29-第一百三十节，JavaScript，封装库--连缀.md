---
layout: post
title: " 第一百三十节，JavaScript，封装库--连缀 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--连缀**





**学习要点：**

**1.连缀介绍**

**2.改写库对象**



**本章我们重点来介绍，在调用库的时候，我们需要能够在前台调用的时候可以同时设置多个操作，比如设置CSS，设置innerHTML，设置click事件等等。那么本节课来讨论这个问题。**



**一．** **连缀介绍**

**所谓连缀，最简单的理解就是一句话同时设置一个或多个节点两个或两个以上的操作。比如：**

[code]

    $().getId('box').css('color', 'red').html('标题').click( function () {alert('a')});
[/code]

**连缀的好处，就是快速方便的设置节点的操作。**



**二．** **改写库对象**

**如果是实现操作连缀，那么我们就需要改写上一节课的对象写法：var Base = {}，这种写法无法在它的原型中添加方法，所以需要使用函数式对象写法：**

**封装库代码**

[code]

     /**
     *feng_zhuang_ku_1.0版本，js封装库，2016/12/29日：林贵秀
     **/
    
    /** 每次调用$创建库对象,使其每次调用都是独立的对象
     **/
    var $ = function () {
        return new feng_zhuang_ku();
    };
    
    /**
     *定义封装库构造函数，创建库对象
     **/
    function feng_zhuang_ku () {
        /**对象说明：
         * this表示对象本身
         * 使用库，首先要  var $ = new feng_zhuang_ku();   首先要new创建对象
         * 再在创建的对象下调用方法或者属性
         * 
         * 大纲：
         * 获取元素标签开始，行号18
         * 连缀-元素节点操作开始，行号64
         * 
         * 
         **/
    
    
        /**------------------------------------------------获取元素标签开始--------------------------------------------**/
        /**获取元素标签说明：
         * jie_dian属性，保存获取到的元素节点，返回数组,
         * huo_qu_id()方法，通过id获取元素标签，适用于获取单个节点，
         * huo_qu_name_zhi()方法，通过元素name值获取指定元素，适用于获取表单元素,
         * huo_qu_name()方法，通过标签名称获取相同标签名的元素，适用于获取多个相同元素节点,
         **/
    
    
        /** jie_dian属性，创建数组，初始化，保存获取到的元素节点，返回数组
         **/
        this.jie_dian = [];
    
        /** huo_qu_id()方法,通过id获取元素标签，参数是id值，将获取到的元素对象添加到，jie_dian属性,适用于获取单个节点
         **/
        this.huo_qu_id = function (id) {
            this.jie_dian.push(document.getElementById(id));
            return this;
        };
    
        /** huo_qu_name_zhi()方法，通过元素name值获取指定元素，参数是元素name值，返回元素相同name值对象集合，
         * 循环元素集合，将每次循环到的元素对象添加到 jie_dian属性，适用于获取表单元素
         **/
        this.huo_qu_name_zhi = function (name) {
            var name_zhi = document.getElementsByName(name);
            for (var i = 0; i < name_zhi.length; i ++){
               this.jie_dian.push(name_zhi[i]);
            }
            return this;
        };
    
        /** huo_qu_name()方法，通过标签名称获取相同标签名的元素，参数是标签名称，返回对象集合
         * 循环元素集合，将每次循环到的元素对象添加到 jie_dian属性，适用于获取多个相同元素节点
         **/
        this.huo_qu_name = function (tag) {
            var name = document.getElementsByTagName(tag);
            for (var i = 0; i < name.length; i ++){
                this.jie_dian.push(name[i]);
            }
            return this;
        };
    
        /**------------------------------------------------获取元素标签结束--------------------------------------------**/
    
    
        /**------------------------------------------------连缀-元素节点操作开始---------------------------------------**/
        /**连缀-元素节点操作说明：
         * css()方法，给获取到的元素设置行内css样式
         * wen_ben()方法，给获取到的元素设置文本，参数是要设置的文本字符串
         * click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
         **/
    
    
        /** css()方法，给获取到的元素设置行内css样式,两个参数，参数1样式名称，参数2样式值
         * 循环jie_dian属性里的节点，将每次循环的节点添加css样式
         **/
        this.css = function (attr,value) {
            for (var i = 0; i < this.jie_dian.length; i ++){
                this.jie_dian[i].style[attr] = value;
            }
            return this;
        };
    
        /** wen_ben()方法，给获取到的元素设置文本，参数是要设置的文本字符串，
         * 循环jie_dian属性里的节点，将每次循环的节点添加元素文本
         **/
        this.wen_ben = function (str) {
            for (var i = 0; i < this.jie_dian.length; i ++){
                this.jie_dian[i].innerHTML = str;
            }
            return this;
        };
    
        /** click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
         * 循环jie_dian属性里的节点，将每次循环的节点添加元素点击事件
         **/
        this.click = function (fu) {
            for (var i = 0; i < this.jie_dian.length; i ++){
                this.jie_dian[i].onclick = fu;
            }
            return this;
        };
        /**------------------------------------------------连缀-元素节点操作结束---------------------------------------**/
    }
[/code]

**前台调用代码**

[code]

     //前台调用代码
    window.onload = function (){
        $().huo_qu_name('div').css('background-color','#ffff3e');
        $().huo_qu_name('p').css('color','#ff2128').css('background-color','#b2bbff').wen_ben('改变').click(function () {
            alert('a');
        });
    };
[/code]



