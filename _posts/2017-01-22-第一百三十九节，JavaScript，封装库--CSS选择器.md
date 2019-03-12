---
layout: post
title: " 第一百三十九节，JavaScript，封装库--CSS选择器 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，封装库--修改元素选择器**

**就是将构造库函数修改成 **元素选择器，像css那样，输入#xxx .xxx xxx  （ **
**获取指定id下的指定class下的指定标签元素**** ）****



****修改后的基础库****

[code]

     /**
     *feng_zhuang_ku_1.0版本，js封装库，2016/12/29日：林贵秀
     **/
    
    /** 前台调用
     * 每次调用$()创建库对象,使其每次调用都是独立的对象
     * $()创建库对象,有一个可选参数，参数有两种方式，1是传入的this，2是传入的字符串
     * 可选参数说明：
     * 传入的this，this，就是当前对象本身
     * 传入的字符串，代表获取元素选择器
     * 参数是元素选择器(id值、class值、标签名称)其中一样的字符串方式，或者是其中几样的字符串组合方式
     * 获取一个元素传参方式 '#xxx'( 表示获取id)，'.xxx'(表示获取class)，'xxx'(表示获取标签)
     * 从父元素向下获取组合方式按照，一个元素传参方式加上空格，如: ('#sdf .hjk p')表示获取id为sdf元素下的class为hjk下的p元素
     **/
    var $ = function (args) {
        return new feng_zhuang_ku(args);
    };
    
    /**
     *定义封装库构造函数，类库
     **/
    function feng_zhuang_ku(args) {
        /** jie_dian属性，创建数组，初始化，保存获取到的元素节点，返回数组
         **/
        this.jie_dian = [];
        if (typeof args == 'string') {                      //如果传入的是字符串，说明是获取元素选择器
            if (args.indexOf(' ') != -1) {
                /**从父元素向下获取组合方式**/
                var fen_ge = args.split(' ');                //将接收的组合式元素名称分割成数组
                var lin_shi = [];                            //保存临时对象的数组，解决被覆盖问题
                var fu_yuan_su = [];                         //保存父元素的数组
                for (var i = 0; i < fen_ge.length; i++) {
                    if (fu_yuan_su.length == 0)fu_yuan_su.push(document);               //如果没有父节点，就把document放入父节点
                    switch (fen_ge[i].charAt(0)) {                                     //判断字符串的第一个字符是什么
                        case '#':                                                      //说明是id
                            lin_shi = [];                                              //清理临时数组，以便父节点失效，子节点有效
                            lin_shi.push(this.huo_qu_id(fen_ge[i].substring(1)));      //去除第一个字符，获取到传入的id元素，保存到临时数组
                            fu_yuan_su = lin_shi;                                      //将临时节点数组放入父节点数字
                            break;                                                     //说明是class
                        case '.':
                            lin_shi = [];                                                                   //清理临时数组，以便父节点失效，子节点有效
                            for (var f = 0; f < fu_yuan_su.length; f++) {                                  //根据父节点的长度循环
                                var tempss = this.huo_qu_class(fen_ge[i].substring(1), fu_yuan_su[f]);     //获取到父节点下的子节点
                                for (var n = 0; n < tempss.length; n++) {                      //循环子节点，将每次循环的子节点添加到临时数组
                                    lin_shi.push(tempss[n]);
                                }
                            }
                            fu_yuan_su = lin_shi;                                               //将临时节点数组放入父节点数字
                            break;
                        default:                                                               //说明是标签
                            lin_shi = [];                                                       //清理临时数组，以便父节点失效，子节点有效
                            for (var j = 0; j < fu_yuan_su.length; j++) {                      //根据父节点的长度循环
                                var temps = this.huo_qu_name(fen_ge[i], fu_yuan_su[j]);        //获取到父节点下的子节点
                                for (var k = 0; k < temps.length; k++) {                       //循环子节点，将每次循环的子节点添加到临时数组
                                    lin_shi.push(temps[k]);
                                }
                            }
                            fu_yuan_su = lin_shi;                                               //将临时节点数组放入父节点数字
                    }
                }
                this.jie_dian = lin_shi;                                            //将临时数组放入jie_dian数组
            } else {
                /**一个元素传参方式**/
                switch (args.charAt(0)) {                                           //判断字符串的第一个字符是什么
                    case '#':                                                       //说明是id
                        this.jie_dian.push(this.huo_qu_id(args.substring(1)));      //去除第一个字符，获取到传入的id元素
                        break;
                    case '.':                                                       //说明是class
                        this.jie_dian = this.huo_qu_class(args.substring(1));       //去除第一个字符，获取到传入的class元素
                        break;
                    default:                                                        //说明是标签
                        this.jie_dian = this.huo_qu_name(args);                     //获取到传入的标签元素
                }
            }
        } else if (typeof args == 'object') {                                       //如果传入的是对象，说明是this，就是当前对象本身
            if (args != undefined) {
                this.jie_dian[0] = args;
            }
        }
    }
    
    /**$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$**/
    
    
    /**$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$**/
    
    
    /**------------------------------------------------获取元素标签开始--------------------------------------------**/
    /**获取元素标签说明：
     * jie_dian属性，保存获取到的元素节点，返回数组,
     *
     * huo_qu_id()方法,通过id获取元素标签，参数是id值，将获取到的元素对象返回给方法本身，无法连缀
     * huo_qu_name()方法，通过标签名称获取相同标签名的元素，
     * huo_qu_class()方法，获取相同class属性的节点，返回包含相同class属性的节点数组，返回给方法本身,无法连缀
     *
     * huo_qu_name_zhi()方法，通过元素name值获取指定元素，适用于获取表单元素,
     * guo_lv_jie_dian()方法，获取多个节点时，过滤jie_dian属性里的数组，就是过滤掉指定索引外的元素对象
     * huo_qu_zi_jie_dian()方法，获取一个元素下的子元素
     **/
    
    
    /** huo_qu_id()方法,通过id获取元素标签，参数是id值，将获取到的元素对象返回给方法本身，无法连缀
     **/
    feng_zhuang_ku.prototype.huo_qu_id = function (id) {
        return document.getElementById(id);
    };
    
    /** huo_qu_name()方法，通过标签名称获取相同标签名的元素，返回包含相同标签名的元素数组，返回给方法本身
     * 两个参数：获取指定元素下的相同标签元素，参数1标签名称，参数2是要获取元素的父元素
     * 一个参数：获取页面所有相同标签元素，参数是标签名称
     **/
    feng_zhuang_ku.prototype.huo_qu_name = function (tag, parentnode) {
        var node = null;
        var lin_shi = [];
        if (parentnode != undefined) {
            node = parentnode;
        } else {
            node = document;
        }
        var tags = node.getElementsByTagName(tag);
        for (var i = 0; i < tags.length; i++) {
            lin_shi.push(tags[i]);
        }
        return lin_shi;
    };
    
    /** huo_qu_class()方法，获取相同class属性的节点，返回包含相同class属性的节点数组，返回给方法本身,无法连缀
     * 一个参数：获取整个页面指定的class属性节点，参数是class属性值
     * 两个参数：获取指定元素区下的class属性节点，参数1是class属性值，参数2是要获取class属性节点的父元素节点
     **/
    feng_zhuang_ku.prototype.huo_qu_class = function (name, parentnode) {
        var node = null;
        var lin_shi = [];
        if (parentnode != undefined) {
            node = parentnode;
        } else {
            node = document;
        }
        var all = node.getElementsByTagName('*');
        for (var i = 0; i < all.length; i++) {
            if (all[i].className == name) {
                lin_shi.push(all[i]);
            }
        }
        return lin_shi;
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
    
    /** guo_lv_jie_dian()方法，获取多个节点时，过滤jie_dian属性里的数组，就是过滤掉指定索引外的元素对象
     * 参数是要保留jie_dian属性里的对象索引
     **/
    feng_zhuang_ku.prototype.guo_lv_jie_dian = function (num) {
        var element = this.jie_dian[num];
        this.jie_dian = [];
        this.jie_dian[0] = element;
        return this;
    };
    
    /** huo_qu_zi_jie_dian()方法，获取一个元素下的子元素
     * 注意首先要获取到父元素，在使用huo_qu_zi_jie_dian()方法
     * 参数是要获取的，子元素(id值、class值、标签名称)其中一样的字符串方式，
     * 传参方式 '#xxx'( 表示获取id)，'.xxx'(表示获取class)，'xxx'(表示获取标签)
     **/
    feng_zhuang_ku.prototype.huo_qu_zi_jie_dian = function (str) {
        var lin_shi = [];                                               //临时数组
        for (var i = 0; i < this.jie_dian.length; i++) {               //根据父元素的长度，循环出父元素
            switch (str.charAt(0)) {                                   //判断字符串的第一个字符是什么
                case '#':                                              //说明是id
                    lin_shi.push(this.huo_qu_id(str.substring(1)));    //获取到父元素下的子元素id等于str的标签，将它添加到临时数组
                    break;
                case '.':                                                     //说明是class
                    var tempss = this.huo_qu_class(str.substring(1), this.jie_dian[i]);
                    for (var k = 0; k < tempss.length; k++) {
                        lin_shi.push(tempss[k]);
                    }
                    break;
                default:                                                      //说明是标签名称
                    var temps = this.huo_qu_name(str, this.jie_dian[i]);
                    for (var j = 0; j < temps.length; j++) {
                        lin_shi.push(temps[j]);
                    }
            }
        }
        this.jie_dian = lin_shi;                                               //将临时数组替换成节点数组
        return this;
    };
    
    /**------------------------------------------------获取元素标签结束--------------------------------------------**/
    
    
    /**------------------------------------------------元素节点操作开始--------------------------------------------**/
    /**元素节点操作说明：
     * c_css()方法，给获取到的元素设置ss样式,或者获取css样式，
     * wen_ben()方法，给获取到的元素设置文本，或者获取文本
     * tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀
     * yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀
     * she_zhi_link_css()方法，设置link连接、或style内嵌、中的CSS样式
     * yi_chu_link_css()方法，移除link连接、或style内嵌、中的CSS样式
     **/
    
    
    /** c_css()方法，给获取到的元素设置ss样式,或者获取css样式，
     * 两个参数：设置样式，参数1样式名称，参数2样式值,设置的行内样式
     * 一个参数：获取样式，参数是样式名称，无法连缀，获取即可用获取行内也可以获取连接
     **/
    feng_zhuang_ku.prototype.c_css = function (attr, value) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 1) {
                return getStyle(this.jie_dian[i], attr); //getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
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
    
    /** tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀
     **/
    feng_zhuang_ku.prototype.tian_jia_class = function (classname) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (hasClass(this.jie_dian[i], classname)) {   //hasClass()函数库函数，判断一个元素的class属性值是否存在
                this.jie_dian[i].className += ' ' + classname;
            }
        }
        return this;
    };
    
    /** yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀
     **/
    feng_zhuang_ku.prototype.yi_chu_class = function (classname) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (hasClass(this.jie_dian[i], classname)) {
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
    
    
    /**------------------------------------------------元素事件开始--------------------------------------------**/
    /**元素事件说明：
     * shu_biao_yi_ru_yi_chu()方法，给元素设置鼠标移入移出事件，接收两个参数，参数是移入和移出时的执行函数(包含代码)
     * xian_shi()方法，设置元素显示,无参
     * yin_cang()方法，设置元素隐藏,无参
     * on_click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
     * yuan_su_ju_zhong()方法，将获取到的区块元素居中到页面，
     * chuang_kou_shi_jian()方法，浏览器窗口事件，当窗口的大小变化时触发函数
     * zhe_zhao_suo_ping()方法，将一个区块元素设置成遮罩锁屏区块
     **/
    
    
    /** shu_biao_yi_ru_yi_chu()方法，给元素设置鼠标移入移出事件，接收两个参数，参数是移入和移出时的执行函数(包含代码)
     *参数1是移入时的执行函数(包含代码)
     *参数2是移出时的执行函数(包含代码)
     **/
    feng_zhuang_ku.prototype.shu_biao_yi_ru_yi_chu = function (yi_ru, yi_chu) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            addEvent(this.jie_dian[i], 'mouseover', yi_ru);
            addEvent(this.jie_dian[i], 'mouseout', yi_chu);
        }
        return this;
    };
    
    /** xian_shi()方法，设置元素显示,无参
     **/
    feng_zhuang_ku.prototype.xian_shi = function () {
        for (var i = 0; i < this.jie_dian.length; i++) {
            this.jie_dian[i].style.display = 'block';
        }
        return this;
    };
    
    /** yin_cang()方法，设置元素隐藏,无参
     **/
    feng_zhuang_ku.prototype.yin_cang = function () {
        for (var i = 0; i < this.jie_dian.length; i++) {
            this.jie_dian[i].style.display = 'none';
            document.documentElement.style.overflow = 'auto';
            removeEvent(window, 'scroll', scrollTop); //遮罩锁屏时有用
        }
        return this;
    };
    
    /** on_click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
     * 循环jie_dian属性里的节点，将每次循环的节点添加元素点击事件
     **/
    feng_zhuang_ku.prototype.on_click = function (fu) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            addEvent(this.jie_dian[i], 'click', fu);
        }
        return this;
    };
    
    /** yuan_su_ju_zhong()方法，将获取到的区块元素居中到页面，
     * 注意：使用此方法时，首先要在css里将目标区块设置成(绝对定位,position: absolute;)
     **/
    feng_zhuang_ku.prototype.yuan_su_ju_zhong = function () {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            var y_style = getStyle(yan_su, 'display'); //getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
            if (y_style === "none") {
                yan_su.style.display = "block";
            }
            var width = yan_su.offsetWidth;
            var height = yan_su.offsetHeight;
            if (y_style === "none") {
                yan_su.style.display = "none";
            }
            var chang_w = getInner().width;
            var chang_h = getInner().height;
            var top = (chang_h - height) / 2;
            var left = (chang_w - width) / 2;
            for (var ii = 0; ii < this.jie_dian.length; ii++) {
                this.jie_dian[ii].style.top = top + 'px';
                this.jie_dian[ii].style.left = left + 'px';
            }
        } else {
            alert("区块元素页面居中,只能设置一个区块元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
    
    /** chuang_kou_shi_jian()方法，浏览器窗口事件，当窗口的大小变化时触发函数
     * 接收一个参数，就是触发时要执行的函数（包含函数功能）
     **/
    feng_zhuang_ku.prototype.chuang_kou_shi_jian = function (fn) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            var yan_su = this.jie_dian[i];
        }
        addEvent(window, 'resize', function () {
            fn();
            if (yan_su.offsetLeft > getInner().width - yan_su.offsetWidth) {
                yan_su.style.left = getInner().width - yan_su.offsetWidth + 'px';
            }
            if (yan_su.offsetTop > getInner().height - yan_su.offsetHeight) {
                yan_su.style.top = getInner().height - yan_su.offsetHeight + 'px';
            }
        });
        return this;
    };
    
    /** zhe_zhao_suo_ping()方法，将一个区块元素设置成遮罩锁屏区块
     * 注意：一般需要在css文件将元素设置成隐藏
     **/
    feng_zhuang_ku.prototype.zhe_zhao_suo_ping = function () {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            var chang_w = getInner().width;  //getInner()函数库函数，跨浏览器获取浏览器视窗大小
            var chang_h = getInner().height;
            yan_su.style.width = chang_w + 'px';
            yan_su.style.height = chang_h + 'px';
            yan_su.style.position = 'absolute';
            yan_su.style.top = '0';
            yan_su.style.left = '0';
            var y_style = getStyle(yan_su, 'display'); //getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
            if (y_style === "block") {
                document.documentElement.style.overflow = 'hidden';
                addEvent(window, 'scroll', scrollTop);
            } else if (y_style === 'none') {
                document.documentElement.style.overflow = 'auto';
            }
        } else {
            alert("遮罩锁屏区块,只能设置一个区块元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
    
    
    /**------------------------------------------------元素事件结束--------------------------------------------**/
    
    
    /**------------------------------------------------插件入口开始--------------------------------------------**/
    /** 插件入口，简单的理解就是通过extend()方法，向此基础库添加一个原型方法
     *  此extend()方法，一般是给插件文件使用的，插件就是通过extend()方法，将插件方法添加到基础库原型的
     *  接收两个参数
     *  参数1是传入要添加的方法名称
     *  参数2是此方法的执行函数（包含代码）
     **/
    feng_zhuang_ku.prototype.extend = function (name, fn) {
        feng_zhuang_ku.prototype[name] = fn;
    };
    /**------------------------------------------------插件入口结束--------------------------------------------**/
[/code]



**HTML代码**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>JavaScript讲解</title>
        <link rel="stylesheet" title='xxx' type="text/css" href="1.css">
        <script type="text/javascript" src="feng_zhuang_ku/han_shu/han_shu.js" charset="utf-8"></script>
        <script type="text/javascript" src="feng_zhuang_ku/feng_zhuang_ku.js" charset="utf-8"></script>
        <script type="text/javascript" src="feng_zhuang_ku/cha_jian/tuo_zhuai.js" charset="utf-8"></script>
        <script type="text/javascript" src="1.js" charset="utf-8"></script>
    </head>
    <body>
    <div id="tou">
        <div class="logo"><img src="img/logo.gif" alt=""></div>
        <div class="ge_ren_zhong_xin">个人中心
            <ul>
                <li><a href="#">设置</a></li>
                <li><a href="#">换肤</a></li>
                <li><a href="#">帮助</a></li>
                <li><a href="#">退出</a></li>
            </ul>
        </div>
        <div class="deng_lu">登录</div>
    </div>
    <div id="login">
        <h2 class="tbu"><img src="img/close.png" alt="" class="close" />网站登录</h2>
        <div class="user">帐 号：<input type="text" name="user" class="text" /></div>
        <div class="pass">密 码：<input type="password" name="pass" class="text" /></div>
        <div class="button"><input type="button" class="submit" value="" /></div>
        <div class="other">注册新用户 | 忘记密码？</div>
    </div>
    <div id="suo_ping">1</div>
    <input type="button" value="按钮" id="button" />
    <a href="http://www.yc60.com" id="a">瓢城Web俱乐部</a>
    
    <div id="box">box</div>
    
    
    <div id="jkf">
        <p>
            <span class="a">pspan</span>
            <span class="a">pspan</span>
            <span class="b">pspan</span>
        </p>
    
    
        <p>
            <span class="a">pspan</span>
            <span>pspan</span>
            <span id="q">pspan</span>
        </p>
    
        <div>
            <span class="a">pspan</span>
            <span>pspan</span>
            <span>pspan</span>
        </div>
    </div>
    <p>
        <span class="a">pspan</span>
        <span class="a">pspan</span>
        <span class="b">pspan</span>
    </p>
    
    </body>
    </html>
[/code]



**css代码**

[code]

     @charset "utf-8";
    * {
        margin: 0;
        padding: 0;
        /*color: #ff583d;*/
    }
    body{
        background: url("img/header_bg.png") repeat-x;
        font-size:14px;
    }
    #tou{
        width: 900px;
        height: 30px;
        margin: 0 auto;
    }
    .logo{
        width: 100px;
        height: 30px;
        float: left;
    }
    .ge_ren_zhong_xin{
        position: relative;
        width: 70px;
        height: 30px;
        line-height: 30px;
        float: right;
        background: url("img/arrow.png") no-repeat right center;
        cursor: pointer;
    }
    ul{
        width: 100px;
        height: 110px;
        list-style-type: none;
        position: absolute;
        top:30px;
        right: -15px;
        background:#FBF7E1;
        border:1px solid #999;
        border-top:none;
        padding:10px 0 0 0;
        display:none;
    }
    ul li {
        height:25px;
        line-height:25px;
        text-indent:20px;
        letter-spacing:1px;
    }
    ul li a {
        display:block;
        text-decoration:none;
        color:#333;
        background:url("img/arrow3.gif") no-repeat 5px 45%;
    }
    ul li a:hover {
        background:#fc0 url("img/arrow4.gif") no-repeat 5px 45%;
    }
    
    
    /*登录*/
    #tou .deng_lu {
        width: 30px;
        height: 30px;
        float: right;
        line-height: 30px;
        margin-right: 10px;
        cursor: pointer;
    }
    /*登录框*/
    #login{
        width: 350px;
        height: 250px;
        border: 1px solid #ccc;
        position:absolute;
        display: none;
        z-index: 9999;
        background-color: #fff;
    }
    #login h2{
        background: rgba(0, 0, 0, 0) url("img/login_header.png") repeat-x scroll 0 0;
        border-bottom: 1px solid #ccc;
        color: #666;
        font-size: 14px;
        height: 40px;
        line-height : 40px;
        text-align: center;
        letter-spacing: 1px;
        margin: 0 0 20px;
        cursor: move;
    }
    #login h2 img{
        cursor: pointer;
        float: right;
        position: relative;
        right: 8px;
        top: 14px;
    }
    #login div.user, #login div.pass {
        color: #666;
        font-size: 14px;
        padding: 5px 0;
        text-align: center;
    }
    #login input.text {
        background: #fff none repeat scroll 0 0;
        border: 1px solid #ccc;
        font-size: 14px;
        height: 25px;
        width: 200px;
    }
    #login .button {
        padding: 20px 0;
        text-align: center;
    }
    #login input.submit {
        background: rgba(0, 0, 0, 0) url("img/login_button.png") no-repeat scroll 0 0;
        border: medium none;
        cursor: pointer;
        height: 30px;
        width: 107px;
    }
    #login .other {
        color: #666;
        padding: 15px 10px;
        text-align: right;
    }
    /*遮罩锁屏区块*/
    #suo_ping{
        z-index: 9998; /*注意：如果遮罩层上面有元素，它的层级要大于9998*/
        background: #000;
        filter: alpha(opacity=50);
        opacity: 0.5;
        display: none;
    }
