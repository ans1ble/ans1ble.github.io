
---
layout: post
title: " 第一百一十六节，JavaScript，DOM操作样式 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，DOM操作样式**



**一．** **操作样式**

**CSS作为(X)HTML的辅助，可以增强页面的显示效果。但不是每个浏览器都能支持最新的CSS能力。CSS的能力和DOM级别密切相关，所以我们有必要检测当前浏览器支持CSS能力的级别。**

**DOM1级实现了最基本的文档处理，DOM2和DOM3在这个基础上增加了更多的交互能力，这里我们主要探讨CSS，DOM2增加了CSS编程访问方式和改变CSS样式信息。**

**DOM一致性检测**

**功能**

|

**版本号**

|

**说明**  
  
---|---|---  
  
**Core**

|

**1.0、2.0、3.0**

|

**基本的DOM,用于表现文档节点树**  
  
**XML**

|

**1.0、2.0、3.0**

|

**Core的XML扩展，添加了对CDATA等支持**  
  
**HTML**

|

**1.0、2.0**

|

**XML的HTML扩展，添加了对HTML特有元素支持**  
  
**Views**

|

**2.0**

|

**基于某些样式完成文档的格式化**  
  
**StyleSheets**

|

**2.0**

|

**将样式表关联到文档**  
  
**CSS**

|

**2.0**

|

**对层叠样式表1级的支持**  
  
**CSS2**

|

**2.0**

|

**对层叠样式表2级的支持**  
  
**Events**

|

**2.0**

|

**常规的DOM事件**  
  
**UIEvents**

|

**2.0**

|

**用户界面事件**  
  
**MouseEvents**

|

**2.0**

|

**由鼠标引发的事件(如：click)**  
  
**MutationEvents**

|

**2.0**

|

**DOM树变化时引发的事件**  
  
**HTMLEvents**

|

**2.0**

|

**HTML4.01事件**  
  
**Range**

|

**2.0**

|

**用于操作DOM树中某个范围的对象和方法**  
  
**Traversal**

|

**2.0**

|

**遍历DOM树的方法**  
  
**LS**

|

**3.0**

|

**文件与DOM树之间的同步加载和保存**  
  
**LS-Async**

|

**3.0**

|

**文件与DOM树之间的异步加载和保存**  
  
**Valuidation**

|

**3.0**

|

**在确保有效的前提下修改DOM树的方法**  
  


**implementation对象的hasFeature()方法**

  
**hasFeature()方法检测浏览器是否支持DOM1级CSS能力或DOM2级CSS能力，参数第一个css级别，参数二css版本，返回布尔值，IE上不精确**  
 **使用方式：**  
 **document.implementation.hasFeature('css级别', 'css版本')**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //检测浏览器是否支持DOM1级CSS能力或DOM2级CSS能力
        alert('DOM1级CSS能力：' + document.implementation.hasFeature('CSS', '2.0'));
        alert('DOM2级CSS能力：' + document.implementation.hasFeature('CSS2', '2.0'));
    };
[/code]

**PS：这种检测方案在IE浏览器上不精确，IE6中，hasFeature()方法只为HTML和版本1.0返回true，其他所有功能均返回false。但IE浏览器还是支持最常用的CSS2模块。**



**1.访问元素的样式,获取行内样式**

****CSS属性及JavaScript调用****

**任何HTML元素标签都会有一个通用的属性：style。它会返回CSSStypeDeclaration对象。下面我们看几个最常见的行内style样式的访问方式。**

**CSS属性及JavaScript调用**

**CSS属性**

|

**JavaScript调用**  
  
---|---  
  
**color**

|

**style.color**  
  
**font-size**

|

**style.fontSize**  
  
**float**

|

**非IE：style.cssFloat**  
  
**float**

|

**IE：style.styleFloat**  
  


**style属性，获取元素节点的行内style样式，也就是行内css样式，返回样式的集合**

