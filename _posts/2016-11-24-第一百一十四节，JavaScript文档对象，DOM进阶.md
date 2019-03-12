
---
layout: post
title: " 第一百一十四节，JavaScript文档对象，DOM进阶 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript文档对象，DOM进阶**



**学习要点：**

**1.DOM类型**

**2.DOM扩展**

**3.DOM操作内容**



**DOM自身存在很多类型，在DOM基础课程中大部分都有所接触，比如Element类型：表示的是元素节点，再比如Text类型：表示的是文本节点。DOM也提供了一些扩展功能。**



**一．** **DOM** **类型**

**DOM基础课程中，我们了解了DOM的节点并且了解怎样查询和操作节点，而本身这些不同的节点，又有着不同的类型。**



**DOM类型**

**类型名**

|

**说明**  
  
---|---  
  
**Node**

|

**表示所有类型值的统一接口，IE不支持**  
  
**Document**

|

**表示文档类型**  
  
**Element**

|

**表示元素节点类型**  
  
**Text**

|

**表示文本节点类型**  
  
**Comment**

|

**表示文档中的注释类型**  
  
**CDATASection**

|

**表示CDATA区域类型**  
  
**DocumentType**

|

**表示文档声明类型**  
  
**DocumentFragment**

|

**表示文档片段类型**  
  
**Attr**

|

**表示属性节点类型**  
  
** **

**1.Node类型，返回值表示 **Node类型的数值****

**Node接口是DOM1级就定义了，Node接口定义了12个数值常量以表示每个节点的类型值。 除了IE之外，所有浏览器都可以访问这个类型。**



**Node的常量**

**常量名**

|

**说明**

|

**nodeType值**  
  
---|---|---  
  
**ELEMENT_NODE**

|

**元素**

|

**1**  
  
**ATTRIBUTE_NODE**

|

**属性**

|

**2**  
  
**TEXT_NODE**

|

**文本**

|

**3**  
  
**CDATA_SECTION_NODE**

|

**CDATA**

|

**4**  
  
**ENTITY_REFERENCE_NODE**

|

**实体参考**

|

**5**  
  
**ENTITY_NODE**

|

**实体**

|

**6**  
  
**PROCESSING_INSTRUCETION_NODE**

|

**处理指令**

|

**7**  
  
**COMMENT_NODE**

|

**注释**

|

**8**  
  
**DOCUMENT_NODE**

|

**文档根**

|

**9**  
  
**DOCUMENT_TYPE_NODE**

|

**doctype,html文档声明类型**

|

**10**  
  
**DOCUMENT_FRAGMENT_NODE**

|

**文档片段**

|

**11**  
  
**NOTATION_NODE**

|

**符号**

|

**12**  
  


** **

**虽然这里介绍了12种节点对象的属性，用的多的其实也就几个而已。**

[code]

    alert(Node.ELEMENT_NODE);                 //1，元素节点类型值
    alert(Node.TEXT_NODE);                    //2，文本节点类型值  
      
    注意：低版本ie不支持，下面会有解决方案
[/code]

**ELEMENT_NODE，表示 **元素节点返回值是1 ，** 实际使用方式如下**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box'); //通过ID获取到目标节点
        //判断元素节点的类型，如果等于文本类型
        if(asf.nodeType === Node.ELEMENT_NODE){  //ELEMENT_NODE，表示元素节点返回值是1
            alert("元素类型节点");
        }else {
            alert("不是元素类型节点")
        }
    };
    
    //元素类型节点
[/code]

**ps:其他属性使用方式相同**

**我们建议使用Node类型的属性来代替1,2这些阿拉伯数字，有可能大家会觉得这样岂不是很繁琐吗？并且还有一个问题就是IE不支持Node类型。**  
**如果只有两个属性的话，用1，2来代替会特别方便，但如果属性特别多的情况下，1、2、3、4、5、6、7、8、9、10、11、12，你根本就分不清哪个数字代表的是哪个节点。当然，如果你只用1，2两个节点，那就另当别论了。**

****Node类型** IE低版本不支持，我们可以模拟一个类，让IE也支持**

