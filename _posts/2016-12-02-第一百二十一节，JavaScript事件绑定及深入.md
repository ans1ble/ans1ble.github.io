
---
layout: post
title: " 第一百二十一节，JavaScript事件绑定及深入 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript事件绑定及深入**





**学习要点：**

**1.传统事件绑定的问题**

**2.W3C事件处理函数**

**3.IE事件处理函数**

**4.事件对象的其他补充**



**事件绑定分为两种：一种是传统事件绑定(内联模型，脚本模型)，一种是现代事件绑定(DOM2级模型)。现代事件绑定在传统绑定上提供了更强大更方便的功能。**



**一．** **传统事件绑定的问题**

**传统事件绑定有内联模型和脚本模型，内联模型我们不做讨论，基本很少去用。先来看一下脚本模型，脚本模型将一个函数赋值给一个事件处理函数。**

[code]

    window.onload =  function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var box = document.getElementById('box');        //获取元素
        box.onclick = function () {                    //元素点击触发事件
            alert('Lee');
        };
    };
[/code]

**问题一：一个事件处理函数触发两次事件**

**如果一个页面引入两个js文件，每个js文件里都有一个window.onload事件，**
**当两组程序或两个JS文件同时执行的时候，后面一个会把前面一个完全覆盖掉。导致前面的window.onload完全失效了。**

**如下：**

[code]

    window.onload =  function () {                //第一组程序项目或第一个JS文件
        alert('Lee');
    };
    
    window.onload = function () {                //第二组程序项目或第二个JS文件
        alert('Mr.Lee');
    };
    //后面一个会把前面一个完全覆盖掉。导致前面的window.onload完全失效了，只能执行到后面这个window.onload
[/code]

**解决覆盖问题，我们可以这样去解决：**

[code]

     //解决覆盖问题
    window.onload = function () {                //第一个要执行的事件，会被覆盖
        alert('Lee');
    };
    
    if (typeof window.onload == 'function') {        //判断之前是否有window.onload
        var saved = null;                        //创建一个保存器
        saved = window.onload;                    //把之前的window.onload保存起来
    }
    
    window.onload = function () {                //最终一个要执行事件
        if (saved) saved();                        //执行之前一个事件，saved()相当于window.onload = function ()
        alert('Mr.Lee');                            //执行本事件的代码
    };
[/code]



**问题二：事件切换器**

**比如一个元素鼠标点击后改变颜色，在点击后又改变颜色，如下**

[code]

     //<div id="box" class="red">测试</div>
    // .red{
    //     width: 200px;
    //     height: 200px;
    //     background-color: #ff0f20;
    // }
    // .blue{
    //     width: 200px;
    //     height: 200px;
    //     background-color: #1516ff;
    // }
    window.onload = function () { //window.onload事件，等待html执行完成后，执行匿名函数
        var box = document.getElementById('box');        //获取元素
        box.onclick = toBlue;            //点击元素后执行toBlue函数
        function toRed() {
            this.className = 'red';    //将元素选择器设置为red
            this.onclick = toBlue;        //再次点击执行toBlue函数
        }
    
        function toBlue() {
            this.className = 'blue';    //将元素选择器设置为blue
            this.onclick = toRed;       //再次点击执行toRed函数
        }
    };
[/code]

**这个切换器在扩展的时候，会出现一些问题：**

**1.如果增加一个执行函数，那么会被覆盖**

[code]

    box.onclick = toAlert;                         //被增加的函数
    box.onclick = toBlue;                        //toAlert被覆盖了
[/code]

**2.如果解决覆盖问题，就必须包含同时执行，但又出新问题**



[code]

    box.onclick = function () {                    //包含进去，但可读性降低
        toAlert();                                //第一次不会被覆盖，但第二次又被覆盖
        toBlue.call(this);                        //还必须把this传递到切换器里
    };
[/code]



**综上的三个问题：覆盖问题、可读性问题、this传递问题。我们来创建一个自定义的事件处理函数，来解决以上三个问题。**

