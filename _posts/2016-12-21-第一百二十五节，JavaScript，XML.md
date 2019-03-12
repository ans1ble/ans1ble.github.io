---
layout: post
title: " 第一百二十五节，JavaScript，XML "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript，XML**



**学习要点：**

**1.IE中的XML**

**2.DOM2中的XML**

**3.跨浏览器处理XML**



**随着互联网的发展，Web应用程序的丰富，开发人员越来越希望能够使用客户端来操作XML技术。而XML技术一度成为存储和传输结构化数据的标准。所以，本章就详细探讨一下JavaScript中使用XML的技术。**

**对于什么是XML，干什么用的，这里就不在赘述了，在以往的XHTML或PHP课程都有涉及到，可以理解成一个微型的结构化的数据库，保存一些小型数据用的。**

** **

**一．** **IE** **中的XML**

**在统一的正式规范出来以前，浏览器对于XML的解决方案各不相同。DOM2级提出了动态创建XML DOM规范，DOM3进一步增强了XML
DOM。所以，在不同的浏览器实现XML的处理是一件比较麻烦的事情。**

**1.创建XMLDOM对象**

**IE浏览器是第一个原生支持XML的浏览器，而它是通过ActiveX对象实现的。这个对象，只有IE有，一般是IE9之前采用。微软当年为了开发人员方便的处理XML，创建了MSXML库，但却没有让Web开发人员通过浏览器访问相同的对象。**

**ActiveXObject()对象，创建xml，ActiveXObject类型，只支持IE，并且只支持IE9以下**

[code]

     var xmlDom = new ActiveXObject('MSXML2.DOMDocument');
[/code]



**ActiveXObject类型**

**XML版本字符串**

|

**说明**  
  
---|---  
  
**Microsoft.XmlDom**

|

**最初随同IE发布，不建议使用**  
  
**MSXML2.DOMDocument**

|

**脚本处理而更新的版本，仅在特殊情况作为备份用**  
  
**MSXML2.DOMDocument.3.0**

|

**在JavaScript中使用，这是最低的建议版本**  
  
**MSXML2.DOMDocument.4.0**

|

**脚本处理时并不可靠，使用这个版本导致安全警告**  
  
**MSXML2.DOMDocument.5.0**

|

**脚本处理时并不可靠，使用这个版本导致安全警告**  
  
**MSXML2.DOMDocument.6.0**

|

**脚本能够可靠处理的最新版本**  
  
**PS：在这六个版本中微软只推荐三种：**

**1.MSXML2.DOMDocument.6.0 最可靠最新的版本**

**2.MSXML2.DOMDocument.3.0 兼容性较好的版本**

**3.MSXML2.DOMDocument     仅针对IE5.5之前的版本**

**这三个版本在不同的windows平台和浏览器下会有不同的支持，那么为了实现兼容，我们应该考虑这样操作：从6.0-
>3.0->备用版本这条路线进行实现。**

**兼容不同 **windows平台****

[code]

    alert(createXMLDOM());   //执行自定义创建xml对象函数
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]



**2.载入XML**

**如果已经获取了XMLDOM对象，那么可以使用loadXML()和load()这两个方法可以分别载入XML字符串或XML文件。**

**loadXML()载入xml字符串，参数是xml字符串**  
 **使用方式：**  
 **ActiveXObject()对象.loadXML('参数是xml字符串')**

[code]

     var xml = createXMLDOM();  //创建xml对象
    xml.loadXML('<root version="1.0"><user>Lee</user></root>');   //loadXML()载入xml字符串，参数是xml字符串
    alert(xml.xml); //XML属性可以获取到xml代码
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]

**loadXML参数直接就是XML字符串，如果想效果更好，可以添加换行符\n。.xml属性可以序列化XML，获取整个XML字符串。**



**加载了xml后获取xml元素和html一样的**

**当你已经可以加载了XML，那么你就可以用之前学习的DOM来获取XML数据，比如标签内的某个文本。**

[code]

     var xml = createXMLDOM();  //创建xml对象
    xml.loadXML('<root version="1.0"><user>Lee</user></root>');   //loadXML()载入xml字符串，参数是xml字符串
    var user = xml.getElementsByTagName('user')[0];    //获取<user>节点
    alert(user.tagName);                            //获取<user>元素标签
    alert(user.firstChild.nodeValue);                //获取<user>里的值Le
    
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]



**load()载入xml文件，参数是xml文件路径**  
 **使用方式：**  
 **ActiveXObject()对象.load('xml文件路径')**

[code]

     var xml = createXMLDOM();  //创建xml对象  
    
