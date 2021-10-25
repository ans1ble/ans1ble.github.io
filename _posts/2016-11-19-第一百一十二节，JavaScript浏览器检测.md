---
layout: post
title: " 第一百一十二节，JavaScript浏览器检测 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript浏览器检测**



**学习要点：**



**1.navigator对象**



**2.客户端检测**

**由于每个浏览器都具有自己独到的扩展，所以在开发阶段来判断浏览器是一个非常重要的步骤。虽然浏览器开发商在公共接口方面投入了很多精力，努力的去支持最常用的公共功能；但在现实中，浏览器之间的差异，以及不同浏览器的“怪癖”却是非常多的，因此客户端检测除了是一种补救措施，更是一种行之有效的开发策略。**



**一．** **navigator** **对象**

****navigator对象是window对象旗下的对象****

**navigator对象最早由Netscape
Navigator2.0引入的navigator对象，现在已经成为识别客户端浏览器的事实标准。与之前的BOM对象一样，每个浏览器中
的navigator对象也都有一套自己的属性。**



**navigator对象的属性或方法**

**属性或方法**

|

**说明**

|

**IE**

|

**Firefox**

|

**Safari/Chrome**

|

**Opera**  
  
---|---|---|---|---|---  
  
**appCodeName**

|

**浏览器的名称。通常是Mozilla，即使在非Mozilla浏览器中也是如此**

|

**3.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**appName**

|

**完整的浏览器名称**

|

**3.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**appMinorVersion**

|

**次版本信息**

|

**4.0+**

|

**-**

|

**-**

|

**9.5+**  
  
**appVersion**

|

**浏览器的版本。一般不与实际的浏览器版本对应**

|

**3.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**buildID**

|

**浏览器编译版本**

|

**-**

|

**2.0+**

|

**-**

|

**-**  
  
**cookieEnabled**

|

**表示cookie是否启用**

|

**4.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**cpuClass**

|

**客户端计算机中使用的CPU类型(x86、68K、Alpha、PPC、other)**

|

**4.0+**

|

**-**

|

**-**

|

**-**  
  
**javaEnabled()**

|

**表示当前浏览器中是否启用了Java**

|

**4.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**language**

|

**浏览器的主语言**

|

**-**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**mimeTypes**

|

**在浏览器中注册的MIME类型数组**

|

**4.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**onLine**

|

**表示浏览器是否连接到了因特网**

|

**4.0+**

|

**1.0+**

|

**-**

|

**9.5+**  
  
**opsProfile**

|

**似乎早就不用了。无法查询**

|

**4.0+**

|

**-**

|

**-**

|

**-**  
  
**oscpu**

|

**客户端计算机的操作系统或使用的CPU**

|

**-**

|

**1.0+**

|

**-**

|

**-**  
  
**platform**

|

**浏览器所在的系统平台**

|

**4.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**plugins**

|

**浏览器中安装的插件信息的数组**

|

**4.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**preference()**

|

**设置用户的首选项**

|

**-**

|

**1.5+**

|

**-**

|

**-**  
  
**product**

|

**产品名称（如Gecko）**

|

**-**

|

**1.0+**

|

**1.0+**

|

**-**  
  
**productSub**

|

**关于产品的次要信息（如Gecko的版本）**

|

**-**

|

**1.0+**

|

**1.0+**

|

**-**  
  
**registerContentHandler()**

|

**针对特定的MIME类型讲一个站点注册为处理程序**

|

**-**

|

**2.0+**

|

**-**

|

**-**  
  
**registerProtocolHandler()**

|

**针对特定的协议将一个站点注册为处理程序**

|

**-**

|

**2.0**

|

**-**

|

**-**  
  
**securityPolicy**

|

**已经废弃。安全策略的名称**

|

**-**

|

**1.0+**

|

**-**

|

**-**  
  
**systemLanguage**

|

**操作系统的语言**

|

**4.0+**

|

**-**

|

**-**

|

**-**  
  
**taintEnabled()**

|

**已经废弃。表示是否运行变量被修改**

|

**4.0+**

|

**1.0+**

|

**-**

|

**7.0+**  
  
**userAgent**

|

**浏览器的用户代理字符串**

|

**3.0+**

|

**1.0+**

|

**1.0+**

|

**7.0+**  
  
**userLanguage**

|

**操作系统的默认语言**

|

**4.0+**

|

**-**

|

**-**

|

**7.0+**  
  
**userProfile**

|

**借以访问用户个人信息的对象**

|

**4.0+**

|

**-**

|

**-**

|

**-**  
  
**vendor**

|

**浏览器的品牌**

