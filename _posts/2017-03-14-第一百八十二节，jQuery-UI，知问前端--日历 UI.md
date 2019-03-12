---
layout: post
title: " 第一百八十二节，jQuery-UI，知问前端--日历 UI "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery-UI，知问前端--日历 UI**



**学习要点：**

**1.调用 datepicker()方法**

**2.修改 datepicker()样式**

**3.datepicker()方法的属性**

**4.datepicker()方法的事件**



**日历（datepicker）UI，可以让用户更加直观的、更加方便的输入日期，并且还考虑不 同国家的语言限制，包括汉语。**



**一．调用 datepicker()方法**

[code]

     $('#date').datepicker();
[/code]



**二．修改 datepicker()样式**

**日历 UI 的 header 背景和对话框 UI 的背景采用的是同一个 class，所以，在此之前已经 被修改。所以，这里无须再修改了。**

[code]

     //无须修改 ui 里的 CSS，直接用 style.css 替代掉
    .ui-widget-header {
        background:url(../img/ui_header_bg.png);
    }
[/code]

**修改当天日期的样式**

[code]

     //修改当天日期的样式
    .ui-datepicker-today .ui-state-highlight {
        border:1px solid #eee;
        color:#f60;
    }
[/code]

**修改选定日期的样式**

[code]

     //修改选定日期的样式
    .ui-datepicker-current-day .ui-state-active {
    　　border:1px solid #eee;
    　　color:#06f;
    }
[/code]

**注意：其他修改方案类似。**



**日历ui是英文的，如果要使用中文，可以引入中文包，也可以将中文包放在ui插件文件的后面**

**中文包代码**

[code]

     //日历ui汉化包
    //Chinese initialisation for the jQuery UI date picker plugin.
    //Written by Cloudream (cloudream@gmail.com).
    jQuery(function($){
        $.datepicker.regional['zh-CN'] = {
            closeText: '关闭',
            prevText: '&#x3C;上月',
            nextText: '下月&#x3E;',
            currentText: '今天',
            monthNames: ['一月','二月','三月','四月','五月','六月',
            '七月','八月','九月','十月','十一月','十二月'],
            monthNamesShort: ['一月','二月','三月','四月','五月','六月',
            '七月','八月','九月','十月','十一月','十二月'],
            dayNames: ['星期日','星期一','星期二','星期三','星期四','星期五','星期六'],
            dayNamesShort: ['周日','周一','周二','周三','周四','周五','周六'],
            dayNamesMin: ['日','一','二','三','四','五','六'],
            weekHeader: '周',
            dateFormat: 'yy-mm-dd',
            firstDay: 1,
            isRTL: false,
            showMonthAfterYear: true,
            yearSuffix: '年'};
        $.datepicker.setDefaults($.datepicker.regional['zh-CN']);
    });
[/code]

**除了中文包，也可以通过属性来汉化**





**三．datepicker()方法的属性**

**日历方法有两种形式：1.datepicker(options)，options 是以对象键值对的形式传参，每个
键值对表示一个选项；2.datepicker('action', param)，action 是操作对话框方法的字符串，param 则是 options
的某个选项。**

**datepicker 国际化选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315144110745-2026544290.png)**



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315144122666-1457358687.png)

**日期格式代码**

d   月份中的天，从 1 到 31  
dd 月份中的天，从 01 到 31  
o  年份中的天，从 1 到 366  
oo 年份中的天，从 001 到 366  
D  星期中的天的缩写名称（Mon、Tue 等）  
DD  星期中的天的全写名称（Monday、Tuesday 等）  
m 月份，从 1 到 12  
mm 月份，从 01 到 12  
M 月份的缩写名称（Jan、February 等）

MM 月份的全写名称（January、February 等）  
y 两位数字的年份（14 表示 2014）  
yy  四位数字的年份（2014）  
@  从 01/01/1997 至今的毫秒数



