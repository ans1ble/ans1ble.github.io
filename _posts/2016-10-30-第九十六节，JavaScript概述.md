
---
layout: post
title: " 第九十六节，JavaScript概述 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript概述**



**学习要点：**

**1.什么是JavaScript**

**2.JavaScript特点**

**3.JavaScript历史**

**4.JavaScript核心**

**5.开发工具集**



**JavaScript诞生于1995年。它当时的目的是为了验证表单输入的验证。因为在JavaScript问世之前，表单的验证都是通过服务器端验证的。而当时都是电话拨号上网的年代，服务器验证数据是一件非常痛苦的事情。**

**经过许多年的发展，JavaScript从一个简单的输入验证成为一门强大的编程语言。所以，学会使用它是非常简单的，而真正掌握它则需要很漫长的时间。那么本套视频就带领大家进入JavaScript课堂，去学习和理解它。**



**一．什么是JavaScript**

**JavaScript是一种具有面向对象能力的、解释型的程序设计语言。更具体一点，它是基于对象和事件驱动并具有相对安全性的客户端脚本语言。因为他不需要在一个语言环境下运行，而只需要支持它的浏览器即可。它的主要目的是，验证发往服务器端的数据、增加Web互动、加强用户体验度等。**



**二．JavaScript特点**

**松散性**

**JavaScript语言核心与C、C++、Java相似，比如条件判断、循环、运算符等。但，它却是一种松散类型的语言，也就是说，它的变量不必具有一个明确的类型。**

**对象属性**

**JavaScript中的对象把属性名映射为任意的属性值。它的这种方式很像哈希表或关联数组，而不像C中的结构体或者C++、Java中的对象。**

**继承机制**

**JavaScript中的面向对象继承机制是基于原型的，这和另外一种不太为人所知的Self语言很像，而和C++以及Java中的继承大不相同。**



**三．JavaScript历史**

**引子**

**大概在1992年，有一家公司Nombas开发一种叫做C--(C-minus-
minus,简称Cmm)的嵌入式脚本语言。后应觉得名字比较晦气，最终改名为ScripEase。而这种可以嵌入网页中的脚本的理念将成为因特网的一块重要基石。**

**诞生**

**1995年，当时工作在Netscape(网景)公司的布兰登(Brendan Eich)为解决类似于“向服务器提交数据之前验证”的问题。在Netscape
Navigator
2.0与Sun公司联手开发一个称之为LiveScript的脚本语言。为了营销便利，之后更名为JavaScript(目的是在Java这课大树下好乘凉)。**

**邪恶的后来者**

**因为JavaScript 1.0如此成功，所以微软也决定进军浏览器，发布了IE 3.0
并搭载了一个JavaScript的克隆版，叫做JScript（这样命名是为了避免与Netscape潜在的许可纠纷），并且也提供了自己的VBScript。**

**标准的重要**

**在微软进入后，有3种不同的JavaScript版本同时存在：Netscape Navigator
3.0中的JavaScript、IE中的JScript以及CEnvi中的ScriptEase。与C和其他编程语言不同的是，JavaScript并没有一个标准来统一其语法或特性，而这3种不同的版本恰恰突出了这个问题。随着业界担心的增加，这个语言标准化显然已经势在必行。**



**ECMA**

**1997年，JavaScript
1.1作为一个草案提交给欧洲计算机制造商协会（ECMA）。第39技术委员会（TC39）被委派来“标准化一个通用、跨平台、中立于厂商的脚本语言的语法和语义”（http://www.ecma-
international.org/memento/TC39.htm）。由来自Netscape、Sun、微软、Borland和其他一些对脚本编程感兴趣的公司的程序员组成的TC39锤炼出了ECMA-262，该标准定义了叫做ECMAScript的全新脚本语言。**

**灵敏的微软、迟钝的网景**