|

**-**

|

**1.0+**

|

**1.0+**

|

**-**  
  
**verdorSub**

|

**有关供应商的次要信息**

|

**-**

|

**1.0+**

|

**1.0+**

|

**-**  
  
** **

**1.浏览器及版本号**

**不同的浏览器支持的功能、属性和方法各有不同。比如IE和Firefox显示的页面可能就会有所略微不同。**

**appName浏览器名称，不怎么精确**

[code]

    alert('浏览器名称：' + navigator.appName);
[/code]

**appVersion浏览器版本**

[code]

    alert('浏览器版本：' + navigator.appVersion);
     //返回：浏览器版本：5.0 (Windows)
[/code]

**userAgent浏览器用户代理字符串，用户浏览器相关信息【常用】**

[code]

    alert('浏览器用户代理字符串：' + navigator.userAgent);
     //返回：Mozilla/5.0 (Windows NT 10.0; WOW64; rv:50.0) Gecko/20100101 Firefox/50.0
[/code]

**platform浏览器所在的系统【常用】**

[code]

    alert('浏览器所在的系统：' + navigator.platform);
     //返回：浏览器所在的系统：Win32
[/code]



**2.浏览器嗅探器【推荐】**

**浏览器嗅探器是一段程序，有了它，浏览器检测就变得简单了。我们这里提供了一个browserdetect.js文件，用于判断浏览器的名称、版本号及操作系统。**

******browserdetect.js文件， **浏览器嗅探器模块源码********

[code]

     var BrowserDetect = {
        init: function () {
            this.browser = this.searchString(this.dataBrowser) || "An unknown browser";
            this.version = this.searchVersion(navigator.userAgent)
                || this.searchVersion(navigator.appVersion)
                || "an unknown version";
            this.OS = this.searchString(this.dataOS) || "an unknown OS";
        },
        searchString: function (data) {
            for (var i=0;i<data.length;i++)    {
                var dataString = data[i].string;
                var dataProp = data[i].prop;
                this.versionSearchString = data[i].versionSearch || data[i].identity;
                if (dataString) {
                    if (dataString.indexOf(data[i].subString) != -1)
                        return data[i].identity;
                }
                else if (dataProp)
                    return data[i].identity;
            }
        },
        searchVersion: function (dataString) {
            var index = dataString.indexOf(this.versionSearchString);
            if (index == -1) return;
            return parseFloat(dataString.substring(index+this.versionSearchString.length+1));
        },
        dataBrowser: [
            {
                string: navigator.userAgent,
                subString: "Chrome",
                identity: "Chrome"
            },
            {     string: navigator.userAgent,
                subString: "OmniWeb",
                versionSearch: "OmniWeb/",
                identity: "OmniWeb"
            },
            {
                string: navigator.vendor,
                subString: "Apple",
                identity: "Safari",
                versionSearch: "Version"
            },
            {
                prop: window.opera,
                identity: "Opera",
                versionSearch: "Version"
            },
            {
                string: navigator.vendor,
                subString: "iCab",
                identity: "iCab"
            },
            {
                string: navigator.vendor,
                subString: "KDE",
                identity: "Konqueror"
            },
            {
                string: navigator.userAgent,
                subString: "Firefox",
                identity: "Firefox"
            },
            {
                string: navigator.vendor,
                subString: "Camino",
                identity: "Camino"
            },
            {        // for newer Netscapes (6+)
                string: navigator.userAgent,
                subString: "Netscape",
                identity: "Netscape"
            },
            {
                string: navigator.userAgent,
                subString: "MSIE",
                identity: "Internet Explorer",
                versionSearch: "MSIE"
            },
            {
                string: navigator.userAgent,
                subString: "Gecko",
                identity: "Mozilla",
                versionSearch: "rv"
            },
            {         // for older Netscapes (4-)
                string: navigator.userAgent,
                subString: "Mozilla",
                identity: "Netscape",
                versionSearch: "Mozilla"
            }
        ],
        dataOS : [
            {
                string: navigator.platform,
                subString: "Win",
                identity: "Windows"
            },
            {
                string: navigator.platform,
                subString: "Mac",
                identity: "Mac"
            },
            {
                   string: navigator.userAgent,
                   subString: "iPhone",
                   identity: "iPhone/iPod"
            },
            {
                string: navigator.platform,
                subString: "Linux",
                identity: "Linux"
            }
        ]
    
    };
    BrowserDetect.init();
[/code]

**将browserdetect.js文件，放到工程目录，并将文件引入html页面即可使用模块的方法**





**调用方式**

|

**说明**  
  
