第一百一十七节，JavaScript，DOM元素尺寸和位置



**学习要点：**

**1.获取元素CSS大小**

**2.获取元素实际大小**

**3.获取元素周边大小**



**本章，我们主要讨论一下页面中的某一个元素它的各种大小和各种位置的计算方式，以便更好的理解。**



**一．获取元素CSS** **大小**



**1.通过style内联获取元素的大小**

    
    
     //<div id="box" style="background-color: #2616ff;width: 200px;height: 200px;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //通过style内联获取元素的大小
        var asf = document.getElementById('box'); //通过ID获取到元素标签
        alert(asf.style.width);  //获取内联元素的宽度
        //200px
        alert(asf.style.height); //获取内联元素的高度
        //200px
    };

**PS：style获取只能获取到行内style属性的CSS样式中的宽和高，如果有获取；如果没有则返回空。**



**2.通过计算获取元素的大小**

    
    
     //<div id="box" style="background-color: #2616ff;width: 200px;height: 200px;">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //通过计算获取元素的大小
        var asf = document.getElementById('box'); //通过ID获取到元素标签
        //浏览器兼容处理，如果getComputedStyle返回真就用getComputedStyle 方法，否则返回null，执行currentStyle
        var style = window.getComputedStyle ? window.getComputedStyle(asf, null) : null || asf.currentStyle;
        alert(style.width);        //获取浏览器计算后的元素宽度，如果有设置就是获取设置的宽度，如果没设置获取默认宽度                        
        alert(style.height);    //获取浏览器计算后的元素高度，如果有设置就是获取设置的高度，如果没设置获取默认高度        
    };

**PS：通过计算获取元素的大小，无关你是否是行内、内联或者链接，它经过计算后得到的结果返回出来。如果本身设置大小，它会返回元素的大小，如果本身没有设置，非IE浏览器会返回默认的大小，IE浏览器返回auto。**



**3.通过CSSStyleSheet对象中的cssRules(或rules)属性获取元素大小，就是获取连接或者内联样式大小**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //通过CSSStyleSheet对象中的cssRules(或rules)属性获取元素大小，就是获取连接或者内联样式大小
        var sheet = document.styleSheets[0];            //获取样式表对象集合里的第一个样式表对象
        //如果浏览器执行cssRules不成功，就执行rules，来获取样式表对象里的选择器集合，得到的是选择器集合
        var rule = (sheet.cssRules || sheet.rules)[0];        //获取第一条css选择器
        alert(rule.style.width);                            //200px、空
        alert(rule.style.height);                            //200px、空
    
    };

**PS：cssRules(或rules)只能获取到内联和链接样式的宽和高，不能获取到行内和计算后的样式。**



**总结：以上的三种CSS获取元素大小的方法，只能获取元素的CSS大小，却无法获取元素本身实际的大小。比如加上了内边距、滚动条类的。**



**二．获取元素实际大小**

**1.clientWidth和clientHeight，这组属性可以获取元素可视区的大小，可以得到元素内容及内边距所占据的空间大小。**

****clientWidth属性， **获取元素可视区的宽度， **可以得到元素内容及内边距所占据的空间大小********

****clientHeight属性， **获取元素可视区的高度， **可以得到元素内容及内边距所占据的空间大小******  
**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //clientWidth和clientHeight，这组属性可以获取元素可视区的大小，可以得到元素内容及内边距所占据的空间大小。
        alert(asf.clientWidth);  //获取实际宽度，包含内边距
        alert(asf.clientHeight);  //获取实际高度，包含内边距
    };

**PS：返回了元素大小，但没有单位，默认单位是px，如果你强行设置了单位，比如100em之类，它还是会返回px的大小。(CSS获取的话，是照着你设置的样式获取)。**

**PS：对于元素的实际大小，clientWidth和clientHeight理解方式如下：**

**1.增加边框，无变化，**

**2.增加外边距，无变化，**

**3.增加滚动条，最终值等于原本大小减去滚动条的大小，**

**4.增加内边距，最终值等于原本大小加上内边距的大小，**