[code]

     //可以同时执行多个同一事件函数
    addEvent(window, 'onload', function () {            //执行到了
        alert('Lee');
    });
    addEvent(window, 'onload', function () {            //执行到了
        alert('Mr.Lee');
    });
    
    function addEvent(obj, type, fn) {      //可以同时执行多个同一事件函数，接收3个参数，第一个要绑定事件的对象，第二个事件，第三个事件激发的函数
        var saved = null;                        //设置一个变量，保存每次触发的事件处理函数
        if (typeof obj[type] == 'function') {    //判断是不是事件
            saved = obj[type];                //如果有，保存起来
        }
        obj[type] = function () {            //然后执行
            if (saved) saved();                    //执行上一个事件函数
            fn.call(this);                        //冒充addEvent里的匿名函数，执行函数，把this传递过去
        };
    }
[/code]

**两个相同函数名的函数误注册了两次或多次**

**PS：以上编写的自定义事件处理函数，还有一个问题没有处理，就是两个相同函数名的函数误注册了两次或多次，那么应该把多余的屏蔽掉。那，我们就需要把事件处理函数进行遍历，如果有同样名称的函数名就不添加即可。(这里就不做了)，**

[code]

     //两个相同函数名的函数误注册了两次或多次
    addEvent(window, 'onload', init);                //注册第一次
    addEvent(window, 'onload', init);                //注册第二次，应该忽略
    function init() {
        alert('123');
    }
    
    
    function addEvent(obj, type, fn) {      //可以同时执行多个同一事件函数，接收3个参数，第一个要绑定事件的对象，第二个事件，第三个事件激发的函数
        var saved = null;                        //设置一个变量，保存每次触发的事件处理函数
        if (typeof obj[type] == 'function') {    //判断是不是事件
            saved = obj[type];                //如果有，保存起来
        }
        obj[type] = function () {            //然后执行
            if (saved) saved();                    //执行上一个事件函数
            fn.call(this);                        //冒充addEvent里的匿名函数，执行函数，把this传递过去
        };
    }
[/code]

**用自定义事件函数注册到切换器上查看效果** ：

[code]

    addEvent(window, 'onload', function () {
        var box = document.getElementById('box');
        addEvent(box, 'onclick', toBlue);
    });
    
    function toRed() {
        this.className = 'red';
        addEvent(this, 'onclick', toBlue);
    }
    
    function toBlue() {
        this.className = 'blue';
        addEvent(this, 'onclick', toRed);
    }
    
    
    function addEvent(obj, type, fn) {      //可以同时执行多个同一事件函数，接收3个参数，第一个要绑定事件的对象，第二个事件，第三个事件激发的函数
        var saved = null;                        //设置一个变量，保存每次触发的事件处理函数
        if (typeof obj[type] == 'function') {    //判断是不是事件
            saved = obj[type];                //如果有，保存起来
        }
        obj[type] = function () {            //然后执行
            if (saved) saved();                    //执行上一个事件函数
            fn.call(this);                        //冒充addEvent里的匿名函数，执行函数，把this传递过去
        };
    }
[/code]



**删除事件处理函数**

**PS：当你单击很多很多次切换后，浏览器直接卡死，或者弹出一个错误：too much
recursion(太多的递归)。主要的原因是，每次切换事件的时候，都保存下来，没有把无用的移除，导致越积越多，最后卡死。**

[code]

    addEvent(window, 'onload',  function () {
        var box = document.getElementById('box');
        addEvent(box, 'onclick', toBlue);
    });
    
    function toRed() {
        this.className = 'red';
        removeEvent(this,onclick);
        addEvent(this, 'onclick', toBlue);
    }
    
    function toBlue() {
        this.className = 'blue';
        removeEvent(this,onclick);
        addEvent(this, 'onclick', toRed);
    }
    
    
    function addEvent(obj, type, fn) {      //可以同时执行多个同一事件函数，接收3个参数，第一个要绑定事件的对象，第二个事件，第三个事件激发的函数
        var saved = null;                        //设置一个变量，保存每次触发的事件处理函数
        if (typeof obj[type] == 'function') {    //判断是不是事件
            saved = obj[type];                //如果有，保存起来
        }
        obj[type] = function () {            //然后执行
            if (saved) saved();                    //执行上一个事件函数
            fn.call(this);                        //冒充addEvent里的匿名函数，执行函数，把this传递过去
        };
    }
    
    function removeEvent(obj, type) {   //删除事件处理函数
        if (obj + [type]) obj[type] = null;         //删除事件处理函数
    }
