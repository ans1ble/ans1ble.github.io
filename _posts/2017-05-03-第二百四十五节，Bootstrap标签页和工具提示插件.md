---
layout: post
title: " 第二百四十五节，Bootstrap标签页和工具提示插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap标签页和工具提示插件**



**学习要点：**

**1.标签页**

**2.工具提示**



**本节课我们主要学习一下 Bootstrap 中的标签页和工具提示插件。**



**一．标签页选项卡**

**标签页也就是通常所说的选项卡功能。**

**基本用法**

**nav样式class类，写在 <ul>里，声明导航区域(Bootstrap)**  
 **nav-tabs样式class类，写在 <ul>里，设置导航样式为选项卡样式(Bootstrap)**  
 **active样式class类，写在 <li>里，设置当前菜单或当前内容为首选(Bootstrap)**  
 **data-toggle="tab"事件，写在 <li>里，设置菜单点击事件(Bootstrap)**  
 **tab-content样式class类，写在 <div>里，设置当前选项卡内容区域(Bootstrap)**  
 **tab-pane样式class类，写在选项卡内容区域里的 <div>里，设置当前选项内容样式(Bootstrap)**  
 **将选项卡的a标签href=对应内容div的id**

[code]

     <ul class="nav nav-tabs">
        <li class="active"><a href="#html5" data-toggle="tab">HTML5</a></li>
        <li><a href="#bootstrap" data-toggle="tab">Bootstrap</a></li>
        <li><a href="#jquery" data-toggle="tab">jQuery</a></li>
        <li><a href="#extjs" data-toggle="tab">ExtJS</a></li>
    </ul>
    <div class="tab-content" style="padding: 10px;">
        <div class="tab-pane active" id="html5">html5</div>
        <div class="tab-pane" id="bootstrap">bootstrap</div>
        <div class="tab-pane" id="jquery">jquery</div>
        <div class="tab-pane" id="extjs">extjs</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503200515242-1283718059.gif)



**可以设置淡入淡出效果 fade，而 in 表示首选的内容默认显示**

**fade样式class类，写在对应内容 <div>里，设置内容淡入淡出效果(Bootstrap)**  
 **in样式class类，写在对应内容 <div>里，设置首选内容淡入淡出效果(Bootstrap)**

[code]

    <ul class="nav nav-tabs">
        <li class="active"><a href="#html5" data-toggle="tab">HTML5</a></li>
        <li><a href="#bootstrap" data-toggle="tab">Bootstrap</a></li>
        <li><a href="#jquery" data-toggle="tab">jQuery</a></li>
        <li><a href="#extjs" data-toggle="tab">ExtJS</a></li>
    </ul>
    <div class="tab-content" style="padding: 10px;">
        <div class="tab-pane active fade in" id="html5">html5</div>
        <div class="tab-pane fade" id="bootstrap">bootstrap</div>
        <div class="tab-pane fade" id="jquery">jquery</div>
        <div class="tab-pane fade" id="extjs">extjs</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503201251226-1559369098.png)





**也可以换成胶囊式**

[code]

     <ul class="nav nav-pills">
        <li class="active"><a href="#html5" data-toggle="tab">HTML5</a></li>
        <li><a href="#bootstrap" data-toggle="tab">Bootstrap</a></li>
        <li><a href="#jquery" data-toggle="tab">jQuery</a></li>
        <li><a href="#extjs" data-toggle="tab">ExtJS</a></li>
    </ul>
    <div class="tab-content" style="padding: 10px;">
        <div class="tab-pane active fade in" id="html5">html5</div>
        <div class="tab-pane fade" id="bootstrap">bootstrap</div>
        <div class="tab-pane fade" id="jquery">jquery</div>
        <div class="tab-pane fade" id="extjs">extjs</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503201508148-704275429.png)



**将内容区域绑定到指定的选项卡导航的id**

**data-target="#xxk"事件，将内容区域绑定到指定的选项卡导航，避免多个导航冲突(Bootstrap)**

