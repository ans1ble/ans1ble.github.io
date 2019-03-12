
---
layout: post
title: " 第一百四十五节，JavaScript，同步动画 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，同步动画**



**将上一节的，移动透明动画，修改成可以支持 **同步动画** ，也就是可以给这个动画方法多个动画任务，让它同时完成**



**原理：**



**向方法里添加一个属性，这个属性是一个对象，**
**同步动画属性，属性值为对象，对象里面是，动画方式:目标量，组合的键值对，只能动画方式加目标量的键值对**



[code]

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
            if (attr == 'opacity') {
                element.style.opacity = parseInt(start) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(start) + ')';
            } else {
                element.style[attr] = start + danwei;
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
[/code]



html代码

[code]

    <div id="ceshsdf">测试</div>
[/code]

css代码

[code]

    /*测试*/
    #ceshsdf{
        width:100px;
        height: 100px;
        background-color: #ff340e;
        position: absolute;
        top: 100px;
        left: 100px;
        opacity:1;
        filter:alpha(opacity=100);
    }
[/code]

前台js代码

[code]

    //测试
        $('#ceshsdf').on_click(function () {
            $('#ceshsdf').yi_dong_tou_ming({
                't':30,
                'step':10,
                mul:{      //同步动画属性，属性值为对象，对象里面是，动画方式:目标量，组合的键值对，只能动画方式加目标量的键值对
                    'w':500,
                    'h':500,
                    'o':30
                }
            });
        });
[/code]

首先要引入函数库和封装库文件

