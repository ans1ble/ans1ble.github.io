---
layout: post
title: " 第一百五十九节，封装库--JavaScript，表单序列化结合ajax提交数据 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，表单序列化结合ajax提交数据**



****封装库， **表单序列化方法******

[code]

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
[/code]



**表单序列化结合ajax提交数据效果图**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170303155430235-180732556.png)**



提交到hj.php，返回

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170303155526454-403734687.png)



前台js

[code]

    var biaodan = $().xu_lie_biao_dan($('form').sh_jd());   //序列化获取表单数据，返回对象
            $().Ajax({                            //执行Ajax数据传输
                method:'post',                    //post方式发送
                url:'hj.php',                     //发送到hj.php
                data:biaodan,                     //发送内容，序列化获取到的表单对象
                success:function (text) {         //执行回调函数
                    alert(text);                  //打印出hj.php接收到的数据
                },
                async:true                        //异步模式
            });
[/code]



hj.php

[code]

    <?php
      echo 'www.jxiou.com';
      print_r($_POST);
    ?>
[/code]



