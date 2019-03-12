---
layout: post
title: " 第一百一十九节，JavaScript事件入门 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript事件入门**



**学习要点：**

**1.事件介绍**

**2.内联模型**

**3.脚本模型**

**4.事件处理函数**



**JavaScript事件是由访问Web页面的用户引起的一系列操作，例如：用户点击。当用户执行某些操作的时候，再去执行一系列代码。**



**一．** **事件介绍**

**事件一般是用于浏览器和用户操作进行交互。最早是IE和Netscape
Navigator中出现，作为分担服务器端运算负载的一种手段。直到几乎所有的浏览器都支持事件处理。而DOM2级规范开始尝试以一种复合逻辑的方式标准化DOM事件。IE9、Firefox、Opera、Safari和Chrome全都已经实现了“DOM2级事件”模块的核心部分。IE8之前浏览器仍然使用其专有事件模型。**

**JavaScript有三种事件模型：内联模型、脚本模型和DOM2模型。**



**二．内联模型**

**这种模型是最传统接单的一种处理事件的方法。在内联模型中，事件处理函数是HTML标签的一个属性，用于处理指定事件。虽然内联在早期使用较多，但它是和HTML混写的，并没有与HTML分离。**

**onclick事件处理函数，也就是鼠标点击后执行一个事件**

**在HTML中把事件处理函数作为属性执行JS代码**

[code]

     <input type="button" value="按钮" onclick="alert('Lee');"  />
[/code]

**在HTML中把事件处理函数作为属性执行JS函数**

[code]

     <!--也可以在js文件里写一个函数，在元素标签里写一个事件，用户点击后执行js文件里的函数-->
    <input type="button" value="按钮" onclick="box();"  />
[/code]

**PS：函数不得放到window.onload里面，这样就看不见了**



**三．** **脚本模型**

**由于内联模型违反了HTML与JavaScript代码层次分离的原则。为了解决这个问题，我们可以在JavaScript中处理事件。这种处理方式就是脚本模型。**

**脚本模型1**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        input.onclick = function () {    //通过元素节点执行一个事件，当用户点击后执行这个匿名函数
            alert('Lee'); //弹窗打印字符串
        };
    };
[/code]

**脚本模型2**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行box函数
        input.onclick = box;  //这里要注意是函数名称，不要加括号，否则会自动执行函数
    
        //box函数
        function box() {    //通过元素节点执行一个事件，当用户点击后执行这个匿名函数
            alert('Lee'); //弹窗打印字符串
        }
    };
[/code]



**四．** **事件处理函数**

**JavaScript可以处理的事件类型为： 鼠标事件、键盘事件、HTML事件。**



**JavaScript事件处理函数及其使用列表**

**事件处理函数**

|

**影响的元素**

|

**何时发生**  
  
---|---|---  
  
**onabort**

|

**图像**

|

**当图像加载被中断时**  
  
**onblur**

|

**窗口、框架、所有表单对象**

|

**当焦点从对象上移开时**  
  
**onchange**

|

**输入框，选择框和文本区域**

|

**当改变一个元素的值且失去焦点时**  
  
**onclick**

|

**链接、按钮、表单对象、图像映射区域**

|

**当用户单击对象时**  
  
**ondblclick**

|

**链接、按钮、表单对象**

|

**当用户双击对象时**  
  
**ondragdrop**

|

**窗口**

|

**当用户将一个对象拖放到浏览器窗口时**  
  
**onError**

|

**脚本**

|

**当脚本中发生语法错误时**  
  
**onfocus**

|

**窗口、框架、所有表单对象**

|

**当单击鼠标或者将鼠标移动聚焦到窗口或框架时**  
  
**onkeydown**

|

**文档、图像、链接、表单**

|

**当按键被按下时**  
  
**onkeypress**

|

**文档、图像、链接、表单**

|

**当按键被按下然后松开时**  
  
**onkeyup**

|

**文档、图像、链接、表单**

|

**当按键被松开时**  
  
**onload**

|

**主题、框架集、图像**

|

**文档或图像加载后**  
  
**onunload**

|

**主体、框架集**

|

**文档或框架集卸载后**  
  
**onmouseout**

|

**链接**

|

**当图标移除链接时**  
  
**onmouseover**

|

**链接**

|

**当鼠标移到链接时**  
  
**onmove**

|

**窗口**

|

**当浏览器窗口移动时**  
  
**onreset**

|

**表单复位按钮**

|

**单击表单的reset按钮**  
  
**onresize**

|

**窗口**

|

**当选择一个表单对象时**  
  
**onselect**

|

**表单元素**

|

**当选择一个表单对象时**  
  
**onsubmit**

|

**表单**

|

**当发送表格到服务器时**  
  