[/code]

**以上的删除事件处理函数只不过是一刀切的删除了，这样虽然解决了卡死和太多递归的问题。但其他的事件处理函数也一并被删除了，导致最后得不到自己想要的结果。如果想要只删除指定的函数中的事件处理函数，那就需要遍历，查找。(这里就不做了)**

** **

**二．** **W3C** **事件处理函数【重点】**

**“DOM2级事件”定义了两个方法，用于添加事件和删除事件处理程序的操作：addEventListener()和removeEventListener()。所有DOM节点中都包含这两个方法，并且它们都接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡)。**

**添加和删除事件**

**addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡),
注意：传参事件名称不加on，IE9以下不支持**  
 **使用方式：**  
 **元素对象.addEventListener(事件名称,事件函数,true或false)**

**1.自动解决覆盖问题，也就是同时存在两个相同的事件两个都能执行，不会覆盖**

[code]

     //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load', function () {
        alert('Lee');
    }, false);
    //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load', function () {
        alert('Mr.Lee');
    }, false);
    //两个事件都执行了，没被覆盖
[/code]

**2.相同事件函数屏蔽问题，也就是一个相同的事件函数重复写了两次，会自动屏蔽只执行一次**

[code]

     //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load',lik, false);  //一个相同的事件函数重复写了两次，会自动屏蔽只执行一次
    window.addEventListener('load',lik, false);
    function lik(){
        alert('测试')
    }
[/code]



**removeEventListener()方法，删除指定的事件方法，接受3个参数，参数和addEventListener创建事件时一样，第一个是创建事件时的事件名称，第二个是创建事件时的执行函数，第三个是冒泡或捕获的布尔值(true表示捕获，false表示冒泡),
注意：传参事件名称不加on，用于一个事件使用完毕后将事件删除，IE9以下不支持**  
 **使用方式：**  
 **创建事件时元素对象.removeEventListener(创建事件时的事件名称,创建事件时的执行事件函数,true或false)**

**3.可以通过addEventListener方法将对象的this传到执行函数里，执行函数里的this就是代表事件对象本身**

[code]

     //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load', function () {  //等待页面加载完后，执行匿名函数
        var box = document.getElementById('box');  //通过ID获取元素节点
        box.addEventListener('click',toBlue , false);  //将获取到的节点绑定一个点击事件,点击执行toBlue函数
    }, false);
    
    function toRed() {
        //此时这里的this代码对象本身box，通过addEventListener()函数传递过来
        this.className = 'red'; //改变对象class属性值
        this.removeEventListener('click', toRed, false);  //此次事件使用完毕，删除此次事件，参数与创建时一样
        this.addEventListener('click', toBlue, false);  //给对象创建一个点击事件，点击后执行toBlue函数
    }
    
    function toBlue() {
        //此时这里的this代码对象本身box，通过addEventListener()函数传递过来
        this.className = 'blue'; //改变对象class属性值
        this.removeEventListener('click', toBlue, false);  //此次事件使用完毕，删除此次事件，参数与创建时一样
        this.addEventListener('click', toRed, false);  //给对象创建一个点击事件，点击后执行toRed函数
    }
[/code]

**  4.添加一个额外的事件，会不会被覆盖，或者只能执行一次**