**dateFormat mm/dd/yy/时间 指定日历返回的日期格式。 设置写入到输入框的年月日格式，如2017-03-12**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
            });
[/code]



**dayNames 英文日期/数组 以数组形式指定星期中的天的长格式。比如：Sunday、Monday 等。中文：星期日，
设置星期几长格式，日历UI如果太小可能无法显示**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNames : ['星期日','星期一','星期二','星期三','星期四','星期五','星期六']     //设置星期几长格式，日历UI如果太小可能无法显示
            });
[/code]



**dayNamesShort 英文日期/数组 以数组形式指定星期中的天的短格式。比如：Sun、Mon 等。
**设置星期几短格式，日历UI如果太小可能无法显示****

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesShort : ['星期日','星期一','星期二','星期三','星期四','星期五','星期六']     //设置星期几短格式，日历UI如果太小可能无法显示
            });
[/code]



**dayNamesMin 英文日期/数组 以数组形式指定星期中的天的最小格式。比如：Su、Mo 等。 ** **设置星期几 **最小**
格式，日历UI如果太小也能显示******

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六']  //设置星期几最小格式，日历UI如果太小也能显示
            });
[/code]



**monthNames 英文月份/数组以 数 组 形 式 指 定 月 份 的 长 格 式 名 称（January、February
等）。数组必须从January 开始。 设置月份的长格式**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月']  //设置月份的长格式
            });
[/code]



**monthNamesShort 英文月份/数组 以数组形式指定月份的短格式名称（Jan、Feb 等）。数组必须从 January 开始。
**设置月份的短格式，默认无法显示，有下拉菜单时有用****

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNamesShort : ['一','二','三','四','五','六','七','八','九','十','十一','十二']  //设置月份的短格式
            });
[/code]



**altField 无/字符串 为日期选择器指定一个 <input>域，就是指定一个输入框，将日期输入到指定的输入框里**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc'   //将日期输入到id为abc的输入框里
            });
[/code]



**altFormat 无/字符串 添加到 <input>域的可选日期格式， **就是指定一个输入框，将日期输入到指定的输入框里的日期格式****

[code]

            $('#date' ).datepicker({
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc',   //将日期输入到id为abc的输入框里
                altFormat : 'yy-mm-dd'  //就是指定一个输入框，将日期输入到指定的输入框里的日期格式
            });
[/code]



**appendText 无/字符串 在日期选择器的 <input>域后面附加文本，就是在输入日期的文本框后面添加文字**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc',   //将日期输入到id为abc的输入框里
                appendText : '(日历)'
            });
[/code]



**showWeek false/布尔值 显示周， 是否显示一年中的第几周**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc',   //将日期输入到id为abc的输入框里
                appendText : '(日历)',
                showWeek : true
            });
[/code]



**weekHeader 'Wk'/字符串 显示周的标题， 设置 **显示一年中的第几周标题****

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc',   //将日期输入到id为abc的输入框里
                appendText : '(日历)',
                showWeek : true,
                weekHeader : '周'
            });
[/code]



**firstDay 0/数值 指定日历中的星期从星期几开始。0 表示星期日。 设置星期几的排序方式，默认从星期日开始**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                altField : '#abc',   //将日期输入到id为abc的输入框里
                appendText : '(日历)',
                showWeek : true,
                weekHeader : '周',
                firstDay : 1
            });
[/code]



**datepicker 外观选项**



**disabled false/布尔值 禁用日历**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                disabled : true   //禁用日历
            });
[/code]



**numberOfMonths 1/数值日历中同时显示的月份个数。默认为 1，如果设置 3 就同时显示 3 个月份。也可以设置数组：[3,2]，3 行 2
列共 6 个。 设置显示日历个数，会按照月份向后显示**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                numberOfMonths : 3   //设置显示日历个数
            });
[/code]



**showOtherMonths false/布尔值如果设置为 true，当月中没有使用的单元格会显示填充，但无法使用。默认为
false，会隐藏无法使用的单元格。 填充空白日期单元格**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                showOtherMonths : true   //填充空白日期单元格
            });
