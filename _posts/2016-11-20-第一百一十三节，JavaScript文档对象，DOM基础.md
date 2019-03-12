
---
layout: post
title: " 第一百一十三节，JavaScript文档对象，DOM基础 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript文档对象，DOM基础**



**学习要点：**

**1.DOM介绍**

**2.查找元素**

**3.DOM节点**

**4.节点操作**



**DOM（Document Object
Model）即文档对象模型，针对HTML和XML文档的API（应用程序接口）。DOM描绘了一个层次化的节点树，运行开发人员添加、移除和修改页面的某一部分。DOM脱胎于Netscape及微软公司创始的DHTML（动态HTML），但现在它已经成为表现和操作页面标记的真正跨平台、语言中立的方式。**



**一．** **DOM** **介绍**

**DOM中的三个字母，D（文档）可以理解为整个Web加载的网页文档；O（对象）可以理解为类似window对象之类的东西，可以调用属性和方法，这里我们说的是document对象；M（模型）可以理解为网页文档的树型结构。**

**DOM有三个等级，分别是DOM1、DOM2、DOM3，并且DOM1在1998年10月成为W3C标准。DOM1所支持的浏览器包括IE6+、Firefox、Safari、Chrome和Opera1.7+。**

**PS：IE中的所有DOM对象都是以COM对象的形式实现的，这意味着IE中的DOM可能会和其他浏览器有一定的差异。**



**1.节点**

**加载HTML页面时，Web浏览器生成一个树型结构，用来表示页面内部结构。DOM将这种树型结构理解为由节点组成。**

**![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161120124553982-835097192.png)**



**从上图的树型结构，我们理解几个概念，html标签没有父辈，没有兄弟，所以html标签为根标签。head标签是html子标签，meta和title标签之间是兄弟关系。如果把每个标签当作一个节点的话，那么这些节点组合成了一棵节点树。**

**PS：后面我们经常把标签称作为元素，是一个意思。**

**2.节点种类：元素节点、文本节点、属性节点。**

**元素节点，其实就是标签**

****属性节点，就是这个标签的属性****

******文本节点，就是标签包含的文本******

**< div title="属性节点">测试Div</div>**



![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161120124856295-1429409381.png)

**二．查找元素，元素节点（查找节点）**

**W3C提供了比较方便简单的定位节点的方法和属性，以便我们快速的对节点进行操作。分别为：getElementById()、getElementsByTagName()、getElementsByName()、getAttribute()、setAttribute()和removeAttribute()。**



**元素节点方法**

**方法**

|

**说明**  
  
---|---  
  
**getElementById()**

|

**获取特定ID元素的节点**  
  
**getElementsByTagName()**

|

**获取相同元素的节点列表**  
  
**getElementsByName()**

|

**获取相同名称的节点列表**  
  
**getAttribute()**

|

**获取特定元素节点属性的值**  
  
**setAttribute()**

|

**设置特定元素节点属性的值**  
  
**removeAttribute()**

|

**移除特定元素节点属性**  
  
**注意： **DOM **文档对象，是操作html文档树的，所以要先执行完html后在执行js才能有效，有两种解决方案******

******1.将引入js的 <script>放到HTML最后面******

******2.使用window.onload事件，就是等待html执行完了在执行js代码******



**1.getElementById()方法，通过id获取对应的标签**

**getElementById()方法，接受一个参数：获取元素的ID值。如果找到相应的元素则返回该元素的HTMLDivElement对象，如果不存在，则返回null。**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');            //获取id为box的元素节点
        alert(asd); //返回获取到的元素节点对象
    };
[/code]

**PS：id表示一个元素节点的唯一性，不能同时给两个或以上的元素节点创建同一个命名的id。某些低版本的浏览器会无法识别getElementById()方法，比如IE5.0-，这时需要做一些判断，可以结合上章的浏览器检测来操作。**

**检测浏览器是否支持 **getElementById()方法****

[code]

     if (document.getElementById) {                //判断是否支持getElementById
    alert('当前浏览器支持getElementById');
    }
[/code]

**元素节点属性**



**属性**

|

**说明**  
  
---|---  
  
**tagName**

|

**获取元素节点的标签名**  
  
**innerHTML**

|

**获取元素节点里的内容，非 W3C DOM规范**  
  


**tagName属性，元素节点对象属性，获取或设置元素节点的标签名**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').tagName;    //getElementById元素节点对象属性，获取元素节点的标签名
        alert(asd); //返回获取元素节点的标签名
        //返回：DIV
    };
[/code]

**innerHTML属性，元素节点对象属性，获取 **或设置** 元素节点里的内容，非W3C DOM规范**

