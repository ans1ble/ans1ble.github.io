---
layout: post
title: " 第二百三十一节，Bootstrap 介绍 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap 介绍**



**学习要点：**

**1.Bootstrap 概述**

**2.Bootstrap 特点**

**3.Bootstrap 结构**

**4.创建第一个页面**

**5.学习的各项准备**



**本节课我们主要了解一下 Boostrap 历史、特点、用途，以及为什么选择 Boostrap 来开 发我们的 Web 项目。**



**一．Bootstrap 概述**

**Bootstrap 是由 Twitter 公司(全球最大的微博)的两名技术工程师研发的一个基于 HTML、CSS、JavaScript
的开源框架。该框架代码简洁、视觉优美，可用于快速、简单地 构建基于 PC 及移动端设备的 Web 页面需求。**





**2010 年 6 月，Twitter 内部的工程师为了解决前端开发任务中的协作统一问题。经历 各种方案后，Bootstrap 最终被确定下来，并于
2011 年 8 月发布。经过很长时间的迭代升 级，由最初的 CSS 驱动项目发展成为内置很多 JavaScript 插件和图标的多功能 Web 前端
的开源框架。**





**Bootstrap 最为重要的部分就是它的响应式布局，通过这种布局可以兼容 PC 端、PAD 以及手机移动端的页面访问。**



**Bootstrap 下载及演示：**

**国内文档翻译官网： http://www.bootcss.com **



**二．Bootstrap 特点**

**Bootstrap 非常流行，得益于它非常实用的功能和特点。主要核心功能特点如下：**

**(1).跨设备、跨浏览器 可以兼容所有现代浏览器，包括比较诟病的 IE7、8。当然，本课程不再考虑 IE9 以下 浏览器。**

**(2).响应式布局 不但可以支持 PC 端的各种分辨率的显示，还支持移动端 PAD、手机等屏幕的响应式切 换显示。**

**(3).提供的全面的组件 Bootstrap 提供了实用性很强的组件，包括：导航、标签、工具条、按钮等一系列组 件，方便开发者调用。**

**(4).内置 jQuery 插件 Bootstrap 提供了很多实用性的 jquery 插件，这些插件方便开发者实现 Web 中各种常规特效。**

**(5).支持 HTML5、CSS3 HTML5 语义化标签和 CSS3 属性，都得到很好的支持。**

**(6).支持 LESS 动态样式 LESS 使用变量、嵌套、操作混合编码，编写更快、更灵活的 CSS。它和 Bootstrap 能 很好的配合开发。**



**三．Bootstrap 结构**

**首先，想要了解 Boostrap 的文档结构，需要在官网先把它下载到本地。Bootstrap 下载地址如下： Bootstrap
下载地址：http://v3.bootcss.com/ (选择生产环境即可，v3.3.4)**

**解压后，目录呈现这样的结构：**

**bootstrap/**

**├── css/**

**│** **├── bootstrap.css css样式文件**

**│  ├── bootstrap.css.map css映射文件**

**│  ├── bootstrap.min.css  css压缩样式文件**

**│  ├── bootstrap-theme.css 主题 **样式** 文件**

**│  ├── bootstrap-theme.css.map  主题映射文件**

**│   ** ** **└──******  bootstrap-theme.min.css   主题压缩样式文件**

**├── js/**

**│  ├── bootstrap.js   js文件**

**│   **├──** bootstrap.min.js   js压缩文件**

******│** **└──npm.js 服务器端引入js文件******

**└── fonts/  跨平台字体文件  
**

**  ├── glyphicons-halflings-regular.eot **

**  ├── glyphicons-halflings-regular.svg **

**  ├── glyphicons-halflings-regular.ttf **

**  ├── glyphicons-halflings-regular.woff **

**  └── glyphicons-halflings-regular.woff2**



**主要分为三大核心目录：css(样式)、js(脚本)、fonts(字体)。**

**1.css 目录中有四个 css 后缀的文件，其中包含 min 字样的，是压缩版本，一般使用 这个；不包含的属于没有压缩的，可以学习了解 css
代码的文件；而 map 后缀的文件则是 css 源码映射表，在一些特定的浏览器工具中使用。**

**2.js 目录包含两个文件，是未压缩和压缩的 js 文件。**

**3.fonts 目录包含了不同后缀的字体文件。**



**四．创建第一个页面**

**我们创建一个 HTML5 的页面，并且将 Bootstrap 的核心文件引入，然后测试是否正常 显示。**

**html**

[code]

     <!DOCTYPE html>
    <html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
        <title>Bootstrap 介绍</title>
        <!--引入bootstrap样式文件-->
        <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    </head>
    <body>
    
    <!--创建一个按钮，执行两个class样式-->
    <button class="btn btn-info">Bootstrap</button>
    
    <!--引入jquery文件-->
    <script src="jquery/jquery.min.js"></script>
    <!--引入bootstrap里的js-->
    <script src="bootstrap/js/bootstrap.min.js"></script>
    </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170426234037569-216643954.png)



**五．学习的各项准备**

**1.测试工具，除了常规的现代浏览器，其次就是作为移动端的测试工具，我们这里采 用的是 Opera Mobile Emulator，和 Chrome
的移动 Web 测试工具。**

**2.所需基础，至少有 HTML5 第一季课程的基础，Bootstrap 内置了很多 jQuery 插件， 虽然使用起来比 jQuery 或 JS
本身要简单的多，但如果有 jQuery 和 JS 课程的基础，那学 习理解力就更加深入；**

**3.课程分辨率：基础课程，我们使用 1024 x 768 来录制，但某些特殊部分，比如响 应式和项目课程，需要大分辨率录制，会采用 1440 x 900
来录制。**