[code]

    //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load', function () {  //等待页面加载完后，执行匿名函数
        var box = document.getElementById('box');  //通过ID获取元素节点
    
        //添加一个额外的事件，会不会被覆盖，或者只能执行一次
        box.addEventListener('click',function () {  //添加一个事件，不会被覆盖
            alert('添加');
        },false);
    
        box.addEventListener('click',toBlue , false);  //将获取到的节点绑定一个点击事件,点击执行toBlue函数
    }, false);
    
    function toRed() {
        //此时这里的this代码对象本身box，通过addEventListener()函数传递过来
        this.className = 'red'; //改变对象class属性值
        this.removeEventListener('click', toRed, false);  //此次事件使用完毕，删除此次事件，参数与创建时一样
        this.addEventListener('click', toBlue, false);  //给对象创建一个点击事件，点击后执行toBlue函数
    }
    
    function toBlue() {
        //此时这里的this代码对象本身box，通过addEventListener()函数传递过来
        this.className = 'blue'; //改变对象class属性值
        this.removeEventListener('click', toBlue, false);  //此次事件使用完毕，删除此次事件，参数与创建时一样
        this.addEventListener('click', toRed, false);  //给对象创建一个点击事件，点击后执行toRed函数
    }
[/code]

**设置冒泡和捕获阶段**

**之前我们上一章了解了事件冒泡，即从里到外触发。我们也可以通过event对象来阻止某一阶段的冒泡。那么W3C现代事件绑定可以设置冒泡和捕获。**

[code]

     //addEventListener()方法，添加事件方法，接受3个参数；事件名、函数、冒泡或捕获的布尔值(true表示捕获，false表示冒泡), 注意：传参事件名称不加on
    window.addEventListener('load', function () {  //等待页面加载完后，执行匿名函数
        var box = document.getElementById('box');  //通过ID获取元素节点
        document.addEventListener('click', function () {  //创建一个点击事件
            alert('document');
        }, true);                                    //把布尔值设置成true，则为捕获，从外向里激发，设为false为冒泡，从里向为激发
        box.addEventListener('click', function () {  //创建一个点击事件
            alert('div');
        }, true);
    }, false);
[/code]

**综上所述：w3c是比较完美的解决了传统事件出现的一些问题，但是IE9以下不支持，IE9以下采用了自己的事件**



**三．** **IE** **事件处理函数【不推荐使用】**

**IE实现了与DOM中类似的两个方法：attachEvent()和detachEvent()。这两个方法接受相同的参数：事件名称和函数。**

**在使用这两组函数的时候，** **先把区别说一下：**

**1.IE不支持捕获，只支持冒泡；**

**2.IE添加事件不能屏蔽重复的函数；**

**3.IE中的this指向的是window而不是DOM对象。**

**4.在传统事件上，IE是无法接受到event对象的，但使用了attchEvent()却可以，但有些区别。**



**attachEvent()方法，IE添加事件方法，接受2个参数，第一个事件名称，第二个事件函数，除IE外不支持**  
 **使用方式：**  
 **元素对象.attachEvent(事件名称,事件函数)**

  
**detachEvent()方法，IE方法，删除一个attachEvent添加的事件，接受2个参数，第一个添加事件时的事件名称，第二个添加事件时的事件函数，
**除IE外不支持****  
 **使用方式：**  
 **元素对象.detachEvent(添加事件时的事件名称,添加事件时的事件函数)**

[code]

     //创建事件.等页面执行完毕后，执行匿名函数
    window.attachEvent('onload',function () {
        //通过ID获取到元素
        var box = document.getElementById('box');
        //给元素添加一个点击事件，点击后执行toBlue函数
        box.attachEvent('onclick',toBlue);
    
    });
    
    
    function toRed() {
        //获取事件的event对象，通过event对象获取到当前元素节点
        var that = window.event.srcElement;
        //将元素的class属性值设置为red
        that.className = 'red';
        //删除上一个创建的对象
        that.detachEvent('onclick', toRed);
        //给元素创建一个点击事件，点击后执行toBlue函数
        that.attachEvent('onclick', toBlue);
    }
    
    function toBlue() {
        //获取事件的event对象，通过event对象获取到当前元素节点
        var that = window.event.srcElement;
        //将元素的class属性值设置为blue
        that.className = 'blue';
        //删除上一个创建的对象                      detachEvent()方法，IE方法，删除一个attachEvent添加的事件，接受2个参数，第一个添加事件时的事件名称，第二个添加事件时的事件函数，
        that.detachEvent('onclick', toBlue);
        //给元素创建一个点击事件，点击后执行toRed函数
        that.attachEvent('onclick', toRed);
    }