[code]

     <ul id="xxk" class="nav nav-pills">
        <li class="active"><a href="#html5" data-toggle="tab">HTML5</a></li>
        <li><a href="#bootstrap" data-toggle="tab">Bootstrap</a></li>
        <li><a href="#jquery" data-toggle="tab">jQuery</a></li>
        <li><a href="#extjs" data-toggle="tab">ExtJS</a></li>
    </ul>
    <div data-target="#xxk" class="tab-content" style="padding: 10px;">
        <div class="tab-pane active fade in" id="html5">html5</div>
        <div class="tab-pane fade" id="bootstrap">bootstrap</div>
        <div class="tab-pane fade" id="jquery">jquery</div>
        <div class="tab-pane fade" id="extjs">extjs</div>
    </div>
[/code]





**使用js执行选项卡**

**方法**

**tab('show')方法，将选项卡导航执行选项卡方法事件， 可以代替data-toggle="tab"**

[code]

    <ul id="xxk" class="nav nav-tabs">
        <li class="active"><a href="#html5">HTML5</a></li>
        <li><a href="#bootstrap">Bootstrap</a></li>
        <li><a href="#jquery">jQuery</a></li>
        <li><a href="#extjs">ExtJS</a></li>
    </ul>
    <div data-target="#xxk" class="tab-content" style="padding: 10px;">
        <div class="tab-pane active fade in" id="html5">html5</div>
        <div class="tab-pane fade" id="bootstrap">bootstrap</div>
        <div class="tab-pane fade" id="jquery">jquery</div>
        <div class="tab-pane fade" id="extjs">extjs</div>
    </div>
[/code]

**js**