[code]

    alert(Node.ELEMENT_NODE);                //1，元素节点类型值
    alert(Node.TEXT_NODE);                    //2，文本节点类型值
    
    //Node类型IE低版本不支持，我们可以模拟一个类，让IE也支持
    //判断Node的类型如果等于undefined，就说明此浏览器不支持Node类型
    if (typeof Node === 'undefined'){
        //通过window创建一个对象全局变量
        window.Node ={
            ELEMENT_NODE:1,
            ATTRIBUTE_NODE:2,
            TEXT_NODE:3,
            CDATA_SECTION_NODE:4,
            ENTITY_REFERENCE_NODE:5,
            ENTITY_NODE:6,
            PROCESSING_INSTRUCETION_NODE:7,
            COMMENT_NODE:8,
            DOCUMENT_NODE:9,
            DOCUMENT_TYPE_NODE:10,
            DOCUMENT_FRAGMENT_NODE:11,
            NOTATION_NODE:12
        };
    }
[/code]



**2.Document类型，返回根节点对象**

**document类型表示文档，或文档的根节点，而这个节点是隐藏的，没有具体的元素标签。也就是所有的html都是在这个节点下的，这个是根**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document);   //document类型表示文档，或文档的根节点
        //返回[object HTMLDocument],返回根节点对象
    
        alert(document.nodeType);  //查看文档类型值
        //返回9，表示文档根
    
        alert(document.childNodes[0]); //获取根元素节点里的第一个子节点
        //返回[object DocumentType]，第一个子节点对象
    
        alert(document.childNodes[0].nodeType); //查看第一个子节点的类型
        //返回10，表示html文档声明类型
    
        alert(document.childNodes[1]); //获取根元素节点里的第二个子节点
        //返回[object HTMLHtmlElement]，第二个子节点对象
    
        alert(document.childNodes[1].nodeType); //查看第二个子节点的类型
        //返回1，表示是元素类型也就是标签
    
        alert(document.childNodes[1].nodeName);  //获取第二个子节点的标签名称
        //HTML，表示是html标签
    };
[/code]



**如果想直接得到
<html>标签的元素节点对象HTMLHtmlElement，不必使用childNodes属性这么麻烦，可以使用documentElement即可。**

**documentElement属性，直接获取根节点下的html节点，返回html节点对象**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.documentElement);  //documentElement属性，直接获取根节点下的html节点，返回html节点对象
        //返回，[object HTMLHtmlElement] html节点对象
    
        alert(document.documentElement.nodeName); //获取html节点的标签名称
        //返回，HTML 标签名称
    };
[/code]



**在很多情况下，我们并不需要得到
<html>标签的元素节点，而需要得到更常用的<body>标签，之前我们采用的是：document.getElementsByTagName('body')[0]，那么这里提供一个更加简便的方法：document.body。**

**body属性，直接获取body标签节点**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.body);  //body属性，直接获取body标签节点
        //返回：[object HTMLBodyElement] body标签节点对象
    
        alert(document.body.nodeName); //获取body标签名称
        //返回：BODY  标签名称
    };
[/code]



**在
<html>之前还有一个文档声明：<!DOCTYPE>会作为某些浏览器的第一个节点来处理，这里提供了一个简便方法来处理：document.doctype。**

**doctype属性，直接获取html文档声明标签节点**  
 **注意：ie7以下不支持，ie7以下只能通过父节点获取子节点得到，并且得到的是文档注释类型，不是元素类型**

PS：IE8中，如果使用子节点访问，IE8之前会解释为注释类型Comment节点，而document.doctype则会返回null。

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.doctype);  //doctype属性，直接获取html文档声明标签节点
        //返回：[object DocumentType] 文档声明标签节点对象
    };
[/code]



**Document中有一些遗留的属性和对象合集，可以快速的帮助我们精确的处理一些任务** **。**

**title属性，获取和设置 <title>标签的值**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.title);  //title属性，获取和设置<title>标签的值
        //返回：JavaScript讲解
    
        alert(document.title = '修改标题');  //设置<title>标签的值
        //返回：修改标题
    };
[/code]

