---
layout: post
title: " 第一百七十节，jQuery，事件对象，event 对象，默认行为，冒泡 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，事件对象，event 对象，默认行为，冒泡**



**学习要点：**

**1.事件对象**

**2.冒泡和默认行为**



**JavaScript 在事件处理函数中默认传递了 event 对象，也就是事件对象。但由于浏览器 的兼容性，开发者总是会做兼容方面的处理。jQuery
在封装的时候，解决了这些问题，并且 还创建了一些非常好用的属性和方法。**



**一．事件对象**

**事件对象就是 event 对象，通过处理函数默认传递接受。之前处理函数的 e 就是 event 事件对象，event 对象有很多可用的属性和方法，我们在
JavaScript 课程中已经详细的了解 过这些常用的属性和方法，这里，我们再一次演示一下。**

**通过处理函数传递事件对象**

[code]

         //通过处理函数传递事件对象
        $('input').bind('click', function (e) { //接受事件对象参数
            alert(e);
        });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170307180233906-1318230108.png)

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170307180243625-1759784398.png)

**type 属性获取这个事件的事件类型，例如：click**

[code]

        $('div').click( function (e) {
            alert(e.type);  //打印click
        });
[/code]



**target 属性获取 **触发** 事件的 DOM
元素，就是触发元素的节点，比如，div下还有一个p，而div做了点击事件，点击div时得到的div节点，点击p时得到的p节点，适应冒泡规则**

[code]

        $('div').click(function (e) {
            alert(e.target);  //打印[object HTMLDivElement]
        });
[/code]



  
**data 属性获取事件调用时的额外数据，也就是可在事件函数里以形式参数的方式传参，用
**data来接收，额外数据，可以是数字、字符串、数组、对象****

[code]

        $('div').bind('click',123456, function (e) {
            alert(e.data);  //打印 123456
        });
[/code]

**注意：如果字符串就传递：'123'、如果是数组就传递：[123,'abc']，如果是对象就传递： {user : 'Lee', age :
100}。数组的调用方式是：e.data[1]，对象的调用方式是：e.data.user。**



  
**relatedTarget 属性获取移入移出目标点离开或进入的那个 DOM 元素，也就是鼠标移入或者移出时，鼠标经过路径中距离事件元素最近的节点**

[code]

        $('span').bind('mouseover', function (e) {
            alert(e.relatedTarget);  //打印 鼠标经过路径中距离事件元素最近的节点
        });
[/code]



  
**currentTarget 属性获取冒泡前触发的 DOM 元素，等同与 this，得到的监听元素的节点，也就是绑定事件的元素节点，不适应冒泡规则**

[code]

        $('div').click( function (e) {
            alert(e.currentTarget);  //打印[object HTMLDivElement]
        });
[/code]



  
**pageX **属性获取相对于页面原点的水平 **坐标，也就是网页左边起始位置与鼠标的位置******



[code]

        $('div').bind('click',function (e) {
            alert(e.screenX);  //打印 网页左边起始位置与鼠标的位置
        });
[/code]







**pageY 属性获取相对于页面原点的垂直坐标， ** ** **也就是网页头部起始位置与鼠标的位置********

[code]

        $('div').bind('click', function (e) {
            alert(e.screenY);  //打印 也就是网页头部起始位置与鼠标的位置
        });
[/code]



  
**screenX   **属性获取显示器屏幕位置的水平 **坐标(非 jQuery 封装)，也就是显示器视口左边位置与鼠标的位置******



[code]

        $('div').bind('click',function (e) {
            alert(e.screenX);  //打印 也就是显示器视口左边位置与鼠标的位置
        });
[/code]







**screenY 属性获取显示器屏幕位置的垂直坐标(非 jQuery 封装)， ** ** **也就是 ** ** **显示器******
视口头部位置与鼠标的位置********

[code]

        $('div').bind('click',function (e) {
            alert(e.screenY);  //打印 也就是显示器视口头部位置与鼠标的位置
        });
[/code]



  
**clientX   **属性获取相对于页面视口的水平 **坐标(非 jQuery 封装)， ** ** ** ** **也就是 ** **
**浏览器****** 视口左边位置与鼠标的位置****************



[code]

        $('div').bind('click',function (e) {
            alert(e.clientX);  //打印 也就是浏览器视口左边位置与鼠标的位置
        });
[/code]







**clientY 属性获取相对于页面视口的垂直坐标(非 jQuery 封装)， ** ** ** **也就是 ** ** **浏览器******
视口头部位置与鼠标的位置**********

[code]

        $('div').bind('click',function (e) {
            alert(e.clientY);  //打印 也就是浏览器视口头部位置与鼠标的位置
        });
[/code]



  
**result 属性获取上一个相同事件的返回值**

[code]

        $('div').bind('click', function () {
            return 123;
        });
    
        $('div').bind('click',function (e) {
            alert(e.result);  //打印 属性获取上一个相同事件的返回值123
        });
[/code]



  
**timeStamp 属性获取事件触发的时间戳**

[code]

        $('div').bind('click', function (e) {
            alert(e.timeStamp);  //打印 属性获取事件触发的时间戳,387015390
        });
[/code]



  
**which 属性获取鼠标的左中右键(1,2,3)，或获取键盘按键返回键码**

[code]

        $('input').bind('mousedown', function (e) {
            alert(e.which);  //打印 属性获取鼠标的左中右键(1,2,3)
        });
[/code]