[code]

    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').innerHTML;    //getElementById元素节点对象属性，获取元素节点里的内容，非W3C DOM规范
        alert(asd); //获取元素节点里的内容，非W3C DOM规范
        //测试Div
    };
[/code]

**HTML 属性的属性**



**属性**

|

**说明**  
  
---|---  
  
**id**

|

**元素节点的 id名称**  
  
**title**

|

**元素节点的 title属性值**  
  
**style**

|

**CSS 内联样式属性值**  
  
**className**

|

**CSS 元素的类**  
  
**id，HTML属性的属性，获取或设置元素节点的id名称**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').id;    //获取标签的id名称
        alert(asd); //元素节点的id名称
        //box
        var asd2 = document.getElementById('box').id = 'person';    //设置标签的id名称
        alert(asd2); //元素节点的id名称
    };
[/code]

**title，HTML属性的属性，获取或设置元素节点的title属性值**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').title;    //获取元素节点的title属性值
        alert(asd); //元素节点的title属性值
        //标题
        var asd2 = document.getElementById('box').title = '修改标题';    //设置元素节点的title属性值
        alert(asd2); //元素节点的title属性值
        //修改标题
    };
[/code]

**style，HTML属性的属性，获取或设置CSS内联样式属性值  **

[code]

    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').style;    //获取CSSStyleDeclaration对象
        alert(asd); //获取CSSStyleDeclaration对象
        //[object CSS2Properties]
        var asd2 = document.getElementById('box').style.color;    //获取style对象中color的值
        alert(asd2); //获取style对象中color的值
        //rgb(245, 42, 45)
        var asd3 = document.getElementById('box').style.color = 'red';    //设置style对象中color的值
        alert(asd3);//获取style对象中color的值
    };
[/code]

**className，HTML属性的属性，获取或设置CSS元素的类 **class属性值****

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box').className;    //获取CSS元素的类class属性值
        alert(asd); //获取CSS元素的类class属性值
        //vdy
        var asd2 = document.getElementById('box').className = 'jhh'; //设置CSS元素的类class属性值
        alert(asd2); //获取CSS元素的类class属性值
        //jhh
    };
[/code]

**获取自定义标签属性的值，非IE不支持【不推荐】**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.getElementById('box').bbb);        //获取自定义属性的值，非IE不支持
    };
[/code]



**2.getElementsByTagName()方法，通过标签名称获取对应的标签**

**getElementsByTagName()方法将返回一个对象数组HTMLCollection(NodeList)，这个数组保存着所有相同元素名的节点列表。有参参数是要获取的标签名称，参数*表示获取所有标签**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByTagName('*');            //获取所有元素
        alert(sdf);  //打印获取到的标签对象数组
        //[object HTMLCollection]
    };
[/code]

**length，判断获取到的标签对象数组长度，就是有多少个标签**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByTagName('li').length;            //获取页面里的所有li标签，length判断长度
        alert(sdf);  //打印获取到的标签对象数组的长度
        //4，说明获取到4个标签
    };
[/code]

**  利用数组索引下标，获取标签数组对象里指定的标签**

[code]

    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByTagName('li')[0];    //利用数组索引下标，获取标签数组对象里指定的标签
        alert(sdf.tagName);  //打印获取到的所有li标签里的第一个标签名称
    };
[/code]

**item()，获取标签数组对象里指定的下标的标签,参数下标数**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByTagName('li').item(0);    //item()，获取标签数组对象里指定的下标的标签,参数下标数
        alert(sdf.tagName);  //打印获取到的所有li标签里的第一个标签名称
    };
[/code]

**  注意：getElementsByTagName()方法的其他属性与getElementById()方法相同**

**PS：不管是getElementById还是getElementsByTagName，在传递参数的时候，并不是所有浏览器都必须区分大小写，为了防止不必要的错误和麻烦，我们必须坚持养成区分大小写的习惯。**



**3.getElementsByName()方法，通过标签的name属性值获取节点，一般用于获取表单**

**getElementsByName()方法可以获取相同名称(name)的元素，返回一个对象数组HTMLCollection(NodeList)。参数
**name属性的值****

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByName('bd');    //通过标签的name属性值获取节点
        alert(sdf);  //打印获取到的name值为bd标签返回数组
        //[object NodeList]
    };
[/code]

**获取指定标签里的属性值**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementsByName('bd')[0];    //通过标签的name属性值获取节点,通过索引获取第一个标签
        alert(sdf.value);  //打印获取到的标签的value值
        //默认
    };
[/code]

**  注意： **getElementsByName()** 方法的其他属性与getElementById()方法相同**