[/code]

[code]

    xmlDom.async = false;  //同步加载,在服务器测试，等待文件加载完毕后在执行代码
[/code]

[code]

    xml.load('demo.xml');   //load()载入xml文件，参数是xml文件路径
    alert(xml.xml);  //打印xml字符串
    var user = xml.getElementsByTagName('user')[0];    //获取<user>节点
    alert(user.tagName);                            //获取<user>元素标签
    alert(user.firstChild.nodeValue);                //获取<user>里的值Le
    
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]



**DOM不单单可以获取XML节点，也可以创建节点**

[code]

     var xmlDom = createXMLDOM();  //创建xml对象
    xmlDom.async = false;  //同步加载,在服务器测试，等待文件加载完毕后在执行代码
    xmlDom.load("demo.xml");  //载入xml文件
    var bbb = xmlDom.createElement('bbb');  //添加一个新节点
    var root = xmlDom.documentElement;  //获取根元素
    root.appendChild(bbb); //将新节点添加到根节点的子节点末尾
    alert(xmlDom.xml);
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]



**3.同步及异步**

**load()方法是用于服务器端载入XML的，并且限制在同一台服务器上的XML文件。那么在载入的时候有两种模式：同步和异步。**

**所谓同步：就是在加载XML完成之前，代码不会继续执行，直到完全加载了XML再返回。好处就是简单方便、坏处就是如果加载的数据停止响应或延迟太久，浏览器会一直堵塞从而造成假死状态。【不推荐】**

[code]

    xmlDom.async =  false;                        //设置同步，false，可以用PHP测试假死
[/code]

**所谓异步：就是在加载XML时，JavaScript会把任务丢给浏览器内部后台去处理，不会造成堵塞，但要配合readystatechange事件使用，所以，通常我们都使用异步方式。**



[code]

    xmlDom.async = true;                        //设置异步，默认
[/code]



**通过异步加载，我们发现获取不到XML的信息。原因是，它并没有完全加载XML就返回了，也就是说，我们需要在浏览器内部加载一点，返回一点，加载一点，返回一点。这个时候，我们需要判断是否完全加载，并且可以使用了，再进行获取输出。
**配合readystatechange事件使用【推荐】****



**XML DOM中onreadystatechange事件**



**就绪状态**

|

**说明**  
  
---|---  
  
**1**

|

**DOM正在加载**  
  
**2**

|

**DOM已经加载完数据**  
  
**3**

|

**DOM已经可以使用，但某些部分还无法访问**  
  
**4**

|

**DOM已经完全可以**  
  
**PS：readyState可以获取就绪状态值**  
  


**onreadystatechange事件,xml对象事件，当加载外部xml文件是激发，通过readyState属性可以获取xml文件加载的状态，见上表**  
 **使用方式：**  
 **写在加载文件的前面**  
 **xml对象.onreadystatechange = 执行函数**

**readyState属性，可以获取到通过onreadystatechange事件加载的xml文件状态，写在事件函数里面,返回状态码见上表**  
 **使用方式：**  
 **xml对象.readyState**

**解决异步不能加载完毕的问题**

[code]

     var xmlDom = createXMLDOM();  //创建xml对象
    xmlDom.async = true; //异步加载
    xmlDom.onreadystatechange = function () {  //onreadystatechange事件,xml对象事件，当加载外部xml文件是激发
        if (xmlDom.readyState == 4){  //readyState属性，可以获取到通过onreadystatechange事件加载的xml文件状态
            //判断当xml文件加载完毕后，打印出xml里的代码
            alert(xmlDom.xml);
        }
    };
    xmlDom.load("demo.xml");  //载入xml文件
    
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]

**PS：可以通过readyState来了解事件的执行次数，将load()方法放到最后不会因为代码的顺序而导致没有加载。并且load()方法必须放在onreadystatechange之后，才能保证就绪状态变化时调用该事件处理程序，因为要先触发**



**虽然可以通过XML DOM文档加载XML文件，但公认的还是XMLHttpRequest对象比较好。这方面内容，我们在Ajax章节详细了解。**



**2.解析错误**

**在加载XML时，无论使用loadXML()或load()方法，都有可能遇到XML格式不正确的情况。为了解决这个问题，微软的XML
DOM提供了parseError属性。**

**parseError属性对象**

**属性**

|

**说明**  
  
---|---  
  
**errorCode**

|

**发生的错误类型的数字代号，没有错误返回0**  
  
**filepos**

|

**发生错误文件中的位置**  
  
**line**

|

**错误行号**  
  
