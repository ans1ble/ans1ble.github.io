---
layout: post
title: " 第一百三十一节，JavaScript，封装库--CSS "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--CSS**

**将封装库里的方法，改成了原型添加方法**

**增加4个方法**

**tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀1**

**yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀2**

**she_zhi_link_css()方法，设置link连接、或style内嵌、中的CSS样式3**

**yi_chu_link_css()方法，移除link连接、或style内嵌、中的CSS样式4**



**封装库代码5**



[code]

    /**
     *feng_zhuang_ku_1.0版本，js封装库，2016/12/29日：林贵秀
     **/
    
    /** 前台调用
     * 每次调用$创建库对象,使其每次调用都是独立的对象
     **/
    var $ = function () {
        return new feng_zhuang_ku();
    };
    
    /**
     *定义封装库构造函数，类库
     **/
    function feng_zhuang_ku() {
        /** jie_dian属性，创建数组，初始化，保存获取到的元素节点，返回数组
         **/
        this.jie_dian = [];
    }
    
    /**对象说明：
     * this表示对象本身
     * 使用库，首先要  $()  创建对象
     * 再在创建的对象下调用方法或者属性
     *
     * 大纲：
     * 获取元素标签开始，行号18
     * 元素节点操作开始，行号64
     *
     *
     **/
    
    
    /**------------------------------------------------获取元素标签开始--------------------------------------------**/
    /**获取元素标签说明：
     * jie_dian属性，保存获取到的元素节点，返回数组,
     * huo_qu_id()方法，通过id获取元素标签，适用于获取单个节点，
     * huo_qu_name_zhi()方法，通过元素name值获取指定元素，适用于获取表单元素,
     * huo_qu_name()方法，通过标签名称获取相同标签名的元素，
     * huo_qu_class()方法，获取相同class属性的节点，将获取到的节点添加到jie_dian属性
     * guo_lv_jie_dian()方法，获取多个节点时，过滤jie_dian属性里的数组，就是过滤掉指定索引外的元素对象
     **/
    
    
    /** huo_qu_id()方法,通过id获取元素标签，参数是id值，将获取到的元素对象添加到，jie_dian属性,适用于获取单个节点
     **/
    feng_zhuang_ku.prototype.huo_qu_id = function (id) {
        this.jie_dian.push(document.getElementById(id));
        return this;
    };
    
    /** huo_qu_name_zhi()方法，通过元素name值获取指定元素，参数是元素name值，返回元素相同name值对象集合，
     * 循环元素集合，将每次循环到的元素对象添加到 jie_dian属性，适用于获取表单元素
     **/
    feng_zhuang_ku.prototype.huo_qu_name_zhi = function (name) {
        var name_zhi = document.getElementsByName(name);
        for (var i = 0; i < name_zhi.length; i++) {
            this.jie_dian.push(name_zhi[i]);
        }
        return this;
    };
    
    /** huo_qu_name()方法，通过标签名称获取相同标签名的元素，
     * 两个参数：获取指定id下的相同标签元素，参数1标签名称，参数2指定区域id值
     * 一个参数：获取页面所有相同标签元素，参数是标签名称
     **/
    feng_zhuang_ku.prototype.huo_qu_name = function (tag, idname) {
        var node = null;
        if (arguments.length == 2) {
            node = document.getElementById(idname);
        } else {
            node = document;
        }
        var name = node.getElementsByTagName(tag);
        for (var i = 0; i < name.length; i++) {
            this.jie_dian.push(name[i]);
        }
        return this;
    };
    
    /** huo_qu_class()方法，获取相同class属性的节点，将获取到的节点添加到jie_dian属性
     * 一个参数：获取整个页面指定的class属性节点，参数是class属性值
     * 两个参数：获取指定id区域里的class属性节点，参数1是class属性值，参数2是指定区域的id值
     **/
    feng_zhuang_ku.prototype.huo_qu_class = function (name, idname) {
        var node = null;
        if (arguments.length == 2) {
            node = document.getElementById(idname);
        } else {
            node = document;
        }
        var all = node.getElementsByTagName('*');
        for (var i = 0; i < all.length; i++) {
            if (all[i].className == name) {
                this.jie_dian.push(all[i]);
            }
        }
        return this;
    };
    
    /** guo_lv_jie_dian()方法，获取多个节点时，过滤jie_dian属性里的数组，就是过滤掉指定索引外的元素对象
     * 参数是要保留jie_dian属性里的对象索引
     **/
    feng_zhuang_ku.prototype.guo_lv_jie_dian = function (num) {
        var element = this.jie_dian[num];
        this.jie_dian = [];
        this.jie_dian[0] = element;
        return this;
    };
    
    /**------------------------------------------------获取元素标签结束--------------------------------------------**/
    
    
    /**------------------------------------------------元素节点操作开始--------------------------------------------**/
    /**素节点操作说明：
     * css()方法，给获取到的元素设置ss样式,或者获取css样式，
     * wen_ben()方法，给获取到的元素设置文本，或者获取文本
     * click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
     * tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀
     * yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀
     * she_zhi_link_css()方法，设置link连接、或style内嵌、中的CSS样式
     * yi_chu_link_css()方法，移除link连接、或style内嵌、中的CSS样式
     **/
    
    
    /** css()方法，给获取到的元素设置ss样式,或者获取css样式，
     * 两个参数：设置样式，参数1样式名称，参数2样式值,设置的行内样式
     * 一个参数：获取样式，参数是样式名称，无法连缀，获取即可用获取行内也可以获取连接
     **/
    feng_zhuang_ku.prototype.css = function (attr, value) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 1) {
                if (typeof window.getComputedStyle != 'undefined') {  //w3c
                    return window.getComputedStyle(this.jie_dian[i], null)[attr];
                } else if (typeof this.jie_dian[i].currentStyle != 'undefined') {  //ie
                    return this.jie_dian[i].currentStyle[attr];
                }
            } else {
                this.jie_dian[i].style[attr] = value;
            }
        }
        return this;
    };
    
    /** wen_ben()方法，给获取到的元素设置文本，或者获取文本
     * 有参：设置文本，参数是要设置的文本字符串。
     * 无参：获取文本。无法连缀
     **/
    feng_zhuang_ku.prototype.wen_ben = function (str) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 0) {
                return this.jie_dian[i].innerHTML;
            }
            this.jie_dian[i].innerHTML = str;
        }
        return this;
    };
    
    /** click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
     * 循环jie_dian属性里的节点，将每次循环的节点添加元素点击事件
     **/
    feng_zhuang_ku.prototype.click = function (fu) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            this.jie_dian[i].onclick = fu;
        }
        return this;
    };
    
    /** tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀
     **/
    feng_zhuang_ku.prototype.tian_jia_class = function (classname) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (!this.jie_dian[i].className.match(new RegExp('(\\s|^)' + classname + '(\\s|$)'))) {
                this.jie_dian[i].className += ' ' + classname;
            }
        }
        return this;
    };
    
    /** yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀
     **/
    feng_zhuang_ku.prototype.yi_chu_class = function (classname) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (this.jie_dian[i].className.match(new RegExp('(\\s|^)' + classname + '(\\s|$)'))) {
                this.jie_dian[i].className = this.jie_dian[i].className.replace(new RegExp('(\\s|^)' + classname + '(\\s|$)'), ' ');
            }
        }
        return this;
    };
    
    /** she_zhi_link_css()方法，设置link连接、或style内嵌、中的CSS样式
     * 在Web应用中，很少用到添加CSS规则和移除CSS规则，一般只用行内和Class；因为添加和删除原本的规则会破坏整个CSS的结构，所以使用需要非常小心。
     * 直接在库对象下使用  如：$().she_zhi_link_css()
     * 四个参数：
     * 参数1，样式表索引位置，就是要操作的样式表位置索引，第几个样式表【数值】
     * 参数2，要添加的选择器名称，【字符串】
     * 参数3，要添加的样式名称和值，如：background:#ff2a16 【字符串】
     * 参数4，将样式和选择器添加到样式表什么位置，【数值】
     **/
    feng_zhuang_ku.prototype.she_zhi_link_css = function (num, selectorText, cssText, position) {
        var sheet = document.styleSheets[num];
        if (typeof sheet.insertRule != 'undefined') {
            sheet.insertRule(selectorText + "{" + cssText + "}", position);
        } else if (typeof sheet.addRule != 'undefined') {
            sheet.addRule(selectorText, cssText, position);
        }
        return this;
    };
    
    /** yi_chu_link_css()方法，移除link连接、或style内嵌、中的CSS样式
     * 在Web应用中，很少用到添加CSS规则和移除CSS规则，一般只用行内和Class；因为添加和删除原本的规则会破坏整个CSS的结构，所以使用需要非常小心。
     * 直接在库对象下使用
     * 两个参数：
     * 参数1，样式表索引位置，就是要操作的样式表位置索引，第几个样式表【数值】
     * 参数2，删除样式表里的第几个选择器【数值】
     **/
    feng_zhuang_ku.prototype.yi_chu_link_css = function (num, position) {
        var sheet = document.styleSheets[num];
        if (typeof sheet.deleteRule != 'undefined') {
            sheet.deleteRule(position);
        } else if (typeof sheet.removeRule) {
            sheet.removeRule(position);
        }
        return this;
    };
    /**------------------------------------------------元素节点操作结束--------------------------------------------**/
[/code]





**前台调用代码6**

[code]

     //前台调用代码
    window.onload = function (){
        /*
        $().huo_qu_class('hj','a').guo_lv_jie_dian(0).css('color','#ff2a16');
        $().huo_qu_class('hj','a').guo_lv_jie_dian(1).css('color','#ff2a16');
        $().huo_qu_class('hj','a').guo_lv_jie_dian(2).css('color','#ff2a16');
        $().huo_qu_class('hj','a').guo_lv_jie_dian(3).css('color','#ff2a16');
        $().huo_qu_class('hj','a').wen_ben('重置');
        $().huo_qu_class('hj','b').tian_jia_class('b').tian_jia_class('c').tian_jia_class('d').yi_chu_class('b').yi_chu_class('c').yi_chu_class('d');
    */
        $().huo_qu_id('li').css('background-color','#ff2a16');
        $().huo_qu_id('li2').css('background-color','#fff133');
    };
[/code]





[code]

     
[/code]