**PS：对于并不是HTML合法的属性，那么在JS获取的兼容性上也会存在差异，IE浏览器支持本身合法的name属性，而不合法的就会出现不兼容的问题。**



**4.getAttribute()方法，获取元素中某个属性的值，首先要获取到节点后，在用 **getAttribute()方法【不推荐】****

**getAttribute()方法将获取元素中某个属性的值。它和直接使用.属性获取属性值的方法有一定区别。参数要获取的属性名称**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').getAttribute('style');    //先通过ID获取到标签节点，然后通过getAttribute()方法获取属性
        alert(sdf);  //打印获取到的标签属性值
        //color: #ff2217
    };
[/code]

[code]

    document.getElementById('box').getAttribute('id');//获取元素的id值
    document.getElementById('box').id;            //获取元素的id值
    
    document.getElementById('box').getAttribute('mydiv');//获取元素的自定义属性值
    document.getElementById('box').mydiv        //获取元素的自定义属性值，非IE不支持
    
    document.getElementById('box').getAttribute('class');//获取元素的class值，IE不支持
    document.getElementById('box').getAttribute('className');//非IE不支持
[/code]

**PS：HTML通用属性style和onclick，IE7更低的版本style返回一个对象，onclick返回一个函数式。虽然IE8已经修复这个bug，但为了更好的兼容，开发人员只有尽可能避免使用getAttribute()访问HTML属性了，或者碰到特殊的属性获取做特殊的兼容处理**



**5.setAttribute()方法，设置或者修改标签的属性和属性值，首先要获取到标签的节点在用 **setAttribute()方法****

**setAttribute()方法将设置元素中某个属性和值。它需要接受两个参数：属性名和值。如果属性本身已存在，那么就会被覆盖。**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').setAttribute('style','color:red'); //给获取到的标签添加一个style
        //此时可以看到标签已经加上了属性，标签里的文字已经是红颜色了
        var sdf2 = document.getElementById('asd').setAttribute('style','color:#216CDE'); //给获取到的标签style属性修改值
        //此时可以看到标签的style属性值已经被修改了
    };
[/code]

**PS：在IE7及更低的版本中，使用setAttribute()方法设置class和style属性是没有效果的，虽然IE8解决了这个bug，但还是不建议使用。**



**6.removeAttribute()方法，移除标签指定的属性， **首先要获取到标签的节点在用 **removeAttribute()******

**removeAttribute()可以移除HTML属性。参数要移除的属性名称**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').setAttribute('style','color:red'); //给获取到的标签添加一个style
        //此时可以看到标签已经加上了属性，标签里的文字已经是红颜色了
        var sdf2 = document.getElementById('asd').removeAttribute('style'); //移除标签指定的属性
        //此时可以看到标签的style属性已经被移除了
    };
[/code]

**PS：IE6及更低版本不支持removeAttribute()方法。**



**三．** **DOM** **节点属性（遍历节点）**

**1.node节点属性**

****node节点属性，只能获取当前节点的信息，并且要先获取到节点，在用属性， 下面 **childNodes属性有详细用到
**nodeName、nodeType和nodeValue。属性********

**节点可以分为元素节点、属性节点和文本节点，而这些节点又有三个非常有用的属性，分别为：nodeName、nodeType和nodeValue。**

**nodeName节点属性，获取或设置节点元素标签名称，和tagName等价，首先要获取到节点，在使用属性**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').nodeName; //nodeName节点属性，获取节点元素标签名称，和tagName等价
        alert(sdf); //打印出节点的标签名称
        //DIV
    };
[/code]

**nodeType节点属性，获取节点元素的类型值，元素节点返回1，属性节点返回2，文本节点返回3，首先要获取到节点，在使用属性**

[code]

    window.onload =  function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').nodeType; //nodeType节点属性，获取节点元素的类型值，元素节点返回1，属性节点返回2，文本节点返回3，首先要获取到节点，在使用属性
        alert(sdf); //节点元素的类型值
        //1,说明是元素节点
    };
[/code]

**nodeValue节点属性，获取 **或设置** 文本节点的文本，元素节点null本身没有类容，首先要获取到节点，在使用属性**

[code]

    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').nodeValue; //nodeValue节点属性，获取节点类容，元素节点本身没有类容，首先要获取到节点，在使用属性
        alert(sdf); //节点类容
        //null,说明元素节点本身没有类容，因为node属性只能获取当前节点
    };
[/code]



**2.层次节点属性**

**节点的层次结构可以划分为：父节点与子节点、兄弟节点这两种。当我们获取其中一个元素节点的时候，就可以使用层次节点属性来获取它相关层次的节点。**