[/code]

**  夸浏览器 ** **自定义**** 创建事件， ** **自定义**** 移除事件， ** **自定义**** 获取目标，用自定义写一个完整的切换器
【但不推荐，下面会说明】**

[code]

    //创建事件，等页面执行完毕后执行匿名函数
    addEvent(window,'load',function () {
        //通过ID获取到元素
        var box = document.getElementById('box');
        //给元素创建一个点击事件，点击后执行toBlue函数
        addEvent(box,'click',toBlue);
    
    });
    
    //切换器
    function toBlue(evt) {
        //获取事件的event对象，通过event对象获取到当前元素节点
        var that = getTarget(evt);
        //将元素的class属性值设置为blue
        that.className = 'blue';
        //删除上一个创建的对象                      detachEvent()方法，IE方法，删除一个attachEvent添加的事件，接受2个参数，第一个添加事件时的事件名称，第二个添加事件时的事件函数，
        removeEvent(that,'click',toBlue);
        //给元素创建一个点击事件，点击后执行toRed函数
        addEvent(that,'click',toRed)
    }
    
    function toRed(evt) {
        //获取事件的event对象，通过event对象获取到当前元素节点
        var that = getTarget(evt);
        //将元素的class属性值设置为blue
        that.className = 'red';
        //删除上一个创建的对象                      detachEvent()方法，IE方法，删除一个attachEvent添加的事件，接受2个参数，第一个添加事件时的事件名称，第二个添加事件时的事件函数，
        removeEvent(that,'click',toRed);
        //给元素创建一个点击事件，点击后执行toRed函数
        addEvent(that,'click',toBlue)
    }
    
    
    
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
    
    //跨浏览器移除事件，移除事件兼容
    function removeEvent(obj, type, fn) {    //移除事件函数，接收3个参数，1事件对象，2事件名称，3事件函数
        //判断浏览器如果支持w3c
        if (obj.removeEventListener) {
            //就用w3c的removeEventListener方法移除对象，将事件名称和事件函数传入移除事件
            obj.removeEventListener(type, fn, false);
        } else if (obj.detachEvent) {      //判断如果浏览器是IE9以下，就用IE的方法detachEvent移除事件
            //将事件名称和事件函数传入移除对象
            obj.detachEvent('on' + type, fn);
        }
    }
    
    //跨浏览器获取事件目标，获取事件目标兼容
    function getTarget(evt) {    //参数接收event对象
        //判断如果浏览器支持w3c获取event对象
        if (evt.target) {
            //返回获取到的event对象里的标签节点，也就是目标
            return evt.target;
        } else if (window.event.srcElement) {   //如果是IE浏览器
            //返回IE方式获取到的event对象里的标签节点，也就是目标
            return window.event.srcElement;
        }
    }
[/code]

**PS：IE中的事件绑定函数attachEvent()和detachEvent()可能在实践中不去使用，有几个原因：1.IE9就将全面支持W3C中的事件绑定函数；2.IE的事件绑定函数无法传递this；3.IE的事件绑定函数不支持捕获；4.同一个函数注册绑定后，没有屏蔽掉；5.有内存泄漏的问题。至于怎么替代，我们将在以后的项目课程中探讨。**





**四．** **事件对象的其他补充**

**在W3C提供了一个属性：relatedTarget；这个属性可以在onmouseover和onmouseout事件中获取从哪里移入和从哪里移出的DOM对象。**

**relatedTarget属性，可以在onmouseover事件和onmouseout事件中获取鼠标从哪里移入和从哪里移出的DOM对象。也就是鼠标移动后获取当前对象最近的一个对象，IE9以下不支持**

**使用方式：**  
 **event对象.relatedTarget**