[/code]



**selectOtherMonths false/布尔值如果设置为 true，表示可以选择上个月或下个月的日期。前提是
showOtherMonths设置为 true。 **填充空白日期单元格也可以选择****

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                showOtherMonths : true,   //填充空白日期单元格
                selectOtherMonths : true  //填充空白日期单元格也可以选择
            });
[/code]



**changeMonth false/布尔值 如果设置为 true，显示快速选择月份的下拉列表。 显示月份的下拉列表，结合月份短格式月份使用**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNamesShort : ['一','二','三','四','五','六','七','八','九','十','十一','十二'],  //设置月份的短格式
                changeMonth : true   //显示月份的下拉列表
    
            });
[/code]

**  长格式和短格式设置一样的，可以显示月字**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true   //显示月份的下拉列表
    
            });
[/code]



**changeYear false/布尔值 如果设置为 true，显示快速选择年份的下来列表。 设置年下拉列表**

[code]

           $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,   
                changeYear : true   //设置年下拉列表
    
            });
[/code]



**isRTL false/布尔值 是否由右向左绘制日历。 将日历框里的内容反排序**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                isRTL : true
    
            });
[/code]



**autoSize false/布尔值 是否自动调整控件大小，以适应当前的日期格式的输入， 是否自动适应输入框大小**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                autoSize : true  //是否自动适应输入框大小
    
            });
[/code]



**showOn 'focus'/字符串 默认值为 focus，获取焦点触发，还有button 点击按钮触发和 both 任一事件发生时触发。
设置日历由一个按钮触发**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showOn : 'button'  //设置日历由一个按钮触发
    
            });
[/code]



**buttonText '...'/字符串 触发按钮上显示的文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showOn : 'button',  //设置日历由一个按钮触发
                buttonText : '选择日期'
    
            });
[/code]



**buttonImage 无/字符串 图片按钮地址**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showOn : 'button',  //设置日历由一个按钮触发
                buttonText : '选择日期',
                buttonImage : '123png'  //图片按钮地址
    
            });
[/code]



**buttonImageOnly false/布尔值 设置为 true 则会使图片代替按钮， 隐藏按钮只显示按钮图片**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showOn : 'button',  //设置日历由一个按钮触发
                buttonText : '选择日期',
                buttonImage : '123png',  //图片按钮地址
                buttonImageOnly : true
    
            });
[/code]



**showButtonPanel false/布尔值 开启显示按钮面板， 日历显示/今天/关闭/两个按钮**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true  //日历显示/今天/关闭/两个按钮
    
            });
[/code]



**closeText 'done'/字符串 设置关闭按钮的文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天'
            });
[/code]



**currentText 'Today'/字符串 设置获取今日日期的按钮文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天'
            });
[/code]



**nextText 'Next'/字符串 设置下一月的 alt 文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天',
                nextText : '下一月',
                prevText : '上一月'
            });
[/code]



**prevText 'Prev'/字符串 设置上一月的 alt 文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天',
                nextText : '下一月',
                prevText : '上一月'
            });
[/code]



**navigationAsDateFormat false/字符串 设置 prev、next 和 current 的文字可以是format 的日期格式。
设置上一月、下一月、今天、3个地方后面是否显示日期格式**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true
            });
[/code]

  
**yearSuffix 无/字符串 附加在年份后面的文本**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                yearSuffix : '年'
            });
[/code]



**showMonthAfterYear false/布尔值 设置为 true，则将月份放置在年份之后， 调整年份和月份的位置**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                // changeMonth : true,
                // changeYear : true,   //设置年下拉列表
                // showButtonPanel : true,  //日历显示/今天/关闭/两个按钮
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                yearSuffix : '年',
                showMonthAfterYear : true  //调整年份和月份的位置
            });
[/code]