**URL属性，获取URL路径**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.URL);  //URL属性，获取URL路径
        //返回：http://localhost:63342/js/1.html?_ijt=d9jd9jpm38tl3bb99qlpgr4rbo 
    };
[/code]

**domain属性，获取域名，要在服务器端**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.domain);  //domain属性，获取域名，要在服务器端
        //返回：localhost 
    };
[/code]

**referrer属性，获取上一个URL，要在服务器端**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.referrer);  //referrer属性，获取上一个URL，要在服务器端,如果上一页没有返回空
    };
[/code]

**anchors属性，获取文档中带name属性的 <a>元素集合**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.anchors);  //anchors属性，获取文档中带name属性的<a>元素集合
    };
[/code]

**links属性，获取文档中带href属性的 <a>元素集合**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.links);  //links属性，获取文档中带href属性的<a>元素集合
    };
[/code]

**forms属性，获取文档中 <form>元素集合**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.forms);  //forms属性，获取文档中<form>元素集合
    };
[/code]

**images属性，获取文档中 <img>元素集合**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.images);  //images属性，获取文档中<img>元素集合
    };
[/code]



**3.Element元素类型**

**Element类型用于表现HTML中的元素节点。在DOM基础那章，我们已经可以对元素节点进行查找、创建等操作，元素节点的nodeType为1，nodeName为元素的标签名。**

**元素节点对象在非IE浏览器可以返回它具体元素节点的对象类型。**



**元素对应类型表**

**元素名**

|

**类型**  
  
---|---  
  
**HTML**

|

**HTMLHtmlElement**  
  
**DIV**

|

**HTMLDivElement**  
  
**BODY**

|

**HTMLBodyElement**  
  
**P**

|

**HTMLParamElement**  
  
**PS：以上给出了部分对应，更多的元素对应类型，直接访问调用即可**



**4.Text类型**

**Text类型用于表现文本节点类型，文本不包含HTML，或包含转义后的HTML。文本节点的nodeType为3。**

**在同时创建两个同一级别的文本节点的时候，会产生分离的两个节点。**



**在同时创建两个同一级别的文本节点的时候，会产生分离的两个节点。**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        var text1 = document.createTextNode('文本1'); //创建一个文本节点
        var text2 = document.createTextNode('文本2'); //创建一个文本节点
        sdf.appendChild(text1); //将新节点添加到sdf节点里子节点末尾
        sdf.appendChild(text2); //将新节点添加到sdf节点里子节点末尾
        alert(sdf.childNodes.length);  //查看元素节点里的子节点集合长度
        //返回2，说明是两个文本节点
        //<div id="box" title="标题">文本1文本2</div>
        //注意：此时添加了两个文本节点，但是用眼睛看就像是一个文本节点，这里一点要注意
    };
[/code]

**normalize()合并同级的文本节点**

**使用方式：**

**目标节点的父节点. **normalize()****

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        var text1 = document.createTextNode('文本1'); //创建一个文本节点
        var text2 = document.createTextNode('文本2'); //创建一个文本节点
        sdf.appendChild(text1); //将新节点添加到sdf节点里子节点末尾
        sdf.appendChild(text2); //将新节点添加到sdf节点里子节点末尾
        alert(sdf.childNodes.length);  //查看元素节点里的子节点集合长度
        //返回2，说明是两个文本节点
        //<div id="box" title="标题">文本1文本2</div>
        //注意：此时添加了两个文本节点，但是用眼睛看就像是一个文本节点，这里一点要注意  
      
    
    
        //normalize()合并同级的文本节点
        sdf.normalize(); //将一个元素节点里的同级多个文本子节点，合并成一个文本子节点
        alert(sdf.childNodes.length); //查看元素节点里的子节点集合长度
        //返回：1 ，说明已经合并了
    };
[/code]

**splitText()分离一个文本节点，参数是要分离的字符数**  
 **使用方式：**  
 **目标文本节点.splitText(分离几个字符)**

[code]

    //<div id="box" title="标题">这是一段文本</div>