[code]

     // <span class="adc">
    // <div id="box" class="red">测试</div>
    // </span>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过ID获取到元素对象
        var box = document.getElementById('box');
        //给元素添加一个事件，当鼠标移入后激发函数
        box.onmouseover = function (evt) {  //接收事件传递的event对象
            //relatedTarget属性，可以在onmouseover事件和onmouseout事件中获取鼠标从哪里移入和从哪里移出的DOM对象。也就是鼠标移动后获取当前对象最近的一个对象
            alert(evt.relatedTarget.tagName);
            //返回：span
        }
    };
[/code]

**当鼠标移出后激发**

[code]

     // <span class="adc">
    // <div id="box" class="red">测试</div>
    // </span>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过ID获取到元素对象
        var box = document.getElementById('box');
        //给元素添加一个事件，当鼠标移出后激发函数
        box.onmouseout = function (evt) {  //接收事件传递的event对象
            //relatedTarget属性，可以在onmouseover事件和onmouseout事件中获取鼠标从哪里移入和从哪里移出的DOM对象。也就是鼠标移动后获取当前对象最近的一个对象
            alert(evt.relatedTarget.tagName);
            //返回：span
        }
    };
[/code]



**IE提供了两组分别用于移入移出的属性：fromElement获取 **移入 **最近对象****
和toElement获取移出最近对象，分别对应onmouseover和onmouseout。**

**fromElement属性，IE属性，对应onmouseover事件，获取移入最近对象**  
 **使用方式：**  
 **event对象.fromElement**

[code]

     // <span class="adc">
    // <div id="box" class="red">测试</div>
    // </span>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过ID获取到元素对象
        var box = document.getElementById('box');
        //给元素添加一个事件，当鼠标移入后激发函数
        box.onmouseover = function () {
            //fromElement属性，IE属性，对应onmouseover事件，获取移入最近对象
            alert(window.event.fromElement.tagName);  //接收事件传递的event对象
            //返回：span
        }
    };
[/code]

**toElement属性，IE属性，对应onmouseout事件，获取移出最近对象**  
 **使用方式：**  
 **event对象.toElement**

[code]

     // <span class="adc">
    // <div id="box" class="red">测试</div>
    // </span>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过ID获取到元素对象
        var box = document.getElementById('box');
        //给元素添加一个事件，当鼠标移出后激发函数
        box.onmouseout = function () {
            //toElement属性，IE属性，对应onmouseout事件，获取移出最近对象
            alert(window.event.toElement.tagName);  //接收事件传递的event对象
            //返回：span
        }
    };
[/code]

**PS：fromElement和toElement如果分别对应相反的鼠标事件，没有任何意义。**



****根据IE和w3c做兼容，** 自定义跨浏览器兼容获取事件最近对象**

[code]

    // <span class="adc">
    // <div id="box" class="red">测试</div>
    // </span>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过ID获取到元素对象
        var box = document.getElementById('box');
        //给元素添加一个事件，当鼠标移入后激发函数
        box.onmouseover = function (evt) { //接收事件传递的event对象
            //执行自定义函数获取鼠标移入或者移出最近对象
            alert(getTarget(evt).tagName);  //将event对象传入自定义函数
            //返回：span
        }
    };
    
    //做的就是跨浏览器兼容操作：
    function getTarget(evt) {
        //如果evt执行不成功，说明是IE9以下的IE浏览器就执行window.event获取event对象
        var e = evt || window.event;                //得到事件对象
        if (e.srcElement) {                        //如果支持srcElement获取事件对象并且，表示IE
            if (e.type == 'mouseover') {            //如果事件属性是鼠标移入
                return e.fromElement;            //就使用fromElement返回最近对象
            } else if (e.type == 'mouseout') {        //如果事件属性是鼠标移入
                return e.toElement;                //就使用toElement返回最近对象
            }
        } else if (e.relatedTarget) {                //如果支持relatedTarget，表示W3C
            return e.relatedTarget;  //通过relatedTarget返回最近对象
        }
    }
[/code]



**  阻止浏览器超链接默认行为，也就是阻止浏览器默认的连接跳转**

**有时我们需要阻止事件的默认行为，比如：一个超链接的默认行为就点击然后跳转到指定的页面。那么阻止默认行为就可以屏蔽跳转的这种操作，而实现自定义操作。**

