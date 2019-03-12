---
layout: post
title: " 第二百一十四节，jQuery EasyUI，Calendar(日历)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Calendar(日历)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404235436019-831734813.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Canlendar(日历)组件的使用方法，这个组件不依赖于其 他组件。**



**一．加载方式**

**class 加载方式**

[code]

     <div id="box" class="easyui-calendar" style="width:200px;height:200px;"></div>
[/code]

**calendar()将一个元素执行日历组件**



**JS 加载调用**

[code]

    $( function () {
        $('#box').calendar({
    
        });
    });
[/code]





**二．属性列表**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404222209050-1830898473.png)

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404222250519-1910552095.png)

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404230248144-2136577461.png)**

**width   number 日历控件宽度。默认值180。**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300
        });
    });
[/code]



**height   number 日历控件高度。默认值180。**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300
        });
    });
[/code]



**fit   boolean 当设置为 true 的时候，将设置日历控件大小自适应父容器。默认值 false。**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            fit:true        //当设置为 true 的时候，将设置日历控件大小自适应父容器。默认值 false。
        });
    });
[/code]



**border   boolean 定义是否显示边框。默认值 true。**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            border:false    //定义是否显示边框。默认值 true。
        });
    });
[/code]



**firstDay   number 定义一周的第一天是星期几。0=星期日、1=星期一 等。定义星期几的排序0从星期日排序1从星期一排序**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            firstDay:1  //定义星期几的排序0从星期日排序1从星期一排序
        });
    });
[/code]



**weeks   array显 示 的 周 列 表 内 容 。 默 认 值
：['S','M','T','W','T','F','S']，定义星期几的显示文字**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            weeks:['S','M','T','W','T','F','S']  //定义星期几的显示文字
        });
    });
[/code]



**months   array显示的月列表内容。默认值：['Jan','Feb', 'Mar', 'Apr', 'May','Jun', 'Jul',
'Aug','Sep', 'Oct', 'Nov', 'Dec']，定义月份显示文字**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            months:['Jan','Feb', 'Mar', 'Apr', 'May','Jun', 'Jul', 'Aug','Sep', 'Oct', 'Nov', 'Dec']
        });
    });
[/code]



**year   number 年日历。下面的例子显示了如何使用指定的年份和月份创建一个日历。设置默认年份**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            year:1984,      //设置默认年份
            month:9,        //设置默认月份
        });
    });
[/code]



**month   number 月日历。 **设置默认月份****

[code]

    $( function () {
        $('#box').calendar({
            width:400,
            height:300,
            year:1984,      //设置默认年份
            month:9,        //设置默认月份
        });
    });
[/code]



**current   date 当前日期，设置默认当前日期**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            year:1984,      //设置默认年份
            month:9,        //设置默认月份
            current:new Date(1984,8,25)  //设置默认当前日期,月份从0开始所以9月就写8月
        });
    });
[/code]



**formatter   date 格式化日期，就是可以给每个日期添加自定义字符**

[code]

    $(function () {
        $('#box').calendar({
            width:400,
            height:300,
            formatter:function (date) {
                return '#' + date.getDate();
            }
        });
    });
[/code]



**styler   date 设置指定日期的样式，设置日期的样式**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
            styler: function (date) {
                if (date.getDate() == 1) {  //将每月1日改变样式
                    return 'background-color:#ccc';
                }
            }
        });
    });
[/code]



**validator   date 设置指定日期是否可以选择**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
            validator: function (date) {
                if (date.getDay() == 1) {  //将每个星期一设置为不可用
                    return false
                }else {
                    return true
                }
            }
        });
    });
[/code]





**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404232952035-1856688677.png)**

**onSelect   date 在用户选择一天的时候触发。**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
            onSelect: function (date) {
                alert(date.getFullYear() + "-" + (date.getMonth() + 1) + "-" + date.getDate());
                // date.getFullYear()用户选择的年
                // date.getMonth()用户选择的月
                // date.getDate()用户选择的日
            }
        });
    });
[/code]



  
**onChange   newDate, oldDate 在用户改变选择的时候触发。**



[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
            onChange: function (newDate, oldDate) {
                alert(newDate + '|' + oldDate);
                // newDate改变后的日期
                // oldDate改变前的日期
            }
        });
    });
[/code]







**四．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170404234045207-414785885.png)**

**options   none 返回参数对象。**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
        });
        alert($('#box').calendar('options'));  //返回参数对象
    });
[/code]



**resize   none 调整日历大小。就是如果日历变形后重置**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
        });
        $('#box').calendar('resize');  //调整日历大小。
    });
[/code]



**moveTo   date 移动日历到指定日期。默认选择日期**

[code]

    $(function () {
        $('#box').calendar({
            width: 400,
            height: 300,
        });
        $('#box').calendar('moveTo',new Date(2015,1,1));  //移动日历到指定日期
    });
[/code]



**我们可以使用$.fn.calendar.defaults 重写默认值对象。**