[/code]

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        alert(sdf.childNodes.length);  //查看元素里的子节点长度
        //返回：1 ，说明是一个文本子节点
        alert(sdf.childNodes[0].nodeValue); //查看文本子节点内容
        //返回：这是一段文本
    
        //splitText()分离一个文本节点，参数是要分离的字符数
        sdf.childNodes[0].splitText(3);  //将文本节点前3个字符分离成一个文本节点
        alert(sdf.childNodes.length);  //查看元素里的子节点长度
        //返回2，说明已经分离了
        alert(sdf.childNodes[0].nodeValue); //查看文本子节点内容
    };
[/code]

**  Text还提供了一些别的DOM操作的方法如下：**

**deleteData()删除一个文本节点里指定范围的字符，参数是要删除字符的起始位置,和结束位置**  
 **使用方式：**  
 **目标文本节点.deleteData(起始位置,结束位置)**

[code]

    //<div id="box" title="标题">这是一段文本</div>
[/code]

[code]

      
     window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        alert(sdf.childNodes[0].nodeValue);  //查看节点里子元素的文本
        //返回：这是一段文本
    
        //deleteData()删除一个文本节点里指定范围的字符，参数是要删除字符的起始位置,和结束位置
        sdf.childNodes[0].deleteData(0,3);  //删除文本节点里的指定文本，从0-3位置删除
        alert(sdf.childNodes[0].nodeValue); //查看删除后的文本
        //返回：段文本
    };
[/code]

**insertData()在文本节点里的指定位置添加指定文本内容**  
 **使用方式：**  
 **目标文本节点.insertData(要添加文本的字符位置,要添加的文本内容)**

[code]

     //<div id="box" title="标题">这是一段文本</div>  
      
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        alert(sdf.childNodes[0].nodeValue);  //查看节点里子元素的文本
        //返回：这是一段文本
    
        //insertData()在文本节点里的指定位置添加指定文本内容
        sdf.childNodes[0].insertData(4,'测试'); //insertData()在文本节点里的指定位置添加指定文本内容
        alert(sdf.childNodes[0].nodeValue);  //查看节点里子元素的文本
        //返回：这是一段测试文本  添加成功
    };
[/code]

**replaceData()在文本节点里的指定范围替换成指定文本内容**  
 **使用方式：**  
 **目标文本节点.replaceData(要替换的起始范围位置,要替换几个字符,要替换的字符串)**

[code]

     //<div id="box" title="标题">这是一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        alert(sdf.childNodes[0].nodeValue);  //查看节点里子元素的文本
        //返回：这是一段文本
    
        //replaceData()在文本节点里的指定范围替换成指定文本内容
        sdf.childNodes[0].replaceData(2,2,'测试'); 
        alert(sdf.childNodes[0].nodeValue);  //查看替换后的文本
        //返回：这是测试文本
    };
[/code]

**substringData()在文本节点里获取指定范围文本内容**  
 **使用方式：**  
 **目标文本节点.substringData(起始范围位置,获取几个字符)**

[code]

     //<div id="box" title="标题">这是一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('box');  //通过id获取到标签
        alert(sdf.childNodes[0].nodeValue);  //查看节点里子元素的文本
        //返回：这是一段文本
    
        //substringData()在文本节点里获取指定范围文本内容
        alert(sdf.childNodes[0].substringData(0,2)); //substringData()在文本节点里获取指定范围文本内容
        //返回：这是
    };
[/code]



**5.Comment类型，html注释节点**

**Comment类型表示文档中的注释。nodeType是8，nodeName是#comment，nodeValue是注释的内容。**

[code]

     //<div id="box" title="标题"><!--这是注释--></div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //非IE获取注释节点
        var asf = document.getElementById('box');  //通过ID获取到注释的父节点
        alert(asf.childNodes.length);  //查看节点里的子节点长度
        //返回1：说明就一个子节点
        alert(asf.childNodes[0].nodeName);  //查看第一个子节点的标签名称
        //返回：#comment 表示是标签名称
        alert(asf.childNodes[0].nodeValue);  //查看第一个子节点的文本内容
        //返回：这是注释
    
        //低版本IE获取注释节点
        var asf2 = document.getElementsByName('!');  //通过标签名称获取到注释标签节点
        alert(asf2.length);  //查看获取到的注释节点长度
    };