**datepicker 日期选择选项**

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315171854432-1628053248.png)

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315171901245-1348951525.png)

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315171908713-1986020671.png)

选择日期的字符串表示方法  
x 当前日期之后的 x 天（其中 x 范围从 1 到 n）比如：1，2  
-x 当前日期之前的 x 天（其中 x 范围从 1 到 n）比如：-1，-2  
xm 当前日期之后的 x 个月（其中 x 范围从 1 到 n）比如：1m，2m  
-xm 当前日期之前的 x 个月（其中 x 范围从 1 到 n）比如：-1m，-2m  
xw 当前日期之后的 x 周（其中 x 范围从 1 到 n）比如：1w，2w  
-xw 当前日期之后的 x 周（其中 x 范围从 1 到 n）比如：-1w，2w



**minDate 无/对象、字符串或数值 日历中可以选择的最小日期， 以当天为基准、向前可以选多少天**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                minDate : 0  //以当天为基准、向前可以选多少天
            });
[/code]



**maxDate 无/对象、字符串或数值 日历中可以选择的最大日期， **以当天为基准、向后可以选多少天****

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                minDate : 0,  //以当天为基准、向前可以选多少天
                maxDate : 0   //以当天为基准、向后可以选多少天
            });
[/code]



**defaultDate 当天/日期 预设默认选定日期。没有指定，则是当天。 一般不设置**



**yearRange 无/日期 设置下拉菜单年份的区间。比如：1950:2020，设置可选年份区间**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                yearRange : '1950:2020'  
            });
[/code]



**hideIfNoPrevNext false/字符串 设置为 true，如果上一月和下一月不存在，则隐藏按钮。 一般在设置基准天、向前或者向后时有用**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                yearRange : '1950:2020',  //一般不设置
                hideIfNoPrevNext : true
            });
[/code]



**gotoCurrent false/布尔值 如果为 true，点击今日且回车后选择的是当前选定的日期，而不是今日。 一般不使用**



**datepicker 视觉选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315180234620-209697055.png)**

**showAnim  fadeIn/字符串 设置 false，无效果。默认效果为：fadeIn。**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                yearRange : '1950:2020',  //一般不设置
                hideIfNoPrevNext : true,
                showAnim : false  //关闭视觉效果
            });
[/code]



  
**duration 300/数值 日历显示或消失时的持续时间，单位毫秒。 设置视觉效果毫秒数**



[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                currentText : '今天dd',
                nextText : '下一月mm',
                prevText : '上一月mm',
                navigationAsDateFormat : true,
                changeMonth : true,
                changeYear : true,   //设置年下拉列表
                yearRange : '1950:2020',  //一般不设置
                hideIfNoPrevNext : true,
                duration : 3000  //设置视觉效果毫秒数
            });
[/code]





**datepicker 可选特效**



**blind 日历从顶部显示或消失**  
 **bounce 日历断断续续地显示或消失，垂直运动**  
 **clip 日历从中心垂直地显示或消失**  
 **slide 日历从左边显示或消失**  
 **drop 日历从左边显示或消失，有透明度变化**  
 **fold 日历从左上角显示或消失**  
 **highlight 日历显示或消失，伴随着透明度和背景色的变化**  
 **puff 日历从中心开始缩放。显示时“收缩”，消失时“生长”**  
 **scale 日历从中心开始缩放。显示时“生长”，消失时“收缩”**  
 **pulsate 日历以闪烁形式显示或消失**  
 **fadeIn 日历显示或消失时伴随透明度变化**





**四．datepicker()方法的事件**

**除了属性设置外，datepicker()方法也提供了大量的事件。这些事件可以给各种不同状态 时提供回调函数。这些回调函数中的 this
值等于对话框内容的 div 对象，不是整个对话框的 div。**

**beforeShow **  
**日历显示之前会被调用。**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                beforeShow : function () {
                    alert('日历显示之前会被调用');
                }
            });
[/code]