[code]

        $('input').bind('keyup',function (e) {
            alert(e.which);  //打印 取键盘按键,返回键码
        });
[/code]



  
**altKey 属性获取是否按下了alt键**

[code]

        $('input').bind('click', function (e) {
            alert(e.altKey);  //打印 属性获取是否按下了alt键
        });
[/code]



  
**shiftKey 属性获取是否按下了shift键**

[code]

        $('input').bind('click', function (e) {
            alert(e.shiftKey);  //打印 属性获取是否按下了shift键
        });
[/code]



  
**ctrlKey 属性获取是否按下了ctrl键**

[code]

        $('input').bind('click', function (e) {
            alert(e.ctrlKey);  //打印 属性获取是否按下了ctrl键
        });
[/code]



  
**metaKey 属性获取是否按下了meta键**

  
**获取是否按下了 alt、shift、ctrl(这三个非 jQuery 封装)或**  
 **meta 键(IE 原生 meta 键，jQuery 做了封装)**





**二．冒泡和默认行为**

**如果在页面中重叠了多个元素，并且重叠的这些元素都绑定了同一个事件，那么就会出 现冒泡问题。**

**冒泡说明**

**html**

[code]

     <div style="width:200px;height:200px;background:red;">
        <input type="button" value="按钮"/>
    </div>
[/code]

**如果3个元素都需要绑定点击事件，这时点击最里面的input，就会产生冒泡行为，外围的元素都会被触发**



[code]

        //如果3个元素都需要绑定点击事件，这时点击最里面的input，就会产生冒泡行为，外围的元素都会被触发
        $('input').bind('click',function () {
            alert('点击input');  //打印
        });
        $('div').bind('click',function () {
            alert('点击div');  //打印
        });
        $(document).bind('click',function () {
            alert('点击document');  //打印
        });
[/code]

**注意：当我们点击文档的时候，只触发文档事件；当我们点击 div 层时，触发了 div 和 文档两个；当我们点击按钮时，触发了按钮、div
和文档。触发的顺序是从小范围到大范围。 这就是所谓的冒泡现象，一层一层往上。**



**jQuery 提供了一个事件对象的方法：event.stopPropagation()；这个方法设置到需要触发
的事件上时，所有上层的冒泡行为都将被取消。**

****stopPropagation()取消事件冒泡行为****

[code]

        $('input').bind('click', function (e) {
            alert('点击input');  //打印
            e.stopPropagation(); //取消冒泡行为
        });
        $('div').bind('click',function (e) {
            alert('点击div');  //打印
            e.stopPropagation(); //取消冒泡行为
        });
        $(document).bind('click',function () {
            alert('点击document');  //打印
        });
[/code]



**默认行为**

**网页中的元素，在操作的时候会有自己的默认行为。比如：右击文本框输入区域，会弹 出系统菜单、点击超链接会跳转到指定页面、点击提交按钮会提交数据。**

**preventDefault()阻止元素的默认行为**

[code]

        $('a').click( function (e) {
            e.preventDefault();  //阻止默认行为后超链接点击后无法跳转
        });
[/code]

**禁止提交表单跳转**

[code]

        $('form').submit( function (e) {
            e.preventDefault(); //阻止默认行为后，禁止提交表单跳转
        });
[/code]



**同时阻止默认行为和取消冒泡行为的简写方案**

**注意：如果想让上面的超链接同时阻止默认行为且禁止冒泡行为，可以把两个方法同时 写上：event.stopPropagation()和
event.preventDefault()。这两个方法如果需要同时启用的时候， 还有一种简写方案代替，就是直接 return false。**

[code]

        $('a').click( function (e) {
            return false;
        });
[/code]



**冒泡和默认行为的一些方法**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170308132847281-344059653.png)**

**preventDefault() 取消某个元素的默认行为**

[code]

    　　$('a').click( function (e) {
            e.preventDefault();  //阻止默认行为后超链接点击后无法跳转
        });
[/code]



  
**isDefaultPrevented() 判断是否调用了 preventDefault()方法**

[code]

     //判断是否取消了元素的默认行为
        $('input').keyup(function (e) {
            e.preventDefault();
            alert(e.isDefaultPrevented());
        });
[/code]



  
**stopPropagation() 取消事件冒泡**

[code]

    $('input').bind('click', function (e) {
            alert('点击input');  //打印
            e.stopPropagation(); //取消冒泡行为
        });
[/code]



  
**isPropagationStopped() 判断是否调用了 stopPropagation()方法**

[code]

     //判断是否调用了 stopPropagation()方法
        $('input').click(function (e) {
            e.stopPropagation();
            alert(e.isPropagationStopped());
        });
[/code]



  
**stopImmediatePropagation() 取消事件冒泡，并取消该事件的后续事件处理函数**

[code]

     //取消冒泡并取消后续事件处理函数
        $('input').click(function (e) {
            alert('input');
            e.stopImmediatePropagation();  //取消冒泡并取消后续事件处理函数
        });
        $('input').click(function () {     //这里属于后续事件，将不执行了
            alert('input2');
        });
        $(document).click(function () {
            alert('document');
        });
[/code]



  
**isImmediatePropagationStopped() 判断是否调用了 stopImmediatePropagation()方法**

[code]

     //判断是否执行了 stopImmediatePropagation()方法
        $('input').click(function (e) {
            e.stopImmediatePropagation();
            alert(e.isImmediatePropagationStopped());
        });
[/code]