[/code]



**6.Attr类型，标签属性类型**

**Attr类型表示文档元素中的属性。nodeType为2，nodeName为属性名，nodeValue为属性值。DOM基础篇已经详细介绍过，略。**



**二．DOM扩展**

**1.呈现模式**

**从IE6开始开始区分标准模式和混杂模式(怪异模式)，主要是看文档的声明。IE为document对象添加了一个名为compatMode属性，这个属性可以识别IE浏览器的文档处于什么模式如果是标准模式，则返回CSS1Compat，如果是混杂模式则返回BackCompat。**

**compatMode属性，识别IE浏览器的文档处于什么模式，标准模式返回CSS1Compat，混杂模式返回BackCompat**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //compatMode属性，识别IE浏览器的文档处于什么模式，标准模式返回CSS1Compat，混杂模式返回BackCompat
        alert(document.compatMode);  //查看IE浏览器的文档处于什么模式
        //返回：CSS1Compat
    
        //如果把html文档声明<!DOCTYPE html>删除了就是混杂模式
        //返回：BackCompat
    };
[/code]

**clientWidth属性，查看节点元素的宽度**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //判断文档处于什么模式，如果是标准模式
        if (document.compatMode == 'CSS1Compat') {
            //如果是标准模式，获取到html节点，查看它的宽度
            alert(document.documentElement.clientWidth);
        } else {
            //如果不是标准模式，获取到body标签节点，查看它的宽度
            alert(document.body.clientWidth);
        }
    };
[/code]

**后来Firefox、Opera和Chrome都实现了这个属性。从IE8后，又引入documentMode新属性，因为IE8有3种呈现模式分别为标准模式8，仿真模式7，混杂模式5。所以如果想测试IE8的标准模式，就判断document.documentMode
> 7 即可。**

****documentMode属性， **识别IE浏览器的文档处于什么模式， **标准模式8，仿真模式7，混杂模式5，返回数值********

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //documentMode属性，识别IE浏览器的文档处于什么模式，标准模式8，仿真模式7，混杂模式5，返回数值
        if (document.documentMode <= 5) {
            alert('混杂模式');
        }else if(document.documentMode <= 7){
            alert('仿真模式');
        }else if(document.documentMode <= 8){
            alert('标准模式');
        }
    };
[/code]



**2.滚动**

**DOM提供了一些滚动页面的方法，如下：**

**scrollIntoView()方法，将一个元素节点设置滚动在可见范围**  
**注意：这里说的可见范围是这样的，比如目标节点在页面底部，而目标节点上面有很多类容，也就是目标节点超出浏览器范围不可见，要手动拖动滚动条才可见，scrollIntoView()方法可以定位滚动条到目标节点可见范围**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        document.getElementById('box').scrollIntoView();    //设置指定可见
    };
[/code]



**3.children属性**

****children属性，获取一个元素节点里的子节点，自动过滤掉空白文本节点 **【推荐】******

**由于子节点空白问题，IE和其他浏览器解释不一致。虽然可以过滤掉，但如果只是想得到有效子节点，可以使用children属性，支持的浏览器为：IE5+、Firefox3.5+、Safari2+、Opera8+和Chrome，这个属性是非标准的。**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');    //通过id获取到元素节点
        alert(asf.children);  //children属性，获取一个元素节点里的子节点，自动过滤掉空白文本节点
        //返回：[object HTMLCollection] 子节点集合对象
        alert(asf.children.length);  //查看子节点的长度
        //返回：3 ，已经自动过滤了空白文本子节点
    
        //循环出所有子节点的标签名称和内容文本
        for (var i = 0; i < asf.children.length; i ++){  //根据子节点长度循环次数
            //每次循环打印出循环到的子节点标签名称和子节点标签文本内容
            alert('标签名称：' + asf.children[i].nodeName + '-' + '标签文本内容：' + asf.children[i].innerHTML);
        }
    };
[/code]



**4.contains()方法**