---|---  
  
**BrowserDetect.browser**

|

**浏览器的名称，例如Firefox，IE**  
  
**BrowserDetect.version**

|

**浏览器的版本，比如，7、11**  
  
**BrowserDetect.OS**

|

**浏览器所宿主的操作系统，比如Windows、Linux**  
  




[code]

    alert(BrowserDetect.browser);            //浏览器名称
    //Firefox
    alert(BrowserDetect.version);                //版本
    //50
    alert(BrowserDetect.OS);                //系统
    //Windows
[/code]



**3.检测插件**

**插件是一类特殊的程序。他可以扩展浏览器的功能，通过下载安装完成。比如，在线音乐、视频动画等等插件。**

**plugins属性，这是一个数组。存储在浏览器已安装插件的完整列表。IE不支持**

[code]

    alert(navigator.plugins); //返回数组
    //[object PluginArray]
[/code]

**plugins属性下的属性**



**属性**

|

**含义**  
  
---|---  
  
**name**

|

**插件名**  
  
**filename**

|

**插件的磁盘文件名**  
  
**length**

|

**plugins数组的元素个数**  
  
**description**

|

**插件的描述信息**  
  


**列出所有的插件名**

[code]

     //列出所有的插件名
    for (var i = 0; i < navigator.plugins.length; i ++) {  //根据数组的长度循环次数
        document.write('插件名称：'+ navigator.plugins[i].name + '<br />'); //循环出插件名称
        document.write('插件的磁盘文件名：'+ navigator.plugins[i].filename + '<br />'); //循环出插件的磁盘文件名
        document.write('插件的描述信息：'+ navigator.plugins[i].description + '<br />'); //循环出插件的描述信息
        document.write('<br>');
    }
[/code]

**  检测非IE浏览器插件是否存在**

[code]

    //检测非IE浏览器插件是否存在
    function hasPlugin(name) {  //创建函数
        var name = name.toLowerCase(); //将接收的字母转换成小写
        for (var i = 0; i < navigator.plugins.length; i ++) {  //根据浏览器插件长度循环次数
            if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1) { //判断循环到的浏览器插件名称转换小写后，用正则查找传入的插件名称是否存在，返回值大于-1说明存在
                return true; //存在返回真
            }
        }
        return false; //不存在返回假
    }
    
    alert(hasPlugin('Flash'));                        //检测Flash是否存在
    alert(hasPlugin('java'));                        //检测Java是否存在
[/code]



**4.ActiveX，IE浏览器没有插件的说法，采用的 **ActiveX控件****

**IE浏览器没有插件，但提供了ActiveX控件。ActiveX控件一种在Web页面中嵌入对象或组件的方法。**

**由于在JS中，我们无法把所有已安装的ActiveX控件遍历出来，但我们还是可以去验证是否安装了此控件。**

**检测IE中的控件**

**ActiveXObject()判断浏览器是否支持控件，如果支持控件接收控件名称检测控件是否存在，存在就可以new
ActiveXObject对象，否则出错，参数控件唯一标识符**

[code]

     //检测IE中的控件
    function hasIEPlugin(name) {  //创建函数
        try {   //尝试执行，执行成功就执行里面的代码，如果出错就执行catch里面的代码
            new ActiveXObject(name); //判断浏览器是否支持控件，如果支持控件接收控件名称检测控件是否存在，存在就可以new ActiveXObject对象，否则出错
            return true; //如果new ActiveXObject对象成功返回真
        } catch (e) {
            return false; //如果出错返回假
        }
    }
    
    //检测Flash
    alert(hasIEPlugin('ShockwaveFlash.ShockwaveFlash'));//执行函数，传入唯一标识符
[/code]

**PS：ShockwaveFlash.ShockwaveFlash是IE中代表FLASH的标识符，你需要检查哪种控件，必须先获取它的标识符**



**跨浏览器检测是否支持Flash，就是将上面两者结合应用**