**PS：所有的事件处理函数都会都有两个部分组成，on +
事件名称，例如click事件的事件处理函数就是：onclick。在这里，我们主要谈论脚本模型的方式来构建事件，违反分离原则的内联模式，我们忽略掉。**

**对于每一个事件，它都有自己的触发范围和方式，如果超出了触发范围和方式，事件处理将失效。**



**1.鼠标事件，页面所有元素都可触发**

**onclick：当用户单击鼠标按钮或按下回车键时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onclick = function () {
            alert('你好')
        }
    };
[/code]

**ondblclick：当用户双击主鼠标按钮时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.ondblclick = function () {
            alert('Lee');
        };
    };
[/code]

**onmousedown：当用户按下了鼠标还未弹起时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onmousedown = function () {
            alert('Lee');
        };
    };
[/code]

**onmouseup：当用户释放鼠标按钮时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onmouseup = function () {
            alert('Lee');
        };
    };
[/code]

**onmouseover：当鼠标移到某个元素上方时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onmouseover = function () {
            alert('Lee');
        };
    };
[/code]

**onmouseout：当鼠标移出某个元素上方时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onmouseout = function () {
            alert('Lee');
        };
    };
[/code]

**onmousemove：当鼠标指针在元素上移动时触发。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件，点击后执行匿名函数
        input.onmousemove = function () {
            alert('Lee');
        };
    };
[/code]



**2.键盘事件**

**onkeydown：当用户按下键盘上任意键触发，如果按住不放，会重复触发。**

[code]

    onkeydown =  function () {
        alert('Lee');
    };
[/code]

**onkeypress：当用户按下键盘上的字符键触发，如果按住不放，会重复触发。代表字符的键**

[code]

    onkeypress =  function () {
        alert('Lee');
    };
[/code]

**onkeyup：当用户释放键盘上的键触发。**

[code]

    onkeyup =  function () {
        alert('Lee');
    };
[/code]



**3.HTML事件**

**onload：当页面完全加载后在window上面触发，或当框架集加载完毕后在框架集上触发。**

[code]

    window.onload =  function () {
        alert('Lee');
    };
[/code]

**onunload：当页面完全卸载后在window上面触发，或当框架集卸载后在框架集上触发。测试需要刷新后才能看到**

[code]

    window.onunload =  function () {
        alert('Lee');
    };
[/code]

**onselect：当用户选择文本框(input或textarea)中的一个或多个字符触发。**

[code]

     //<input type="text" value="文本"/>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件
        input.onselect = function () {
            alert('Lee');
        };
    };
[/code]

**  onchange：当文本框(input或textarea)内容改变且失去焦点后触发。也就是修改文本框内容后，鼠标在网页的其他任意地方点击后激发**

[code]

    //<input type="text" value="文本"/>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件
        input.onchange = function () {
            alert('Lee');
        };
    };
[/code]

**onfocus：当页面或者元素获得焦点时在window及相关元素上面触发。比如，当鼠标点击输入框获得焦点时激发**

[code]

     //<input type="text" value="文本"/>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件
        input.onfocus = function () {
            alert('Lee');
        };
    };
[/code]

**onblur：当页面或元素失去焦点时在window及相关元素上触发。。比如，当鼠标点击输入框后鼠标离开输入框后，点击页面其他部位激发  
**

[code]

     //<input type="text" value="文本"/>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var input = document.getElementsByTagName('input')[0];        //得到input对象
        //通过元素对象，添加一个事件
        input.onblur = function () {
            alert('Lee');
        };
    };
[/code]

**onsubmit：当用户点击提交按钮在 <form>元素上触发。**

[code]

    // <form>
    //     <input type="text" value="文本"/>
    //     <button type="submit">提交</button>   
    // </form> window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数 //脚本模型，事件 //通过标签名称获取到第一个元素节点 var form = document.getElementsByTagName('form')[0]; //得到input对象 //通过元素对象，添加一个事件 form.onsubmit = function () { alert('Lee'); }; };
[/code]

**onreset：当用户点击重置按钮在 <form>元素上触发。**

[code]

    // <form>
    //     <input type="text" value="文本"/>
    //     <button type="submit">提交</button>
    //     <button type="reset">重置</button>
    // </form>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //脚本模型，事件
        //通过标签名称获取到第一个元素节点
        var form = document.getElementsByTagName('form')[0];        //得到input对象
        //通过元素对象，添加一个事件
        form.onreset = function () {
            alert('Lee');
        };
    };
[/code]

**onresize：当窗口或框架的大小变化时在window或框架上触发。**

[code]

    window.onresize =  function () {
        alert('Lee');
    };
[/code]

**onscroll：当用户滚动带滚动条的元素时触发。**

[code]

    window.onscroll =  function () {
        alert('Lee');
    };
[/code]