**PS：如果说没有设置任何CSS的宽和高度，那么非IE浏览器会算上滚动条和内边距的计算后的大小，而IE浏览器则返回0。**



**2.scrollWidth和scrollHeight，这组属性可以获取滚动内容的元素大小。**

**scrollWidth获取滚动内容的元素宽度**

**scrollHeight获取滚动内容的元素高度**



    
    
    //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //scrollWidth和scrollHeight，这组属性可以获取滚动内容的元素大小。
        alert(asf.scrollWidth);  //scrollWidth获取滚动内容的元素宽度
        alert(asf.scrollHeight);  //scrollHeight获取滚动内容的元素高度
    };



**PS：返回了元素大小，默认单位是px。如果没有设置任何CSS的宽和高度，它会得到计算后的宽度和高度。**

**PS：对于元素的实际大小，scrollWidth和scrollHeight理解如下:**

**1.增加边框，不同浏览器有不同解释：**

**a)          Firefox和Opera浏览器会增加边框的大小**

**b)         IE、Chrome和Safari浏览器会忽略边框大小**

**c)          IE浏览器只显示它本来内容的高度**

**2.增加内边距，最终值会等于原本大小加上内边距大小**

**3.增加滚动条，最终值会等于原本大小减去滚动条大小**

**4.增加外边据，无变化。**

**5.增加内容溢出，Firefox、Chrome和IE获取实际内容高度，Opera比前三个浏览器获取的高度偏小，Safari比前三个浏览器获取的高度偏大。**





**3.offsetWidth和offsetHeight，这组属性可以返回元素实际大小，包含边框、内边距和滚动条。**

**offsetWidth获取元素实际宽度，包含边框、内边距和滚动条**  
 **offsetHeight获取元素实际高度，包含边框、内边距和滚动条**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //offsetWidth和offsetHeight，这组属性可以返回元素实际大小，包含边框、内边距和滚动条。
        alert(asf.offsetWidth);  //offsetWidth获取元素实际宽度，包含边框、内边距和滚动条
        alert(asf.offsetHeight);  //offsetHeight获取元素实际高度，包含边框、内边距和滚动条
    };

**PS：返回了元素大小，默认单位是px。如果没有设置任何CSS的宽和高度，他会得到计算后的宽度和高度。**

**PS：对于元素的实际大小，offsetWidth和offsetHeight理解如下：**

**1.增加边框，最终值会等于原本大小加上边框大小，为220；**

**2.增加内边距，最终值会等于原本大小加上内边距大小，为220；**

**3.增加外边据，无变化；**

**4.增加滚动条，无变化，不会减小；**

**PS：对于元素大小的获取，一般是块级(block)元素并且以设置了CSS大小的元素较为方便。如果是内联元素(inline)或者没有设置大小的元素就尤为麻烦，所以，建议使用的时候注意。**



**三．** **获取元素周边大小**

**1.clientLeft和clientTop这组属性可以获取元素设置了左边框和上边框的大小。**

**clientLeft获取左边框的宽度**  
 **clientTop获取上边框的宽度**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //clientLeft和clientTop这组属性可以获取元素设置了左边框和上边框的大小。
        alert(asf.clientLeft);  //clientLeft获取左边框的宽度
        alert(asf.clientTop);  //clientTop获取上边框的宽度
    };

**PS：目前只提供了Left和Top这组，并没有提供Right和Bottom。如果四条边宽度不同的话，可以直接通过计算后的样式获取，或者采用以上三组获取元素大小的减法求得。**





**2.offsetLeft和offsetTop这组属性可以获取当前元素相对于父元素的位置。**

**offsetLeft获取当前元素相对于父元素左边的位置**  
 **offsetTop获取当前元素相对于父元素上边的位置**  
 **offsetParent获取当前元素的父元素对象**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //offsetLeft和offsetTop这组属性可以获取当前元素相对于父元素的位置
        alert(asf.offsetLeft);  //offsetLeft获取当前元素相对于父元素左边的位置
        alert(asf.offsetTop);  //offsetTop获取当前元素相对于父元素上边的位置
        //offsetParent获取当前元素的父元素对象
        alert(asf.offsetParent);  //offsetParent获取当前元素的父元素对象
    
        //如果有两层要获取两层总共的位置
        //当前元素上位置加父元素上位置
        alert(asf.offsetTop + asf.offsetParent.offsetTop);
    };