[code]

     //检测非IE浏览器插件是否存在
    function hasPlugin(name) {  //创建函数
        var name = name.toLowerCase(); //将接收的字母转换成小写
        for (var i = 0; i < navigator.plugins.length; i ++) {  //根据浏览器插件长度循环次数
            if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1) { //判断循环到的浏览器插件名称转换小写后，用正则查找传入的插件名称是否存在，返回值大于-1说明存在
                return true; //存在返回真
            }
        }
        return false; //不存在返回假
    }
    
    //检测IE中的控件
    function hasIEPlugin(name) {  //创建函数
        try {   //尝试执行，执行成功就执行里面的代码，如果出错就执行catch里面的代码
            new ActiveXObject(name); //判断浏览器是否支持控件，如果支持控件接收控件名称检测控件是否存在，存在就可以new ActiveXObject对象，否则出错
            return true; //如果new ActiveXObject对象成功返回真
        } catch (e) {
            return false; //如果出错返回假
        }
    }
    
    //跨浏览器检测是否支持Flash
    function hasFlash() {
        //首先调用上面函数，检测非IE浏览器
        var result = hasPlugin('Flash');  //调用非IE浏览器插件是否存在接收插件名称，如果返回假，说明两个情况，一是插件不存在，二是IE浏览器
        if (!result) {  //如果非IE浏览器插件是否存返回假
            result = hasIEPlugin('ShockwaveFlash.ShockwaveFlash'); //执行检测IE中的控件函数，接收控件唯一标识符名称，
            //如果返回真，说明是IE浏览器，如果返回假，说明没有Flash插件
        }
        return result; //最终返回结果
    }
    
    //检测Flash
    alert(hasFlash()); //执行检测函数
[/code]



**5.MIME类型，IE浏览器不支持**

**MIME是指多用途因特网邮件扩展。它是通过因特网发送邮件消息的标准格式。现在也被用于在因特网中交换各种类型的文件。**

**PS：mimeType[]数组在IE中不产生输出。**

**mimeTypes对象的属性**

**属性**

|

**含义**  
  
---|---  
  
**type**

|

**MIME类型名**  
  
**description**

|

**MIME类型的描述信息**  
  
**enabledPlugin**

|

**指定MIME类型配置好的plugin对象引用**  
  
**suffixes**

|

**MIME类型所有可能的文件扩展名**  
  


**mimeTypes MIME类型返回数组**

[code]

     //mimeTypes MIME类型返回数组
    alert(navigator.mimeTypes);
    //返回：[object MimeTypeArray]/
[/code]

**遍历非IE下所有MIME类型信息**

[code]

     //遍历非IE下所有MIME类型信息
    for (var i = 0; i < navigator.mimeTypes.length; i++) {
        if (navigator.mimeTypes[i].enabledPlugin != null) {
            document.write('<dl>');
            document.write('<dd>类型名称：' + navigator.mimeTypes[i].type + '</dd>');
            document.write('<dd>类型引用：' + navigator.mimeTypes[i].enabledPlugin.name + '</dd>');
            document.write('<dd>类型描述：' + navigator.mimeTypes[i].description + '</dd>');
            document.write('<dd>类型后缀：' + navigator.mimeTypes[i].suffixes + '</dd>');
            document.write('</dl>')
        }
    }
[/code]



**二．客户端检测**

**客户端检测一共分为三种，分别为：能力检测、怪癖检测和用户代理检测，通过这三种检测方案，我们可以充分的了解当前浏览器所处系统、所支持的语法、所具有的特殊性能。**

**1.能力检测**

**能力检测又称作为特性检测，检测的目标不是识别特定的浏览器，而是识别浏览器的能力。能力检测不必估计特定的浏览器，只需要确定当前的浏览器是否支持特定的能力，就可以给出可行的解决方案。**

[code]

     //能力检测
    var width = window.innerWidth;                //返回浏览器本身的宽度，返回数字类型
    
    if (typeof width != 'number') {                //如果返回不是数字类型，说明是IE，就使用document
        if (document.compatMode == 'CSS1Compat') {
            width = document.documentElement.clientWidth;
        } else {
            width = document.body.clientWidth;    //非标准模式使用body
        }
    }
    alert(width);
[/code]

**PS：上面其实有两块地方使用了能力检测，第一个就是是否支持innerWidth的检测，第二个就是是否是标准模式的检测，这两个都是能力检测**



**2.怪癖检测(bug检测)**

**与能力检测类似，怪癖检测的目标是识别浏览器的特殊行为。但与能力检测确认浏览器支持什么能力不同，怪癖检测是想要知道浏览器存在什么缺陷(bug)。**

**bug一般属于个别浏览器独有，在大多数新版本的浏览器被修复。在后续的开发过程中，如果遇到浏览器bug我们再详细探讨。**

[code]

     var box = {
        toString : function () {}                    //创建一个toString()，和原型中重名了,IE就不打印了
    };
    for (var o in box) {
        alert(o);                                //IE浏览器的一个bug，不识别了
    }
[/code]



**3.用户代理检测**

**用户代理检测通过检测用户代理字符串来确定实际使用的浏览器。在每一次HTTP请求过程中，用户代理字符串是作为响应首部发送的，而且该字符串可以通过JavaScript的navigator.userAgent属性访问。**