**style属性，获取到样式集合后，可以使用样式属性名称获取或设置属性值**  
 **使用方式：**  
 **目标节点.style**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        alert(yshi.style); //style属性，获取元素节点的行内style样式，也就是行内css样式，返回样式的集合
        //返回：[object CSS2Properties] 样式集合
    
        //通过样式属性名称，获取属性值
        alert(yshi.style.color);  //查看color颜色属性值
        //返回;rgb(255, 34, 23) 浏览器计算过的颜色属性值
    
        alert(yshi.style.background); //查看背景颜色属性值
        //返回;#fff137   浏览器计算过的颜色属性值
    
        alert(yshi.style.fontSize);  //查看字体大小属性值
        //注意：属性名称单词如果是两段或者三段的，如：font-size，在写属性名称时将(-)分隔符去掉，分隔符后面的第一个字母大写，如：fontSize
        //返回：20px
    
        //alert(yshi.style.float);  //查看浮动属性值，
        //注意：float 是js的保留字，如果遇到关键字或保留字，在属性名称前加小写的css,然后将属性名称第一个字母大写，如下
        //alert(yshi.style.cssFloat); //查看浮动属性值，
        //但是cssFloat    IE浏览器不支持，IE可以将前面的css换成style，如：styleFloat
        //alert(yshi.style.styleFloat);
        //但是styleFloat   除了IE外其他浏览器也不支持
        //所以我们需要做一个兼容
        //做一个逻辑或，第一个不支持，就会用第二个
        alert(yshi.style.cssFloat || yshi.style.styleFloat);    //非IE用cssFloat，IE用styleFloat
        
    };
[/code]

**以上取值方式也可以赋值，最后一种赋值可以如下：**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //三元运算，判断如果浏览器支持cssFloat就用cssFloat，如果不支持就用styleFloat
        typeof yshi.style.cssFloat != 'undefined' ? yshi.style.cssFloat = 'right' : yshi.style.styleFloat = 'right';
    };
[/code]



**DOM2级样式规范为style定义了一些属性和方法**



**DOM2级样式规范为style定义了一些属性和方法**

**属性或方法**

|

**说明**  
  
---|---  
  
**cssText**

|

**访问或设置style中的CSS代码**  
  
**length**

|

**CSS属性的数量**  
  
**parentRule**

|

**CSS信息的CSSRule对象**  
  
**getPropertyCSSValue(name)**

|

**返回包含给定属性值的CSSValue对象**  
  
**getPropertyPriority(name)**

|

**如果设置了!important，则返回，否则返回空字符串**  
  
**item(index)**

|

**返回指定位置CSS属性名称**  
  
**removeProperty(name)**

|

**从样式中删除指定属性**  
  
**setProperty(name,v,p)**

|

**给属性设置为相应的值，并加上优先权**  
  
** **



**cssText属性，获取行内style样式里的所有css代码**  
 **使用方式：**  
 **目标节点.style.cssText**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //cssText属性，获取行内style样式里的所以css代码
        alert(yshi.style.cssText); //获取行内style样式里的所以css代码
        //返回;color: rgb(255, 34, 23); background: rgb(255, 241, 55) none repeat scroll 0% 0%; font-size: 20px; float: right;
    };
[/code]

**length属性，获取行内style样式里的属性长度，也就是有多少个样式，IE不支持**  
 **使用方式：**  
 **目标节点.style.length**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //length属性，获取行内style样式里的属性长度，也就是有多少个样式，IE不支持
        alert(yshi.style.length); //获取行内style样式里的属性长度
        //返回：12  不是很准确，没什么用
    };
[/code]

**removeProperty()方法，移除行内style样式里的某个css属性，参数是要移除的样式属性名称，IE不支持**  
 **使用方式：**  
 **目标节点.style.removeProperty(' ** **要移除的样式属性名称**** ')**

[code]

    //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //removeProperty()方法，移除行内style样式里的css属性，参数是要移除的样式属性名称，IE不支持
        yshi.style.removeProperty('color'); //移除行内style样式里的css属性
    };
[/code]

**setProperty()方法，设置行内style样式里的某个css属性，参数一属性名称，参数二属性值，IE不支持**  
 **使用方式：**  
 **目标节点.style.removeProperty('属性名称','属性值')**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //setProperty()方法，设置行内style样式里的某个css属性，参数一属性名称，参数二属性值，IE不支持
        yshi.style.setProperty('color','#0078D7'); //设置行内style样式里的某个css属性
    };
[/code]

**PS：Firefox、Safari、Opera9+、Chrome支持这些属性和方法。IE只支持cssText，而getPropertyCSSValue()方法只有Safari3+和Chrome支持。**

