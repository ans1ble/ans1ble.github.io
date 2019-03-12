
---
layout: post
title: " 第一百三十七节，JavaScript，封装库---修缮拖拽 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，封装库---修缮拖拽**

****修缮拖拽****

[code]

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
                    } else if (left > getInner().width - yan_su.offsetWidth) {
                        left = getInner().width - yan_su.offsetWidth;
                    }
                    if (top < 0) {
                        top = 0;
                    } else if (top > getInner().height - yan_su.offsetHeight) {
                        top = getInner().height - yan_su.offsetHeight;
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
[/code]





**前台代码**

**html代码**

[code]

     <div id="login">
        <h2 class="tbu"><img src="img/close.png" alt="" class="close" />网站登录</h2>
        <div class="user">帐 号：<input type="text" name="user" class="text" /></div>
        <div class="pass">密 码：<input type="password" name="pass" class="text" /></div>
        <div class="button"><input type="button" class="submit" value="" /></div>
        <div class="other">注册新用户 | 忘记密码？</div>
    </div>
[/code]

**前台js代码**

[code]

     //拖拽
        $().huo_qu_id('login').tuo_zhuai('tbu');
[/code]