**用户代理代理检测，主要通过navigator.userAgent来获取用户代理字符串的，通过这组字符串，我们来获取当前浏览器的版本号、浏览器名称、系统名称。**

**PS：在服务器端，通过检测用户代理字符串确定用户使用的浏览器是一种比较广为接受的做法。但在客户端，这种测试被当作是一种万不得已的做法，且饱受争议，其优先级排在能力检测或怪癖检测之后。饱受争议的原因，是因为它具有一定的欺骗性。**

**userAgent获取用户代理字符串，通过这组字符串，我们来获取当前浏览器的版本号、浏览器名称、系统名称。**

[code]

    document.write(navigator.userAgent);             //页面形式输出得到用户代理字符串
    //返回：Mozilla/5.0 (Windows NT 10.0; WOW64; rv:50.0) Gecko/20100101 Firefox/50.0 （火狐浏览器）
    //Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; InfoPath.2; rv:11.0) like Gecko （IE浏览器）
[/code]

**各种浏览器返回信息**

**Firefox14.0.1**

**Mozilla/5.0 (Windows NT 5.1; rv:14.0) Gecko/20100101 Firefox/14.0.1**



**Firefox3.6.28**

**Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9.2.28) Gecko/20120306
Firefox/3.6.28**



**Chrome20.0.1132.57 m**

**Mozilla/5.0 (Windows NT 5.1) AppleWebKit/536.11 (KHTML, like Gecko)
Chrome/20.0.1132.57 Safari/536.11**



**Safari5.1.7**

**Mozilla/5.0 (Windows NT 5.1) AppleWebKit/534.57.2 (KHTML, like Gecko)
Version/5.1.7 Safari/534.57.2**



**IE7.0**

**Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 1.1.4322; .NET
CLR 2.0.50727; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729)**



**IE8.0**

**Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0; .NET CLR
1.1.4322; .NET CLR 2.0.50727; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729)**



**IE6.0**

**Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322; .NET
CLR 2.0.50727; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729)**



**Opera12.0**

**Opera/9.80 (Windows NT 5.1; U; zh-cn) Presto/2.10.289 Version/12.00**



**Opera7.54**

**Opera/7.54 (Windows NT 5.1; U) [en]**



**Opera8**

**Opera/8.0 (Window NT 5.1; U; en)**



**Konqueror (Linux集成，基于KHTML呈现引擎的浏览器)**

**Mozilla/5.0 (compatible; Konqueror/3.5; SunOS) KHTML/3.5.0 (like Gecko)**



**只要仔细的阅读这些字符串，我们可以发现，这些字符串包含了浏览器的名称、版本和所宿主的操作系统。**

**浏览器 **引擎****

**每个浏览器有它自己的呈现引擎：所谓呈现引擎，就是用来排版网页和解释浏览器的引擎。通过代理字符串发现，我们归纳出浏览器对应的引擎：**

**IE -- Trident，       IE8体现出来了，之前的未体现**

**Firefox -- Gecko，**

**Opera -- Presto，   旧版本根本无法体现呈现引擎**

**Chrome -- WebKit   WebKit是KHTML呈现引擎的一个分支，后独立开来**

**Safari -- WebKit**

**Konqueror -- KHTML**



****浏览器 **引擎检测******