**PS：style属性仅仅只能获取行内的CSS样式，对于另外两种形式内联 <style>和链接<link>方式则无法获取到。**



**获取浏览器计算后的样式，缺点不能赋值**

**虽然可以通过style来获取单一值的CSS样式，但对于复合值的样式信息，就需要通过计算样式来获取。DOM2级样式，window对象下提供了getComputedStyle()方法。接受两个参数，需要计算的样式元素，第二个伪类(:hover)，如果没有没有伪类，就填null。**

**getComputedStyle()方法方法，获取浏览器计算后的样式(设置样式和默认样式)，接受两个参数，第一个目标元素节点，第二个伪类(:hover)也就是如果是a标签，如果没有没有伪类，就填null。返回浏览器计算后的样式对象.IE不支持**  
 **使用方式：**  
 **window.getComputedStyle(目标元素节点,伪类或null)**

**获取到浏览器计算后的样式对象后同样可以通过样式属性名称来获取属性值**

**获取样式属性值时的注意事项**  
 **注意：属性名称单词如果是两段或者三段的，如：font-size，在写属性名称时将(-)分隔符去掉，分隔符后面的第一个字母大写，如：fontSize**  
 **注意：float 是js的保留字，如果遇到关键字或保留字，在属性名称前加小写的css,然后将属性名称第一个字母大写，如：cssFloat**  
 **但是cssFloat IE浏览器不支持，IE可以将前面的css换成style，如：styleFloat**  
 **但是styleFloat 除了IE外其他浏览器也不支持**  
 **所以关键字保留字需要结合两种做兼容**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //getComputedStyle()方法方法，获取浏览器计算后的样式(设置样式和默认样式)，接受两个参数，第一个目标元素节点，第二个伪类(:hover)也就是如果是a标签，如果没有没有伪类，就填null。
        var style = window.getComputedStyle(yshi,null);  //获取浏览器计算后的样式(设置样式和默认样式)
        alert(style);  //查看浏览器计算后的样式对象
        //返回;[object CSS2Properties]
        alert(style.alignSelf);  //同样可以通过属性名称来获取或设置值
    };
[/code]



**getComputedStyle()方法，IE不支持，但有个类似的属性可以使用currentStyle属性**

**currentStyle属性，获取ie浏览器计算后的样式(设置样式和默认样式)，返回浏览器计算后的样式对象**  
 **使用方式：**  
 **目标元素节点.currentStyle**  
 **得到计算后的样式对象后可以通过样式属性名称来获取值**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        //currentStyle属性，获取ie浏览器计算后的样式(设置样式和默认样式)，返回浏览器计算后的样式对象
        var style = yshi.currentStyle;  //获取ie浏览器计算后的样式
        alert(style); //查看返回对
        //通过样式属性名称来获取值
        alert(style .color);
    };
[/code]

**用currentStyle，结合getComputedStyle()方法做一个兼容**

[code]

     //<div id="box" style="color: #ff2217; background: #fff137; font-size: 20px; float: right;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
    
        //用currentStyle，结合getComputedStyle()方法做一个兼容
        var style = window.getComputedStyle ? window.getComputedStyle(yshi, null) : null || yshi.currentStyle;
        alert(style .color);                            //颜色在不同的浏览器会有rgb()格式
        alert(style .border);                            //不同浏览器不同的结果
        alert(style .fontFamily);                        //计算显示复合的样式值
        alert(style.style.fontFamily);                    //空
    };
[/code]

**PS：border属性是一个综合属性，所以他在Chrome显示了，Firefox为空，IE为undefined。所谓综合性属性，就是XHTML课程里所的简写形式，所以，DOM在获取CSS的时候，最好采用完整写法兼容性最好，比如：border-
top-color之类的。**

**注意：采用计算后的样式获取，不仅仅可以获取浏览器默认样式，还可以获取行内样式、内联和连接样式，因为不管你在哪里设置的css样式，最终会驻留在浏览器的计算样式里**



**2.操作样式表，内联样式和连接样式**

****内联样式和连接样式，** 通过id和class调用是最常用的方法。 **我们可以通过改变id或者 **class的值类改变样式******

****通过改变id的值类改变样式**  
**