**beforeShowDay**  
 **beforeShowDay(date)方法在显示日历中的每个日期时会**  
 **被调用(date 参数是一个 Date 类对象)。该方法必须返回**  
 **一个数组来指定每个日期的信息：**  
 **1.该日期是否可以被选择（数组的第一项，为 true 或 false）**  
 **2.该日期单元格上使用的 CSS 类**  
 **3.该日期单元格上显示的字符串提示信息。**

**getDate()会得到当前选定的所有日期**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                beforeShowDay : function (date) {
                    if (date.getDate() == 1) {  //判断日期等于1的
                        return [false,'a','不能选择'];  //第一个返回false将1禁止，第二关返回class为a可以到css里取设置样式，第三个返回提示
                    }else {
                        return [true];
                    }
                }
            });
[/code]



**onChangeMonthYear**  
 **onChangeMonthYear(year, month,inst)方法在日历中显示**  
 **的月份或年份改变时会被调用。或者 changeMonth 或**  
 **changeYear 为 true 时，下拉改变时也会触发。Year 当前**  
 **的年，month 当年的月，inst 是一个对象，可以调用一些**  
 **属性获取值。**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                onChangeMonthYear : function (year,month,inst) {
                    //alert('当年份或者月份改变时激活');
                    //alert(year); //得到改变后的年份
                    //alert(month); //得到改变后的月份
                    alert(inst.id); //得到当前对话框的对象
                }
            });
[/code]



**onClose**  
 **onClose(dateText, inst)方法在日历被关闭的时候调用。**  
 **dateText 是当时选中的日期字符串，inst 是一个对象，可**  
 **以调用一些属性获取值。**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                onClose : function (dateText, inst) {
                    //alert('在日历被关闭的时候调用');
                    alert(dateText); //得到选择后的年月日
                    //alert(inst.id); //得到当前对话框的对象
                }
            });
[/code]



**onSelect**  
 **onSelect(dateText, inst)方法在选择日历的日期时被调用。**  
 **dateText 是当时选中的日期字符串，inst 是一个对象，可**  
 **以调用一些属性获取值。**



[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭',
                onSelect : function (dateText, inst) {
                    //alert('在选择日历的日期时被调用');
                    alert(dateText); //得到选择后的年月日
                    //alert(inst.id); //得到当前对话框的对象
                }
            });
[/code]



**注意：jQuery UI 只允许使用选项中定义的事件。目前还不可以试用 on()方法来管理。**



**datepicker('action', param)方法**

**
![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170315185125838-1779103433.png)**



**datepicker('show') jQuery 对象 显示日历**

[code]

            $('#date' ).datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭'
            });
            $('#date').datepicker('show');
[/code]

**下面使用相同**

**datepicker('hide') jQuery 对象 隐藏日历**



**datepicker('getDate') jQuery 对象 获取当前选定日历**



**datepicker('setDate',date) jQuery 对象 设置当前选定日历**



**datepicker('destroy') jQuery 对象 删除日历，直接阻断。**



**datepicker('widget') jQuery 对象 获取日历的 jQuery 对象**



**datepicker('isDisabled') jQuery 对象 获取日历是否禁用**



**datepicker('refresh') jQuery 对象 刷新一下日历**



**datepicker('option', param) 一般值 获取 options 属性的值， 第二个参数是要获取的属性名称**

[code]

            $('#date').datepicker({
                dateFormat : 'yy-mm-dd',      //设置写入到输入框的年月日格式，如2017-03-12
                dayNamesMin : ['日','一','二','三','四','五','六'],  //设置星期几最小格式
                monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的长格式
                monthNamesShort : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],  //设置月份的短格式
                closeText : '关闭'
            });
            alert($('#date').datepicker('option', 'closeText'));
[/code]

**下面相同，只是下面是设置属性**

**datepicker('option', param,value)jQuery 对象 设置 options 属性的值，
第二关参数是要设置的属性名称，第三个参数是要设置的属性值**

