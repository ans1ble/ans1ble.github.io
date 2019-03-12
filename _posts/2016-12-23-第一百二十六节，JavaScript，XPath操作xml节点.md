---
layout: post
title: " 第一百二十六节，JavaScript，XPath操作xml节点 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第一百二十六节，JavaScript，XPath操作xml节点**



**学习要点：**

**1.IE中的XPath**

**2.W3C中的XPath**

**3.XPath跨浏览器兼容**



**XPath是一种节点查找手段，对比之前使用标准DOM去查找XML中的节点方式，大大降低了查找难度，方便开发者使用。但是，DOM3级以前的标准并没有就XPath做出规范；直到DOM3在首次推荐到标准规范行列。大部分浏览器实现了这个标准，IE则以自己的方式实现了XPath。**



**一．IE中的XPath**

**在IE8及之前的浏览器，XPath是采用内置基于ActiveX的XML
DOM文档对象实现的。在每一个节点上提供了两个方法：selectSingleNode()和selectNodes()。**

**selectSingleNode()方法接受一个XPath模式（也就是查找路径），找到匹配的第一个节点并将它返回，没有则返回null。**

**selectSingleNode()方法，查找xml节点，查找单一节点如果有相同的节点只返回第一个节点，有参参数是要查找的节点路径，此方法只支持IE并且是IE9以下**  
 **使用方式**  
 **XML DOM对象.selectSingleNode('要查找的节点路径')**

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    //通过XML DOM对象查找xml标签节点
    var chzhao = xmldom.selectSingleNode('root/user'); //selectSingleNode()方法，查找xml节点，有参参数是要查找的节点路径，此方法只支持IE并且是IE9以下
    alert(serializeXML(chzhao)); //执行序列化函数，序列化查找到的节点
    alert(chzhao.tagName); //打印查找到的元素标签名称
    alert(chzhao.firstChild.nodeValue); //打印查找到的元素文本内容
    
    
    
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



**上下文节点**

**上下文节点：我们通过xmlDom这个对象实例调用方法，而xmlDom这个对象实例其实就是一个上下文节点，这个节点指针指向的是根，也就是root元素之前。那么如果我们把这个指针指向user元素之前，那么结果就会有所变化。**

**通过xmlDom，并且使用root/user的路径**

[code]

     //通过xmlDom，并且使用root/user的路径
    
    var user = xmlDom.selectSingleNode('root/user');
    
    alert(user.tagName);                                                //user
[/code]

**通过xmlDom.documentElement，并且使用user路径，省去了root**

[code]

     //通过xmlDom.documentElement，并且使用user路径，省去了root
    
    var user = xmlDom.documentElement.selectSingleNode('user');
    
    alert(user.tagName);                                                //user
[/code]

**通过xmlDom，并且使用user路径，省去了root**

[code]

     //通过xmlDom，并且使用user路径，省去了root
    
    var user = xmlDom.selectSingleNode('user');
    
    alert(user.tagName);                                                //找不到了，出错 ** **
[/code]

**PS：xmlDom和xmlDom.documentElement都是上下文节点，主要就是定位当前路径查找的指针，而xmlDom对象实例的指针就是在最根上。**



**XPath** **常用语法**



**通过user[n]来获取第n+1条节点，PS：XPath其实是按1为起始值的，也就是通过索引位置来获取对应的标签**

[code]

     //通过user[n]来获取第n+1条节点，PS：XPath其实是按1为起始值的
    var user = xmlDom.selectSingleNode('root/user[1]');
    alert(user.xml);
[/code]

**通过text()获取节点内的值**

[code]

     //通过text()获取节点内的值
    var user = xmlDom.selectSingleNode('root/user/text()');
    alert(user.xml);
    alert(user.nodeValue);
[/code]

**通过//user 表示在整个xml获取到user节点，不关心任何层次，通过双斜杠获取节点**

[code]

     //通过//user表示在整个xml获取到user节点，不关心任何层次
    var user = xmlDom.selectSingleNode('//user');
    alert(user.xml);    
[/code]

**通过root//user表示在root包含的层次下获取到user节点，在root内不关心任何层次， **通过指定节点下双斜杠获取节点****

[code]

     //通过root//user表示在root包含的层次下获取到user节点，在root内不关心任何层次
    var user = xmlDom.selectSingleNode('root//user');
    alert(user.tagName);    
[/code]

**通过root/user[@id=6]表示获取user中id=6的节点，通过id获取指定节点**

[code]

     //通过root/user[@id=6]表示获取user中id=6的节点
    var user = xmlDom.selectSingleNode('root/user[@id=6]');
    alert(user.xml);    
[/code]

**PS：更多的XPath语法，可以参考XPath手册或者XML DOM手册进行参考，这里只提供了最常用的语法。**