**contains()方法，判断一个节点是否是另外一个节点的子节点，返回布尔值**  
 **使用方式：**  
 **要判断的父节点.contains(要判断的子节点)**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');    //通过id获取到元素节点
        //contains()方法，判断一个节点是否是另外一个节点的子节点，返回布尔值
        alert(asf.contains(asf.children[0])); //判断asf节点里的第一个子节点是否是asf的子节点
        //true
    };
[/code]



**PS：早期的Firefox不支持这个方法，新版的支持了，其他浏览器也都支持，Safari2.x浏览器支持的有问题，无法使用。所以，必须做兼容。**



**在Firefox的DOM3级实现中提供了一个替代的方法compareDocumentPosition()方法。这个方法确定两个节点之间的关系。**

**compareDocumentPosition()方法，判断两个节点之间的关系，返回关系掩码**  
 **使用方式：**  
 **要判断的a节点.compareDocumentPosition(要判断的b节点)**

**关系掩码表**

**掩码**

|

**节点关系**  
  
---|---  
  
**1**

|

**无关(节点不存在)**  
  
**2**

|

**居前(节点在参考点之前)**  
  
**4**

|

**居后(节点在参考点之后)**  
  
**8**

|

**包含(节点是参考点的祖先)**  
  
**16**

|

**被包含(节点是参考点的后代)**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');    //通过id获取到元素节点
        //compareDocumentPosition()方法，判断两个节点之间的关系，返回关系掩码
        alert(asf.compareDocumentPosition(asf.children[0])); //判断asf节点里的第一个子节点与asf节点是什么关系
        //返回：20，
        //为什么会出现20，那是因为满足了4和16两项，最后相加了
    };
[/code]  
  
**PS：为什么会出现20，那是因为满足了4和16两项，最后相加了。为了能让所有浏览器都可以兼容，我们必须写一个兼容性的函数。**



**contains()方法和compareDocumentPosition()方法的兼容方式**

**自定义一个判断两个节点关系的函数， **判断一个节点是否是另外一个节点的子节点，返回布尔值****



[code]

    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    
    //contains()方法和compareDocumentPosition()方法的兼容方式
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //首先创建两个节点，用于判断它们之间的关系
        var jd1 = document.getElementById('box');  //获取到父节点
        var jd2 = jd1.children[0]; //获取到子节点
    
        //执行判断两个节点关系函数
        alert(containsjr(jd1,jd2));
    
        //自定义兼容函数
        function containsjr(jdx1,jdx2) {  //函数接收两个参数，第一个参数父节点，第二个参数子节点
            //判断浏览器如果支持contains()方法 ，并且非Safari浏览器 ，导入浏览器检测模块browserdetect.js
            if (typeof jdx1.contains != 'undefined' && !(BrowserDetect.browser == 'Safari' && BrowserDetect.version < 3)){
                //返回contains()方法执行后的结果
                return jdx1.contains(jdx2); //contains()方法，判断一个节点是否是另外一个节点的子节点，返回布尔值
            }else if(typeof jdx1.compareDocumentPosition == 'function'){  //判断浏览器如果支持compareDocumentPosition方法
                return jdx1.compareDocumentPosition(jdx2) > 16; //compareDocumentPosition()方法，判断两个节点之间的关系，返回关系掩码
            }else {
                //更低的浏览器兼容，通过递归一个个获取他的父节点是否存在
                var node = jdx2.parentNode; //通过子节点获取父节点
                //do...while语句是一种先运行，后判断的循环语句。也就是说，不管条件是否满足，至少先运行一次循环体。
                do {
                    if (node === jdx1){ //判断通过子节点获取到的父节点如果等于函数传参的父节点
                        return true;
                    }else {
                        node = node.parentNode; //否则node变量等于父节点的父节点
                    }
                }while (node != null);
                return false;
            }
        }
    };
[/code]



**三．** **DOM** **操作内容**

**虽然在之前我们已经学习了各种DOM操作的方法，这里所介绍是innerText、innerHTML、outerText和outerHTML等属性。除了之前用过的innerHTML之外，其他三个还么有涉及到。**

**1.innerText属性【推荐】**

****innerText属性，设置或**** **获取一个元素的文本内容，获取(如有html直接过滤掉)，** **设置文本 (如有html转义)**