[code]

     var client = function () {                        //创建一个自我执行构造函数
        //初始化浏览器引擎
        var engine = {                            //创建对象呈现引擎
            ie : false,
            gecko : false,
            webkit : false,
            khtml : false,
            opera : false,
    
            ver : 0                            //具体的版本号
        };
    
    
        //核心引擎检测程序区
        var ua = navigator.userAgent;  //得到用户代理字符串
        alert(ua);
        //检测opera浏览器
        if(window.opera){  //opera浏览器支持opera对象，判断opera对象返回真，说明是opera引擎浏览器在访问
            engine.opera = true; //将浏览器引擎opera改为真
            engine.ver = window.opera.version(); //使用opera.version()方法获取版本号，重新赋值给览器引擎ver
    
        //接下来，我们通过正则表达式来获取WebKit引擎和它的版本号。谷歌和苹果浏览器
        }else if (/AppleWebKit\/(\S+)/.test(ua)){
            engine.ver = RegExp['$1'];                //获取WebKit版本号
            engine.webkit = true;                  //将浏览器引擎webkit改为真
    
        //下面，我们通过正则表达式来获取Gecko引擎和它的版本号，火狐浏览器
        }else if(/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){   //获取Gecko和它的版本号
            engine.ver = RegExp['$1'];
            engine.gecko = true;               //将浏览器引擎gecko改为真
    
        //最后，我们通过正则表达式来获取IE的引擎和它的版本号。因为IE8之前没有呈现引擎，所以，我们只有通过"MSIE"这个共有的字符串来获取。
        }else if(/MSIE ([^;]+)/.test(ua)){
            engine.ver = RegExp['$1']; //获取IE和它的版本号
            engine.ie = true; //将浏览器引擎ie改为真
        }
    
        return {                           //创建对象
            engine : engine                    //返回呈现引擎对象
        };
    }();                                        //自我执行
    
    //判断打印区
    //opera引擎
    if(client.engine.opera){ //判断opera对象返回真，说明是opera浏览器在访问
        alert('目前使用的是opera引擎浏览器，版本号为' + client.engine.ver); //打印出浏览器名称和版本号
    }
    //引擎webkit,谷歌和苹果浏览器
    if(client.engine.webkit){
        alert('目前使用的是WebKit引擎浏览器，版本号为' + client.engine.ver); //打印出浏览器名称和版本号
    }
    
    //引擎Gecko，火狐浏览器
    if(client.engine.gecko){
        alert('目前使用的是WebKit引擎浏览器，版本号为' + client.engine.ver); //打印出浏览器名称和版本号
    }
    
    //引擎ie,ie浏览器
    if(client.engine.ie){
        alert('目前使用的是ie引擎浏览器，版本号为' + client.engine.ver); //打印出浏览器名称和版本号
    }
[/code]



**由上面的情况，我们需要检测呈现引擎可以分为五大类：IE、Gecko、WebKit、KHTML和Opera。**

**var client = function () {
//创建一个对象**

**        var engine = {                                           //呈现引擎**

**               ie : false,**

**               gecko : false,**

**               webkit : false,**

**               khtml : false,**

**               opera : false,**

**              **

**               ver : 0
//具体的版本号**

**        };**

**       **

**        return {                                                   **

**               engine : engine
//返回呈现引擎对象**

**        };**

**}();
//自我执行**

** **

**alert(client.engine.ie);                                        //获取ie**

** **

**以上的代码实现了五大引擎的初始化工作，分别给予true的初值，并且设置版本号为0。**

**下面我们首先要做的是判断Opera，因为Opera浏览器支持window.opera对象，通过这个对象，我们可以很容易获取到Opera的信息。**

**for (var p in window.opera) {
//获取window.opera对象信息**

**        document.write(p + "<br />");**

**}**

** **

**        if (window.opera) {
//判断opera浏览器**

**               engine.ver = window.opera.version();
//获取opera呈现引擎版本**

**               engine.opera = true;
//设置真**

**        }**

** **

**接下来，我们通过正则表达式来获取WebKit引擎和它的版本号。**

**else if (/AppleWebKit\/(\S+)/.test(ua)) {              //正则WebKit**

**        engine.ver = RegExp['$1'];                         //获取WebKit版本号**

**        engine.webkit = true;**

**}**

** **

**然后，我们通过正则表达式来获取KHTML引擎和它的版本号。由于这款浏览器基于Linux，我们无法测试。**

**//获取KHTML和它的版本号**

**        else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua))
{**

**               engine.ver = RegExp['$1'];**

**               engine.khtml = true;**

**        }**

** **

**下面，我们通过正则表达式来获取Gecko引擎和它的版本号。**

**else if (/rv:([^\\)]+)\\) Gecko\/\d{8}/.test(ua)) {      //获取Gecko和它的版本号**

**        engine.ver = RegExp['$1'];**

**        engine.gecko = true;**

**}**

** **

**最后，我们通过正则表达式来获取IE的引擎和它的版本号。因为IE8之前没有呈现引擎，所以，我们只有通过"MSIE"这个共有的字符串来获取。**

**else if (/MSIE ([^;]+)/.test(ua)) {                        //获取IE和它的版本号**

**        engine.ver = RegExp['$1'];**

**        engine.ie = true;**

**}**

** **

**上面获取各个浏览器的引擎和引擎的版本号，但大家也发现了，其实有些确实是浏览器的版本号。所以，下面，我们需要进行浏览器名称的获取和浏览器版本号的获取。**

**根据目前的浏览器市场份额，我们可以给一下浏览器做检测：IE、Firefox、konq、opera、chrome、safari。**

**        var browser = {
//浏览器对象**

**               ie : false,**

**               firefox : false,**

**               konq : false,**

**               opera : false,**

**               chrome : false,**

**               safari : false,**

**              **

**               ver : 0,
//具体版本**

**               name : ''
//具体的浏览器名称**

**};**