**【不推荐】把ID改变会带来灾难性的问题，比如id还关联着js，改变id后就不关联了**

[code]

     //<div id="box1">测试1</div>
    
    // #box1{
    //     color: #ff3226; 红色
    // }
    // #box2{
    //     color: #33ff38; 绿色
    // }
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box1');  //通过ID获取到目标节点
        //目前是红色
        //通过改变id的值类改变样式
        yshi.id = 'box2';
        //改变id后就是绿色了
    };
[/code]



**className属性，获取或改变元素节点的class值**

****通过改变class的值类改变样式****

****使用方式：****

****元素节点. **className******

[code]

     //<div id="box1">测试1</div>
    
    // .box1{
    //     color: #ff3226; 红色
    // }
    // .box2{
    //     color: #33ff38; 绿色
    // }
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box1');  //通过ID获取到目标节点
        //目前是红色
        //className属性，获取或改变元素节点的class值
        yshi.className = 'box2';
        //改变class值后就是绿色了
    };
[/code]

**在添加className的时候，我们想给一个元素添加多个class多个值，或者多个值里删除一个值都是需要重写
**className的，为了方便，我们需要自定义能够给 **class追加值，和删除值的函数******



******自定义 ** ** **class值的操作函数【推荐】************

[code]

     //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var yshi = document.getElementById('box');  //通过ID获取到目标节点
        addClass(yshi,'box2');  //添加class属性值
        addClass(yshi,'box3');  //添加class属性值
        removeClass(yshi,'box2');  //删除一个class属性值
    
    
        //判断一个class属性值是否存在函数
        function hasClass(element, className) {  //接收两个参数，第一个目标元素节点，第二个要判断的class属性值
            //通过正则查找函数接收class属性值.如果在元素节点class属性值里存在返回true,反之返回false
            return !!element.className.match(new RegExp('(\\s|^)'+className+'(\\s|$)'));
        }
    
    
        //添加一个class属性值函数
        //给class属性添加一个属性值，如果不存在就添加，如果存在不做任何动作
        function addClass(element, className) {   //接收两个参数，第一个目标元素节点，第二个要添加的class属性值
            //将接收到的两个参数传入判断函数里，判断要添加的class属性值是否存在
            if (!hasClass(element, className)) {
                //不存在就添加此class属性值
                element.className += " " + className;
            }
        }
    
    
        //删除一个class属性值函数
        //给class属性删除一个属性值，如果存在就删除，如果不存在不做任何动作
        function removeClass(element, className) {   //接收两个参数，第一个目标元素节点，第二个要删除的class属性值
            //将接收到的两个参数传入判断函数里，判断要删除的class属性值是否存在
            if (hasClass(element, className)) {
                //如果存在通过正则匹配到此属性值，替换成一个空格
                element.className = element.className.replace(new RegExp('(\\s|^)'+className+'(\\s|$)'),' ');
            }
        }
    
    };
[/code]



**获取内联样式和连接样式**

**查看是否支持DOM2级样式表，IE异常，但也是支持 **DOM2级样式表的****

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        alert(document.implementation.hasFeature('StyleSheets', '2.0')); //查看是否支持DOM2级样式表
        //返回布尔值
    };
[/code]

**操作样式表，首先获取到样式表标签，连接样式获取到 <link>节点，内联样式获取到<style>标签节点**

[code]

    //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //连接样式
        var link = document.getElementsByTagName('link'); //连接样式获取到<link>节点
        alert(link);  //返回包含所有link标签的数组
        //返回：[object HTMLCollection]  包含所有link标签的数组
        alert(link[0]); //获取第一个link标签
        //返回：[object HTMLLinkElement]  第一个link标签对象
    
        //内联样式
        var style = document.getElementsByTagName('style');  //内联样式获取到<style>节点
        alert(style);  //返回包含所有<style>标签的数组
        alert(style[0]); //获取第一个style标签
    
    };
[/code]



**sheet属性,得到样式标签里的css样式表对象,非IE支持**  
 **使用方式：**  
 **样式标签节点.sheet**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //连接样式
        var link = document.getElementsByTagName('link')[0]; //连接样式获取到<link>节点
        alert(link.sheet);   //sheet属性,得到样式标签里的css样式表对象
        //返回;[object CSSStyleSheet]
    };