**使用方式：**

**目标节点.innerText**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        alert(asf.innerText);   //innerText属性，设置或获取一个元素的文本内容，获取(如有html直接过滤掉)，设置文本(如有html转义)
        //返回
        // 测试1
        // 测试2
        // 测试3
        asf.innerText = '<b>修改</b>';  //重新设置节点内容
        alert(asf.innerText);  //重新查看节点内容
        //<b>修改</b>
    };
[/code]

**PS
：除了Firefox火狐浏览器之外，其他浏览器均支持这个方法。但Firefox的DOM3级提供了另外一个类似的属性：textContent，做上兼容即可通用。**

**textContent属性(只有火狐支持)，设置或获取一个元素的文本内容，获取(如有html直接过滤掉)，设置文本(如有html转义)**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        alert(asf.textContent);   //textContent属性，设置或获取一个元素的文本内容，获取(如有html直接过滤掉)，设置文本(如有html转义)
        //返回
        // 测试1
        // 测试2
        // 测试3
        asf.textContent = '<b>修改</b>';  //重新设置节点内容
        alert(asf.textContent);  //重新查看节点内容
        //<b>修改</b>
    };
[/code]

**  innerText和textContent兼容方案**

[code]

    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        alert(getInnerText(asf)); //获取节点文本
        setInnerText(asf,'<b>赋值</b>')
        alert(getInnerText(asf)); //获取节点文本
    
    };
    
    //兼容方案
    //获取方案
    function getInnerText(element) { //接收节点
        //三元运算，判断节点的textContent类型等于string，执行element.textContent，否则执行element.innerText
        return (typeof element.textContent == 'string') ? element.textContent : element.innerText;
    }
    
    //设置方案
    function setInnerText(element, text) { //接收节点，和要设置的字符串
        if (typeof element.textContent == 'string') {
            element.textContent = text;
        } else {
            element.innerText = text;
        }
    }
[/code]

**2.innerHTML属性【推荐】**

****innerHTML属性，获取节点里的文本内容，不过滤html****

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        alert(asf.innerHTML); //获取节点里的文本内容，不过滤html
        asf.innerHTML = '<b>123</b>'; //设置节点里的文本内容，可解析HTML
        alert(asf.innerHTML); ////获取节点里的文本内容，不过滤html
    };
[/code]



**PS：关于最常用的innerHTML属性和节点操作方法的比较，在插入大量HTML标记时使用innerHTML的效率明显要高很多。因为在设置innerHTML时，会创建一个HTML解析器。这个解析器是浏览器级别的(C++编写)，因此执行JavaScript会快的多。但，创建和销毁HTML解析器也会带来性能损失。最好控制在最合理的范围内，如下：**

[code]

     for (var i = 0; i < 10; i ++) {
    ul.innerHTML = '<li>item</li>';            //避免频繁
    }
    //改
    for (var i = 0; i < 10; i ++) {
    a = '<li>item</li>';                        //临时保存
    }
    ul.innerHTML = a;
[/code]



**虽然innerHTML可以插入HTML，但本身还是有一定的限制，也就是所谓的作用域元素，离开这个作用域就无效了**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        asf.innerHTML = "<script>alert('Lee');</script>";    //<script>元素不能被执行
        asf.innerHTML = "<style>background:red;</style>";    //<style>元素不能被执行
    
    };
[/code]



**3.outerText**

**outerText在取值的时候和innerText一样，同时火狐不支持，而赋值方法相当危险，他不单替换了文本内容，还将节点元素直接抹去。【不建议使用】**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        asf.outerText = '<b>123</b>';  //给节设置文本内容
        alert(document.getElementById('box'));            //null，建议不去使用
    
    };
[/code]

**4.outerHTML**

**outerHTML属性在取值和innerHTML一致，但和outerText也一样，很危险，赋值的之后会将元素抹去。 **【不建议使用】****

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试3</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取一个节点
        asf.outerHTML = '123'; //设置节点文本内容
        alert(document.getElementById('box'));            //null，建议不去使用，火狐旧版未抹去
    };
[/code]