** **

**对于获取IE浏览器的名称和版本，可以直接如下：**

**else if (/MSIE ([^;]+)/.test(ua)) {**

**               engine.ver = browser.ver = RegExp['$1'];     //设置版本**

**               engine.ie = browser.ie = true;
//填充保证为true**

**               browser.name = 'Internet Explorer';             //设置名称**

**}**

** **

**对于获取Firefox浏览器的名称和版本，可以如下：**

**else if (/rv:([^\\)]+)\\) Gecko\/\d{8}/.test(ua)) {**

**               engine.ver = RegExp['$1'];**

**               engine.gecko = true;**

**               if (/Firefox\/(\S+)/.test(ua)) {**

**                      browser.ver = RegExp['$1'];                //设置版本**

**                      browser.firefox = true;
//填充保证为true**

**                      browser.name = 'Firefox';                    //设置名称**

**               }**

**}**

** **

**对于获取Chrome和safari浏览器的名称和版本，可以如下：**

**else if (/AppleWebKit\/(\S+)/.test(ua)) {**

**               engine.ver = RegExp['$1'];**

**               engine.webkit = parseFloat(engine.ver);**

**               if (/Chrome\/(\S+)/.test(ua)) {**

**                      browser.ver = RegExp['$1'];**

**                      browser.chrome = true;**

**                      browser.name = 'Chrome';**

**               } else if (/Version\/(\S+)/.test(ua)) {**

**                      browser.ver = RegExp['$1'];**

**                      browser.chrome = true;**

**                      browser.name = 'Safari';**

**               }**

**}**

** **

**PS：对于Safari3之前的低版本，需要做WebKit的版本号近似映射。而这里，我们将不去深究，已提供代码。**

** **

**浏览器的名称和版本号，我们已经准确的获取到，最后，我们想要去获取浏览器所宿主的操作系统。**

**        var system = {
//操作系统**

**               win : false,
//windows**

**               mac : false,
//Mac**

**               x11 : false
//Unix、Linux**

**        };**

** **

**        var p = navigator.platform;                                //获取系统**

**        system.win = p.indexOf('Win') == 0;
//判断是否是windows**

**        system.mac = p.indexOf('Mac') == 0;                 //判断是否是mac**

**        system.x11 = (p == 'X11') || (p.indexOf('Linux') == 0)
//判断是否是Unix、Linux**

** **

**PS：这里我们也可以通过用户代理字符串获取到windows相关的版本，这里我们就不去深究了，提供代码和对应列表。**

** **

**Windows版本**

|

**IE4+**

|

**Gecko**

|

**Opera < 7**

|

**Opera 7+**

|

**WebKit**  
  
---|---|---|---|---|---  
  
**95**

|

**"Windows 95"**

|

**"Win95"**

|

**"Windows 95"**

|

**"Windows 95"**

|

**n/a**  
  
**98**

|

**"Windows 98"**

|

**"Win98"**

|

**"Windows 98"**

|

**"Windows 98"**

|

**n/a**  
  
**NT4.0**

|

**"Windows NT"**

|

**"WinNT4.0"**

|

**"Windows NT 4.0"**

|

**"Windows NT 4.0"**

|

**n/a**  
  
**2000**

|

**"Windows NT 5.0"**

|

**"Windows NT5.0"**

|

**"Windows 2000"**

|

**"Windows NT 5.0"**

|

**n/a**  
  
**ME**

|

**"Win 9X 4.90"**

|

**"Win 9x 4.90"**

|

**"Windows ME"**

|

**"Win 9X 4.90"**

|

**n/a**  
  
**XP**

|

**"Windows NT 5.1"**

|

**"Windows NT 5.1"**

|

**"Windows XP"**

|

**"Windows NT 5.1"**

|

**"Windows NT 5.1"**  
  
**Vista**

|

**"Windows NT 6.0"**

|

**"Windows NT 6.0"**

|

**n/a**

|

**"Windows NT 6.0"**

|

**"Windows NT 6.0"**  
  
**7**

|

**"Windows NT 6.1"**

|

**"Windows NT 6.1"**

|

**n/a**

|

**"Windows NT 6.1"**

|

**"Windows NT 6.1"**  
  
**  浏览器检测完整版**