**PS：offsetParent中，如果本身父元素是
<body>，非IE返回body对象，IE返回html对象。如果两个元素嵌套，如果上父元素没有使用定位position:absolute，那么offsetParent将返回body对象或html对象。所以，在获取offsetLeft和offsetTop时候，CSS定位很重要。**

**如果说，在很多层次里，外层已经定位，我们怎么获取里层的元素距离body或html元素之间的距离呢？也就是获取任意一个元素距离页面上的位置。那么我们可以编写函数，通过不停的向上回溯获取累加来实现。**

**如果多层的话，就必须使用循环或递归。**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        alert(offsetLeft(asf));
    
        //如果多层的话，就必须使用循环或递归。
        function offsetLeft(element) {
            var left = element.offsetLeft;                //得到第一层距离
            var parent = element.offsetParent;            //得到第一个父元素
    
            while (parent !== null) {                    //如果还有上一层父元素
            left += parent.offsetLeft;                //把本层的距离累加
            parent = parent.offsetParent;            //得到本层的父元素
            }                                    //然后继续循环
            return left;
        }
    
    };



**3.scrollTop和scrollLeft这组属性可以获取滚动条被隐藏的区域大小，也可设置定位到该区域。就是溢出隐藏部分的大小**

**scrollTop获取或设置滚动条上面被隐藏的区域大小**  
 **scrollLeft获取或设置滚动条左边被隐藏的区域大小**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //scrollTop和scrollLeft这组属性可以获取滚动条被隐藏的区域大小，也可设置定位到该区域。就是溢出隐藏部分的大小
        alert(asf.scrollTop);  //scrollTop获取或设置滚动条上面被隐藏的区域大小
        alert(asf.scrollLeft);  //scrollLeft获取或设置滚动条左边被隐藏的区域大小
        scrollStart(asf);
    
        //如果要让滚动条滚动到最初始的位置，那么可以写一个函数：
        function scrollStart(element) {
            if (element.scrollTop != 0){
                element.scrollTop = 0;
            }
        }
        
    };



**DOM的方法获取元素位置**

**getBoundingClientRect()方法，获取元素位置，这个方法返回一个矩形对象，包含四个属性：left、top、right和bottom。分别表示元素各边与页面上边和左边的距离。**

**使用方式：**

**元素节点. **getBoundingClientRect().要获取的元素方位****

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //getBoundingClientRect()方法，获取元素位置，这个方法返回一个矩形对象，包含四个属性：left、top、right和bottom。分别表示元素各边与页面上边和左边的距离。
        var fw = asf.getBoundingClientRect();
        alert(fw.top);   //查看元素上位置
        alert(fw.right);  //查看元素右位置
        alert(fw.bottom);  //查看元素下面位置
        alert(fw.left);   //查看元素左面位置
    
    };

**PS：IE、Firefox3+、Opera9.5、Chrome、Safari支持，在IE中，默认坐标从(2,2)开始计算，导致最终距离比其他浏览器多出两个像素，我们需要做个兼容。**

    
    
     //<div id="box" class="box1">测试1</div>
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var asf = document.getElementById('box');  //通过ID获取到元素节点
        //getBoundingClientRect()方法，获取元素位置，这个方法返回一个矩形对象，包含四个属性：left、top、right和bottom。分别表示元素各边与页面上边和左边的距离。
        alert(getRect(asf).top); //执行函数，获取函数里的对象属性
    
        //各版本浏览器兼容
        function getRect(element) {
            var rect = element.getBoundingClientRect();
            var top = document.documentElement.clientTop;
            var left = document.documentElement.clientLeft;
    
            return {
                top : rect.top - top,
                bottom : rect.bottom - top,
                left : rect.left - left,
                right : rect.right - left
            }
        }
    };

**PS：分别加上外边据、内边距、边框和滚动条，用于测试所有浏览器是否一致。**

