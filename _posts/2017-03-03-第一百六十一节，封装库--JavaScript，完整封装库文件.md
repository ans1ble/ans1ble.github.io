---
layout: post
title: " 第一百六十一节，封装库--JavaScript，完整封装库文件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，完整封装库文件**

[code]

     /**
     *feng_zhuang_ku_1.0版本，js封装库，2016/12/29日：林贵秀
     **/
    
    
    /** 前台调用
     * 每次调用$()创建库对象,使其每次调用都是独立的对象
     * $()创建库对象,有一个可选参数，参数有两种方式，1是传入的this，2是传入的字符串
     * 可选参数说明：
     * 传入的this，this，就是当前对象本身
     *
     * 传入的字符串，代表获取元素选择器
     * 参数是元素选择器(id值、class值、标签名称)其中一样的字符串方式，或者是其中几样的字符串组合方式
     * 获取一个元素传参方式 '#xxx'( 表示获取id)，'.xxx'(表示获取class)，'xxx'(表示获取标签)
     * 从父元素向下获取组合方式按照，一个元素传参方式加上空格，如: ('#sdf .hjk p')表示获取id为sdf元素下的class为hjk下的p元素
     *
     * 传入一个匿名函数，表示是dom页面文档加载，在匿名函数里写代码，表示等待页面文档加载完毕后执行函数里的代码
     * 加载dom页面文档结构后执行函数，不等待图片，音频视频等文件加载
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
        } else if (typeof args == 'function') {
            this.dom_dom(args);
        }
    }
    
    
    
    /**█████████████████████████████████████████████████封装库█████████████████████████████████████████████████████████**/
    
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃获取元素标签开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
     /**获取元素标签说明：
     * jie_dian属性，保存获取到的元素节点，返回数组,
     *
     * huo_qu_id()方法,通过id获取元素标签，参数是id值，将获取到的元素对象返回给方法本身，无法连缀
     * huo_qu_name()方法，通过标签名称获取相同标签名的元素，
     * huo_qu_class()方法，获取相同class属性的节点，返回包含相同class属性的节点数组，返回给方法本身,无法连缀
     * hq_form_name()方法，获取表单里，指定name值的元素节点，也就是获取表单里指定名称的元素节点，在form元素对象下使用
     * hq_value()方法，获取和设置表单里节点的value属性值
     * huo_qu_name_zhi()方法，通过元素name值获取指定元素，适用于获取表单元素,
     * shang_jd()方法，获取当前节点同级的上一个节点
     * xia_jd()方法，获取当前节点同级的下一个节点
     * hq_jd()方法,多个节点时，获取某一个节点，并返回这个节点对象,参数是节点索引
     * sh_jd()方法,多个节点时，获取首个节点，并返回这个节点对象,无参
     * w_jd()方法,多个节点时，获取末个节点，并返回这个节点对象,无参
     * guo_lv_jie_dian()方法，多个节点时，获取某一个节点，并且feng_zhuang_ku对象
     * jd_length()方法，获取一个节点集合的长度
     * hq_suo_yin()方法，获取一个节点在，父节点下，子节点集合里的索引，也就是在集合里的下标
     * hq_shu_xing_zhi()方法，获取或设置一个节点的属性值
     * huo_qu_zi_jie_dian()方法，获取一个元素下的子元素
     * dom_dom()方法，加载dom页面文档结构后执行函数，不等待图片，音频视频等文件加载
     **/
    
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃元素节点操作开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    /**元素节点操作说明：
     * c_css()方法，给获取到的元素设置ss样式,或者获取css样式，
     * shzh_tou_ming_du()方法，给元素设置透明度
     * wen_ben()方法，给获取到的元素设置文本，或者获取文本
     * wen_ben_guo_lv()方法，给获取到的元素设置文本，或者获取文本，会过滤html标签
     * tian_jia_class()方法，给获取到的元素添加class属性，参数是class属性值，可以连缀
     * yi_chu_class()方法，给获取到的元素移除class属性，参数是要移除的class属性值，可以连缀
     * she_zhi_link_css()方法，设置link连接、或style内嵌、中的CSS样式
     * yi_chu_link_css()方法，移除link连接、或style内嵌、中的CSS样式
     * tuo_zhuai()方法，将一个弹窗元素实现拖拽功能
     **/
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃元素事件开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    /**元素事件说明：
     * shu_biao_yi_ru_yi_chu()方法，给元素设置鼠标移入移出事件，接收两个参数，参数是移入和移出时的执行函数(包含代码)
     * xian_shi()方法，设置元素显示,无参
     * yin_cang()方法，设置元素隐藏,无参
     * yuan_su_shi_jian()方，给元素添加一个元素事件
     * on_click()方法，给获取到的元素添加一个点击事件，参数是一个匿名函数（包含函数功能），
     * dian_ji_qie_huan()方法，设置点击切换，将元素设置成点击切换，也就是点击目标元素后，循环执行方法里的函数
     * yuan_su_ju_zhong()方法，将获取到的区块元素居中到页面，
     * chuang_kou_shi_jian()方法，浏览器窗口事件，当窗口的大小变化时触发函数
     * zhe_zhao_suo_ping()方法，将一个区块元素设置成遮罩锁屏区块
     * jie_chu_suo_ping()方法，将一个锁屏区块元素解除锁屏，
     **/
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃元素动画开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    /**
     * 元素动画说明
     * yi_dong_tou_ming()方法，将一个元素，
     *
     **/
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃插件入口开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    
    /** 插件入口，简单的理解就是通过extend()方法，向此基础库添加一个原型方法
     **/
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃ajax通讯▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    /**
     * ajax()方法，ajax通讯方法，跨页面向动态页面发送或获取数据
     **/
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃表单序列化▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    /**
     * xu_lie_biao_dan()方法，表单序列化方法，将自动获取指定表单里面的各项字段name值和value值，无法连缀
     **/
    /**█████████████████████████████████████████████████封装库██████████████████████████████████████████████████████████**/
    
    
    
    
    /**------------------------------------------------获取元素标签开始--------------------------------------------**/
    
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
            if ((new RegExp('(\\s|^)' + name + '(\\s|$)')).test(all[i].className)){
                lin_shi.push(all[i]);
            }
        }
        return lin_shi;
    };
    
    /** hq_form_name()方法，获取表单里，指定name值的元素节点，也就是获取表单里指定名称的元素节点，在form元素对象下使用
     *  参数是要获取表单里的元素name值，也就是名称
     *  返回表单里有相同name值的节点集合
     **/
    feng_zhuang_ku.prototype.hq_form_name = function (name) {
        for (var i = 0; i < this.jie_dian.length; i++){
            this.jie_dian[i] = this.jie_dian[i][name];
        }
        return this;
    };
    
    /** hq_value()方法，获取和设置表单里节点的value属性值
     *  无参为获取表单里节点的value属性值
     *  有参为设置表单里节点的value属性值，参数是要设置的value属性值
     **/
    feng_zhuang_ku.prototype.hq_value = function (str) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 0) {
                return this.jie_dian[i].value;
            }
            this.jie_dian[i].value = str;
        }
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
    
    /** shang_jd()方法，获取当前节点同级的上一个节点
     **/
    feng_zhuang_ku.prototype.shang_jd = function () {
        for (var i = 0; i < this.jie_dian.length; i ++) {
            this.jie_dian[i] = this.jie_dian[i].previousSibling;
            if (this.jie_dian[i] == null) throw new Error('找不到上一个同级元素节点！');
            if (this.jie_dian[i].nodeType == 3) this.shang_jd();
        }
        return this;
    };
    
    /** xia_jd()方法，获取当前节点同级的下一个节点
     **/
    feng_zhuang_ku.prototype.xia_jd = function () {
        for (var i = 0; i < this.jie_dian.length; i ++) {
            this.jie_dian[i] = this.jie_dian[i].nextSibling;
            if (this.jie_dian[i] == null) throw new Error('找不到下一个同级元素节点！');
            if (this.jie_dian[i].nodeType == 3) this.xia_jd();
        }
        return this;
    };
    
    /** hq_jd()方法,多个节点时，获取某一个节点，并返回这个节点对象,参数是节点索引
     **/
    feng_zhuang_ku.prototype.hq_jd = function (num) {
        return this.jie_dian[num];
    };
    
    /** sh_jd()方法,多个节点时，获取首个节点，并返回这个节点对象,无参
     **/
    feng_zhuang_ku.prototype.sh_jd = function () {
        return this.jie_dian[0];
    };
    
    /** w_jd()方法,多个节点时，获取末个节点，并返回这个节点对象,无参
     **/
    feng_zhuang_ku.prototype.w_jd = function () {
        return this.jie_dian[this.jie_dian.length - 1];
    };
    
    /** guo_lv_jie_dian()方法，多个节点时，获取某一个节点，并且feng_zhuang_ku对象
     * 参数是要获取jie_dian属性里的对象索引
     **/
    feng_zhuang_ku.prototype.guo_lv_jie_dian = function (num) {
        var element = this.jie_dian[num];
        this.jie_dian = [];
        this.jie_dian[0] = element;
        return this;
    };
    
    /** jd_length()方法，获取一个节点集合的长度
     **/
    feng_zhuang_ku.prototype.jd_length = function () {
        return this.jie_dian.length;
    };
    
    /** hq_suo_yin()方法，获取一个节点在，父节点下，子节点集合里的索引，也就是在集合里的下标
     **/
    feng_zhuang_ku.prototype.hq_suo_yin = function () {
        var children = this.jie_dian[0].parentNode.children;
        for (var i = 0; i < children.length; i++){
            if (this.jie_dian[0] == children[i]) return i;
        }
    };
    
    /** hq_shu_xing_zhi()方法，获取或设置一个节点的属性值
     * 1个参数，获取属性值，参数是属性名称
     * 2个参数，设置属性值，第1个属性名称，第2个属性值
     **/
    feng_zhuang_ku.prototype.hq_shu_xing_zhi = function (shu_xing, zhi) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 1) {
                return this.jie_dian[i].getAttribute(shu_xing);
            } else if (arguments.length == 2){
                this.jie_dian[i].setAttribute(shu_xing,zhi);
            }
        }
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
    
    /**  dom_dom()方法，加载dom页面文档结构后执行函数，不等待图片，音频视频等文件加载
     *  参数是页面文档加载后要执行的函数
     **/
    feng_zhuang_ku.prototype.dom_dom = function (fn) {
        dom_jia_zai(fn);
        return this;
    };
    
    /**------------------------------------------------获取元素标签结束--------------------------------------------**/
    
    
    
    /**------------------------------------------------元素节点操作开始--------------------------------------------**/
    
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
    
    /** shzh_tou_ming_du()方法，给元素设置透明度
     *  参数是要设置的透明度值，为百分比值，如10%，就是10
     **/
    feng_zhuang_ku.prototype.shzh_tou_ming_du = function (zhi) {
        for (var i = 0; i < this.jie_dian.length; i++){
            this.jie_dian[i].style.opacity = zhi / 100;
            this.jie_dian[i].style.filter = 'alpha(opacity='+ zhi +')';
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
    
    /** wen_ben_guo_lv()方法，给获取到的元素设置文本，或者获取文本，会过滤html标签
     * 有参：设置文本，参数是要设置的文本字符串。如果有html标签会自动转换成字符串形式在设置
     * 无参：获取文本。如果有html标签获取后会自动过滤html标签，无法连缀
     **/
    feng_zhuang_ku.prototype.wen_ben_guo_lv = function (str) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            if (arguments.length == 0) {
                if(typeof this.jie_dian[i].innerText == 'string'){
                    return this.jie_dian[i].innerText;
                }else if (typeof this.jie_dian[i].textContent == 'string'){
                    return this.jie_dian[i].textContent;
                }
            }else if (typeof this.jie_dian[i].innerText == 'string'){
                this.jie_dian[i].innerText = str;
            }else if (typeof this.jie_dian[i].textContent == 'string'){
                this.jie_dian[i].textContent = str;
            }
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
    
    
    /** tuo_zhuai()方法，将一个弹窗元素实现拖拽功能
     * 注意：有参设置拖拽点区块，只有弹窗的这个拖拽点区块才能拖拽，无参整个弹窗可以拖拽
     * 注意：一般需要在css文件将弹窗元素里的某一个区块光标设置成提示可以拖拽，如：cursor: move; （设置拖拽点）
     * 有一个参数，参数是弹窗元素里的拖拽点区块的字符串class值（设置拖拽点的class值）设置后弹窗元素里的这个拖拽点区块才能拖拽
     **/
    feng_zhuang_ku.prototype.tuo_zhuai = function (tuo_zhuai_dian) {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            var sum = arguments.length;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            addEvent(yan_su, 'mousedown', function (e) {
                if (trim(yan_su.innerHTML).length == 0)e.preventDefault();
                var e1 = getEvent(e);  //getEvent()函数库函数，跨浏览器获取事件对象,事件event对象,
                var diffx = e1.clientX - yan_su.offsetLeft;
                var diffy = e1.clientY - yan_su.offsetTop;
                if (sum == 1) {
                    if (e.target.className === tuo_zhuai_dian) {
                        addEvent(document, 'mousemove', move);
                        addEvent(document, 'mouseup', up);
                    }
                } else if (sum == 0) {
                    addEvent(document, 'mousemove', move);
                    addEvent(document, 'mouseup', up);
                }
                function move(e) {
                    var e2 = getEvent(e);
                    var left = e2.clientX - diffx;
                    var top = e2.clientY - diffy;
                    if (left < 0) {
                        left = 0;
                    }else if(left <= gun_dong_tiao_wei_zhi().left){
                        left = gun_dong_tiao_wei_zhi().left;
                    }else if (left > getInner().width + gun_dong_tiao_wei_zhi().left - yan_su.offsetWidth) {
                        left = getInner().width + gun_dong_tiao_wei_zhi().left - yan_su.offsetWidth;
                    }
                    if (top < 0) {
                        top = 0;
                    }else if(top <= gun_dong_tiao_wei_zhi().top){
                        top = gun_dong_tiao_wei_zhi().top;
                    }else if (top > getInner().height + gun_dong_tiao_wei_zhi().top - yan_su.offsetHeight) {
                        top = getInner().height + gun_dong_tiao_wei_zhi().top - yan_su.offsetHeight;
                    }
                    yan_su.style.left = left + 'px';
                    yan_su.style.top = top + 'px';
                    if (typeof yan_su.setCapture != 'undefined') {
                        yan_su.setCapture();
                    }
                }
    
                function up() {
                    removeEvent(document, 'mousemove', move);
                    removeEvent(document, 'mouseup', up);
                    if (typeof yan_su.releaseCapture != 'undefined') {
                        yan_su.releaseCapture();
                    }
                }
            });
        } else {
            alert("将一个弹窗元素实现拖拽功能,只能设置一个弹窗元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
    /**------------------------------------------------元素节点操作结束--------------------------------------------**/
    
    
    /**------------------------------------------------元素事件开始--------------------------------------------**/
    
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
        }
        return this;
    };
    
    /** yuan_su_shi_jian()方，给元素添加一个元素事件
     *  两个参数，参数1事件名称不加on，参数2事件函数
     **/
    feng_zhuang_ku.prototype.yuan_su_shi_jian = function (ming_cheng,fn) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            addEvent(this.jie_dian[i],ming_cheng, fn);
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
    
    /** dian_ji_qie_huan()方法，设置点击切换，将元素设置成点击切换，也就是点击目标元素后，循环执行方法里的函数
     * 参数是点击后要执行的函数，可以是多个函数，点击一次循环执行一个函数，从第一个开始，循环完毕后再次循环从第一个开始
     **/
    feng_zhuang_ku.prototype.dian_ji_qie_huan = function () {
        for (var i = 0; i < this.jie_dian.length; i++) {
            (function (jiedian, args) {
                var count = 0;                                          //计数器
                addEvent(jiedian, 'click', function () {                //给对象添加点击事件
                    args[count++ % args.length].call(this);             //点击后计数器数值求于作为下标执行传入的函数，计数器在累加,将对象传入
                });
            })(this.jie_dian[i], arguments);                            //通过arguments接收传入方法的函数
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
            var top = (chang_h - height) / 2 + gun_dong_tiao_wei_zhi().top;
            var left = (chang_w - width) / 2 + gun_dong_tiao_wei_zhi().left;
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
            if (yan_su.offsetLeft > getInner().width + gun_dong_tiao_wei_zhi().left - yan_su.offsetWidth) {
                yan_su.style.left = getInner().width + gun_dong_tiao_wei_zhi().left - yan_su.offsetWidth + 'px';
                if (yan_su.offsetLeft <= 0 + gun_dong_tiao_wei_zhi().width){
                    yan_su.style.left = 0 + gun_dong_tiao_wei_zhi().left + 'px';
                }
            }
            if (yan_su.offsetTop > getInner().height + gun_dong_tiao_wei_zhi().top - yan_su.offsetHeight) {
                yan_su.style.top = getInner().height + gun_dong_tiao_wei_zhi().top - yan_su.offsetHeight + 'px';
                if (yan_su.offsetTop <= 0 + gun_dong_tiao_wei_zhi().top){
                    yan_su.style.top = 0 + gun_dong_tiao_wei_zhi().top + 'px';
                }
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
            fixedScroll.top = gun_dong_tiao_wei_zhi().top;
            fixedScroll.left = gun_dong_tiao_wei_zhi().left;
            var chang_w = getInner().width;  //getInner()函数库函数，跨浏览器获取浏览器视窗大小
            var chang_h = getInner().height;
            yan_su.style.width = chang_w + gun_dong_tiao_wei_zhi().left + 'px';
            yan_su.style.height = chang_h + gun_dong_tiao_wei_zhi().top + 'px';
            yan_su.style.position = 'absolute';
            yan_su.style.top = '0';
            yan_su.style.left = '0';
            var y_style = getStyle(yan_su, 'display'); //getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
            if (y_style === "block") {
                addEvent(window, 'scroll', fixedScroll);  //定位滚动条
                gdt_cao_zuo('y');  //隐藏滚动条
            }
        } else {
            alert("遮罩锁屏区块,只能设置一个区块元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    };
    
    /** jie_chu_suo_ping()方法，将一个锁屏区块元素解除锁屏
     * 注意：一般需要在css文件将元素设置成隐藏
     **/
    feng_zhuang_ku.prototype.jie_chu_suo_ping = function () {
        for (var i = 0; i < this.jie_dian.length; i++) {
            this.jie_dian[i].style.display = 'none';
        }
        removeEvent(window, 'scroll', fixedScroll);  //删除定位滚动条
        gdt_cao_zuo('x');  //显示滚动条
        return this;
    };
    
    /**------------------------------------------------元素事件结束--------------------------------------------**/
    
    
    /**------------------------------------------------元素动画开始--------------------------------------------**/
    /**
     * 元素动画说明
     * yi_dong_tou_ming()方法，将一个元素，
     * 1，x将元素横向左移动或者右移动
     * 2, y将元素竖向上移动或者下移动
     * 3，w将元素动画增加或者减少宽度
     * 4，h将元素动画增加或者减少高度
     * 5，o将元素动画增加或者减少透明度
     * 注意：也可以写其他css属性名称（全称），来动画增加或者减少css属性的数值，必须是值为数值的css属性，如：font-size
     * *******************************************
     *
     **/
    
    
    
    
    /** yi_dong_tou_ming()方法，动态改变css属性说明
     * * yi_dong_tou_ming()方法，将一个元素，进行一下动画操作
     * 1，x将元素横向左移动或者右移动
     * 2, y将元素竖向上移动或者下移动
     * 3，w将元素动画增加或者减少宽度
     * 4，h将元素动画增加或者减少高度
     * 5，o将元素动画增加或者减少透明度
     * 注意：也可以写其他css属性名称（全称），来动画增加或者减少css属性的数值，必须是值为数值的css属性，如：font-size
     * *************************************
     *  x将元素横向左移动或者右移动，首先将目标设置定位，position:absolute;
     *  o将元素动画增加或者减少透明度，结合css里元素原始透明度filter: alpha(opacity=0);opacity: 0;
     *  *************************************
     *  yi_dong_tou_ming()方法，参数说明
     *  参数是一个对象如下
     *  yi_dong_tou_ming({
                'attr':'x',        【为动画方式】，   x.为横向移动，y.为竖向移动，w.为增加宽度动画，h.为增加高度动画，o.为透明度动画，【必填】
                                                      注意：也可以写其他css属性名称（全称），来动画增加或者减少css属性的数值，必须是值为数值的css属性，如：font-size
                                                      o.为透明度动画,设置透明度动画时，必须先在css里设置初始透明度如：opacity:1;filter:alpha(opacity=100);
                                                      否则IE9以下无法实现透明度动画
    
                'type':'1',        【动画模式】，     0.匀速模式，1.缓冲模式【可选，默认缓冲】
                'speed':6,         【缓冲速度】，     动画模式为缓冲时设置，【可选，默认为6】,以此值改变跨度.每一次动画动态增加或者减少，实现缓冲效果
    
                'start':50,        【动画起始位置】， 起始的像素或者透明度【可选，默认为对象原始位置】一般不需要传
                                                      注意：动画起始位置，一般按钮动画使用，如果是鼠标触动动画，会不停的初始化，因为鼠标一动就改变了动画起始位置
    
                'target':100,      【目标量】，       就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度【可先，注意目标量不填，增量必填】
                'alter':50,        【增量】，         就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度【可先，注意增量不填，目标量必填】
                'step':7,          【跨度】，         每一次动画增加或者减少的，像素或者透明度,【可选，默认20】
                'danwei':'em',     【属性值单位】     danwei.为属性值单位，也就是以什么单位来计算css属性，如是px还是em等，不传默认px
                't':50 ,           【每次动画时间】， 也就是多少毫秒执行一次动画【可选，默认10】
                fn:function () {   【回调函数，列队】， 回调函数，用于动画执行完毕后执行函数，在回调函数里在写入动画，就是列队动画，也就是一个动画执行完毕后执行第二个动画
    
                }
                mul:{              【同步动画对象】，用于同时要执行多个动画，同步动画属性，属性值为对象，对象里面是，动画方式:目标量，组合的键值对，只能动画方式加目标量的键值对
                                    同步动画，除了动画方式和目标量外，其他的都是在同步动画对象外设置，因为他们是统一的其他参数
                    'w':101,
                    'h':500,
                    'o':30
                }
            });
     **/
    feng_zhuang_ku.prototype.yi_dong_tou_ming = function (obj) {
        for (var i = 0; i < this.jie_dian.length; i++) {
            var element = this.jie_dian[i];
             // attr，为动画方式，
             // x.为横向移动
             // y.为竖向移动
             // w.为增加宽度动画
             // h.为增加高度动画
             // o.为透明度动画
            var attr = obj['attr'] == 'x' ? 'left' : obj['attr'] == 'y' ? 'top' :
                obj['attr'] == 'w' ? 'width' : obj['attr'] == 'h' ? 'height' :
                    obj['attr'] == 'o' ? 'opacity' : obj['attr'] != undefined ? obj['attr'] : 'left';
    
            // start.为动画起始位置，
            // 如果输入了动画起始位置，值就为输入的起始位置，移动动画是像素值（如100），透明度动画是透明度百分比（如50）
            // 如果没输入，默认移动动画获取的对象原始像素位置，透明度动画获取的对象原始透明度，除以100等于原始透明度百分比
            var start = obj['start'] != undefined ? obj['start'] :
                attr == 'opacity' ? parseFloat(getStyle(element, attr)) * 100 :
                    parseInt(getStyle(element, attr));
    
             // t.为每次动画时间，也就是多少毫秒执行一次动画
             // 不传默认，是10毫秒执行一次动画
            var t = obj['t'] != undefined ? obj['t'] : 10;
    
             // step.为跨度，每一次动画增加或者减少的，像素或者透明度
            var step = obj['step'] != undefined ? obj['step'] : 20;
    
            // danwei.为属性值单位，也就是以什么单位来计算css属性，如是px还是em等，不传默认px
            var danwei = obj['danwei'] != undefined ? obj['danwei'] : 'px';
    
             // alter.为增量，就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度
            var alter = obj['alter'];
    
             // target.为目标量，就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度
             // 注意，增量，是在原始上增加或者减少多少，目标量是在原始的基础上增加或者减少到目标
            var target = obj['target'];
    
            //mul,接收的，obj对象里的mul属性，而mul属性是一个对象，由动画方式加目标量组合的键值对，也就是要同步动画的参数
            var mul = obj['mul'];    //接收同步动画（参数对象）
    
             // speed.为缓冲速度，动画模式为缓冲时，以此值改变step.每一次动画动态增加或者减少，实现缓冲效果
             // 不传，默认为6
            var speed = obj['speed'] != undefined ? obj['speed'] : 6;
    
             // type.为动画模式，匀速为匀速模式，缓冲为缓冲模式
             // 不传，默认为缓冲模式
            var type = obj['type'] == 0 ? 'constant' : obj['type'] == 1 ? 'buffer' : 'buffer';
    
            if (alter != undefined && target == undefined) {
                target = alter + start;
            } else if (alter == undefined && target == undefined && mul == undefined) {
                throw new Error('alter增量，或target目标量，或者同步动画对象，必须传一个！');
            }
            if (start > target) step = -step;
    
            if (!isNaN(start)) {
                if (attr == 'opacity') {
                    element.style.opacity = parseInt(start) / 100;
                    element.style.filter = 'alpha(opacity=' + parseInt(start) + ')';
                } else {
                    element.style[attr] = start + danwei;
                }
            }
    
            if (mul == undefined){      //判断如果同步动画对象没有传，说明是单个动画
                mul = {};               //创建mul对象
                mul[attr] = target;     //将单个动画的，动画方式当作对象键，将目标量当作值，组合成键值对到对象里
            }
    
            clearInterval(element.timer);                            //给对每个象创建定时器并停止定时器
            element.timer = setInterval(function () {               //将对象下的定时器开启
                //创建一个布尔值，这个值可以了解对个动画是否执行完毕
                var flag = true;    //表示都执行完毕了
    
                //循环同步动画对象
                for (var i in mul) {
                    attr = i == 'x' ? 'left' : i == 'y' ? 'top' :
                        i == 'w' ? 'width' : i == 'h' ? 'height' :
                            i == 'o' ? 'opacity' : i != undefined ? i : 'left';            //得到同步动画对象里的，动画方式
                    target = mul[i];                                                       //得到同步动画对象里的，目标量
    
                    if (type == 'buffer') {
                        step = attr == 'opacity' ? (target - parseFloat(getStyle(element, attr)) * 100) / speed :
                        (target - parseInt(getStyle(element, attr))) / speed;
                        step = step > 0 ? Math.ceil(step) : Math.floor(step);
                    }
                    if (attr == 'opacity') {
                        if (step == 0) {
                            setOpacity();
                        } else if (step > 0 && Math.abs(parseFloat(getStyle(element, attr)) * 100 - target) <= step) {
                            setOpacity();
                        } else if (step < 0 && (parseFloat(getStyle(element, attr)) * 100 - target) <= Math.abs(step)) {
                            setOpacity();
                        } else {
                            var temp = parseFloat(getStyle(element, attr)) * 100;
                            element.style.opacity = parseInt(temp + step) / 100;
                            element.style.filter = 'alpha(opacity=' + parseInt(temp + step) + ')';
                        }
                        //判断目标值不等于元素当前值，说明动画还没到达目标值，将flag修改成false
                        if (parseInt(target) !=  parseInt(parseFloat(getStyle(element, attr)) * 100)) flag = false;
                    } else {
                        if (step == 0) {
                            setTarget();
                        } else if (step > 0 && Math.abs(parseInt(getStyle(element, attr)) - target) <= step) {
                            setTarget();
                        } else if (step < 0 && (parseInt(getStyle(element, attr)) - target) <= Math.abs(step)) {
                            setTarget();
                        } else {
                            element.style[attr] = parseInt(getStyle(element, attr)) + step + danwei;
                        }
                        //判断目标值不等于元素当前值，说明动画还没到达目标值，将flag修改成false
                        if (parseInt(target) != parseInt(getStyle(element, attr))) flag = false;
                    }
                }
                //判断flag = true;了说明元素的当前值已经达到目标值，可以停止定时器了
                if (flag) {
                    clearInterval(element.timer);       //停止定时器
                    if (obj.fn != undefined)obj.fn();   //判断如果传入了回调函数，动画执行完毕后执行回调函数,列队动画
                }
            }, t);
            function setTarget() {
                element.style[attr] = target + danwei;
            }
            function setOpacity() {
                element.style.opacity = parseInt(target) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(target) + ')';
            }
        }
        return this;
    };
    /**------------------------------------------------元素动画结束--------------------------------------------**/
    
    
    /**------------------------------------------------插件入口开始--------------------------------------------**/
    /** 插件入口，简单的理解就是通过extend()方法，向此基础库添加一个原型方法
     *  此extend()方法，一般是给插件文件使用的，插件就是通过extend()方法，将插件方法添加到基础库原型的
     *  接收两个参数
     *  参数1是传入要添加的方法名称
     *  参数2是此方法的执行函数（包含代码）
     *  使用方法：$().ext_end(方法名称，方法匿名函数)
     *
     **/
    feng_zhuang_ku.prototype.ext_end = function (name, fn) {
        feng_zhuang_ku.prototype[name] = fn;
    };
    /**------------------------------------------------插件入口结束--------------------------------------------**/
    
    
    /**------------------------------------------------ajax通讯开始--------------------------------------------**/
    
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
    feng_zhuang_ku.prototype.Ajax = function (obj) {
        //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2来模拟执行，如果支持JSON对象就用JSON对象
        //开源库json2写在函数库里
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
    /**------------------------------------------------ajax通讯结束--------------------------------------------**/
    
    
    /**------------------------------------------------表单序列化开始--------------------------------------------**/
    
    /** xu_lie_biao_dan()方法，表单序列化方法，将自动获取指定表单里面的各项字段name值和value值，无法连缀
     *  参数是要获取指定表单的原生态对象
     *  返回，包含表单数据的对象，如，{表单数据}
     **/
    feng_zhuang_ku.prototype.xu_lie_biao_dan = function (form) {
        var parts = {};
                for (var i = 0; i < form.elements.length; i++) {    //根据表单字段长度循环
                    var filed = form.elements[i];                   //得到没一项表单的字段
                    switch (filed.type) {                           //判断得到字段的属性
                        case undefined:
                        case 'submit':
                        case 'reset':
                        case 'file':
                        case 'button':
                            break;                                   //如果是以上几种的一种直接跳出
                        case 'radio':
                        case 'checkbox':
                            if (!filed.selected) break;              //如果是以上两种，判断是否被勾选，没勾选直接跳出
                        case 'select-one':
                        case 'select-multiple':
                            for (var j = 0; j < filed.options.length; j++) {     //下拉选项
                                var option = filed.options[j];
                                if (option.selected) {
                                    var optvalue = '';
                                    if (option.hasAttribute) {                   //非ie
                                        optvalue = (option.hasAttribute('value') ? option.value : option.text);             //value值存在取value值，value值不存在取text值
                                    } else {  //ie
                                        optvalue = (option.attributes('value').specified ? option.value : option.text);     //value值存在取value值，value值不存在取text值
                                    }
                                    parts[filed.name] = optvalue;                                                           //如果不是以上情况，将表单字段的name值加上value值，添加到对象
                                }
    
                            }
                            break;
                        default:
                            parts[filed.name] = filed.value;                                                                //如果不是以上情况，将表单字段的name值加上value值，添加到对象
                    }
                }
                return parts;
    };
    
    /**------------------------------------------------表单序列化结束--------------------------------------------**/
    
    
    
    
    
    
    
    /**█████████████████████████████████████████████████函数库██████████████████████████████████████████████████████**/
    
    /** 函数库说明：
     * sys浏览器检测对象，对象下有8个属性
     * dom_jia_zai()函数，DOM页面加载函数，等待页面结构加载完毕后就执行函数，不需要等待页面音频视频等文件加载完毕，提高加载速度
     * addEvent()函数库函数，跨浏览器添加事件绑定,注意：传入事件名称时不要on
     * removeEvent()函数库函数，跨浏览器删除事件绑定,注意：传入事件名称时不要on
     * getInner()函数库函数，跨浏览器获取浏览器视窗大小
     * gun_dong_tiao_wei_zhi()函数库函数，获取滚动条头部与浏览器头部的位置，获取底部滚动条与浏览器左边的位置
     * ju_li_liu_lan_qi_tou()函数库函数，跨浏览器获取当前元素的头部与浏览器头部的位置是多少
     * getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
     * hasClass()函数库函数，判断一个元素的class属性值是否存在
     * yuan_su_da_xiao()函数库函数，获取指定元素的绝对大小（包含边框）
     * getEvent()函数库函数，跨浏览器获取事件对象,事件event对象,
     * preDef()函数库函数，阻止事件默认行为,
     * trim()函数库函数，删除字符串的前后空格
     * scrollTop()函数库函数，滚动条清零，使滚动条无法下拉
     * gdt_cao_zuo()函数库函数，显示和隐藏浏览器滚动条
     * fixedScroll()函数库函数，定位滚动条
     * pd_shuzu()函数库函数，判断一个类容是否存在一个数组中，返回布尔值
     * sh_jd_suo_yin()函数库函数，获取当前节点的上一个节点，在父元素的索引
     * xia_jd_suo_yin()函数库函数，获取当前节点的下一个节点，在父元素的索引
     **/
    /**-----------------------------------------------------------------------------------------------------------------**/
    
    /** sys浏览器检测对象，对象下有8个属性
     * liu_lan_qi属性，检测浏览器名称和版本号，如：alert(sys.liu_lan_qi);
     * xi_tong属性，检测浏览器运行环境，如：alert(sys.xi_tong);
     * ie属性，检测IE浏览器的版本号，返回IE浏览器的版本号
     * firefox属性，检测firefox浏览器的版本号，返回firefox浏览器的版本号
     * chrome属性，检测chrome浏览器的版本号，返回chrome浏览器的版本号
     * opera属性，检测opera浏览器的版本号，返回opera浏览器的版本号
     * safari属性，检测safari浏览器的版本号，返回safari浏览器的版本号
     * webkit属性，检测webkit浏览器的版本号，返回webkit浏览器的版本号
     **/
    (function () {                       //闭包，自我执行
        window.sys = {};                  //全局变量对象，保存浏览器信息
        var ua = navigator.userAgent.toLowerCase();           //获取浏览器信息，并转化成小写
        var s = [];                                           //浏览器信息数组
        /**判断IE浏览器**/
        if ((/msie ([\d.]+)/).test(ua)) {                      //IE10以下判断字段为：msie x版本号
            s = ua.match(/msie ([\d.]+)/);                    //如果有获取到msie x版本号返回数组
            sys.liu_lan_qi = '浏览器为IE：' + s[1];            //向sys对象添加liu_lan_qi属性，属性值等于获取到的数组第二个元素
            sys.ie = s[1];
        } else if ((/trident/).test(ua)) {                      //ie10以上判断字段为：trident
            s = ua.match(/rv:([\d.]+)/);                      //如果有获取到trident字段返回数组
            sys.liu_lan_qi = '浏览器为IE：' + s[1];
            sys.ie = s[1];
        }
        /**判断火狐浏览器**/
        if ((/firefox\/([\d.]+)/).test(ua)) {                  //火狐判断字段为：firefox
            s = ua.match(/firefox\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为firefox：' + s[1];
            sys.firefox = s[1];
        }
        /**判断谷歌浏览器**/
        if ((/chrome\/([\d.]+)/).test(ua)) {                    //谷歌判断字段为：chrome
            s = ua.match(/chrome\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为chrome：' + s[1];
            sys.chrome = s[1];
        }
        /**判断Opera浏览器**/
        if ((/opera\/.*version\/([\d.]+)/).test(ua)) {         //谷歌判断字段为：opera 与 version
            s = ua.match(/opera\/.*version\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为Opera：' + s[1];
            sys.opera = s[1];
        }
        /**判断safari浏览器**/
        if ((/version\/([\d.]+).*safari/).test(ua)) {         //谷歌判断字段为：version 与 safari
            s = ua.match(/version\/([\d.]+).*safari/);
            sys.liu_lan_qi = '浏览器为Opera：' + s[1];
            sys.safari = s[1];
        }
        /**判断webkit浏览器**/
        if ((/webkit/).test(ua)) {                  //webkit判断字段为：webkit
            s = ua.match(/webkit\/([\d.]+)/);
            sys.liu_lan_qi = '浏览器为webkit：' + s[1];
            sys.webkit = s[1];
        }
        /**判断系统**/
        if (Boolean(navigator.platform)) {
            sys.xi_tong = '环境系统为：' + navigator.platform;
        } else {
            alert("无法检测到环境系统")
        }
    })();
    
    /** dom_jia_zai()函数，DOM页面加载函数，等待页面结构加载完毕后就执行函数，不需要等待页面音频视频等文件加载完毕，提高加载速度
     * 参数是页面结构加载完毕后要执行的函数
     * 一般前写前台js文件时，使用此方法加载DOM页面后执行代码，提高速度
     **/
    function dom_jia_zai(fn) {
        var isReady = false;
        var timer = null;
    
        function doReady() {
            if (timer) clearInterval(timer);
            if (isReady) return;
            isReady = true;
            fn();
        }
    
        if ((sys.opera && sys.opera < 9) || (sys.firefox && sys.firefox < 3) || (sys.webkit && sys.webkit < 525)) {
            timer = setInterval(function () {
                if (document && document.getElementById && document.getElementsByTagName && document.body) {
                    doReady();
                }
            }, 1);
        } else if (document.addEventListener) {//W3C
            addEvent(document, 'DOMContentLoaded', function () {
                fn();
                removeEvent(document, 'DOMContentLoaded', arguments.callee);
            });
        } else if (sys.ie && sys.ie < 9) {
            var timer = null;
            timer = setInterval(function () {
                try {
                    document.documentElement.doScroll('left');
                    doReady();
                } catch (e) {
                }
            }, 1);
        }
    }
    
    
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
     * e.target属性，在事件函数里写e.target属性，获取到事件对象元素的标签节点（包含一个事件对象里的子节点）
     **/
    function addEvent(obj, type, fn) {
        if (typeof obj.addEventListener != 'undefined') {
            obj.addEventListener(type, fn, false);
        } else {
            if (!obj.events) obj.events = {};                               //创建一个存放事件的哈希表(散列表)
            if (!obj.events[type]) {                                        //第一次执行时执行
                obj.events[type] = [];                                      //创建一个存放事件处理函数的数组
                if (obj['on' + type]) obj.events[type][0] = fn;             //把第一次的事件处理函数先储存到第一个位置上
            } else {
                if (addEvent.equal(obj.events[type], fn)) return false;    //同一个注册函数进行屏蔽，不添加到计数器中
            }
            obj.events[type][addEvent.ID++] = fn;                           //从第二次开始我们用事件计数器来存储
            obj['on' + type] = addEvent.exec;                               //执行事件处理函数
        }
    }
    /*-------------------------------------------------------------------------------------*/
    //为每个事件分配一个计数器
    //JS一切皆为对象，所以addEvent.ID语法正确，实际上是个全局变量
    addEvent.ID = 1;
    addEvent.exec = function (event) {                          //执行事件处理函数
        var e = event || addEvent.fixEvent(window.event);
        var es = this.events[e.type];
        for (var i in es) {
            es[i].call(this, e);
        }
    };
    addEvent.equal = function (es, fn) {                        //同一个注册函数进行屏蔽
        for (var i in es) {
            if (es[i] == fn) return true;
        }
        return false;
    };
    addEvent.fixEvent = function (event) {                      //把IE常用的Event对象配对到W3C中去
        event.preventDefault = addEvent.fixEvent.preventDefault;
        event.stopPropagation = addEvent.fixEvent.stopPropagation;
        event.target = event.srcElement;
        return event;
    };
    addEvent.fixEvent.preventDefault = function () {            //IE阻止默认行为
        this.returnValue = false;
    };
    addEvent.fixEvent.stopPropagation = function () {           //IE取消冒泡
        this.cancelBubble = true;
    };
    /*---------------------------------------------------------------------------------------*/
    
    
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
            if (obj.events) {
                for (var i in obj.events[type]) {
                    if (obj.events[type][i] == fn) {
                        delete obj.events[type][i];
                    }
                }
            }
        }
    }
    
    /** getInner()函数库函数，跨浏览器获取浏览器视窗大小
     * 返回一个对象，里面有两个属性
     * width属性，代表浏览器视窗宽度
     * height属性，代表浏览器视窗高度
     **/
    function getInner() {
        if (typeof window.innerWidth != 'undefined') {
            return {
                width: window.innerWidth,
                height: window.innerHeight
            }
        } else {
            return {
                width: document.documentElement.clientWidth,
                height: document.documentElement.clientHeight
            }
        }
    }
    
    /** gun_dong_tiao_wei_zhi()函数库函数，获取滚动条头部与浏览器头部的位置，获取底部滚动条与浏览器左边的位置
     * 无参
     * 返回一个对象
     * 对象有两个属性
     * top，返回，滚动条头部与浏览器头部的位置
     * left，返回，滚动条底部与浏览器底部的位置
     **/
    function gun_dong_tiao_wei_zhi() {
        return{
            top:document.documentElement.scrollTop || document.body.scrollTop,
            left:document.documentElement.scrollLeft || document.body.scrollLeft
        };
    }
    
    /** ju_li_liu_lan_qi_tou()函数库函数，跨浏览器获取当前元素的头部与浏览器头部的位置是多少
     *  参数是要获取的元素对象
     **/
    function ju_li_liu_lan_qi_tou(element) {
        var top = element.offsetTop;
        var parent = element.offsetParent;
        while (parent != null){
            top += parent.offsetTop;
            parent = parent.offsetParent;
        }
        return top;
    }
    
    /** getStyle()函数库函数，跨浏览器获取元素Style，样式指定属性
     * 两个参数
     * 参数1接收元素对象
     * 参数2接收css样式名称
     * 返回指定元素的指定样式值
     **/
    function getStyle(jie_dian, attr) {
        var value;
        if (typeof window.getComputedStyle != 'undefined') {//W3C
            value = window.getComputedStyle(jie_dian, null)[attr];
        } else if (typeof jie_dian.currentStyle != 'undeinfed') {//IE
            value = jie_dian.currentStyle[attr];
        }
        return value;
    }
    
    /** hasClass()函数库函数，判断一个元素的class属性值是否存在
     * 两个参数
     * 参数1接收元素对象
     * 参数2接收class属性值
     * 返回指定元素的class属性值是否存在，
     **/
    function hasClass(jie_dian, className) {
        return jie_dian.className.match(new RegExp('(\\s|^)' + className + '(\\s|$)'));
    }
    
    /** yuan_su_da_xiao()函数库函数，获取指定元素的绝对大小（包含边框）
     * 接收一个参数，参数是元素对象
     * 返回一个对象，里面有两个属性
     * width属性，元素的宽度
     * height属性，元素的高度
     **/
    function yuan_su_da_xiao(jie_dian) {
        return {
            width: jie_dian.offsetWidth,
            height: jie_dian.offsetHeight
        }
    }
    
    /** getEvent()函数库函数，跨浏览器获取事件对象,事件event对象,
     * 这个对象包含着所有与事件有关的信息。包括导致事件的元素、事件的类型、以及其它与特定事件相关的信息。
     * 接收一个参数，参数是事件函数的形式参数，也就是事件函数的形式参数接收到的event对象
     * 返回event对象,
     **/
    function getEvent(event) {
        return event || window.event;
    }
    
    /** preDef()函数库函数，阻止事件默认行为,
     * 接收一个参数，参数是事件函数的形式参数，也就是事件函数的形式参数接收到的event对象
     **/
    function preDef(event) {
        var e = getEvent(event);
        if (typeof e.preventDefault != 'undefined') {//W3C
            e.preventDefault();
        } else {//IE
            e.returnValue = false;
        }
    }
    
    /** trim()函数库函数，删除字符串的前后空格
     * 接收一个参数，参数是要删除前后空格的字符串
     **/
    function trim(str) {
        return str.replace(/(^\s*)|(\s*$)/g, '');
    }
    
    /** scrollTop()函数库函数，滚动条清零，使滚动条无法下拉
     * 无参
     **/
    function scrollTop() {
        document.documentElement.scrollTop = 0;
        document.body.scrollTop = 0;
    }
    
    /** gdt_cao_zuo()函数库函数，显示和隐藏浏览器滚动条
     * 有参，x为显示滚动条，y为隐藏滚动条
     **/
    function gdt_cao_zuo(zhi) {
        if (zhi == 'x'){
            parseFloat(sys.firefox) < 4 ? document.body.style.overflow = 'auto' : document.documentElement.style.overflow = 'auto';
        }else if(zhi == 'y'){
            parseFloat(sys.firefox) < 4 ? document.body.style.overflow = 'hidden' : document.documentElement.style.overflow = 'hidden';
        }else {
            alert('gdt_cao_zuo()函数库函数,参数不正确');
        }
    }
    
    /** fixedScroll()函数库函数，定位滚动条
     *  fixedScroll.left参数，是外部通过fixedScroll属性方式传递的，如外部fixedScroll.left = getScroll().left;
     **/
    function fixedScroll() {
        setTimeout(function () {
            window.scrollTo(fixedScroll.left, fixedScroll.top);
        }, 100);
    }
    
    /** pd_shuzu()函数库函数，判断一个类容是否存在一个数组中，返回布尔值
     * 参数1判断的数组，参数2判断的内容
     **/
    function pd_shuzu(shuzu, value) {
        for (var i in shuzu) {
            if (shuzu[i] === value) return true;
        }
        return false;
    }
    
    /** sh_jd_suo_yin()函数库函数，获取当前节点的上一个节点，在父元素的索引
     *  参数1，当前元素在父元素的索引
     *  参数2，父元素原生对象
     *  如果当前索引是开始位置0，返回的总索引减一
     *  如果当前索引是结束位置，返回的当前索引减一
     **/
    function sh_jd_suo_yin(suoy,fjid) {
        var length = fjid.children.length;    //获取父节点里所有子节点的长度
        if (suoy == 0) return length - 1;
        return parseInt(suoy) - 1;
    }
    
    /** xia_jd_suo_yin()函数库函数，获取当前节点的下一个节点，在父元素的索引
     *  参数1，当前元素在父元素的索引
     *  参数2，父元素原生对象
     *  如果当前索引是开始位置0，返回的当前索引减一
     *  如果当前索引是结束位置，返回0
     **/
    function xia_jd_suo_yin(suoy,fjid) {
        var length = fjid.children.length;    //获取父节点里所有子节点的长度
        if (suoy == length - 1) return 0;
        return parseInt(suoy) + 1;
    }
    
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃开源库json2开始▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    
    /** json2.js 开源库json2，
     *  如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
     **/
    
    if (typeof JSON !== 'object') {
        JSON = {};
    }
    (function () {
        'use strict';
        function f(n) {
            return n < 10 ? '0' + n : n;
        }
    
        if (typeof Date.prototype.toJSON !== 'function') {
            Date.prototype.toJSON = function (key) {
                return isFinite(this.valueOf())
                    ? this.getUTCFullYear() + '-' +
                f(this.getUTCMonth() + 1) + '-' +
                f(this.getUTCDate()) + 'T' +
                f(this.getUTCHours()) + ':' +
                f(this.getUTCMinutes()) + ':' +
                f(this.getUTCSeconds()) + 'Z'
                    : null;
            };
            String.prototype.toJSON =
                Number.prototype.toJSON =
                    Boolean.prototype.toJSON = function (key) {
                        return this.valueOf();
                    };
        }
        var cx = /[\u0000\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,
            escapable = /[\\\"\x00-\x1f\x7f-\x9f\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,
            gap,
            indent,
            meta = {    // table of character substitutions
                '\b': '\\b',
                '\t': '\\t',
                '\n': '\\n',
                '\f': '\\f',
                '\r': '\\r',
                '"': '\\"',
                '\\': '\\\\'
            },
            rep;
    
        function quote(string) {
            escapable.lastIndex = 0;
            return escapable.test(string) ? '"' + string.replace(escapable, function (a) {
                var c = meta[a];
                return typeof c === 'string'
                    ? c
                    : '\\u' + ('0000' + a.charCodeAt(0).toString(16)).slice(-4);
            }) + '"' : '"' + string + '"';
        }
    
        function str(key, holder) {
            var i,          // The loop counter.
                k,          // The member key.
                v,          // The member value.
                length,
                mind = gap,
                partial,
                value = holder[key];
            if (value && typeof value === 'object' &&
                typeof value.toJSON === 'function') {
                value = value.toJSON(key);
            }
            if (typeof rep === 'function') {
                value = rep.call(holder, key, value);
            }
            switch (typeof value) {
                case 'string':
                    return quote(value);
                case 'number':
                    return isFinite(value) ? String(value) : 'null';
                case 'boolean':
                case 'null':
                    return String(value);
                case 'object':
                    if (!value) {
                        return 'null';
                    }
                    gap += indent;
                    partial = [];
                    if (Object.prototype.toString.apply(value) === '[object Array]') {
                        length = value.length;
                        for (i = 0; i < length; i += 1) {
                            partial[i] = str(i, value) || 'null';
                        }
                        v = partial.length === 0
                            ? '[]'
                            : gap
                            ? '[\n' + gap + partial.join(',\n' + gap) + '\n' + mind + ']'
                            : '[' + partial.join(',') + ']';
                        gap = mind;
                        return v;
                    }
                    if (rep && typeof rep === 'object') {
                        length = rep.length;
                        for (i = 0; i < length; i += 1) {
                            if (typeof rep[i] === 'string') {
                                k = rep[i];
                                v = str(k, value);
                                if (v) {
                                    partial.push(quote(k) + (gap ? ': ' : ':') + v);
                                }
                            }
                        }
                    } else {
                        for (k in value) {
                            if (Object.prototype.hasOwnProperty.call(value, k)) {
                                v = str(k, value);
                                if (v) {
                                    partial.push(quote(k) + (gap ? ': ' : ':') + v);
                                }
                            }
                        }
                    }
                    v = partial.length === 0
                        ? '{}'
                        : gap
                        ? '{\n' + gap + partial.join(',\n' + gap) + '\n' + mind + '}'
                        : '{' + partial.join(',') + '}';
                    gap = mind;
                    return v;
            }
        }
    
        if (typeof JSON.stringify !== 'function') {
            JSON.stringify = function (value, replacer, space) {
                var i;
                gap = '';
                indent = '';
                if (typeof space === 'number') {
                    for (i = 0; i < space; i += 1) {
                        indent += ' ';
                    }
                } else if (typeof space === 'string') {
                    indent = space;
                }
                rep = replacer;
                if (replacer && typeof replacer !== 'function' &&
                    (typeof replacer !== 'object' ||
                    typeof replacer.length !== 'number')) {
                    throw new Error('JSON.stringify');
                }
                return str('', {'': value});
            };
        }
        if (typeof JSON.parse !== 'function') {
            JSON.parse = function (text, reviver) {
                var j;
    
                function walk(holder, key) {
                    var k, v, value = holder[key];
                    if (value && typeof value === 'object') {
                        for (k in value) {
                            if (Object.prototype.hasOwnProperty.call(value, k)) {
                                v = walk(value, k);
                                if (v !== undefined) {
                                    value[k] = v;
                                } else {
                                    delete value[k];
                                }
                            }
                        }
                    }
                    return reviver.call(holder, key, value);
                }
    
                text = String(text);
                cx.lastIndex = 0;
                if (cx.test(text)) {
                    text = text.replace(cx, function (a) {
                        return '\\u' +
                            ('0000' + a.charCodeAt(0).toString(16)).slice(-4);
                    });
                }
                if (/^[\],:{}\s]*$/
                        .test(text.replace(/\\(?:["\\\/bfnrt]|u[0-9a-fA-F]{4})/g, '@')
                            .replace(/"[^"\\\n\r]*"|true|false|null|-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?/g, ']')
                            .replace(/(?:^|:|,)(?:\s*\[)+/g, ''))) {
                    j = eval('(' + text + ')');
                    return typeof reviver === 'function'
                        ? walk({'': j}, '')
                        : j;
                }
                throw new SyntaxError('JSON.parse');
            };
        }
    }());
    /**▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃开源库json2结束▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃▃**/
    
    /**█████████████████████████████████████████████████函数库██████████████████████████████████████████████████████**/
[/code]