[code]

    var client = function(){
    
        //rendering engines
        var engine = {            
            ie: 0,
            gecko: 0,
            webkit: 0,
            khtml: 0,
            opera: 0,
    
            //complete version
            ver: null  
        };
        
        //browsers
        var browser = {
            
            //browsers
            ie: 0,
            firefox: 0,
            safari: 0,
            konq: 0,
            opera: 0,
            chrome: 0,
    
            //specific version
            ver: null
        };
    
        
        //platform/device/OS
        var system = {
            win: false,
            mac: false,
            x11: false,
            
            //mobile devices
            iphone: false,
            ipod: false,
            ipad: false,
            ios: false,
            android: false,
            nokiaN: false,
            winMobile: false,
            
            //game systems
            wii: false,
            ps: false 
        };    
    
        //detect rendering engines/browsers
        var ua = navigator.userAgent;    
        if (window.opera){
            engine.ver = browser.ver = window.opera.version();
            engine.opera = browser.opera = parseFloat(engine.ver);
        } else if (/AppleWebKit\/(\S+)/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.webkit = parseFloat(engine.ver);
            
            //figure out if it's Chrome or Safari
            if (/Chrome\/(\S+)/.test(ua)){
                browser.ver = RegExp["$1"];
                browser.chrome = parseFloat(browser.ver);
            } else if (/Version\/(\S+)/.test(ua)){
                browser.ver = RegExp["$1"];
                browser.safari = parseFloat(browser.ver);
            } else {
                //approximate version
                var safariVersion = 1;
                if (engine.webkit < 100){
                    safariVersion = 1;
                } else if (engine.webkit < 312){
                    safariVersion = 1.2;
                } else if (engine.webkit < 412){
                    safariVersion = 1.3;
                } else {
                    safariVersion = 2;
                }   
                
                browser.safari = browser.ver = safariVersion;        
            }
        } else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)){
            engine.ver = browser.ver = RegExp["$1"];
            engine.khtml = browser.konq = parseFloat(engine.ver);
        } else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){    
            engine.ver = RegExp["$1"];
            engine.gecko = parseFloat(engine.ver);
            
            //determine if it's Firefox
            if (/Firefox\/(\S+)/.test(ua)){
                browser.ver = RegExp["$1"];
                browser.firefox = parseFloat(browser.ver);
            }
        } else if (/MSIE ([^;]+)/.test(ua)){    
            engine.ver = browser.ver = RegExp["$1"];
            engine.ie = browser.ie = parseFloat(engine.ver);
        }
        
        //detect browsers
        browser.ie = engine.ie;
        browser.opera = engine.opera;
        
    
        //detect platform
        var p = navigator.platform;
        system.win = p.indexOf("Win") == 0;
        system.mac = p.indexOf("Mac") == 0;
        system.x11 = (p == "X11") || (p.indexOf("Linux") == 0);
    
        //detect windows operating systems
        if (system.win){
            if (/Win(?:dows )?([^do]{2})\s?(\d+\.\d+)?/.test(ua)){
                if (RegExp["$1"] == "NT"){
                    switch(RegExp["$2"]){
                        case "5.0":
                            system.win = "2000";
                            break;
                        case "5.1":
                            system.win = "XP";
                            break;
                        case "6.0":
                            system.win = "Vista";
                            break;
                        case "6.1":
                            system.win = "7";
                            break;
                        default:
                            system.win = "NT";
                            break;                
                    }                            
                } else if (RegExp["$1"] == "9x"){
                    system.win = "ME";
                } else {
                    system.win = RegExp["$1"];
                }
            }
        }
        
        //mobile devices
        system.iphone = ua.indexOf("iPhone") > -1;
        system.ipod = ua.indexOf("iPod") > -1;
        system.ipad = ua.indexOf("iPad") > -1;
        system.nokiaN = ua.indexOf("NokiaN") > -1;
        
        //windows mobile
        if (system.win == "CE"){
            system.winMobile = system.win;
        } else if (system.win == "Ph"){
            if(/Windows Phone OS (\d+.\d+)/.test(ua)){;
                system.win = "Phone";
                system.winMobile = parseFloat(RegExp["$1"]);
            }
        }
        
        
        //determine iOS version
        if (system.mac && ua.indexOf("Mobile") > -1){
            if (/CPU (?:iPhone )?OS (\d+_\d+)/.test(ua)){
                system.ios = parseFloat(RegExp.$1.replace("_", "."));
            } else {
                system.ios = 2;  //can't really detect - so guess
            }
        }
        
        //determine Android version
        if (/Android (\d+\.\d+)/.test(ua)){
            system.android = parseFloat(RegExp.$1);
        }
        
        //gaming systems
        system.wii = ua.indexOf("Wii") > -1;
        system.ps = /playstation/i.test(ua);
        
        //return it
        return {
            engine:     engine,
            browser:    browser,
            system:     system        
        };
    
    }();
[/code]