[/code]



**前台js代码**

[code]

     //前台调用代码
    addEvent(window, 'load', function () {
        //个人中心和登录框
        $('#tou .ge_ren_zhong_xin').shu_biao_yi_ru_yi_chu(function () {                     //获取到个人中心元素，执行鼠标移入移除方法
            $(this).c_css('background', 'url(img/arrow2.png) no-repeat right center');     //移入鼠标改变人中心背景图片
            $('.ge_ren_zhong_xin ul').xian_shi();                                         //移入鼠标显示个人中心下拉区块
        }, function () {
            $(this).c_css('background', 'url(img/arrow.png) no-repeat right center');    //移出鼠标改变人中心背景图片
            $('.ge_ren_zhong_xin ul').yin_cang();                                          //移出鼠标隐藏个人中心下拉区块
        });
        $('#login .close').on_click(function () {
            $('#login').yin_cang();
            $('#suo_ping').yin_cang();
        });
        $('#tou .deng_lu').on_click(function () {                                          //获取登录，添加点击事件
            $('#login').xian_shi().yuan_su_ju_zhong().chuang_kou_shi_jian(function () {  //点击后，显示登录框，登录框居中，添加窗口事件
                $('#login').yuan_su_ju_zhong();                                              //窗口改变时再次执行登录框居中
                $('#suo_ping').zhe_zhao_suo_ping()
            });
            $('#suo_ping').xian_shi().zhe_zhao_suo_ping();
        });
        $('#login').tuo_zhuai('tbu');
    
        $('#jkf p #q').c_css('font-size','80px').c_css('color','#ff583d');
    
    
    
    
    
    });
[/code]