[/code]

**styleSheet属性,得到样式标签里的css样式表对象,只支持IE， **styleSheet还有别的获取
**css样式表对象方式，而且都兼容，下面会说到******  
 **使用方式：**  
 **样式标签节点.styleSheet**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //连接样式
        var link = document.getElementsByTagName('link')[0]; //连接样式获取到<link>节点
        alert(link.styleSheet);   //styleSheet属性,得到样式标签里的css样式表对象,只支持IE
        //返回;[object CSSStyleSheet]
    };
[/code]

**结合上面两者情况做一个兼容**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //连接样式
        var link = document.getElementsByTagName('link')[0]; //连接样式获取到<link>节点
        //如果sheet执行不成功，就执行styleSheet
        var sheet = link.sheet || link.styleSheet;  //做一个兼容
        alert(sheet); //返回:css样式表对象
    };
[/code]



**styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】，所有浏览器兼容**  
 **使用方式：不需要获取样式标签节点就能直接获取到样式表对象**  
 **document.styleSheets**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets; //获取样式表对象集合
        alert(style.length); //查看样式表集合长度，也就是有几个样式表
        //返回：1 说明只有一个样式表
    };
[/code]



**样式表对象的属性和方法**

**属性或方法**

|

**说明**  
  
---|---  
  
**disabled**

|

**获取和设置样式表是否被禁用**  
  
**href**

|

**如果是通过 <link>包含的，则样式表为URL，否则为null**  
  
**media**

|

**样式表支持的所有媒体类型的集合**  
  
**ownerNode**

|

**指向拥有当前样式表节点的指针**  
  
**parentStyleSheet**

|

**@import导入的情况下，得到父CSS对象**  
  
**title**

|

**ownerNode中title属性的值**  
  
**type**

|

**样式表类型字符串**  
  
**cssRules**

|

**样式表包含样式规则的集合，IE不支持**  
  
**ownerRule**

|

**@import导入的情况下，指向表示导入的规则，IE不支持**  
  
**deleteRule(index)**

|

**删除cssRules集合中指定位置的规则，IE不支持**  
  
**insertRule(rule, index)**

|

**向cssRules集合中指定位置插入rule字符串，IE不支持**  
  
**样式表对象的属性和方法，首先要获取到样式表对象后使用**



**disabled属性，获取和设置样式表是否被禁用，false没有禁用，true被禁用**  
 **使用方式：**  
 **样式表对象.disabled**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
        alert(style.disabled); //disabled属性，获取和设置样式表是否被禁用，false没有禁用，true被禁用
        //返回：false
        style.disabled = true;  //设置样式表禁用
        alert(style.disabled);
    };
[/code]

**href属性，如果是通过 <link>包含的，获取样式表的URL，否则为null**  
 **使用方式：**  
 **样式表对象.href**

[code]

     //<link rel="stylesheet" type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //href属性，如果是通过<link>包含的，获取样式表的URL，否则为null
        alert(style.href);
        //返回：http://localhost:63342/js/1.css
    
    };
[/code]

**media属性，获取样式表支持的所有媒体类型的集合，也就是 <link
media='xxx'>获取link标签里的media属性，返回集合，支持度不好**  
 **使用方式：**  
 **样式表对象.media**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //media属性，获取样式表支持的所有媒体类型的集合，也就是<link media='xxx'>获取link标签里的media属性,返回集合
        alert(style.media);
        alert(style.media[0]);    //第一个media的值
    
    };
[/code]

**title属性，获取样式表连接的title，也就是 <link title='xxx'>获取link标签里的title属性值，**  
 **使用方式：**  
 **样式表对象.title**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //title属性，获取样式表连接的title，也就是<link title='xxx'>获取link标签里的title属性值，
        alert(style.title);
        //返回;xxx
    };
[/code]

**cssRules属性，获取样式表规则集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合,IE9以下不支持**  
 **使用方式：**  
 **样式表对象.cssRules**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //cssRules属性，获取样式表规则集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合
        alert(style.cssRules);
        //返回;[object CSSRuleList]  代码块集合
        alert(style.cssRules[0]); //获取第一个代码块，也就是第一个选择器
        //返回：[object CSSStyleRule]   第一个选择器对象
    
        //cssText属性可以获取到对象选择器里的样式代码，IE9以下不支持
        alert(style.cssRules[0].cssText);
        //返回：.box1 { color: rgb(255, 50, 38); }
    
        //selectorText属性可以获取到对象选择器的名称，也就是选择符，IE9以下不支持
        alert(style.cssRules[0].selectorText);
        //返回：.box1
    };
