---
layout: post
title: " 第一百二十节，JavaScript事件对象 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript事件对象**





**学习要点：**

**1.事件对象**

**2.鼠标事件**

**3.键盘事件**

**4.W3C与IE**



**JavaScript事件的一个重要方面是它们拥有一些相对一致的特点，可以给你的开发提供更多的强大功能。最方便和强大的就是事件对象，他们可以帮你处理鼠标事件和键盘敲击方面的情况，此外还可以修改一般事件的捕获/冒泡流的函数。**



**一．** **事件对象**

**事件处理函数的一个标准特性是，以某些方式访问的事件对象包含有关于当前事件的上下文信息。**

**事件处理三部分组成：对象.事件处理函数=函数。例如：单击文档任意处。**

[code]

     //在页面任意地方单击鼠标触发事件
    document.onclick = function () {
        alert('Lee');
    };
[/code]

**PS：以上程序的名词解释：click表示一个事件类型，单击。onclick表示一个事件处理函数或绑定对象的属性(或者叫事件监听器、侦听器)。document表示一个绑定的对象，用于触发某个元素区域。function()匿名函数是被执行的函数，用于触发后执行。**



**除了用匿名函数的方法作为被执行的函数，也可以设置成独立的函数。**

[code]

     //在页面任意地方单击鼠标触发事件
    document.onclick = box;                        //直接赋值函数名即可，无须括号
    function box() {
        alert('Lee');
    }
[/code]



**this关键字和上下文**

**在面向对象那章我们了解到：在一个对象里，由于作用域的关系，this代表着离它最近对象。**

**这里的 **this代表的input元素对象，因为 ** **input元素对象被onclick绑定了********

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        input.onclick = function () {
            alert(this.value);                    //HTMLInputElement，this表示input对象
        };
    };
[/code]

**从上面的拆分，我们并没有发现本章的重点：事件对象。那么事件对象是什么？它在哪里呢？当触发某个事件时，会产生一个事件对象，这个对象包含着所有与事件有关的信息。包括导致事件的元素、事件的类型、以及其它与特定事件相关的信息。**



**事件对象**

**事件对象，我们一般称作为event对象，这个对象是浏览器通过函数把这个对象作为参数传递过来的。那么首先，我们就必须验证一下，在执行函数中没有传递参数，是否可以得到隐藏的参数。**

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        box();
    
        function box() {                            //普通空参函数
            alert(arguments.length);                    //0，没有得到任何传递的参数
        }
    
        input.onclick = function () {                    //事件绑定的执行函数
            alert(arguments.length);                    //1，得到一个隐藏参数
        };
    };
[/code]



**event对象。**

****这个对象包含着所有与事件有关的信息。包括导致事件的元素、事件的类型、以及其它与特定事件相关的信息。****

**通过上面两组函数中，我们发现，通过事件绑定的执行函数是可以得到一个隐藏参数的。说明，浏览器会自动分配一个参数，这个参数其实就是event对象。**

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        input.onclick = function () {
            alert(arguments[0]);                    //MouseEvent，鼠标事件对象
        };
    };
[/code]

**事件执行的函数，可以设置一个形式参数，这个形式参数接收到的是 **浏览器传过来的
**event对象，也就是MouseEvent，鼠标事件对象******

**上面这种做法比较累，那么比较简单的做法是，直接通过接收参数来得到即可**

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        input.onclick = function (evt) {                //接受event对象，名称不一定非要event
            alert(evt);                                //MouseEvent，鼠标事件对象
        };
    };
[/code]

**直接接收event对象，是W3C的做法，IE不支持，IE自己定义了一个event对象，直接在window.event获取即可。**

**兼容版本**

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        input.onclick = function (evt) {
            var e = evt || window.event;                //实现跨浏览器兼容获取event对象
            alert(e);
        };
    };
[/code]



**二．** **鼠标事件**

**鼠标事件是Web上面最常用的一类事件，毕竟鼠标还是最主要的定位设备。那么通过事件对象可以获取到鼠标按钮信息和屏幕坐标获取等。**

**1.鼠标按钮**

**只有在主鼠标按钮被单击时(常规一般是鼠标左键)才会触发click事件，因此检测按钮的信息并不是必要的。但对于onmousedown和onmouseup事件来说，则在其event对象存在一个button属性，表示按下或释放按钮。**



**button属性，返回鼠标信息的数值**  
 **使用方式：**  
 **event对象.button**