**虽然网景开发了JavaScript并首先提交给ECMA标准化，但因计划改写整个浏览器引擎的缘故，网景晚了整整一年才推出“完全遵循ECMA规范”的JavaScript1.3。而微软早在一年前就推出了“完全遵循ECMA规范”的IE4.0。这导致一个直接恶果：JScript成为JavaScript语言的事实标准。**

**标准的发展**

**在接下来的几年里，国际标准化组织及国际电工委员会（ISO/IEC）也采纳ECMAScript作为标准（ISO/IEC-16262）。从此，Web浏览器就开始努力（虽然有着不同程度的成功和失败）将ECMAScript作为JavaScript实现的基础。**

**山寨打败原创**

**JScript成为JavaScript语言的事实标准，加上Windows绑定着IE浏览器，几乎占据全部市场份额，因此，1999年之后，所有的网页都是基于JScript来开发的。而JavaScript1.x变成可怜的兼容者。**

**网景的没落与火狐的崛起**

**网景在微软强大的攻势下，1998年全面溃败。但，星星之火可以燎原。同年成立Mozilla项目中Firefox(火狐浏览器)在支持JavaScript方面无可比拟，在后来的时间里一步步蚕食IE的市场，成为全球第二大浏览器。**

**谷歌的野心**

**Google
Chrome，又称Google浏览器，是一个由Google（谷歌）公司开发的开放原始码网页浏览器。他以简洁的页面，极速的浏览，一举成为全球第三大浏览器。随着移动互联网的普及，嵌有Android系统的平板电脑和智能手机，在浏览器这块将大有作为。**

**苹果的战略**

**Safari浏览器是苹果公司各种产品的默认浏览器，在苹果的一体机(iMac)、笔记本(Mac)、MP4(ipod)、iphone(智能手机)、ipad(平板电脑)，并且在windows和Linux平台都有相应版本。目前市场份额全球第四，但随着苹果的产品不断的深入人心，具有称霸之势。**

**幸存者**

**Opera的全球市场份额第五，2%左右。它的背后没有财力雄厚的大公司，但它从“浏览器大战”存活下来的，有着非常大的潜力。**



**四．JavaScript核心**

**虽然JavaScript和ECMAScript通常被人们用来表达相同的含义，但JavaScript的含义却比ECMA-262中规定的要多得多。一个完整的JavaScript应该由下列三个不同的部分组成。**

**1.核心(ECMAScript)**

**2.文档对象模型(DOM)**

**3.浏览器对象模型(BOM)**



**ECMAScript介绍**

**由ECMAScript-262定义的ECMAScript与Web浏览器没有依赖关系。ECMAScript定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。我们常见的Web浏览器只是ECMAScript实现可能的宿主环境之一。**

**既然他不依赖于Web浏览器，那么他还在哪些环境中寄宿呢？比如：ActionScript、ScriptEase等。而他的组成部分有：语法、类型、语句、关键字、保留字、操作符、对象等。**



**ECMAScript版本**

**ECMAScript目前有四个版本，1、2、3、4、5版本，这里不再进行详细探讨。有兴趣的同学，可以搜索查阅。**

**Web浏览器对ECMAScript的支持**

**到了2008年，五大主流浏览器(IE、Firefox、Safari、Chrome、Opera)全部做到了与ECMA-262兼容。其中，只有Firefox力求做到与该标准的第4版兼容。以下是支持表。**

**浏 览 器**

|

**ECMAScript兼容性**  
  
---|---  
  
**Netscape Navigator 2**

|

**\----**  
  
**Netscape Navigator 3**

|

**\----**  
  
**Netscape Navigator 4 -- 4.05**

|

**\----**  
  
**Netscape Navigator 4.06 -- 4.79**

|

**第1版**  
  
**Netscape 6+ (Mozilla 0.6.0+)**

|

**第3版**  
  
**Internet Explorer 3**

|

**\----**  
  
**Internet Explorer 4**

|

**\----**  
  