[code]

    $( function () {
        $('#xxk a').on('click', function (e) {
            e.preventDefault();
            $(this).tab('show');
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503203305242-1039657687.png)



**事件**

**show.bs.tab 在调用 tab 方法时触发(Bootstrap)**  
 **shown.bs.tab 在显示整个标签时触发(Bootstrap)**

**js**

[code]

    $( function () {
        $('#xxk a').on('click', function (e) {
            e.preventDefault();
            $(this).tab('show');
        });
        $('#xxk a').on('show.bs.tab', function () {
            alert('调用 tab 时触发！');
        });
        $('#xxk a').on('shown.bs.tab', function () {
            alert('显示完 tab 时触发！');
        });
    });
[/code]

**HTML**

[code]

     <ul id="xxk" class="nav nav-tabs">
        <li class="active"><a href="#html5">HTML5</a></li>
        <li><a href="#bootstrap">Bootstrap</a></li>
        <li><a href="#jquery">jQuery</a></li>
        <li><a href="#extjs">ExtJS</a></li>
    </ul>
    <div data-target="#xxk" class="tab-content" style="padding: 10px;">
        <div class="tab-pane active fade in" id="html5">html5</div>
        <div class="tab-pane fade" id="bootstrap">bootstrap</div>
        <div class="tab-pane fade" id="jquery">jquery</div>
        <div class="tab-pane fade" id="extjs">extjs</div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503203844898-1324997074.png)







**二．工具提示**

**工具提示就是通过鼠标移动选定在特定的元素上时，显示相关的提示语。**

**基本实例**

**以下两个必须**

**data-toggle="tooltip"事件，写在需要工具提示的元素里，鼠标放上去显示根据提示(Bootstrap)**  
 **tooltip()方法，在需要工具提示的元素上使用，将当前元素执行工具提示(Bootstrap)**

**html**

[code]

     <a id="section" href="#" data-toggle="tooltip" title="超文本标识符">HTML5</a>
[/code]

**js**

[code]

    $( function () {
        $('#section').tooltip();
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503222454195-2014840314.png)



**工具提示有很多属性来配置提示的显示，具体如下：**

**data-animation 默认  true，在 tooltip 上应用一个 CSS fade 动画。如果设置
false，则不应用。设置是否工具提示淡入淡出**

**data-html 默认  false，不允许提示内容格式为 html。如果设置为 true，则可以设置 html
格式的提示内容。提示内容是否支持html标签**

**data-placement 默认值  top，还有 bottom、left、right 和 auto。如果 auto 会自行调整合适的位置，如果是
auto left则会尽量在左边显示，但左边不行就靠右边。设置提示信息位置**

**data-selector 默认  false，可以选择绑定指定的选择器。可以绑定一个自定义属性的元素**

**data-original-title 默认空字符串，提示语的内容。优先级比 title 低， 设置提示内容**

**title 默认字空符串， 提示语的内容。**

**data-trigger 默认值  hover foucs，表示怎么触发
tooltip，其他值为：click、manual。多个值用空格隔开，manual手动不能和其他同时设置。设置触发提示方式**

**data-delay 默认值 0，延迟触发 tooltip(毫秒)，如果传数字则，表示 show/hide 的毫秒数，如果传对象，结构为：
{show:500,hide:100}，设置提示显示和隐藏的延迟时间**

**data-container 默认值  false，将 tooltip 附加到特定的元素上。比如组合按钮组提示，容器不够，可以附加 body
上。container : 'body'，也就是如果提示信息被容器遮挡，可以设置一个外层div，将提示信息的容器重新指定到设置的div上**

**data-template 更改提示框的 HTML 提示语的模版，默认值为：**  
 ** <div class='tooltip'>**  
 ** <div class='tooltip-arrow'></div>**  
 ** <div class='tooltip-inner'></div>**  
 ** </div>**

**部分属性使用方法，其他相同**

[code]

     <a id="section" href="#" data-toggle="tooltip" title="超文本标识符"
       data-animation="true"
       data-html="true"
       data-placement="right"
       data-trigger="hover"
       data-delay="0"
    >HTML5</a>
[/code]

**js**

[code]

     $(function () {
        $('#section').tooltip();
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503225856242-1525591903.gif)





**js使用属性方法，将上面的属性 去掉 **data就是js里使用的属性 ，如 **data-delay就是 ** ** **delay********
** **  
********

**html**

[code]

     <a id="section" href="#" data-toggle="tooltip" title="<b>超文本标识符</b>">HTML5</a>
[/code]

**js   注意这是部分属性的js使用方式其他相同**

[code]

    $(function () {
        $('#section').tooltip({
            placement:"right",      //设置提示信息位置右
            html:"false"            //设置提示内容支持html标签
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170503231419851-1041461156.gif)





**工具提示方法**

**show工具提示方法参数，在工具提示元素上使用，显示工具提示(Bootstrap)**  
 **hide工具提示方法参数，在工具提示元素上使用，隐藏工具提示(Bootstrap)**  
 **toggle工具提示方法参数，在工具提示元素上使用，反转显示和隐藏工具提示(Bootstrap)**  
 **destroy工具提示方法参数，在工具提示元素上使用，隐藏并销毁工具提示(Bootstrap)**

**html**



[code]

    <a id="section" href="#" data-toggle="tooltip" title="<b>超文本标识符</b>">HTML5</a>
[/code]



**js**

[code]

    $( function () {
        $('#section').tooltip({
            placement: "right",      //设置提示信息位置右
            html: "false"            //设置提示内容支持html标签
        });
        $('#section').tooltip('show');
        //隐藏
        $('#section').tooltip('hide');
        //反转显示和隐藏
        $('#section').tooltip('toggle');
        //隐藏并销毁
        $('#section').tooltip('destroy');
    });
[/code]





**工具提示事件**

**show.bs.tooltip 在 show 方法调用时立即触发(Bootstrap)**  
 **shown.bs.tooltip 在提示框完全显示给用户之后触发(Bootstrap)**  
 **hide.bs.tooltip 在 hide 方法调用时立即触发(Bootstrap)**  
 **hidden.bs.tooltip 在提示框完全隐藏之后触发(Bootstrap)**

**html**

[code]

     <a id="section" href="#" data-toggle="tooltip" title="<b>超文本标识符</b>">HTML5</a>
[/code]

**js**

[code]

    $( function () {
        $('#section').tooltip({
            placement: "right",      //设置提示信息位置右
            html: "false"            //设置提示内容支持html标签
        });
        $('#section').on('show.bs.tooltip', function () {
            alert('调用 show 时触发！');
        });
        $('#section').on('shown.bs.tooltip', function () {
            alert('在提示框完全显示给用户之后触发！');
        });
        $('#section').on('hide.bs.tooltip', function () {
            alert('在 hide 方法调用时立即触发！');
        });
        $('#section').on('hidden.bs.tooltip', function () {
            alert('在提示框完全隐藏之后触发！');
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504002908679-934631885.png)