[code]

     //<input type="text" value="文本"/>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var input = document.getElementsByTagName('input')[0];
        input.onmouseup = function (evt) {     //当鼠标释放时
            var e = evt || window.event;                //实现跨浏览器兼容获取event对象
            alert(e.button);   //button属性，返回鼠标信息的数值
            //点击右鼠标返回0
            //中鼠标返回1
            //左鼠标返回2
            //注意：但是IE返回不一样，IE有自己的数值
        };
    };
[/code]



**非IE(W3C)中的button属性**

**值**

|

**说明**  
  
---|---  
  
**0**

|

**表示主鼠标按钮(常规一般是鼠标左键)**  
  
**1**

|

**表示中间的鼠标按钮(鼠标滚轮按钮)**  
  
**2**

|

**表示次鼠标按钮(常规一般是鼠标右键)**  
  


**IE中的button属性**

**值**

|

**说明**  
  
---|---  
  
**0**

|

**表示没有按下按钮**  
  
**1**

|

**表示主鼠标按钮(常规一般是鼠标左键)**  
  
**2**

|

**表示次鼠标按钮(常规一般是鼠标右键)**  
  
**3**

|

**表示同时按下了主、次鼠标按钮**  
  
**4**

|

**表示按下了中间的鼠标按钮**  
  
**5**

|

**表示同时按下了主鼠标按钮和中间的鼠标按钮**  
  
**6**

|

**表示同时按下了次鼠标按钮和中间的鼠标按钮**  
  
**7**

|

**表示同时按下了三个鼠标按钮**  
  
** **

**PS：在绝大部分情况下，我们最多只使用主次中三个单击键，IE给出的其他组合键一般无法使用上。所以，我们只需要做上这三种兼容即可。**

****鼠标按钮信息兼容****

[code]

     //当用户在页面释放鼠标时，执行匿名函数
    document.onmouseup = function (evt) {  //设置一个参数接收浏览器传过来的event对象
        if (getButton(evt) == 0) {   //将接收到的对象传入getButton函数，判断返回0打印里面的字符串
            alert('按下了左键！');
        } else if (getButton(evt) == 1) {   //将接收到的对象传入getButton函数，判断返回1打印里面的字符串
            alert('按下了中键！');
        } else if (getButton(evt) == 2) {   //将接收到的对象传入getButton函数，判断返回2打印里面的字符串
            alert('按下了右键！');
        }
    };
    
    function getButton(evt) {    //跨浏览器左中右键单击相应，接收event对象
        //如果没有获取到event对象，说明是ie浏览器就用window.event获取
        var e = evt || window.event;
        if (evt) {        //如果event对象为真，
            return e.button;         //就返回鼠标对应的数值
        } else if (window.event) {  //判断如果ie方式返回真，就要做兼容，因为IE和w3c标准返回数值代表不同
            switch (e.button) {  //判断event对象返回值
                case 1 :         //如果IE方式返回值是1
                    return 0;    //返回w3c标准数值，使其统一
                case 4 :         //如果IE方式返回值是4
                    return 1;    //返回w3c标准数值，使其统一
                case 2 :         //如果IE方式返回值是2
                    return 2;    //返回w3c标准数值，使其统一
            }
        }
    }
[/code]



**2.可视区及屏幕坐标**

**事件对象提供了两组来获取浏览器坐标的属性，一组是页面可视区 **坐标** ，另一组是屏幕坐标。**



**坐标属性**

**属性**

|

**说明**  
  
---|---  
  
**clientX**

|

**可视区X坐标，距离左边框的位置**  
  
**clientY**

|

**可视区Y坐标，距离上边框的位置**  
  
**screenX**

|

**屏幕区X坐标，距离左屏幕的位置**  
  
**screenY**

|

**屏幕区Y坐标，距离上屏幕的位置**  
  


**clientX属性，可视区X坐标，距离左边框的位置**  
 **clientY **属性，** 可视区Y坐标，距离上边框的位置**  
 **screenX **属性，** 屏幕区X坐标，距离左屏幕的位置**  
 **screenY **属性，** 屏幕区Y坐标，距离上屏幕的位置**

**使用方式：**

****event对象. **clientX******

****其他相同****

[code]

     //当用户在页面任意地方点击鼠标，执行匿名函数
    document.onclick = function (evt) {  //接收一个event对象
        //如果无法接收event对象，说明是ie浏览器，就用ie方式获取event对象
        var e = evt || window.event;
        //打印clientX属性，可视区X坐标，距离左边框的位置加，clientY属性，可视区Y坐标，距离上边框的位置
        alert(e.clientX + ',' + e.clientY);
        //打印screenX属性，屏幕区X坐标，距离左屏幕的位置加，screenY属性，屏幕区Y坐标，距离上屏幕的位置
        alert(e.screenX + ',' + e.screenY);
    };