**Internet Explorer 5**

|

**第1版**  
  
**Internet Explorer 5.5 -- 7**

|

**第3版**  
  
**Internet Explorer 8**

|

**第3.1版(不完全兼容)**  
  
**Internet Explorer 9**

|

**第5版**  
  
**Opera 6 - 7.1**

|

**第2版**  
  
**Opera 7.2+**

|

**第3版**  
  
**Opera 11+**

|

**第5版**  
  
**Safari 3+**

|

**第3版**  
  
**Firefox 1--2**

|

**第3版**  
  
**Firefox 3/4/5/6/7/8/9**

|

**第3/5版**  
  


**文档对象模型(DOM)**

**文档对象模型(DOM，Document Object Model)是针对XML但经过扩展用于HTML的应用程序编程接口(API，Application
Programming Interface)。**

**DOM有三个级别，每个级别都会新增很多内容模块和标准(有兴趣可以搜索查询)。以下是主流浏览器对DOM支持的情况：**

**浏 览 器**

|

**DOM兼容性**  
  
---|---  
  
**Netscape Navigator 1 -- 4.x**

|

**\----**  
  
**Netscape Navigator 6+(Mozilla 0.6.0+)**

|

**1级、2级(几乎全部)、3级(部分)**  
  
**Internet Explorer 2 -- 4.x**

|

**\----**  
  
**Internet Explorer 5**

|

**1级(最小限度)**  
  
**Internet Explorer 5.5 -- 7**

|

**1级(几乎全部)**  
  
**Opera 1 -- 6**

|

**\----**  
  
**Opera 7 -- 8.x**

|

**1级(几乎全部)、2级(部分)**  
  
**Opera 9+**

|

**1级、2级(几乎全部)、3级(部分)**  
  
**Safari 1.0x**

|

**1级**  
  
**Safari 2+**

|

**1级、2级(部分)**  
  
**Chrome 0.2+**

|

**1级、2级(部分)**  
  
**Firefox 1+**

|

**1级、2级(几乎全部)、3级(部分)**  
  


**浏览器对象模型(BOM)**

**访问和操作浏览器窗口的浏览器对象模型(BOM，Browser Object
Model)。开发人员使用BOM可以控制浏览器显示页面以外的部分。而BOM真正与众不同的地方(也是经常会导致问题的地方)，还是它作为JavaScript实现的一部分，至今仍没有相关的标准。**



**JavaScript版本**

**身为Netscape“继承人”的Mozilla公司，是目前唯一沿用最初的JavaScript版本编号的浏览器开发商。在网景把JavaScript转手给Mozilla项目的时候，JavaScript在浏览器中最后的版本号是1.3。后来，随着Mozilla继续开发，JavaScript版本号逐步递增。**

**浏 览 器**

|

**JavaScript版本**  
  
---|---  
  
**Netscape Navigator 2**

|

**1.0**  
  
**Netscape Navigator 3**

|

**1.1**  
  
**Netscape Navigator 4**

|

**1.2**  
  
**Netscape Navigator 4.06**

|

**1.3**  
  
**Netscape 6+ (Mozilla 0.6.0+)**

|

**1.5**  
  
**Firefox 1**

|

**1.5**  
  
**Firefox 1.5**

|

**1.6**  
  
**Firefox 2**

|

**1.7**  
  
**Firefox 3**

|

**1.8**  
  
**Firefox 3.1+**

|

**1.9**  
  


**五．开发工具集**

**代码编辑器：Notepad++。(在360软件管家里找到，直接下载安装即可)**

**浏览器：谷歌浏览器，火狐浏览器，IE浏览器，IETest工具等。**

**PS：学习JavaScript需要一定的基础，必须有xhtml+css基础、至少一门服务器端编程语言的基础(比如PHP)、一门面向对象技术(比如Java)、至少有一个Web开发的项目基础(例如留言板程序等)。**