**linepos**

|

**遇到错误行号那一行上的字符的位置**  
  
**reason**

|

**错误的解释信息**  
  
**parseError属性对象，是处理加载xml文件时遇到错误的对象，对象下有5个属性分别返回错误类型，见上表**



**使用方式：**  
 **xml对象.parseError.错误属性**

[code]

     var xmlDom = createXMLDOM();  //创建xml对象
    xmlDom.async = true; //异步加载
    xmlDom.onreadystatechange = function () {  //onreadystatechange事件,xml对象事件，当加载外部xml文件是激发
        if (xmlDom.readyState == 4) {  //readyState属性，可以获取到通过onreadystatechange事件加载的xml文件状态
            //判断当xml文件加载完毕后，执行里面代码
            if (xmlDom.parseError.errorCode == 0) {  //判断文件是否有错
                //如果没有错误，打印出xml代码
                alert(xmlDom.xml);
            } else {  //如果有错误
                //创建一个错误对象，打印出相应的错误类型
                throw new Error('错误行号：' + xmlDom.parseError.line +
                    '\n错误代号：' + xmlDom.parseError.errorCode +
                    '\n错误解释：' + xmlDom.parseError.reason);
            }
        }
    };
    xmlDom.load("demo.xml");  //载入xml文件
    
    
    
    //兼容不同windows平台
    function createXMLDOM() {  //自定义函数，创建xml对象
        var version = [   //创建数组，元素是ActiveXObject类型
                                'MSXML2.DOMDocument.6.0',
                                'MSXML2.DOMDocument.3.0',
                                'MSXML2.DOMDocument'
        ];
        for (var i = 0; i < version.length; i ++) {  //根据数组的长度循环次数
            try {  //尝试执行循环到的ActiveXObject类型
                var xmlDom = new ActiveXObject(version[i]);  //执行成功
                return xmlDom;  //返回创建xml对象，并且退出当前函数
            } catch (e) {  //如果出错
                //跳过
            }
        }
        //创建一个错误对象，抛出错误
        throw new Error('您的系统或浏览器不支持MSXML！');        //循环后抛出错误
    }
[/code]



**二．DOM2中的XML**

**  **DOM2中无法实现字符串方式创建xml对象****

**IE可以实现了对XML字符串或XML文件的读取，其他浏览器也各自实现了对XML处理功能。DOM2级在document.implementaion中引入了createDocument()方法。IE9、Firefox、Opera、Chrome和Safari都支持这个方法。**

**implementaion对象，xml对象**  
 **使用方式;**  
 **document.implementaion.createDocument()**

**createDocument()方法，创建xml对象，3个参数，参数一命名空间xml没有命名空间留空字符串，参数二xml根标签，参数三文档声明，没有文档声明写null**  
 **使用方式：**  
 **document.implementaion.createDocument('',xml根标签,null)**

**1.创建XMLDOM对象**

[code]

     //1.创建XMLDOM对象
    var xmlDom = document.implementation.createDocument('','root',null);    //创建xmlDom
    var us = xmlDom.createElement('us');                            //创建us新元素节点
    xmlDom.getElementsByTagName('root')[0].appendChild(us);            //将新元素节点添加到root下
    var value = xmlDom.createTextNode('Lee');                        //创建文本节点
    xmlDom.getElementsByTagName('us')[0].appendChild(value);        //将文本节点添加到us下
    alert(xmlDom.getElementsByTagName('root')[0].tagName);  //打印出根元素的标签名称
    alert(xmlDom.getElementsByTagName('us')[0].firstChild.nodeValue); //打印出user元素的标签下的文本节点值
[/code]

**PS：由于DOM2中不支持loadXML()方法，所以，无法简易的直接创建XML字符串。所以，只能采用以上的做法。**

**PS：createDocument()方法需要传递三个参数，命名空间，根标签名和文档声明，由于JavaScript管理命名空间比较困难，所以留空即可。文档声明一般根本用不到，直接null即可。命名空间和文档声明留空，表示创建XMLDOM对象不需要命名空间和文档声明。**

**PS：命名空间的用途是防止太多的重名而进行的分类，文档类型表明此文档符合哪种规范，而这里创建XMLDOM不需要使用这两个参数，所以留空即可。**



**2.载入XML**

**DOM2只支持load()方法，载入一个同一台服务器的外部XML文件。当然，DOM2也有async属性，来表面同步或异步，默认异步。**

****不管在同步或异步来获取load()方法只有Mozilla的Firefox才能支持，只不过新版的Opera也是支持的，其他浏览器则不支持****

**同步情况下**