[/code]



**3.修改键**

**有时，我们需要通过键盘上的某些键来配合鼠标来触发一些特殊的事件。这些键为：Shfit、Ctrl、Alt和Meat(Windows中就是Windows键，苹果机中是Cmd键)，它们经常被用来修改鼠标事件和行为，所以叫修改键。**

**修改键属性**

**属性**

|

**说明**  
  
---|---  
  
**shiftKey**

|

**判断是否按下了Shfit键**  
  
**ctrlKey**

|

**判断是否按下了ctrlKey键**  
  
**altKey**

|

**判断是否按下了alt键**  
  
**metaKey**

|

**判断是否按下了windows键，IE不支持**  
  
**shiftKey判断是否按下了Shfit键**  
 **ctrlKey判断是否按下了ctrlKey键**  
 **altKey判断是否按下了alt键**  
 **metaKey判断是否按下了windows键，IE不支持**

**使用方式：**

****event对象. **shiftKey******

**其他相同**

[code]

     //当用户在页面任意地方点击是，执行匿名函数
    document.onclick = function (evt) {  //接收一个参数event对象
        alert(getKey(evt)); //执行函数打印，将event对象当做参数传入函数
    };
    
    function getKey(evt) {  //定义函数，接收event对象
        //如果浏览器不支持直接获取event对象，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        var keys = [];   //创建一个空数组
    
        if (e.shiftKey) keys.push('shift');      //判断如果用户按下了shift键，向数组里添加一个元素
        if (e.ctrlKey) keys.push('ctrl');    //判断如果用户按下了ctrl键，向数组里添加一个元素
        if (e.altKey) keys.push('alt');      //判断如果用户按下了alt键，向数组里添加一个元素
    
        return keys;  //返回数组
    }
[/code]



**三．** **键盘事件**

**用户在使用键盘时会触发键盘事件。“DOM2级事件”最初规定了键盘事件，结果又删除了相应的内容。最终还是使用最初的键盘事件，不过IE9已经率先支持“DOM3”级键盘事件。**

**1.键码**

**在发生onkeydown和onkeyup事件时，event对象的keyCode属性中会包含一个代码，与键盘上一个特定的键对应。对数字字母字符集，keyCode属性的值与ASCII码中对应小写字母或数字的编码相同。字母中大小写不影响。
也就是每一个键对应一个数字**

**keyCode属性，返回按键对应的按键码，注意：事件要是键盘事件如onkeydown**  
 **使用方式：**  
 **event对象.keyCode**

[code]

     //当用户按下任意键时，执行匿名函数
    document.onkeydown = function (evt) {  //接收event对象
        //如果无法直接获取event对象，说明是IE浏览器就用IE的方法window.event获取event对象
        var e = evt || window.event;
        alert(e.keyCode);     //打印按键对应的数字码
    };
[/code]

**不同的浏览器在onkeydown和onkeyup事件中，会有一些特殊的情况：**

**在Firefox和Opera中，分号键时keyCode值为59，也就是ASCII中分号的编码；而IE和Safari返回186，即键盘中按键的键码。**

**PS：其他一些特殊情况由于浏览器版本太老和市场份额太低，这里不做补充。**



**2.字符编码**

**Firefox、Chrome和Safari的event对象都支持一个charCode属性，这个属性只有在发生onkeypress事件时才包含值，而且这个值是按下的那个键所代表字符的ASCII编码。此时的keyCode属性通常等于0或者也可能等于所按键的编码。IE和Opera则是在keyCode属性中保存字符的ASCII编码。**

**charCode属性，字符键所代表字符的ASCII编码，注意：事件要是onkeypress键盘事件如onkeypress，**  
 **使用方式：**  
 **event对象.charCode**

[code]

     //当用户按下字符键时，执行匿名函数
    document.onkeypress = function (evt) {  //接收event对象
        //如果无法直接获取event对象，说明是IE浏览器就用IE的方法window.event获取event对象
        var e = evt || window.event;
        alert(e.charCode);     //打印字符键所代表字符的ASCII编码
    };
[/code]

**字符按键支持所有浏览器兼容**