**selectNodes()方法，查找xml节点，返回相同名称的节点集合，有参参数是要查找的节点路径，此方法只支持IE并且是IE9以下**  
 **使用方式**  
 **XML DOM对象.selectNodes('要查找的节点路径')**

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    //通过XML DOM对象查找xml标签节点
    var chzhao = xmldom.selectNodes('root/user'); //selectNodes()方法，查找xml节点，返回相同名称的节点集合，有参参数是要查找的节点路径，此方法只支持IE并且是IE9以下
    alert(chzhao.length); //查看节点集合长度
    alert(serializeXML(chzhao[0])); //通过索引，执行序列化函数，序列化查找到的节点
    alert(chzhao[0].tagName); //通过索引打印查找到的元素标签名称
    alert(chzhao[0].firstChild.nodeValue); //通过索引打印查找到的元素文本内容
    
    
    
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



**二．W3C** **下的XPath**

**在DOM3级XPath规范定义的类型中，最重要的两个类型是XPathEvaluator和XPathResult。其中，XPathEvaluator用于在特定上下文对XPath表达式求值。**

**XPathEvaluator的方法**

**方法**

|

**说明**  
  
---|---  
  
**createExpression(e, n)**

|

**将XPath表达式及命名空间转化成XPathExpression**  
  
**createNSResolver(n)**

|

**根据n命名空间创建一个新的XPathNSResolver对象**  
  
**evaluate(e, c, n ,t ,r)**

|

**结合上下文来获取XPath表达式的值**  
  
**W3C实现XPath查询节点比IE来的复杂，首先第一步就是需要得到XPathResult对象的实例。得到这个对象实例有两种方法，一种是通过创建XPathEvaluator对象执行evaluate()方法，另一种是直接通过上下文节点对象(比如xmlDom)来执行evaluate()方法。**

**XPathResult对象**

****XPathEvaluator** 类型**

**第一个方式，首先new   **XPathEvaluator** **类型，然后执行 **XPathEvaluator** ** **类型下的
**evaluate()方法来创建 ** ** ** **XPathResult对象******************

**evaluate()方法，创建XPathResult对象有5个参数，1要查找的xml标签路径，2上下文节点对象也就是XMLDOM对象，3命名空间求解器(通常是null)，4返回结果类型，5保存结果的XPathResult对象(通常是null)。**  
 **使用方式：**  
 **XPathResult对象.evaluate(要查找的xml标签路径,XMLDOM对象,null,返回结果类型,null)**

**对于返回的结果类型，有10中不同的类型，常用的是红字的两个类型**

**常量**

|

**说明**  
  
---|---  
  
**XPathResult.ANY_TYPE**

|

**返回符合XPath表达式类型的数据**  
  
**XPathResult.ANY_UNORDERED_NODE_TYPE**

|

**返回匹配节点的节点集合，但顺序可能与文档中的节点的顺序不匹配**  
  
**XPathResult.BOOLEAN_TYPE**

|

**返回布尔值**  
  
**XPathResult.FIRST_ORDERED_NODE_TYPE**

|

**返回只包含一个节点的节点集合，且这个节点是在文档中第一个匹配的节点**  
  
**XPathResult.NUMBER_TYPE**

|

**返回数字值**  
  
**XPathResult.ORDERED_NODE_ITERATOR_TYPE**

|

**返回匹配节点的节点集合，顺序为节点在文档中出现的顺序。这是最常用到的结果类型**  
  
**XPathResult.ORDERED_NODE_SNAPSHOT_TYPE**

|

**返回节点集合快照，在文档外捕获节点，这样将来对文档的任何修改都不会影响这个节点列表**  
  
**XPathResult.STRING_TYPE**

|

**返回字符串值**  
  
**XPathResult.UNORDERED_NODE_ITERATOR_TYPE**

|

**返回匹配节点的节点集合，不过顺序可能不会按照节点在文档中出现的顺序排列**  
  
**XPathResult.UNORDERED_NODE_SNAPSHOT_TYPE**

|

**返回节点集合快照，在文档外捕获节点，这样将来对文档的任何修改都不会影响这个节点列表**  
  
**PS：上面的常量过于繁重，对于我们只需要学习了解，其实也就需要两个：1.获取一个单一节、2.获取一个节点集合。**

**两种方式创建 ** ** ** ** ** ** ** ** **XPathResult对象********************

**使用XPathEvaluator对象创建XPathResult**

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    
    //使用XPathEvaluator对象创建XPathResult
    var eva = new XPathEvaluator();  //创建XPathResult对象
    //evaluate()方法，创建XPathResult对象有5个参数，1要查找的xml标签路径，2上下文节点对象也就是XMLDOM对象，3命名空间求解器(通常是null)，4返回结果类型，5保存结果的XPathResult对象(通常是null)。
    var result = eva.evaluate('root/user', xmldom , null,XPathResult.FIRST_ORDERED_NODE_TYPE, null);
    alert(result); //返回单一节点集合
    
    
    
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

**使用上下文节点对象(xmlDom)创建XPathResult对象，就是直接在XMLDOM对象执行evaluate()方法**

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    
    //使用上下文节点对象(xmlDom)创建XPathResult
    var result = xmldom.evaluate('root/user', xmldom, null,XPathResult.FIRST_ORDERED_NODE_TYPE, null);
    alert(result);  //返回单一节点集合
    
    
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