**层次节点属性**

**属性**

|

**说明**  
  
---|---  
  
**childNodes**

|

**获取当前元素节点的所有子节点**  
  
**firstChild**

|

**获取当前元素节点的第一个子节点**  
  
**lastChild**

|

**获取当前元素节点的最后一个子节点**  
  
**ownerDocument**

|

**获取该节点的文档根节点，相当与document**  
  
**parentNode**

|

**获取当前节点的父节点**  
  
**previousSibling**

|

**获取当前节点的前一个同级节点**  
  
**nextSibling**

|

**获取当前节点的后一个同级节点**  
  
**attributes**

|

**获取当前元素节点的所有属性节点集合**  
  
**1.childNodes属性，获取元素和文本节点**

**childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点。首先要获取到元素节点在使用属性，**
**返回包含子节点和文本节点的数组**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>  
      
    
    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes; //childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点
        alert(sdf); //返回包含子节点和文本节点的数组
        //[object NodeList]
        alert(sdf.length) //查看数组长度
        //3，说明有3个包含子节点和文本节点
        alert(sdf[0]); //通过索引下标来获取第一个元素
        //[object Text]，第一个是文本节点
    };
[/code]

**使用childNodes[n]返回子节点对象的时候，有可能返回的是元素子节点，比如
HTMLElement；也有可能返回的是文本子节点，比如Text。元素子节点可以使用nodeName或者tagName获取标签名称，而文本子节点可以使用nodeValue获取文本。**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>  
      
    
    window.onload = function(){ //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes; //childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点
        alert(sdf); //返回包含子节点和文本节点的数组
    
        //通过循环加判断，得到包含子节点和文本节点数组里的子节点标签名称，和文本节点的文本类容
        for (var i = 0 ; i < sdf.length; i ++){  //根据数组的长度来循环次数
            if (sdf[i].nodeType == 1){  //通过数组下标得到节点元素，nodeType查看节点元素的类型值，
                //如果类型值返回1说明是元素节点，也就是标签
                alert('元素节点：' + sdf[i].nodeName);  //元素节点nodeName打印出标签名称
            }else if(sdf[i].nodeType == 3){  //通过数组下标得到节点元素，nodeType查看节点元素的类型值，
                //如果类型值返回3说明是文本节点，也就文本类容
                alert('文本节点：' + sdf[i].nodeValue);  //元素节点nodeName打印出标签名称
            }
    
        }
    
    };
[/code]

****innerHTML和nodeValue两个区别****

**PS：在获取到文本节点的时候，是无法使用innerHTML这个属性输出文本内容的。这个非标准的属性必须在获取元素节点的时候，才能输出里面包含的文本。**

**PS：innerHTML和nodeValue第一个区别，就是取值的。那么第二个区别就是赋值的时候，nodeValue会把包含在文本里的HTML转义成特殊字符，从而达到形成单纯文本的效果。**

[code]

    box.childNodes[0].nodeValue = '<strong>abc</strong>'; //结果为：<strong>abc</strong>
        box.innerHTML = '<strong>abc</strong>';        //结果为：abc
[/code]



**2.firstChild和lastChild属性**

**firstChild用于获取当前元素节点的第一个子节点，相当于childNodes[0]；**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').firstChild; //firstChild用于获取当前元素节点的第一个子节点，相当于childNodes[0]；
        alert(sdf); //打印出第一个文本子节点的对象
        //[object Text]
        alert(sdf.nodeValue);//打印出第一个文本子节点的文本类容  
        //测试  
    
    };
[/code]

**lastChild用于获取当前元素节点的最后一个子节点，**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').lastChild; //lastChild用于获取当前元素节点的最后一个子节点，
        alert(sdf); //打印出最后一个文本子节点的对象
        //[object Text]
        alert(sdf.nodeValue);//打印出最后一个文本子节点的文本类容
        //文本
    };
[/code]



**3.ownerDocument属性**

**ownerDocument属性返回该节点的文档对象根节点，返回的对象相当于document。**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').ownerDocument; //ownerDocument属性返回该节点的文档对象根节点，返回的对象相当于document。
        alert(sdf); //打印文档对象根节点
        //[object HTMLDocument]
    };
[/code]



**4.parentNode、previousSibling、nextSibling属性**

**parentNode属性返回该节点的父节点，**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').parentNode; //parentNode属性返回该节点的父节点，
        alert(sdf); //打印该节点的父节点
        //[object HTMLBodyElement]
    };
[/code]