[code]

     //同步情况下
    var xmlDom = document.implementation.createDocument('','root',null);  //创建xml对象
    xmlDom.async = false; //加载文件方式同步，加载XML完成之前，代码不会继续执行，直到完全加载了XML再返回
    xmlDom.load('demo.xml'); //加载xml文件
    alert(xmlDom.getElementsByTagName('user')[0].tagName);  //获取user标签的，标签名称
[/code]

**异步情况下**

[code]

     //异步情况下
    var xmlDom = document.implementation.createDocument('', 'root', null);
    xmlDom.async = true;  //异步
    addEvent(xmlDom, 'load', function () {                    //异步直接用onload即可，等待页面加载完毕后执行函数
        alert(this.getElementsByTagName('user')[0].tagName);  //打印当前xml对象里，user元素的，标签名称
    });
    xmlDom.load('demo.xml'); //加载xml文件
    
    
    //跨浏览器添加事件，添加事件兼容
    function addEvent(obj, type, fn) {     //添加事件函数，接收3个参数，1事件对象，2事件名称，3事件函数
        //判断浏览器如果支持w3c
        if (obj.addEventListener) {
            //就用w3c的addEventListener方法添加对象，将事件名称和事件函数传入添加事件
            obj.addEventListener(type, fn, false);
        } else if (obj.attachEvent) {   //判断如果浏览器是IE9以下，就用IE的方法attachEvent添加事件
            //将事件名称和事件函数传入创建对象
            obj.attachEvent('on' + type, fn);
        }
    }
[/code]

**PS：不管在同步或异步来获取load()方法只有Mozilla的Firefox才能支持，只不过新版的Opera也是支持的，其他浏览器则不支持。**





**3.DOMParser类型，用于定义字符串方式xml**

**由于DOM2没有loadXML()方法直接解析XML字符串，所以提供了DOMParser类型来创建XML
DOM对象。IE9、Safari、Chrome和Opera都支持这个类型。
**DOMParser下面有一个方法parseFromString()创建xml对象****

******parseFromString()方法，创建xml对象，用于创建
**DOMParser类型的xml对象，有两个参数，参数一是xml字符串，参数二是xml类型text/xml********

********使用方式：********