**相对而言，第二种简单方便一点，但evaluate方法有五个属性：1.XPath路径、2.上下文节点对象、3.命名空间求解器(通常是null)、4.返回结果类型、5保存结果的XPathResult对象(通常是null)。**



**获取xml节点**

**1.获取一个单一节点**

**singleNodeValue属性，得到XPathResult对象里的 **单一**
节点对象，获取返回类型XPathResult.FIRST_ORDERED_NODE_TYPE **的节点对象****

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    
    var result = xmldom.evaluate('root/user', xmldom, null,XPathResult.FIRST_ORDERED_NODE_TYPE, null);
    if (result !== null) {
        //singleNodeValue属性，得到XPathResult对象里的节点对象
        alert(result.singleNodeValue.tagName);            //打印出节点的标签名称
    }
    
    
    
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

**2.获取节点集合**

**
iterateNext()方法，得到XPathResult对象里的集合节点对象，获取返回类型XPathResult.ORDERED_NODE_ITERATOR_TYPE的节点对象**

[code]

    var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    
    //使用上下文节点对象(xmlDom)创建XPathResult,返回类型为xml标签集合
    var result = xmldom.evaluate('root/user', xmldom, null,XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);
    if (result !== null) {  //判断集合不为空
        var nodes = []; //创建空数组
        var node = result.iterateNext();  //获取到集合里的一个标签对象
        while (node !== null) { //判断获取集合里的一个标签对象不为空，循环这个节点集合
            nodes.push(node); //将循环到的节点添加到初始化数组
            node = result.iterateNext(); //再次取集合里的一个标签对象，进行迭代
        }
    }
    
    alert(serializeXML(nodes[0])); //序列化打印第一个节点
    alert(serializeXML(nodes[1])); //序列化打印第二个节点
    
    
    
    
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

**PS：节点集合的获取方式，是通过迭代器遍历而来的，我们保存到数据中就模拟出IE相似的风格。**



**三．XPath** **跨浏览器兼容**

**如果要做W3C和IE的跨浏览器兼容，我们要思考几个问题：1.如果传递一个节点的下标，IE是从0开始计算，W3C从1开始计算，可以通过传递获取下标进行增1减1的操作来进行。2.独有的功能放弃，为了保证跨浏览器。3.只获取单一节点和节点列表即可，基本可以完成所有的操作。**

**  跨浏览器获取单一节点**

[code]

    var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    var jied = selectSingleNode(xmldom,'root/user');  //执行跨浏览器获取单一节点函数
    alert(serializeXML(jied));  //序列化节点标签
    
    
    
    //跨浏览器获取单一节点，返回单一节点对象
    function selectSingleNode(xmlDom, xpath) {  //加收两个参数，参数1XML DOM对象，参数二要查找的标签路径
        var node = null;  //初始化
    
        if (typeof xmlDom.evaluate != 'undefined') {  //判断XML DOM对象下的evaluate方法不等于undefined，说明支持，就用ie9以下的方式
            var patten = /\[(\d+)\]/g;  //正则
            var flag = xpath.match(patten); //返回正则匹配到的字符串
            var num = 0; //初始化
            if (flag !== null) {
                num = parseInt(RegExp.$1) + 1;
                xpath = xpath.replace(patten, '[' + num + ']');
            }
            var result = xmlDom.evaluate(xpath, xmlDom, null,XPathResult.FIRST_ORDERED_NODE_TYPE, null);
            if (result !== null) {
                node = result.singleNodeValue;
            }
        } else if (typeof xmlDom.selectSingleNode != 'undefined') {  //w3c方式
            node = xmlDom.selectSingleNode(xpath);
        }
    
        return node;
    }
    
    
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

**跨浏览器获取节点集合**

[code]

     var xml = '<root><user id="5">Lee</user><user id="6">Koko</user></root>';  //定义xml字符串
    var xmldom = getXMLDOM(xml); //创建XML DOM对象,接收xml字符串
    var jied = selectNodes(xmldom,'root/user');  //执行跨浏览器获取集合节点函数
    alert(serializeXML(jied[0]));  //序列化节点标签
    
    
    //跨浏览器获取节点集合，返回节点集合
    function selectNodes(xmlDom, xpath) { //接收两个参数，参数1XML DOM对象，参数2要查找的节点标签路径
        var nodes = [];
    
        if (typeof xmlDom.evaluate != 'undefined') {
            var patten = /\[(\d+)\]/g;
            var flag = xpath.match(patten);
            var num = 0;
            if (flag !== null) {
                num = parseInt(RegExp.$1) + 1;
                xpath = xpath.replace(patten, '[' + num + ']');
            }
            var node = null;
            var result = xmlDom.evaluate('root/user', xmlDom, null, XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);
            if (result !== null) {
                while ((node = result.iterateNext()) !== null) {
                    nodes.push(node);
                }
            }
        } else if (typeof xmlDom.selectNodes != 'undefined') {
            nodes = xmlDom.selectNodes(xpath);
        }
    
        return nodes;
    }
    
    
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

**PS：在传递xpath路径时，没有做验证判断是否合法，有兴趣的同学可以自行完成。在XML还有一个重要章节是XSLT和EX4，由于在使用频率的缘故，我们暂且搁置。**