**previousSibling属性返回该节点的前一个同级节点， **就是当前节点同级的上一个节点****

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes[2]; //获取当前节点里的第3个子节点包含文本节点
        alert(sdf); //打印当前节点
        //[object Text] 说明是文本节点
        alert(sdf.nodeValue); //打印当前文本节点的文本
        //文本
        alert(sdf.previousSibling); //previousSibling属性返回该节点的前一个同级节点，就是当前节点同级的上一个节点
        //[object HTMLElement] 说明是标签节点
        alert(sdf.previousSibling.nodeName); //打印当前节点的标签
        //B
    };
[/code]

**nextSibling属性返回该节点的后一个同级节点。就是当前节点同级的下一个节点**

[code]

     //<div id="asd">测试<b>这一段</b>文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes[0]; //获取当前节点里的第一个子节点包含文本节点
        alert(sdf); //打印第一个子节点，是一个文本节点，就是（测试）
        //[object Text]
        alert(sdf.nextSibling); //nextSibling属性返回该节点的后一个同级节点。就是当前节点同级的下一个节点
        //[object HTMLElement] //说明是一个元素节点
        alert(sdf.nextSibling.nodeName);//获取当前节点的标签名称
        //b ,就是b标签
        
    };
[/code]



**5.attributes属性，获取元素标签属性节点**

**attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性
        alert(sdf); //打印当前标签节点的标签属性集合
    };
[/code]

**length查看当前标签节点的标签属性集合长度**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性
        alert(sdf); //打印当前标签节点的标签属性集合
        alert(sdf.length); //length查看当前标签节点的标签属性集合长度
        //3,说明当前标签有3个标签属性
    };
[/code]

**通过索引来获取标签节点的标签属性集合里的指定标签属性对象**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性
        alert(sdf[0]); //通过索引来获取标签节点的标签属性集合里的指定标签属性
        //[object Attr] 标签属性对象
    };
[/code]

**nodeType查看当前节点的类型，1元素类型，2属性类型，3文本类型**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes[0]; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性,用索引获取第一个标签属性
        alert(sdf.nodeType); //nodeType查看当前节点的类型，1元素类型，2属性类型，3文本类型
        //2,说明是属性类型
    };
[/code]

**nodeValue获取标签属性的值，首先要获取到标签属性节点后在使用**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes[0]; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性,用索引获取第一个标签属性
        alert(sdf.nodeValue); //nodeValue获取标签属性的值，首先要获取到标签属性节点后在使用
        //asd,第一个属性的值为asd
    };
[/code]

**nodeName获取标签属性的名称，首先要获取到标签属性节点后在使用**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性,
        alert(sdf[0].nodeName); //nodeName获取标签属性的名称，首先要获取到标签属性节点后在使用
        //id
    };
[/code]

**通过属性名称获取属性值，首先要获取到标签属性节点集合**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性,
        alert(sdf['id'].nodeValue); //通过属性名称获取属性值，首先要获取到标签属性节点集合
    };
    //asd
[/code]

**循环打印出标签的所有属性和属性值**

[code]

     //<div id="asd" title="标题" style="color: #ff2217">测试这一段文本</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').attributes; //attributes属性返回该节点的属性节点集合。首先获取到元素节点后在用这个属性,
    
        for (var i = 0; i < sdf.length; i ++){  //根据属性集合的长度循环次数
            if(sdf[i].nodeType === 2){  //通过下标获取属性集合数据，判断返回类型，如果返回时2说明是标签属性类型
                alert('属性：' + sdf[i].nodeName + ':' + sdf[i].nodeValue); //打印出标签属性的属性名称和属性值
            }
        }
    };
    
    //属性：id:asd
    //属性：title:标题
    //属性：style:color: #ff2217
[/code]



**6.忽略空白文本节点，在获取子元素时遇到空白文本节点**

[code]

     // <div id="asd" title="标题" style="color: #ff2217">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes; //childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点，返回包含子节点和文本节点的数组
        alert(sdf.length); //查看子节点包含文本节点集合的长度
        //火狐浏览器返回7
        //IE返回3
        //说明浏览器解析方式不同，IE解释忽略了p标签前的空白，火狐将p标签前的空白算成空白文本了
    };
[/code]

**PS：在非IE中，标准的DOM具有识别空白文本节点的功能，所以在火狐浏览器是7个，而IE自动忽略了，如果要保持一致的子元素节点，需要手工忽略掉它。**

**忽略空白字符**