[code]

    window.onload =  function () { //window.onload事件，等待html执行完成后，执行匿名函数
    //当用户按下字符键时，执行匿名函数
        document.onkeypress = function (evt) {  //接收event对象
            alert(getCharCode(evt));  //执行兼容函数
    
            function getCharCode(evt) {  //接收event对象
                //如果无法直接获取event对象，说明是IE浏览器，就用IE的window.event获取event对象
                var e = evt || window.event;
                //判断event对象的charCode属性如果是数字类型
                if (typeof e.charCode == 'number') {
                    //执行charCode属性
                    return e.charCode;
                } else {
                    //否则执行keyCode属性
                    return e.keyCode;
                }
            }
    
        };
    };
[/code]

**  可以使用String.fromCharCode()将ASCII编码转换成实际的字符。**

[code]

    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
    //当用户按下字符键时，执行匿名函数
        document.onkeypress = function (evt) {  //接收event对象
            alert(String.fromCharCode(getCharCode(evt)));  //将返回的ASCII编码转换成实际的字符
    
            function getCharCode(evt) {  //接收event对象
                //如果无法直接获取event对象，说明是IE浏览器，就用IE的window.event获取event对象
                var e = evt || window.event;
                //判断event对象的charCode属性如果是数字类型
                if (typeof e.charCode == 'number') {
                    //执行charCode属性
                    return e.charCode;
                } else {
                    //否则执行keyCode属性
                    return e.keyCode;
                }
            }
    
        };
    };
[/code]



**keyCode属性和charCode属性区别如下：比如当按下“a键（重视是小写的字母）时，**

**在Firefox中会获得**

**onkeydown： keyCode is 65   charCode is 0**

**onkeyup：       keyCode is 65 charCode is 0**

**onkeypress： keyCode is 0   charCode is 97**

** **

**在IE中会获得**

**onkeydown： keyCode is 65   charCode is undefined**

**onkeyup：    keyCode is 65  charCode is undefined**

**onkeypress： keyCode is 97   charCode is undefined**

** **

**而当按下shift键时，在Firefox中会获得**

**onkeydown：keyCode is 16   charCode is 0**

**onkeyup： keyCode is 16    charCode is 0**

** **

**在IE中会获得**

**onkeydown：keyCode is 16   charCode is undefined**

**onkeyup： keyCode is 16   charCode is undefined**

** **

**onkeypress：不会获得任何的charCode属性值，因为按shift并没输入任何的字符，并且也不会触发onkeypress事务**

** **

**PS：在onkeydown事务里面，事务包含了keyCode属性 – 用户按下的按键的物理编码。**

**在onkeypress里，keyCode属性包含了字符编码，即默示字符的ASCII码。如许的情势实用于所有的浏览器 –
除了火狐，它在onkeypress事务中的keyCode属性返回值为0。**



**四．** **W3C** **与IE**

**在标准的DOM事件中，event对象包含与创建它的特定事件有关的属性和方法。触发的事件类型不一样，可用的属性和方法也不一样。**



**W3C中event对象的属性和方法**

**属性/方法**

|

**类型**

|

**读/写**

|

**说明**  
  
---|---|---|---  
  
**bubbles**

|

**Boolean**

|

**只读**

|

**表明事件是否冒泡**  
  
**cancelable**

|

**Boolean**

|

**只读**

|

**表明是否可以取消事件的默认行为**  
  
**currentTarget**

|

**Element**

|

**只读**

|

**其事件处理程序当前正在处理事件的那个元素**  
  
**detail**

|

**Integer**

|

**只读**

|

**与事件相关的细节信息**  
  
**eventPhase**

|

**Integer**

|

**只读**

|

**调用事件处理程序的阶段：1表示捕获阶段，2表示“处理目标”，3表示冒泡阶段**  
  
**preventDefault()**

|

**Function**

|

**只读**

|

**取消事件的默认行为。如果cancelabel是true，则可以使用这个方法**  
  
**stopPropagation()**

|

**Function**

|

**只读**

|

**取消事件的进一步捕获或冒泡。如果bubbles为true，则可以使用这个方法**  
  
**target**

|

**Element**

|

**只读**

|

**事件的目标**  
  
**type**

|

**String**

|

**只读**

|

**被触发的事件的类型**  
  
**view**

|

**AbstractView**

|

**只读**

|

**与事件关联的抽象视图。等同于发生事件的window对象**  
  
** **

**IE中event对象的属性**

**属性**

|

**类型**

|

**读/写**

|

**说明**  
  
---|---|---|---  
  
**cancelBubble**

|

**Boolean**

|

**读/写**

|

**默认值为false，但将其设置为true就可以取消事件冒泡**  
  
**returnValue**

|

**Boolean**

|

