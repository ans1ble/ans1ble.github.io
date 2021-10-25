---
layout: post
title: " 第一百一十八节，JavaScript，动态加载脚本和样式 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，动态加载脚本和样式**



****一动态脚本****

**当网站需求变大，脚本的需求也逐步变大。我们就不得不引入太多的JS脚本而降低了整站的性能，所以就出现了动态脚本的概念，在适时的时候加载相应的脚本。**

**比如：我们想在需要检测浏览器的时候，再引入检测文件。**



**1动态加载js文件**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //判断要加载的文件是否加载成功
        alert(typeof BrowserDetect);
    };
    
    
    //注意：判断加载写在，window.onload外面，也就是先加载代码，不然网页执行后在生成<script>元素标签就连接不了
    //设置一个变量，值为true再加载，值为false不加载文件
    var flag = true;
    
    if (flag) { //判断flag值为真时，执行加载js文件函数
        loadScript('browserdetect.js');
    }
    
    //定义加载js函数，接收一个参数要加载的js我们路径名称
    function loadScript(url) {
        //创建<script>元素标签
        var script = document.createElement('script');
        //向标签添加属性
        script.type = 'text/javascript';
        //向标签添加属性
        script.src = url;
        //向标签添加属性
        script.charset = 'utf-8';
        //通过标签名称获取到第一个<head>标签，将新创建<script>元素标签添加到<head>标签的子标签末尾
        document.getElementsByTagName('head')[0].appendChild(script);
    }
[/code]

**  2多态加载js代码**

[code]

    //注意：判断加载写在，window.onload外面，也就是先加载代码，不然网页执行后在生成<script>元素标签就连接不了
    //设置一个变量，值为true再加载，值为false不加载代码
    var flag = true;
    
    if (flag) { //判断flag值为真时，执行加载js代码函数
        loadScript(); //执行函数
    }
    
    //定义加载js代码函数，
    function loadScript() {
        //创建一个script标签
        var script = document.createElement('script');
        //向标签添加属性
        script.type = 'text/javascript';
        //向标签添加属性
        script.charset = 'utf-8';
        //要执行的代码
        script.text = "alert('你好')";
        //将script标签添加到第一个head标签的子标签末尾
        document.getElementsByTagName('head')[0].appendChild(script);
    }
[/code]

**PS：当然，如果不支持text，那么就可以针对不同的浏览器特性来使用不同的方法。这里就忽略写法了。**



****二动态样式****

**为了动态的加载样式表，比如切换网站皮肤。样式表有两种方式进行加载，一种是 <link>标签，一种是<style>标签。**

**1动态加载css文件**

[code]

     //动态执行link，加载css文件
    var flag = true;   //设置一个变量，值为true加载文件，false不加载
    
    //判断执行函数
    if (flag) {
        loadStyles('1.css');  //执行加载文件函数
    }
    
    function loadStyles(url) {  //接收一个参数，css文件路径名称
        //创建link标签元素
        var link = document.createElement('link');
        //添加link标签属性
        link.rel = 'stylesheet';
        //添加link标签属性
        link.type = 'text/css';
        //添加link标签属性
        link.href = url;
        //将新创建的link标签，添加到第一个head标签的子元素末尾
        document.getElementsByTagName('head')[0].appendChild(link);
    }
[/code]

**2动态加载css代码**

[code]

     //动态加载css代码
    var flag = true;  //设置一个变量，值为true加载样式代码，值为false不加载
    
    if (flag) {  //判断flag为真执行里面代码
        //创建一个style元素标签
        var style = document.createElement('style');
        //添加style元素属性
        style.type = 'text/css';
        //获取到第一个head标签，将新创建的style元素标签添加到head标签的子元素末尾
        document.getElementsByTagName('head')[0].appendChild(style);
        //执行样式函数
        insertRule(document.styleSheets[0], '#box', 'background:red', 0);
    }
    
    function insertRule(sheet, selectorText, cssText, position) {  //执行函数，接收4个参数，参数1css样式对象，参数2选择器名称，参数3样式代码，参数4要添加的位置
            //如果是非IE
        if (sheet.insertRule) { //判断如果为真
            //通过insertRule方法向样式表对象添加一个选择器
            sheet.insertRule(selectorText + "{" + cssText + "}", position);
            //如果是IE
        } else if (sheet.addRule) { //判断如果为真
            //通过addRule方法向样式表对象添加一个选择器
            sheet.addRule(selectorText, cssText, position);
        }
    }
[/code]