[code]

     // <div id="asd" title="标题" style="color: #ff2217">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes; //childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点，返回包含子节点和文本节点的数组
        alert(hul(sdf).length); //将子节点集合当做参数传入忽略空白函数，得到返回值后在检测长度
        //所有浏览器返回3，说明都忽略了空白文本节点
    };
    
    //创建忽略空白字符函数
    function hul(jh) {
        var ret = [];                                      //空数组，保存不是空白文本节点的节点
        for (var i = 0; i < jh.length; i ++){              //根据子节点集合长度循环次数
            //判断如果循环到的子节点类型是文本节点类型，并且子节点文本类容是空白类容
            if(jh[i].nodeType === 3 && /^\s+$/.test(jh[i].nodeValue)){
                continue;              //退出当前循环，继续后面的循环
            }else {                   //上来条件不成立，说明不是空白文本节点
                ret.push(jh[i]);      //将节点添加到数组
            }
        }
        return ret; //返回数组
    }
[/code]

**PS：上面的方法，采用的忽略空白文件节点的方法，把得到元素节点累加到数组里返回。那么还有一种做法是，直接删除空白节点即可。**

**  移除空文本节点**

**removeChild()删除一个节点里的指定子节点,参数要删除的子节点在节点集合里的下标，先要获取到要删除的子节点的父节点后，在父节点使用这个方法删除里面的子节点**

[code]

     // <div id="asd" title="标题" style="color: #ff2217">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>  
      
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd').childNodes; //childNodes属性可以获取某一个元素节点的所有子节点，这些子节点包含元素子节点和文本子节点，返回包含子节点和文本节点的数组
        alert(hul(sdf).length); //将子节点集合当做参数传入忽略空白函数，得到返回值后在检测长度
        //所有浏览器返回3，说明都删除了空白文本节点
    };
    
    //创建删除空文本节点符函数
    function hul(jh) {
        for (var i = 0; i < jh.length; i ++){              //根据子节点集合长度循环次数
            //判断如果循环到的子节点类型是文本节点类型，并且子节点文本类容是空白类容
            if(jh[i].nodeType === 3 && /^\s+$/.test(jh[i].nodeValue)){
                //得到空白节点之后从当前节点，获取到父节点上，在父节点删除子节点
                jh[i].parentNode.removeChild(jh[i]);
            }
        }
        return jh; //最后返回删除后的节点集合
    }
[/code]

**如果firstChild、lastChild、previousSibling和nextSibling在获取节点的过程中遇到空白节点，我们该怎么处理掉呢？**

**firstChild(获取当前元素节点的第一个子节点)、lastChild(获取当前元素节点的最后一个子节点)、previousSibling(当前节点同级的上一个节点)和nextSibling(就是当前节点同级的下一个节点)**

[code]

     // <div id="asd" title="标题" style="color: #ff2217">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var sdf = document.getElementById('asd'); //获取当前ID的节点
        alert(hul(sdf).firstChild.nodeName); //将当前节点当做参数传给删除空文本节点函数，最后获取第一个子节点的标签名称
        //p,可以看到已经删除空白文本子节点
    
    };
    
    //创建删除空文本节点函数
    function hul(jh) {
        for (var i = 0; i < jh.childNodes.length; i ++){              //根据子节点集合长度循环次数
            //判断如果循环到的子节点类型是文本节点类型，并且子节点文本类容是空白类容
            if(jh.childNodes[i].nodeType === 3 && /^\s+$/.test(jh.childNodes[i].nodeValue)){
                //得到空白节点之后从当前节点，获取到父节点上，在父节点删除子节点
                jh.childNodes[i].parentNode.removeChild(jh.childNodes[i]);
            }
        }
        return jh; //最后返回删除后的节点集合
    }
[/code]



**四．** **节点操作，（操作节点）**

**DOM不单单可以查找节点，也可以创建节点、复制节点、插入节点、删除节点和替换节点。**



**节点操作方法**

**方法**

|

**说明**  
  
---|---  
  
**write()**

|

**这个方法可以把任意字符串插入到文档中**  
  
**createElement()**

|

**创建一个元素节点**  
  
**appendChild()**

|

**将新节点追加到子节点列表的末尾**  
  
**createTextNode()**

|

**创建一个文件节点**  
  
**insertBefore()**

|

**将新节点插入在前面**  
  
**repalceChild()**

|

**将新节点替换旧节点**  
  
**cloneNode()**

|

**复制节点**  
  
**removeChild()**

|

**移除节点**  
  


**1.write()方法**

**write()方法可以把任意字符串插入到文档中去。插入文本或者标签低版本浏览器会覆盖原有的html内容，不推荐使用**

[code]

    document.write('<p>这是一段文本</p>');  //向浏览器插入一条p标签
[/code]



**2.createElement()方法**