[/code]

**deleteRule()方法，删除样式表对象里的指定代码块，也就是选择器，参数是要删除第几个选择器， **IE9以下不支持****  
 **使用方式：**  
 **样式表对象.deleteRule(删除第几个选择器)**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //deleteRule()方法，删除样式表对象里的指定代码块，也就是选择器，参数是要删除第几个选择器
        style.deleteRule(0); //删除样式表对象里的第一个选择器
    };
[/code]

**insertRule()方法，向样式表对象里添加一条规则，也就是添加一个选择器，两个参数，第一个要添加的选择器、名称{加样式}，第二个参数要添加的位置，
** **IE9以下不支持******  
 **使用方式：**  
 **样式表对象.insertRule('选择器名称{加样式}',添加的位置)**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //insertRule()方法，向样式表对象里添加一条规则，也就是添加一个选择器，两个参数，第一个要添加的选择器、名称{加样式}，第二个参数要添加的位置
        style.insertRule(".box3{color: #33ff38}",0); //向样式表对象里添加一条规则
    };
[/code]



**注意：以上讲到的IE9以下不支持，IE有替代**

**PS：除了几个不用和IE不支持的我们忽略了，还有三个有IE对应的另一种方式：支持IE的**

**rules属性，IE用于替代cssRules属性，获取样式表规则集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合，非IE不支持**  
 **使用方式：**  
 **样式表对象.rules**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //rules属性，IE用于替代cssRules属性，获取样式表规则集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合，非IE不支持
        alert(style.rules);  //获取css选择器集合
    };
[/code]

**removeRule()方法，IE用于替代deleteRule()方法，删除样式表对象里的指定代码块，也就是选择器，参数是要删除第几个选择器，非IE不支持**  
 **使用方式：**  
 **样式表对象.removeRule(要删除第几个选择器)**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //removeRule()方法，IE用于替代deleteRule()方法，删除样式表对象里的指定代码块，也就是选择器，参数是要删除第几个选择器，非IE不支持
        style.removeRule(0);  //删除指定选择器
    };
[/code]

**addRule()方法，IE用于替代insertRule()方法，向样式表对象里添加一条规则，也就是添加一个选择器，3个参数，第一个选择器名称，第二个样式，第三要添加的个位置，非IE不支持**  
 **使用方式：**  
 **样式表对象.addRule("选择器名称","样式",要添加的个位置)**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //addRule()方法，IE用于替代insertRule()方法，向样式表对象里添加一条规则，也就是添加一个选择器，3个参数，第一个选择器名称，第二个样式，第三要添加的个位置，非IE不支持
        style.addRule(".box3","background-color: #33ff38",0);  //向样式表对象里添加一条规则
    };
[/code]



**跨浏览器解决方案，【重点】**

**  跨浏览器兼容，删除一个样式表对象里的一条指定选择器**

[code]

    //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
        shchu(style,0)
    
        //跨浏览器兼容，删除一个样式表对象里的一条指定选择器
        function shchu(style,position) {  //接收两个参数，第一个样式表对象，第二个要删除第几个选择器
            //判断deleteRule()方法，删除样式表对象里的指定代码块，如果为真，说明浏览器支持deleteRule()
            if(style.deleteRule){
                style.deleteRule(position);   //删除指定的选择器
            }else if(style.removeRule){      //判断removeRule()方法，删除样式表对象里的指定代码块，如果为真，说明浏览器支持removeRule()
                style.removeRule(position);   //删除指定的选择器
            }
        }
    };
[/code]