**读/写**

|

**默认值为true，但将其设置为false就可以取消事件的默认行为**  
  
**srcElement**

|

**Element**

|

**只读**

|

**事件的目标**  
  
**type**

|

**String**

|

**只读**

|

**被触发的事件类型**  
  
** **

**在这里，我们只看所有浏览器都兼容的属性或方法，也就是按照IE的来做兼容，因为IE有的，w3c都有，w3c有的IE不一定有**

**首先第一个我们了解一下W3C中的target和IE中的srcElement，都表示事件的目标。**

**srcElement属性，是IE中event对象的属性，获取事件event对象的标签节点**  
 **target属性，是W3C中event对象的属性，获取事件event对象的标签节点**

**所以要做兼容**

[code]

     //当用户在页面任意地方单击鼠标时，激发匿名函数
    document.onclick = function (evt) {  //接收事件的event对象
        var target = getTarget(evt);   //将event对象传入函数执行自定义函数，将函数赋值给一个变量
        alert(target.tagName);   //打印event对象里获取到的元素标签名称
    };
    
    function getTarget(evt) {  //自定义函数
        //如果无法直接获取event对象，说明是IE浏览器，就用IE的window.event获取event对象
        var e = evt || window.event;
        //兼容方式获取到event对象事件的元素标签节点，也就是目标
        return e.target || e.srcElement;                
    }
[/code]

**  通过事件得到元素节点后，可以对元素进行读写等操作**



**事件流**

**事件流是描述的从页面接受事件的顺序，当几个都具有事件的元素层叠在一起的时候，那么你点击其中一个元素，并不是只有当前被点击的元素会触发事件，而层叠在你点击范围的所有元素都会触发事件。事件流包括两种模式：冒泡和捕获。**

**事件冒泡，是从里往外逐个触发。事件捕获，是从外往里逐个触发。那么现代的浏览器默认情况下都是冒泡模型，而捕获模式则是早期的Netscape默认情况
。而现在的浏览器要使用DOM2级模型的事件绑定机制才能手动定义事件流模式。 **事件流模式讲到 **事件绑定机制后在说******

******![](https://images2015.cnblogs.com/blog/955761/201612/955761-20161202080228724-1489888528.png)******

**  冒泡模式**

[code]

    // <body>
    // <div id="box" style="background-color: #ff0f20;width: 200px;height: 200px;">
    //     <input type="button" value="确定">
    // </div>
    // </body>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        document.onclick = function () {
            alert('我是document');
        };
        document.documentElement.onclick = function () {
            alert('我是html');
        };
        document.body.onclick = function () {
            alert('我是body');
        };
        document.getElementById('box').onclick = function () {
            alert('我是div');
        };
        document.getElementsByTagName('input')[0].onclick = function () {
            alert('我是input');
        };
    };
    //当点击一个元素时，会冒泡向外激发事件，也就是点击一个元素激发事件后会自动激发父元素的事件
[/code]



**cancelBubble属性，是IE中event对象的属性，默认值为false，但将其设置为true就可以取消事件冒泡**  
 **stopPropagation()方法，是W3C中event对象的方法，取消事件的进一步捕获或冒泡。**

**取消冒泡模式：要在哪个元素取消，就在哪个元素执行取消冒泡函数**

[code]

     // <body>
    // <div id="box" style="background-color: #ff0f20;width: 200px;height: 200px;">
    //     <input type="button" value="确定">
    // </div>
    // </body>
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        document.onclick = function () {
            alert('我是document');
        };
        document.documentElement.onclick = function () {
            alert('我是html');
        };
        document.body.onclick = function () {
            alert('我是body');
        };
        document.getElementById('box').onclick = function () {
            alert('我是div');
        };
        document.getElementsByTagName('input')[0].onclick = function (evt) {
            //执行取消冒泡函数
            stopPro(evt);  //将event对象传入函数
            alert('我是input');
        };
    };
    //当点击一个元素时，会冒泡向外激发事件，也就是点击一个元素激发事件后会自动激发父元素的事件
    
    //在阻止冒泡的过程中，W3C和IE采用的不同的方法，那么我们必须做一下兼容。
    function stopPro(evt) {  //取消冒泡函数
        //如果无法直接获取event对象，说明是IE浏览器，就用IE的window.event获取event对象
        var e = evt || window.event;
        //如果window.event获取event对象能执行就用cancelBubble = true取消冒泡，否则就用stopPropagation()取消冒泡
        window.event ? e.cancelBubble = true : e.stopPropagation();
    }
[/code]