**传统方式屏蔽超链接跳转【不推荐】**

[code]

     //<a href="http://www.baidu.com">百度</a>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过元素名称获取到目标元素对象
        var link = document.getElementsByTagName('a')[0];
        //给元素对象添加一个点击事件，点击后执行函数
        link.onclick = function () {
            //返回假，屏蔽元素跳转，也就是屏蔽掉超链接跳转
            return false;
        }
    };
[/code]

**PS：虽然return false；可以实现这个功能，但有漏洞；第一：必须写到最后，这样导致中间的代码执行后，有可能执行不到return
false；第二：return false写到最前那么之后的自定义操作就失效了。所以，最好的方法应该是在最前面就阻止默认行为，并且后面还能执行代码。**

**preventDefault()方法，W3C，阻止默认行为，阻止超链接跳转，但ie9以下不支持**  
 **使用方式：**  
 **event对象.preventDefault()**

[code]

     //<a href="http://www.baidu.com">百度</a>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过元素名称获取到目标元素对象
        var link = document.getElementsByTagName('a')[0];
        //给元素对象添加一个点击事件，点击后执行函数
        link.onclick = function (evt) {
            evt.preventDefault();   //W3C，阻止默认行为，阻止超链接跳转，但ie9以下不支持
        }
    };
[/code]



**returnValue属性，IE阻止默认行为，阻止超链接跳转，只支持IE9以下**  
 **使用方式：**  
 **event对象.returnValue = false**

[code]

     //<a href="http://www.baidu.com">百度</a>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过元素名称获取到目标元素对象
        var link = document.getElementsByTagName('a')[0];
        //给元素对象添加一个点击事件，点击后执行函数
        link.onclick = function () {
            window.event.returnValue = false;  //returnValue属性，IE阻止默认行为，阻止超链接跳转，只支持IE
        }
    };
[/code]



**跨浏览器兼容， **阻止默认行为，阻止超链接跳转****

[code]

     //<a href="http://www.baidu.com">百度</a>
    
    //等待页面加载完成后执行匿名函数
    window.onload =  function () {
        //通过元素名称获取到目标元素对象
        var link = document.getElementsByTagName('a')[0];
        //给元素对象添加一个点击事件，点击后执行函数
        link.onclick = function (evt) {
            preDef(evt);  //执行函数跨浏览器兼容，阻止超链接跳转，将event对象传入
        }
    };
    
    //跨浏览器兼容，跨浏览器兼容，阻止默认行为，阻止超链接跳转
    function preDef(evt) { //接收event对象
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //判断W3C，阻止默认行为，如果为真
        if (e.preventDefault) {
            //就用W3C，阻止默认行为
            e.preventDefault();
        } else {
            //否则就用ie的属性returnValue阻止行为
            e.returnValue = false;
        }
    }
[/code]



**上下文菜单事件：oncontextmenu，当我们右击网页的时候，会自动出现windows自带的菜单。那么我们可以使用oncontextmenu事件来修改我们指定的菜单，但前提是把右击的默认行为取消掉。**

**oncontextmenu事件，oncontextmenu事件用来修改我们指定的菜单，但前提是把右击的默认行为取消掉。**  
 **使用方式：**  
 **对象.oncontextmenu.执行函数**

