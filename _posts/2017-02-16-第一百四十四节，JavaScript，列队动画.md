第一百四十四节，JavaScript，列队动画

**JavaScript，列队动画**

**将上一节的，移动透明动画，修改成可以支持列队，也就是可以给这个动画方法多个动画任务，让它完成一个动画任务后，在执行第二个动画任务**

**原理：**

**就是在原有的动画方法里加一个回调函数，当动画执行完毕后执行回调函数，再在回调函数里写入动画任务去执行，实现列队动画**



    
    
    /** yi_dong_tou_ming()方法，说明
     * * yi_dong_tou_ming()方法，将一个元素，进行一下动画操作
     * 1，x将元素横向左移动或者右移动
     * 2, y将元素竖向上移动或者下移动
     * 3，w将元素动画增加或者减少宽度
     * 4，h将元素动画增加或者减少高度
     * 5，o将元素动画增加或者减少透明度
     * *************************************
     *  x将元素横向左移动或者右移动，首先将目标设置定位，position:absolute;
     *  o将元素动画增加或者减少透明度，结合css里元素原始透明度filter: alpha(opacity=0);opacity: 0;
     *  *************************************
     *  yi_dong_tou_ming()方法，参数说明
     *  参数是一个对象如下
     *  yi_dong_tou_ming({
                'attr':'x',        【为动画方式】，   x.为横向移动，y.为竖向移动，w.为增加宽度动画，h.为增加高度动画，o.为透明度动画，【必填】
                'type':'1',        【动画模式】，     0.匀速模式，1.缓冲模式【可选，默认缓冲】
                'speed':6,         【缓冲速度】，     动画模式为缓冲时设置，【可选，默认为6】,以此值改变跨度.每一次动画动态增加或者减少，实现缓冲效果
    
                'start':50,        【动画起始位置】， 起始的像素或者透明度【可选，默认为对象原始位置】
                                                      注意：动画起始位置，一般按钮动画使用，如果是鼠标触动动画，会不停的初始化，因为鼠标一动就改变了动画起始位置
    
                'target':100,      【目标量】，       就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度【可先，注意目标量不填，增量必填】
                'alter':50,        【增量】，         就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度【可先，注意增量不填，目标量必填】
                'step':7,          【跨度】，         每一次动画增加或者减少的，像素或者透明度,【可选，默认20】
                't':50             【每次动画时间】， 也就是多少毫秒执行一次动画【可选，默认10】
                fn:function () {   【每次动画时间】， 回调函数，用于动画执行完毕后执行函数，在回调函数里在写入动画，就是列队动画，也就是一个动画执行完毕后执行第二个动画
    
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
                    obj['attr'] == 'o' ? 'opacity' : 'left';
    
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
    
             // alter.为增量，就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度
            var alter = obj['alter'];
    
             // target.为目标量，就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度
             // 注意，增量，是在原始上增加或者减少多少，目标量是在原始的基础上增加或者减少到目标
            var target = obj['target'];
    
             // speed.为缓冲速度，动画模式为缓冲时，以此值改变step.每一次动画动态增加或者减少，实现缓冲效果
             // 不传，默认为6
            var speed = obj['speed'] != undefined ? obj['speed'] : 6;
    
             // type.为动画模式，匀速为匀速模式，缓冲为缓冲模式
             // 不传，默认为缓冲模式
            var type = obj['type'] == 0 ? 'constant' : obj['type'] == 1 ? 'buffer' : 'buffer';
            if (alter != undefined && target == undefined) {
                target = alter + start;
            } else if (alter == undefined && target == undefined) {
                throw new Error('alter增量或target目标量必须传一个！');
            }
            if (start > target) step = -step;
            if (attr == 'opacity') {
                element.style.opacity = parseInt(start) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(start) + ')';
            } else {
                element.style[attr] = start + 'px';
            }
            clearInterval(element.timer);                            //给对每个象创建定时器并停止定时器
            element.timer = setInterval(function () {               //将对象下的定时器开启
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
                } else {
                    if (step == 0) {
                        setTarget();
                    } else if (step > 0 && Math.abs(parseInt(getStyle(element, attr)) - target) <= step) {
                        setTarget();
                    } else if (step < 0 && (parseInt(getStyle(element, attr)) - target) <= Math.abs(step)) {
                        setTarget();
                    } else {
                        element.style[attr] = parseInt(getStyle(element, attr)) + step + 'px';
                    }
                }
                //document.getElementById('aaa').innerHTML += step + '<br />';
            }, t);
            function setTarget() {
                element.style[attr] = target + 'px';
                clearInterval(element.timer);
                if (obj.fn != undefined)obj.fn();   //判断如果传入了回调函数，动画执行完毕后执行回调函数
            }
            function setOpacity() {
                element.style.opacity = parseInt(target) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(target) + ')';
                clearInterval(element.timer);
                if (obj.fn != undefined)obj.fn();    //判断如果传入了回调函数，动画执行完毕后执行回调函数
            }
        }
        return this;
    };



html代码

    
    
    <div id="liedui">列队动画</div>

css代码

    
    
    #liedui{
        width: 100px;
        height: 100px;
        background-color: #ff340e;
        position: absolute;
        top: 100px;
        left: 100px;
    }

前台js代码

    
    
    //列队动画
        $('#liedui').on_click(function () {
            var _this = this;
            $(_this).yi_dong_tou_ming({                         //先执行这第一个动画
                'attr': 'w',     //动画模式
                'target': 500,   //目标量
                'step': 7,       //跨度
                't': 50,         //每次动画时间
                fn: function () {                              //等待第一个动画执行完毕后，再在动画回调函数里执行第二个动画
                    $(_this).yi_dong_tou_ming({
                        'attr': 'h',     //动画模式
                        'target': 200,   //目标量
                        'step': 7,       //跨度
                        't': 50          //每次动画时间
                    });
                }
            });
        });







**PS：对于多个动画冲突导致终止问题，是因为只采用了一个定时器，我们可以对每个动画分配一个定时器即可解决。**



    
    
    /** yi_dong_tou_ming()方法，说明
     * * yi_dong_tou_ming()方法，将一个元素，进行一下动画操作
     * 1，x将元素横向左移动或者右移动
     * 2, y将元素竖向上移动或者下移动
     * 3，w将元素动画增加或者减少宽度
     * 4，h将元素动画增加或者减少高度
     * 5，o将元素动画增加或者减少透明度
     * *************************************
     *  x将元素横向左移动或者右移动，首先将目标设置定位，position:absolute;
     *  o将元素动画增加或者减少透明度，结合css里元素原始透明度filter: alpha(opacity=0);opacity: 0;
     *  *************************************
     *  yi_dong_tou_ming()方法，参数说明
     *  参数是一个对象如下
     *  yi_dong_tou_ming({
                'attr':'x',        【为动画方式】，   x.为横向移动，y.为竖向移动，w.为增加宽度动画，h.为增加高度动画，o.为透明度动画，【必填】
                'type':'1',        【动画模式】，     0.匀速模式，1.缓冲模式【可选，默认缓冲】
                'speed':6,         【缓冲速度】，     动画模式为缓冲时设置，【可选，默认为6】,以此值改变跨度.每一次动画动态增加或者减少，实现缓冲效果
    
                'start':50,        【动画起始位置】， 起始的像素或者透明度【可选，默认为对象原始位置】
                                                      注意：动画起始位置，一般按钮动画使用，如果是鼠标触动动画，会不停的初始化，因为鼠标一动就改变了动画起始位置
    
                'target':100,      【目标量】，       就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度【可先，注意目标量不填，增量必填】
                'alter':50,        【增量】，         就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度【可先，注意增量不填，目标量必填】
                'step':7,          【跨度】，         每一次动画增加或者减少的，像素或者透明度,【可选，默认20】
                't':50             【每次动画时间】， 也就是多少毫秒执行一次动画【可选，默认10】
                fn:function () {   【每次动画时间】， 回调函数，用于动画执行完毕后执行函数，在回调函数里在写入动画，就是列队动画，也就是一个动画执行完毕后执行第二个动画
    
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
                    obj['attr'] == 'o' ? 'opacity' : 'left';
    
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
    
             // alter.为增量，就是在对象原始的像素或者透明度上，增加或者减少像素或者透明度
            var alter = obj['alter'];
    
             // target.为目标量，就是在原始的像素或者透明度上，增加或者减少到目标量的像素或者透明度
             // 注意，增量，是在原始上增加或者减少多少，目标量是在原始的基础上增加或者减少到目标
            var target = obj['target'];
    
             // speed.为缓冲速度，动画模式为缓冲时，以此值改变step.每一次动画动态增加或者减少，实现缓冲效果
             // 不传，默认为6
            var speed = obj['speed'] != undefined ? obj['speed'] : 6;
    
             // type.为动画模式，匀速为匀速模式，缓冲为缓冲模式
             // 不传，默认为缓冲模式
            var type = obj['type'] == 0 ? 'constant' : obj['type'] == 1 ? 'buffer' : 'buffer';
            if (alter != undefined && target == undefined) {
                target = alter + start;
            } else if (alter == undefined && target == undefined) {
                throw new Error('alter增量或target目标量必须传一个！');
            }
            if (start > target) step = -step;
            if (attr == 'opacity') {
                element.style.opacity = parseInt(start) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(start) + ')';
            } else {
                element.style[attr] = start + 'px';
            }
            clearInterval(element.timer);                            //给对每个象创建定时器并停止定时器
            element.timer = setInterval(function () {               //将对象下的定时器开启
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
                } else {
                    if (step == 0) {
                        setTarget();
                    } else if (step > 0 && Math.abs(parseInt(getStyle(element, attr)) - target) <= step) {
                        setTarget();
                    } else if (step < 0 && (parseInt(getStyle(element, attr)) - target) <= Math.abs(step)) {
                        setTarget();
                    } else {
                        element.style[attr] = parseInt(getStyle(element, attr)) + step + 'px';
                    }
                }
                //document.getElementById('aaa').innerHTML += step + '<br />';
            }, t);
            function setTarget() {
                element.style[attr] = target + 'px';
                clearInterval(element.timer);
                if (obj.fn != undefined)obj.fn();   //判断如果传入了回调函数，动画执行完毕后执行回调函数
            }
            function setOpacity() {
                element.style.opacity = parseInt(target) / 100;
                element.style.filter = 'alpha(opacity=' + parseInt(target) + ')';
                clearInterval(element.timer);
                if (obj.fn != undefined)obj.fn();    //判断如果传入了回调函数，动画执行完毕后执行回调函数
            }
        }
        return this;
    };