**跨浏览器兼容，添加一个样式表对象里的一条指定选择器**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
        tianjia(style,'.box3','background-color: #2616ff;',2);
    
    
        //跨浏览器兼容，添加一个样式表对象里的一条指定选择器
        function tianjia(style,xzq,yshi,position) {  //接收4个参数，第一个是样式表对象，第二个是选择器名称，第三个是样式，第四个是要添加的位置
            //判断insertRule()方法，向样式表对象里添加一条规则，如果为真，说明浏览器支持
            if(style.insertRule){
                style.insertRule(xzq + '{' + yshi + '}',position);  //向样式表对象里添加一条规则
            }else if(style.addRule){   //判断addRule()方法，向样式表对象里添加一条规则，如果为真，说明浏览器支持
                style.addRule(xzq,yshi,position);  //向样式表对象里添加一条规则
            }
        }
    };
[/code]

**解决跨浏览器 **获取样式表里的css选择器集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合****

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //解决跨浏览器获取样式表里的css选择器集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合
        //如果浏览器执行cssRules不成功，就执行rules，来获取样式表对象里的选择器集合，得到的是选择器集合
        var rules = style.cssRules || style.rules;
        alert(rules);
    };
[/code]



**用以上方式获取到样式选择器后，可以通过选择器 **CSSStyleRule** 属性和方法来获取或者设置**



**CSSStyleRule可以使用的属性**

**属性**

|

**说明**  
  
---|---  
  
**cssText**

|

**获取当前整条规则对应的文本，IE不支持**  
  
**parentRule**

|

**@import导入的，返回规则或null，IE不支持**  
  
**parentStyleSheet**

|

**当前规则的样式表，IE不支持**  
  
**selectorText**

|

**获取当前规则的选择符文本**  
  
**style**

|

**返回CSSStyleDeclaration 对象，可以获取和设置样式**  
  
**type**

|

**表示规则的常量值，对于样式规则，值为1，IE不支持**  
  


**cssText属性，获取当前css选择器样式文本**  
 **使用方式：**  
 **css选择器对象.cssText**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //解决跨浏览器获取样式表里的css选择器集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合
        //如果浏览器执行cssRules不成功，就执行rules，来获取样式表对象里的选择器集合，得到的是选择器集合
        var rules = style.cssRules || style.rules;
        alert(rules[1].cssText);   //cssText属性，获取当前css选择器样式文本
        //返回;.box2 { color: rgb(51, 255, 56); }
    };
[/code]

**selectorText属性，获取当前css选择器名称**  
 **使用方式：**  
 **css选择器对象.selectorText**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //解决跨浏览器获取样式表里的css选择器集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合
        //如果浏览器执行cssRules不成功，就执行rules，来获取样式表对象里的选择器集合，得到的是选择器集合
        var rules = style.cssRules || style.rules;
        alert(rules[1].selectorText);   //selectorText属性，获取当前css选择器名称
        //返回;.box2
    };
[/code]

**style属性，获取或设置当前css选择器里指定样式的值，后面跟要获取或设置的样式名称**  
 **使用方式：**  
 **css选择器对象.style.color**

[code]

     //<link rel="stylesheet" title='xxx' type="text/css" href="1.css">
    
    // @charset "utf-8";
    // .box1{
    //     color: #ff3226;
    // }
    // .box2{
    //     color: #33ff38;
    // }
    
    //<div id="box" class="box1">测试1</div>
    
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //styleSheet属性,直接获取css样式表对象，有几个样式表就能获取到几个样式表对象，返回集合，既可以获取到内联样式又可以获取到连接样式【推荐】
        var style = document.styleSheets[0]; //获取样式表对象集合里的第一个样式表对象
    
        //解决跨浏览器获取样式表里的css选择器集合，也就是css代码块的集合，代码块就是一个选择器，要可以理解为css选择器集合
        //如果浏览器执行cssRules不成功，就执行rules，来获取样式表对象里的选择器集合，得到的是选择器集合
        var rules = style.cssRules || style.rules;
        alert(rules[0].style.color);   //style属性，获取或设置当前css选择器里指定样式的值，后面跟要获取或设置的样式名称
        //返回;rgb(51, 255, 56)
        rules[0].style.color = '#33ff38';  //重新设置color值
    };
[/code]

**PS：Chrome浏览器在本地运行时会出现问题，rules会变成null，只要把它放到服务器上允许即可正常。**



**总结：三种操作CSS的方法，第一种style行内，可读可写；第二种行内、内联和链接浏览器计算过后的样式，使用getComputedStyle或currentStyle，可读不可写；第三种cssRules或rules，内联和链接可读可写。**