[code]

     //HTML代码
    /*
    <textarea id="wb" placeholder="请输入您的内容"></textarea>
    <ul id="cd">
        <li>菜单1</li>
        <li>菜单2</li>
        <li>菜单3</li>
    </ul>
     */
    
    //css代码
    /*
    #wb{
        width: 400px;
        height: 400px;
    }
    #cd{
        width: 100px;
        height: 100px;
        background-color: #b2bbff;
        display: none;
    }
     */
    
    //等待页面加载完成后执行匿名函数
    addEvent(window,'load',function () {
        //通过ID获取到文本框
        var wb = document.getElementById('wb');
        //给文本框添加一个菜单事件
        addEvent(wb,'contextmenu',function (evt) {
            preDef(evt); //执行自定义函数，屏蔽了浏览器默认菜单
            //通过ID获取到菜单ul标签
            var cd = document.getElementById('cd');
            //将标签的style属性设置一个值，display = 'block'，将区块显示出来
            cd.style.display = 'block';
            //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
            var e = evt || window.event;
            //通过event对象获取鼠标坐标，将坐标设置成css定位的位置
            cd.style.left = e.clientX + 'px';
            //通过event对象获取鼠标坐标，将坐标设置成css定位的位置
            cd.style.top = e.clientX + 'px';
            //在根元素创建一个点击事件，当点击鼠标左键时隐藏菜单区块
            addEvent(document,'click',function () {
                cd.style.display = 'none';
            })
        })
    });
    
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
    
    
    //跨浏览器兼容，阻止默认行为
    function preDef(evt) { //接收event对象
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //判断W3C，阻止默认行为，如果为真
        if (e.preventDefault) {
            //就用W3C，阻止默认行为
            e.preventDefault();
        } else {
            //否则就用ie的属性returnValue阻止行为
            e.returnValue = false;
        }
    }
[/code]

**PS：oncontextmenu事件很常用，这直接导致浏览器兼容性较为稳定。**





**卸载前事件：onbeforeunload，这个事件可以帮助在离开本页的时候给出相应的提示，“离开”或者“返回”操作。**

**onbeforeunload事件，这个事件可以帮助在离开本页的时候给出相应的提示，“离开”或者“返回”操作。**  
 **使用方式：**  
 **对象.onbeforeunload.执行函数**



[code]

    //当用户离开当前页面时激发函数
    addEvent(window,'beforeunload',function (evt) {
        //屏蔽当前对象的默认行为
        preDef(evt);
    });
    
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
    
    
    //跨浏览器兼容，阻止默认行为
    function preDef(evt) { //接收event对象
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //判断W3C，阻止默认行为，如果为真
        if (e.preventDefault) {
            //就用W3C，阻止默认行为
            e.preventDefault();
        } else {
            //否则就用ie的属性returnValue阻止行为
            e.returnValue = false;
        }
    }
[/code]



**鼠标滚轮(mousewheel)和DOMMouseScroll，用于获取鼠标上下滚轮的距离。**

**onmousewheel事件，当用户滚动鼠标滚轮时激发函数， **非火狐****  
 **wheelDelta属性，用于获取鼠标上下滚轮的距离，非火狐**

[code]

     //当用户滚动鼠标滚轮时激发函数
    addEvent(document,'mousewheel',function (evt) {  //非火狐
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //获取鼠标滚轮滚动的距离
        alert(e.wheelDelta);
    });
    
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





**onDOMMouseScroll事件，当用户滚动鼠标滚轮时激发函数，** **火狐**  
 **detail属性，用于获取鼠标上下滚轮的距离，火狐**

[code]

     //当用户滚动鼠标滚轮时激发函数
    addEvent(document,'DOMMouseScroll',function (evt) {  
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //获取鼠标滚轮滚动的距离
        alert(evt.detail * 30);
    });
    
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





**浏览器兼容**

[code]

     //当用户滚动鼠标滚轮时激发函数
    addEvent(document,'DOMMouseScroll',function (evt) {  //火狐
        alert(getWD(evt));    //执行自定义函数
    });
    addEvent(document,'mousewheel',function (evt) {  //非火狐
        alert(getWD(evt));    //执行自定义函数
    });
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
    
    //自定义获取鼠标滚动的距离，浏览器兼容
    function getWD(evt) {   //event对象
        //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
        var e = evt || window.event;
        //如果不是IE用wheelDelta获取距离
        if (e.wheelDelta) {
            return e.wheelDelta;
        } else if (e.detail) {  //如果是IE用detail获取距离
            return -evt.detail * 30;
        }
    }
[/code]

**PS ：通过浏览器检测可以确定火狐只执行DOMMouseScroll。**

**DOMContentLoaded
事件和readystatechange事件，有关DOM加载方面的事件，关于这两个事件的内容非常多且繁杂，我们先点明在这里，在项目课程中使用的时候详细讨论。**