********DOMParser对象. ** ** **parseFromString( ** ** ** **xml字符串******** ,' **
** ** **text/xml******** ')**************

[code]

    var xmlParser = new DOMParser();                        //创建DOMParser对象
    //创建xml字符串
    var xmlStr = '<root><user>Lee</user></root>';    //XML字符串
    var xmlDom = xmlParser.parseFromString(xmlStr, 'text/xml');    //创建XML DOM对象
    alert(xmlDom.getElementsByTagName('user')[0].tagName);    //获取user元素标签名
[/code]

**PS：XML
DOM对象是通过DOMParser对象中的parseFromString方法来创建的，两个参数：XML字符串和内容类型text/xml。**



**4.XMLSerializer类型，用于序列化XML输出**

**由于DOM2没有序列化XML的属性，所以提供了XMLSerializer类型来帮助序列化XML字符串。IE9、Safari、Chrome和Opera都支持这个类型。
**XMLSerializer类型下面有一个serializeToString()方法序列化XML****

********serializeToString()方法， **用于序列化XML输出，有一个参数xml对象 **DOM************

************使用方式：************

**************XMLSerializer对象. ** ** ** **serializeToString( ** ** ** **
**xml对象 **DOM************ )**********************

[code]

    var xmlParser = new DOMParser();                        //创建DOMParser对象
    //创建xml字符串
    var xmlStr = '<root><user>Lee</user></root>';    //XML字符串
    var xmlDom = xmlParser.parseFromString(xmlStr, 'text/xml');    //创建XML DOM对象
    
    var serializer = new XMLSerializer();            //创建XMLSerializer对象
    var xml = serializer.serializeToString(xmlDom);    //序列化XML
    alert(xml); //序列化打印出xml
[/code]



**5.解析错误**

**在DOM2级处理XML发生错误时，并没有提供特有的对象来捕获错误，而是直接生成另一个错误的XML文档，通过这个文档可以获取错误信息。**

[code]

     var xmlParser = new DOMParser();                        //创建DOMParser对象
    //创建xml字符串
    var xmlStr = '<user>Lee</user></root>';    //XML字符串
    var xmlDom = xmlParser.parseFromString(xmlStr, 'text/xml');    //创建XML DOM对象
    
    var serializer = new XMLSerializer();            //创建XMLSerializer对象
    var xml = serializer.serializeToString(xmlDom);    //序列化XML
    //获取xml错误序列化后的错误文件parsererror标签，标签里面是错误信息
    var errors = xmlDom.getElementsByTagName('parsererror');
    if (errors.length > 0) {  //判断错误文件标签大于0说明xml有错误
        //创建一个错误对象，获取第一个parsererror标签，并且获取到标签的文本内容
        throw new Error('XML格式有误：' + errors[0].textContent);
    }
    
    alert(xml); //序列化打印出xml,如果出错会得到一个错误文件
[/code]

**PS：errors[0].firstChild.nodeValue也可以使用errors[0].textContent来代替。**



**三．** **跨浏览器处理XML**

**如果要实现跨浏览器就要思考几个个问题：1.load()只有IE、Firefox、Opera支持，所以无法跨浏览器；2.获取XML
DOM对象顺序问题，先判断先进的DOM2的，然后再去判断落后的IE；3.针对不同的IE和DOM2级要使用不同的序列化。4.针对不同的报错进行不同的报错机制。**

[code]

     var xml = '<root><user>Lee</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    alert(serializeXML(xmldom)); //打印序列化xml,接收XML DOM对象
    
    
    //首先，我们需要跨浏览器获取XML DOM
    function getXMLDOM(xmlStr) {  //自定义跨浏览器创建xml DOM对象，接收一个参数xml字符串
        var xmlDom = null;  //初始化一个对象
    
        if (typeof window.DOMParser != 'undefined') {        //判断DOMParser类型不等于undefined说明支持
            //创建DOMParser对象，并且创建xml DOM对象
            xmlDom = (new DOMParser()).parseFromString(xmlStr, 'text/xml');
            //获取错误信息的parsererror标签
            var errors = xmlDom.getElementsByTagName('parsererror');
            //判断错误信息标签返回集合长度大于0，说明xml有错误
            if (errors.length > 0) {
                //创建一个错误对象，获取到第一个错误标签，并且获取到他的文本内容
                throw new Error('XML解析错误：' + errors[0].firstChild.nodeValue);
            }
        //如果不支持DOMParser类型，尝试IE的方法
        } else if (typeof window.ActiveXObject != 'undefined') {    //判断ActiveXObject类型不等于undefined说明支持
            var version = [  //创建一个数组，元素分别为3个xml版本
                'MSXML2.DOMDocument.6.0',
                'MSXML2.DOMDocument.3.0',
                'MSXML2.DOMDocument'
            ];
            for (var i = 0; i < version.length; i++) {  //根据数组的长度循环次数
                try {
                    //尝试着执行每次循环到的xml版本，创建xml对象
                    xmlDom = new ActiveXObject(version[i]);
                } catch (e) {  //如果出错跳过执行第二次循环
                    //跳过
                }
            }
            xmlDom.loadXML(xmlStr);  //载入xml字符串
            if (xmlDom.parseError != 0) {  //判断载入xml错误返回代码，如果不等于0说明xml有错
                //创建一个错误对象，返回错误的解释信息
                throw new Error('XML解析错误：' + xmlDom.parseError.reason);
            }
        } else {  //如果 上面两种方式都不支持
            //创建一个错误对象，抛出您所使用的系统或浏览器不支持XML DOM！
            throw new Error('您所使用的系统或浏览器不支持XML DOM！');
        }
    
        return xmlDom;  //最后返回创建的xmlDOM对象
    }
    
    //其次，我们还必须跨浏览器序列化XML
    function serializeXML(xmlDom) {  //序列化xml函数，接收xmlDOM对象对象
        var xml = '';  //初始化一个变量等于空字符串
        if (typeof XMLSerializer != 'undefined') {  //判断XMLSerializer类型，不等于undefined，说明支持序列化
            //给xml重新赋值，创建XMLSerializer对象，并且使用serializeToString方法序列化
            xml = (new XMLSerializer()).serializeToString(xmlDom);
        //如果不支持XMLSerializer类型
        } else if (typeof xmlDom.xml != 'undefined') { //判断IE方式xmlDOM对象下的xml属性是否等于undefined，不等于说明支持
            //给xml重新赋值，序列化xml
            xml = xmlDom.xml;
        } else { //如果上面两种都不支持
            //创建一个错误对象，抛出无法解析XML！错误信息
            throw new Error('无法解析XML！');
        }
        return xml; //最后返回序列化
    }
[/code]

**PS：由于兼容性序列化过程有一定的差异，可能返回的结果字符串可能会有一些不同。至于load()加载XML文件则因为只有部分浏览器支持而无法跨浏览器。**