**createElement()方法可以创建一个元素节点。参数要创建的元素标签名称，只是创建了元素节点，并没有写入文档，只是驻留在内存中**

[code]

    document.createElement('p');         //创建一个元素节点
[/code]

**ps:一般要先获取到父节点，后在createElement()方法创建元素节点，在结合appendChild()方法添加**



**3. appendChild()方法**

**appendChild()方法将一个新节点添加到某个节点的子节点列表的末尾上。** **参数** **createElement()方法**
**创建的节点，首先要获取到要添加节点的父节点**

**使用方式：**

**父节点. **appendChild(创建的新节点变量);****

****如：asd.appendChild(ys);****



[code]

    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');  //获取id为box的元素节点
        var ys = document.createElement('p');      //创建一个新元素节点<p>
        asd.appendChild(ys);                       //把新元素节点<p>添加到当前节点的子节点末尾
    };
    
    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p></p>
    // </div>
[/code]



**4.createTextNode()方法**

**createTextNode()方法创建一个文本节点。 **并没有写入文档，只是驻留在内存中，参数文本节点文本****

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');  //获取id为box的元素节点
        var ys = document.createTextNode('添加文本');      //reateTextNode()方法创建一个文本节点。并没有写入文档，只是驻留在内存中，
        asd.appendChild(ys);                       //把新文本节点添加到当前节点的子节点末尾
    };
    
    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     添加文本
    // </div>
[/code]

**将文本节点添加到元素节点里**

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');  //获取id为box的元素节点
        var ys = document.createElement('p');      //创建一个新元素节点<p>
        asd.appendChild(ys); //将新元素节点添加到当前节点的子节点末尾
    
        var text = document.createTextNode('测试2');      //reateTextNode()方法创建一个文本节点。并没有写入文档，只是驻留在内存中，
        ys.appendChild(text);                       //把新文本节点添加到新创建元素节点里
    };
    
    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试1</p>
    //     <p>测试2</p>
    // </div>
[/code]



**5.insertBefore()方法**

**insertBefore()方法可以把节点创建到指定节点的前面。第一个参数是要创建的标签名称，第二个参数是要在它之前创建节点的目标节点变量，首先获取到目标节点通过目标节点获取到父节点后在使用
**insertBefore()****

**使用方式：**

**目标节点变量.父节点. **insertBefore(创建节点变量,目标节点)****

**如：asd.parentNode.insertBefore(ys,asd);**

[code]

     // <body>
    // <div id="box" title="标题">测试</div>
    // </body>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');  //获取id为box的元素节点
        var ys = document.createElement('p');      //创建一个新元素节点<p>
        asd.parentNode.insertBefore(ys,asd);       //insertBefore()方法可以把节点创建到指定节点的前面
    };
    // <body>
    //     <p></p>
    //     <div id="box" title="标题"></div>
    // </body>
[/code]

**PS：insertBefore()方法可以给当前元素的前面创建一个节点，但却没有提供给当前元素的后面创建一个节点。那么，我们可以用已有的知识创建一个insertAfter()函数。**

**自定义给当前元素的后面创建一个节点**

[code]

     // <body>
    // <div id="box" title="标题">测试</div>
    // </body>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asd = document.getElementById('box');  //获取id为box的元素节点
        var ys = document.createElement('p');      //创建一个新元素节点<p>
        insertAfter(ys,asd); //调用自定义给当前元素的后面创建一个节点
    };
    
    function insertAfter(chjian,mubao) { //自定义一个函数，给当前元素的后面创建一个节点，给目标节点后面添加一个节点，接收两个参数，第一个创建节点变量，第二个目标节点
        //得到父节点,通过目标节点找到目标节点的父节点
        var parent = mubao.parentNode;
        //判断，父节点里最后一个子节点如果等于，目标节点
        if (parent.lastChild === mubao) {
            //就在父节点的，子节点末尾添加一个新节点
            parent.appendChild(chjian);
        }else {
            //否则,在父节点上向指定子节点的前面添加一个新节点,mubao.nextSibling,目标节点是当前节点同级的下一个节点，就把指针指向了当前节点后面
            parent.insertBefore(chjian, mubao.nextSibling);
        }
    
    }
    // <body>
    //     <div id="box" title="标题"></div>
    //     <p></p>
    // </body>
[/code]

** **

**createElement在创建一般元素节点的时候，浏览器的兼容性都还比较好。但在几个特殊标签上，比如iframe、input中的radio和checkbox、button元素中，可能会在IE6,7以下的浏览器存在一些不兼容。**

[code]

     // <body>
    // <div id="box" title="标题">测试</div>
    // </body>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = null; //创建一个空对象
        //用浏览器检测browserdetect.js，判断如果是ie浏览器，并且版本小于或者等于7
        if (BrowserDetect.browser == 'Internet Explorer' && BrowserDetect.version <= 7) {
            //判断IE6,7，使用字符串的方式
            input = document.createElement("<input type=\"radio\" name=\"sex\">");  //创建一个元素节点，值包含元素属性
        } else {
            //标准浏览器，使用标准方式
            input = document.createElement('input');  //创建一个新元素节点
            input.setAttribute('type', 'radio');  //设置一个新元素节点的属性和属性值
            input.setAttribute('name', 'sex');    //设置一个新元素节点的属性和属性值
        }
        //通过标签名称获取到body，将创建的新节添加到子节点列表的末尾
        document.getElementsByTagName('body')[0].appendChild(input);
    };
    
    // <body>
    //     <div id="box" title="标题"></div>
    //     <input name="sex" type="radio">
    // </body>
[/code]



**6.repalceChild()方法**

**replaceChild()方法可以把节点替换成指定的节点。参数第一个是创建节点的变量，第二个是目标节点，注意：替换节点会覆盖节点里的文本**

**使用方式：**

**目标节点.父节点. **replaceChild( **创建节点的变量, **目标节点**** )****

[code]

    //<div id="box" title="标题"></div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box'); //通过ID获取到目标节点
        var chj = document.createElement('p');  //创建一个新元素节点
        //通过目标节点，找到父节点，然后替换节点，参数第一个是创建节点变量，第二个是目标节点变量
        asf.parentNode.replaceChild(chj,asf);  //replaceChild()方法可以把节点替换成指定的节点。
    };
    // <body>
    //     <p></p>
    // </body>
[/code]



**7.cloneNode()方法**

**cloneNode()方法可以把子节点复制出来。也就是克隆子节点，参数** **true表示复制元素节点包含元素节点里的文本，**
**false表示只复制元素节点不包含元素节点里的文本**

**使用方式：**

**目标节点的父节点.获取到目标节点. **cloneNode(**** **true** ** **)****

****复制节点后可以赋值给一个变量，然后添加到一个节点****

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box'); //通过ID获取到目标节点的父节点,我们要复制这个节点里的子节点
        //将父节点传入hul函数去除里面的空白文本子节点，然后获取到第一个子节点,cloneNode(true)复制节点
        var fzh = hul(asf).firstChild.cloneNode(true);
        //在父节点上，将复制的子节点，添加到子节点列表末尾
        asf.appendChild(fzh);        //添加到子节点列表末尾
    
    };
    
    //创建删除空文本节点函数
    function hul(jh) {
        for (var i = 0; i < jh.childNodes.length; i ++){              //根据子节点集合长度循环次数
            //判断如果循环到的子节点类型是文本节点类型，并且子节点文本类容是空白类容
            if(jh.childNodes[i].nodeType === 3 && /^\s+$/.test(jh.childNodes[i].nodeValue)){
                //得到空白节点之后从当前节点，获取到父节点上，在父节点删除子节点
                jh.childNodes[i].parentNode.removeChild(jh.childNodes[i]);
            }
        }
        return jh; //最后返回删除后的节点集合
    }
    //可以看到已经把第一个子节点复制添加到了子节点列表的末尾
    // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    //     <p>测试1</p>
    // </div>
[/code]



**8.removeChild()方法**

**removeChild()删除指定节点，参数是要删除的目标节点**

**使用方式：**

**目标节点的父节点. **removeChild(目标节点)****

[code]

     // <div id="box" title="标题">
    //     <p>测试1</p>
    //     <p>测试2</p>
    // </div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box'); //通过ID获取到目标节点的父节点,我们要删除第一个子节点
        //将父节点传入函数删除里面的空白文本子节点，然后在父节点删除目标节，参数是目标节点
        hul(asf).removeChild(asf.firstChild);
    };
    
    //创建删除空文本节点函数
    function hul(jh) {
        for (var i = 0; i < jh.childNodes.length; i ++){              //根据子节点集合长度循环次数
            //判断如果循环到的子节点类型是文本节点类型，并且子节点文本类容是空白类容
            if(jh.childNodes[i].nodeType === 3 && /^\s+$/.test(jh.childNodes[i].nodeValue)){
                //得到空白节点之后从当前节点，获取到父节点上，在父节点删除子节点
                jh.childNodes[i].parentNode.removeChild(jh.childNodes[i]);
            }
        }
        return jh; //最后返回删除后的节点集合
    }
    // <div id="box" title="标题">
    //     <p>测试2</p>
    // </div>
[/code]



