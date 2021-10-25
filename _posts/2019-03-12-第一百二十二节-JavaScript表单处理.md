---
layout: post
title: " 第一百二十二节，JavaScript表单处理 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

## JavaScript表单处理

### 学习要点：

1.表单介绍

2.文本框脚本

3.选择框脚本

为了分担服务器处理表单的压力，JavaScript提供了一些解决方案，从而大大打破了处处依赖服务器的局面。

一．表单介绍

在HTML中，表单是由\<form>元素来表示的，而在JavaScript中，表单对应的则是HTMLFormElement类型。HTMLFormElement继承了HTMLElement，因此它拥有HTML元素具有的默认属性，并且还独有自己的属性和方法：

*HTMLFormElement属性和方法*

**属性或方法** | **说明**  
---|---  
**acceptCharset** | **服务器能够处理的字符集**  
**action** | **接受请求的URL**  
**elements** |**表单中所有控件的集合**  
**enctype** | **请求的编码类型**  
**length** | **表单中控件的数量**  
**name** |**表单的名称**  
**target** | **用于发送请求和接受响应的窗口名称**  
**reset()** | **将所有表单重置**  
**submit()** | **提交表单**  

**获取表单\<form>对象的方法有很多种，如下：**

``` javaScript
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var form =  document.getElementById('get');  //通过ID获取到表单form标签
        alert(form.tagName);  //打印出form标签
    
        var form2 = document.getElementsByTagName('form');  //通过标签名称获取到标签元素数组
        alert(form2[0].tagName); //通过数组下标，打印出form标签
    
        var form3 = document.rgj;  //通过name名称直接获取元素【不推荐】
        alert(form3.tagName);  //打印出form标签
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
```

**PS：最后一种方法使用name名称直接获取元素，已经不推荐使用，这是向下兼容的早期用法。问题颇多，比如有两个相同名称的，变成数组；而且这种方式以后有可能会不兼容。**

**forms属性，直接获取表单\<form>标签，后面可以跟下标获取指定的<form>标签，也可以跟name名称来获取指定的<form>标签**

**使用方式：**  
 **document.forms[下标或者name名称]**

```javaScript

     //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var form = document.forms[0];  //forms属性，直接获取表单<form>标签，后面可以跟下标获取指定的<form>标签，也可以跟name名称来获取指定的<form>标签
        alert(form.tagName);  //打印出标签名称
    
        var form2 = document.forms['rgj'];
        alert(form2.tagName);  //打印出标签名称
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
```

**onsubmit表单提交事件，当用户提交表单时激发函数**  
 **表单form对象.onsubmit = 执行函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button>提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var form = document.forms[0];  //forms属性，直接获取表单<form>标签，
        //onsubmit表单提交事件，当用户提交表单时激发函数
        addEvent(form,'submit',function () {
            alert('提交');  //当用户提交时打印提交
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
```

  **form对象可以阻止默认行为，阻止后无法提交表单**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button>提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var form = document.forms[0];  //forms属性，直接获取表单<form>标签，
        //onsubmit表单提交事件，当用户提交表单时激发函数
        addEvent(form,'submit',function (evt) {
            preDef(evt); //阻止form默认行为，阻止后不可以提交
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
```



**submit()方法，用来自定义提交方法，也就是可以用这个方法自定义提交元素**  
 **使用方式：**  
 **form对象.submit()**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button type="button">按钮</button>     这个是普通按钮不能提交，我们可以用submit()方法自定义成提交按钮
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        var an =  document.getElementById('an');  //通过id获取到普通按钮
        //给普通按钮添加一个点击事件，点击后执行匿名函数
        addEvent(an,'click',function () {
            get.submit();  //给表单添加提交方法
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
```

**  PS：在表单中尽量避免使用name="submit"或id="submit"等命名，这会和submit()方法发生冲突导致无法提交。**



**解决用户不停重复提交**

**提交数据最大的问题就是重复提交表单。因为各种原因，当一条数据提交到服务器的时候会出现延迟等长时间没反映，导致用户不停的点击提交，从而使得重复提交了很多相同的请求，或造成错误、或写入数据库多条相同信息。**

**有两种方法可以解决这种问题：第一种就是提交之后，立刻禁用点击按钮；第二种就是提交之后取消后续的表单提交操作。**

****第一种就是提交之后，立刻禁用点击按钮；只适用于按钮提交【不推荐】****

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button id="tj" type="submit">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //给form标签添加一个提交事件，提交后执行匿名函数
        addEvent(get,'submit',function () {
            //当第一个提交成功后，将提交按钮的disabled属性设置成true，禁止提交
            document.getElementById('tj').disabled = true;
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
```

****第二种就是提交之后取消后续的表单提交操作。适用于各种提交，【推荐】****

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button id="tj" type="submit">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        var jil = false;  //记录提交
        //给form标签添加一个提交事件，提交后执行匿名函数
        addEvent(get,'submit',function (evt) {
            //阻止表单默认行为，也就是阻止表单提交
            preDef(evt);
            //如果记录等于true，表示提交过了，直接退出
            if (jil == true) return;
            jil = true;  //如果没提交过，就改变记录
            get.submit();  //提交数据
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
```

**PS：在某些浏览器，F5只能起到缓存刷新的效果，有可能获取不到真正的源头更新的数据。那么使用ctrl+F5就可以把源头给刷出来。**



**重置表单**

**用户点击重置按钮时，表单会被初始化。虽然这个按钮还得以保留，但目前的Web已经很少去使用了。因为用户已经填写好各种数据，不小心点了重置就会全部清空，用户体验极差。**

**有两种方法调用reset事件，第一个就是直接type="reset"即可；第二个就是使用fm.reset()方法调用即可。**

**onreset事件，表单重置事件，当用户点击重置后激发函数**  
 **使用方式：**  
 **form对象.onreset = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button id="tj" type="submit">提交</button>
    //     <button id="zhzh" type="reset">重置</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //给form标签添加一个重置事件，当点击重置后激发函数
        addEvent(get,'reset',function () {
            alert('你点击了重置');
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
```

**reset()方法，自定义重置方法，可以用这个给表单设置一个重置**  
 **使用方式：**  
 **form对象.reset()**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button id="tj" type="submit">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //添加一个根元素点击事件，当在页面任意地方点击后执行函数
        addEvent(document,'click',function () {
            get.reset();  //执行重置方法，重置表单
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
```



**表单字段**

**如果想访问表单元素，可以使用之前章节讲到的DOM方法访问。但使用原生的DOM访问虽然比较通用，但不是很便利。表单处理中，我们建议使用HTML
DOM，它有自己的elements属性，该属性是表单中所有元素的集合。**

**elements属性，获取表单form元素里的表单字段，也就是form标签里的其他属于form的标签，主要只能获取到表单字段其他元素无效，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段，如果多个字段
**name值相同时返回相同 ** **name值的字段集合********  
 **使用方式：**  
 **form元素.elements**  
 **form元素.elements[下标或者name值]**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch">
    //     <button id="tj" type="submit">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        alert(get.elements);  //获取表单字段集合
        alert(get.elements[0]);  //通过下标获取表单里的第一个元素
        alert(get.elements['mch']); //通过name值获取第一个元素
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
```



**共有的表单字段属性**

**除了\<fieldset>元素之外，所有表单字段都拥有相同的一组属性。由于<input>类型可以表示多种表单字段，因此有些属性只适用于某些字段。以下罗列出共有的属性：**



**属性或方法**|**说明**  
  ---|---  
  **disabled**|**布尔值，表示当前字段是否被禁用**  
  **form**|**指向当前字段所属表单的指针，只读**  
  **name**|*当前字段的名称**  
  **readOnly**|**布尔值，表示当前字段是否只读**  
  **tabIndex**|**表示当前字段的切换**  
  **type**|**当前字段的类型**  
  **value**|**当前字段的值**  
  
  **重点看几个最常用的，其他使用方式相同**
  
  **value属性，获取或设置当前元素的value值**  
  
  **使用方式：**  
  
  **当前元素.value**  
  
  **当前元素.value = 'xxxx'**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        alert(mch.value);  //获取当前元素的value值
        mch.value = '默认值2'; //设置当前元素的value值
    
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
```



**form属性，获取当前元素所属form标签**  
 **使用方式：**  
 **当前元素.form**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        alert(mch.form);  //form属性，获取当前元素所属form标签
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
```



**disabled属性，获取或者设置当前元素的，禁用当前字段**  
 **使用方式：**  
 **当前元素.disabled**  
 **当前元素.disabled = true**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        alert(mch.disabled);  //disabled属性，获取或者设置当前元素的，禁用当前字段
        mch.disabled = true; //设置禁用当前字段
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
```



**type属性，获取或者设置当前元素字段类型，【极不推荐】**  
 **使用方式：**  
 **当前元素.type**  
 **当前元素.type = 'xxx'**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        alert(mch.type);  //type属性，获取或者设置当前元素字段类型，
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
```

**  type属性获取返回属性值如下**

**除了\<fieldset>字段之外，所有表单字段都有type属性。对于<input>元素，这个值等于HTML属性的type值。对于非<input>元素，这个type的属性值如下：**

**元素说明**|**HTML标签**|**type属性的值**  
---|---|---  
**单选列表**|**< select>...</select>**|**select-one**  
**多选列表**|**< select multiple>...</select>**|**select-multiple**  
**自定义按钮**|**< button>...</button>**|**button**  
**自定义非提交按钮**|**< button type="button">...</button>**|**button**
**自定义重置按钮**|**< button type="reset">...</button>**|**reset**
**自定义提交按钮**|**< button type="submit">...</button>**|**submit**  

**PS：
\<input>和\<button>元素的type属性是可以动态修改的，而<select>元素的type属性则是只读的。(在不必要的情况下，建议不修改type)。**

**共有的表单字段方法**

**每个表单字段都有两个方法：foucs()和blur()。**

**方法**|**说明**  
---|---  
**focus()**|**将焦点定位到表单字段里**  
**blur()**|**从元素中将焦点移走**  
  
**focus()方法，将焦点定位到表单字段里**  
 **使用方式：**  
 **当前元素.focus()**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        mch.focus(); //focus()方法，将焦点定位到表单字段里
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
```



**blur()方法，从元素中将焦点移走**  
 **使用方式：**  
 **当前元素.blur()**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        mch.blur(); //blur()方法，从元素中将焦点移走
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
```

**共有的表单字段事件**

**表单共有的字段事件有以下三种：**

**事件名**|**说明**    
---|---  
**onblur**|**当字段失去焦点时触发**  
**onchange**|**对于 <input>和<textarea>元素，在改变value并失去焦点时触发；对于<select>元素，在改变选项时触发**  
**onfocus**|**当前字段获取焦点时触发**  

**onfocus事件，当前字段获取焦点时触发**  

 **使用方式：**  

 **当前元素.onfocus = 函数**

```html

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //给当前元素添加一个onfocus事件，当前字段获取焦点时触发
        addEvent(mch,'focus',function () {
            alert('获取焦点');
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
```



**onblur事件，当字段失去焦点时触发**  
 **使用方式：**  
 **当前元素.onblur = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //给当前元素添加一个事件，onblur事件，当字段失去焦点时触发
        addEvent(mch,'blur',function () {
            alert('失去焦点');
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
```



**onchange事件，对于 <input>和<textarea>元素，在改变value并失去焦点时触发；对于<select>元素，在改变选项时触发**  
 **使用方式：**  
 **当前元素.onchange = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="默认值">
    //     <button id="tj" type="submit" name="mch2">提交</button>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //给当前元素添加一个事件，onchange事件，对于<input>和<textarea>元素，在改变value并失去焦点时触发；对于<select>元素，在改变选项时触发
        addEvent(mch,'change',function () {
            alert('改变value并失去焦点');
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
```

**PS：关于blur和change事件的关系，并没有严格的规定。在某些浏览器中，blur事件会先于change事件发生；而在其他浏览器中，则恰好相反。**



**二．** **文本框脚本**

**在HTML中，有两种方式来表现文本框：一种是单行文本框 <input
type="text">，一种是多行文本框<textarea>。虽然<input>在字面上有value值，而<textarea>却没有，但通过都可以通过value获取他们的值。**

**获取单行文本框和多行文本框的 **value值****

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        var wb = get.elements['wb'];   //过name值获取到多行文本框
        alert(mch.value);  //获取单行文本框的value值
        alert(wb.value);  //获取多行文本框的value值
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
```

**PS：使用表单的value是最推荐使用的，它是HTML
DOM中的属性，不建议使用标准DOM的方法。也就是说不要使用getAttribute()获取value值。原因很简单，对value属性的修改，不一定会反映在DOM中。**



**除了value值，还有一个属性对应的是defaultValue，可以得到原本的value值，不会因为值的改变而变化。**

**defaultValue属性，获取表单原本的value值，不会因为值的改变而变化。**  
 **使用方式：**  
 **当前元素.defaultValue**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        mch.value = '修改';  //修改了value值
        alert(mch.value);   //获取到文本框的value值
        alert(mch.defaultValue);   //defaultValue属性，获取表单原本的value值，不会因为值的改变而变化。
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
```



**select()方法，将当前文本框里的文本选中，**  
 **使用方式：**  
 **当前元素.select()**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        mch.select();  //select()方法，将当前文本框里的文本选中，
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
```



**选择部分文本**

**在使用文本框内容的时候，我们有时要直接选定部分文本，这个行为还没有标准。Firefox的解决方案是：setSelectionRange()方法。这个方法接受两个参数：索引和长度。**

**setSelectionRange()方法,选择文本框里指定范围的文本，这个方法接受两个参数：索引和长度。开始位置，选择几位,IE9以下不支持**  
 **使用方式：**  
 **当前对象.setSelectionRange(开始位置，选择几位)**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //setSelectionRange()方法,选择文本框里指定范围的文本，这个方法接受两个参数：索引和长度。开始位置，选择几位
        mch.setSelectionRange(0,3);
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
```

**除了IE，其他浏览器都支持这种写法(IE9+支持)**



**IE9以下想要选择部分文本，可以使用IE的范围操作。**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window,'load',function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        var range = mch.createTextRange();        //创建一个文本范围对象
        range.collapse(true);                    //将指针移到起点
        range.moveStart('character', 0);            //移动起点，character表示逐字移动
        range.moveEnd('character', 1);                //移动终点，同上
        range.select();                                //焦点选定
    
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
```



**结合上面兼容浏览器方案**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        getSelectText(mch,1,4); //执行选择文本框里指定范围的文本函数
    
        //浏览器兼容，执行选择文本框里指定范围的文本函数
        function getSelectText(text, start, num) {  //接收3个参数，参数1元素对象。参数2开始位置，参数3获取结束位置
            if (text.setSelectionRange) {
                text.setSelectionRange(start, num);
                text.focus();
            } else if (text.createTextRange) {
                var range = text.createTextRange();        //创建一个文本范围对象
                range.collapse(true);                    //将指针移到起点
                range.moveStart('character', start);            //移动起点，character表示逐字移动
                range.moveEnd('character', num - start);                //移动终点，同上
                range.select();
            }
        }
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
```



**onselect事件，选中文本框文本后触发**  
 **使用方式：**  
 **元素对象.onselect = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //onselect事件，选中文本框文本后触发
        addEvent(mch,'select',function () {
            alert('选择文本');
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
```



**取得选择的文本**

**如果我们想要取得选择的那个文本，就必须使用一些手段。目前位置，没有任何规范解决这个问题。Firefox为文本框提供了两个属性：selectionStart和selectionEnd。**

**selectionStart属性，获取在文本框选择文本的起始位置，IE9以下不支持**  
 **selectionEnd属性，获取在文本框选择文本的结束位置，IE9以下不支持**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        //onselect事件，选中文本框文本后触发
        addEvent(mch,'select',function () {
            alert(mch.selectionStart);  //selectionStart属性，获取在文本框选择文本的起始位置
            alert(mch.selectionEnd);   //selectionEnd属性，获取在文本框选择文本的结束位置
            //获取到对象的value值，在用字符串截取函数，将鼠标选择的起始位置和结束位置，传入函数截取到选择的字符串
            alert(this.value.substring(this.selectionStart, this.selectionEnd));
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
```



**除了IE，其他浏览器均支持这两个属性（IE9+已支持）。IE不支持，而提供了另一个方案：selection对象，属于document。这个对象保存着用户在整个文档范围内选择的文本信息。导致我们需要做浏览器兼容。**

****selection对象，属于document。这个对象保存着用户在整个文档范围内选择的文本信息**** ** **，IE支持****

****createRange().text，获取 ** **范围内选择的文本信息， ** **IE支持************

**取得选择的文本浏览器兼容**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <p id="p"></p>
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var mch = get.elements['mch'];  //通过name值获取到第一个表单字段
        var p = document.getElementById('p');  //通过ID获取p元素标签
        //onselect事件，选中文本框文本后触发
        addEvent(mch,'select',function (){
            //p元素的文本内容等于执行自定义兼容选择文本函数，将文本框元素传入函数
            p.innerHTML = getSelect(mch);
        });
    });
    
    //取得选择的文本浏览器兼容
    function getSelect(text) {  //接收元素对象
        //判断浏览器如果支持selectionStart属性
        if (typeof text.selectionStart == 'number') {  //说明不是IE
            //获取到对象的value值，在用字符串截取函数，将鼠标选择的起始位置和结束位置，传入函数截取到选择的字符串
            return text.value.substring(text.selectionStart, text.selectionEnd);
        } else if (document.selection) {  //说明是IE
            return document.selection.createRange().text;
        }
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
```

**PS：有一个最大的问题，就是IE在触发select事件的时候，在选择一个字符后立即触发，而其他浏览器是选择想要的字符释放鼠标键后才触发。所以，如果使用alert()的话，导致跨浏览器的不兼容。我们没有办法让浏览器行为保持统一，但可以通过不去使用alert()来解决。**


**过滤输入**

**为了使文本框输入指定的字符，我们必须对输入进的字符进行验证。有一种做法是判断字符是否合法，这是提交后操作的。那么我们还可以在提交前限制某些字符键，**

****屏蔽某些字符键，让用户不能输入不合法的字符，比如屏蔽除数字键外的字符键，这样用户就只能输入数字****

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
    
        //屏蔽非数字键的输入
        addEvent(wb, 'keypress', function (evt) {  //给文本框添加一个键盘按键事件，当按下键盘按键时激发函数
            //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
            var e = evt || window.event;
            var anjbm = getCharCode(e);  //执行自定义夸浏览器获取按键的编码函数
            var anj = String.fromCharCode(anjbm); //将按键的编码转换成对应的按键字符
            if (!/\d/.test(anj) && e.charCode > 8){  //正则判断如果输入的不是数字，并且字符键所代表字符的ASCII编码大于8
                preDef(evt); //阻止默认行为，也就是不能输入，只能输入数字
            }
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
    
    //夸浏览器获取按键的编码
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
```

```

    if (!/\d/.test(anj) && e.charCode > 8)
```

**PS：前半段条件判断只有数字才可以输入，导致常规按键，比如光标键、退格键、删除键等无法使用。部分浏览器比如Firfox，需要解放这些键，而非字符触发的编码均为0；在Safari3之前的浏览器，也会被阻止，而它对应的字符编码全部为8，所以最后就加上charCode> 8的判断即可。**

**PS：当然，这种过滤还是比较脆落的，我们还希望能够阻止裁剪、复制、粘贴和中文字符输入操作才能真正屏蔽掉这些。**

**剪贴板事件**

**如果要阻止裁剪、复制和粘贴，那么我们可以在剪贴板相关的事件上进行处理，JavaScript提供了六组剪贴板相关的事件：**

**事件名**|**说明**  
---|---  
**copy**|**在发生复制操作时触发**  
**cut**|**在发生裁剪操作时触发**  
**paste**|**在发生粘贴操作时触发**  
**beforecopy**|**在发生复制操作前触发**  
**beforecut**|**在发生裁剪操作前触发**  
**beforepaste**|**在发生粘贴操作前触发**  
  
**由于剪贴板没有标准，导致不同的浏览器有不同的解释。Safari、Chrome和Firefox中，凡是before前缀的事件，都需要在特定条件下触发。而IE则会在操作时之前触发带before前缀的事件。**

**如果我们想要禁用裁剪、复制、粘贴，那么只要阻止默认行为即可。**

**oncut事件，在发生剪切操作时触发**  
 **使用方式：**  
 **元素对象.oncut = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
        //oncut事件，在发生剪切操作时触发
        addEvent(wb,'cut',function () {
            alert('在发生剪切操作时触发');
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
```

**阻止用户剪切行为**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
        //oncut事件，在发生剪切操作时触发
        addEvent(wb,'cut',function (evt) {  //接收event对象
            preDef(evt);  //阻止默认行为
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
```



**oncopy事件，在发生复制操作时触发**  
 **使用方式：**  
 **元素对象.oncopy = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
        //oncopy事件，在发生复制操作时触发
        addEvent(wb,'copy',function (evt) {  //接收event对象
            preDef(evt);  //阻止默认行为,不允许复制
            alert('阻止了复制行为')
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
```

**onpaste事件，在发生粘贴操作时触发**  
 **使用方式：**  
 **元素对象.onpaste = 函数**

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
        //onpaste事件，在发生粘贴操作时触发
        addEvent(wb,'paste',function (evt) {  //接收event对象
            preDef(evt);  //阻止默认行为,不允许粘贴
            alert('阻止了粘贴行为');
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
```

**当我们裁剪和复制的时候，我们可以访问剪贴板里的内容，但问题是FireFox，Opera浏览器不支持访问剪贴板。并且，不同的浏览器也有自己不同的理解。所以，这里我们就不在赘述。**



**文本框屏蔽中文输入法**

**最后一个问题影响到可能会影响输入的因素就是：输入法。我们知道，中文输入法，它的原理是在输入法面板上先存储文本，按下回车就写入英文文本，按下空格就写入中文文本。**

**有一种解决方案是通过CSS来禁止调出输入法：**

```

    style="ime-mode:disabled"                     //CSS直接编写
    元素对象.style.imeMode = 'disabled';            //或在JS里设置也可以
```

**PS：但我们也发先，Chrome浏览器却无法禁止输入法调出。所以，为了解决谷歌浏览器的问题，最好还要使用正则验证已输入的文本。**



****使用正则验证已输入的文本【推荐】****

```

     // <form id="get" name="rgj">
    //     用户名:<input type="text" name="mch" value="单行文本框">
    //     <textarea name="wb">多行文本框</textarea>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var wb = get.elements['wb'];  //通过name值获取到多行文本框
        //onkeyup：当用户释放键盘上的键触发
        addEvent(wb,'keyup',function (evt) {  //接收event对象
            if(/[^\d]/g.test(wb.value)){  //正则匹配判断当用户输入非数字时
                alert('请输入数字！');
            }
            wb.value = wb.value.replace(/[^\d]/g, '');    //正则匹配当用户输入的是非数字时，把非数字都替换成空
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
```



**自动切换焦点**

**为了增加表单字段的易用性，很多字段在满足一定条件时(比如长度)，就会自动切换到下一个字段上继续填写。**

```

     // <form id="get" name="rgj">
    //  <input type="text" name="user1" maxlength="1" />    //只能写1个
    //     <input type="text" name="user2" maxlength="2" />    //只能写2个
    //     <input type="text" name="user3" maxlength="3" />    //只能写3个
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        //给指定元素添加一个键盘事件，当按键释放时激发自定义函数
        addEvent(get.elements['user1'], 'keyup', tabforward);
        addEvent(get.elements['user2'], 'keyup', tabforward);
        addEvent(get.elements['user3'], 'keyup', tabforward);
    
        //自定义函数，当用户输入到指定位字符后。自动切换焦点
        function tabforward(evt) {   //接收event对象
            //如果不能执行evt，说明是IE浏览器就用window.event获取event对象
            var e = evt || window.event;
            //判断元素的value长度，如果等于maxlength设置的长度
            if (this.value.length == this.maxLength) {
                //遍历所有字段
                for (var i = 0; i < get.elements.length; i++) {
                    //找到当前字段
                    if (get.elements[i] == this) {
                        if (this.maxLength == get.elements.length) {
                            //中途返回
                            return;
                        }
                        //就把焦点移入下一个
                        get.elements[i + 1].focus();
                    }
                }
            }
        }
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
```



**三．** **选择框脚本**

**选择框是通过
<select>和<option>元素创建的，除了通用的一些属性和方法外，HTMLSelectElement类型还提供了如下的属性和方法：**

**HTMLSelectElement对象（ <select>元素的属性）**

**属性/方法**|**说明**  
---|---  
**add(new,rel)**|**插入新元素，并指定位置**  
**multiple**|**布尔值，是否允许多项选择**  
**options**|**< option>元素的HTMLColletion集合**  
**remove(index)**|**移除给定位置的选项**    
**selectedIndex**|**基于0的选中项的索引，如果没有选中项，则值为-1**  
**size**|**选择框中可见的行数**  

**在DOM中，每个 <option>元素都有一个HTMLOptionElement对象，以便访问数据，这个对象有如下一些属性：**

**HTMLOptionElement对象（ <option>元素的属性）**

**属性**|**说明**  
---|---  
**index**|**当前选项在options集合中的索引**  
**label**|**当前选项的标签**  
**selected**|**布尔值，表示当前选项是否被选中**  
**text**|**选项的文本**  
**value**|**选项的值**  
  
**options属性，获取 <select>元素里的<option>标签集合**  
 **使用方式：**  
 **select元素.options**  
 **select元素.options[0] 通过下标获取到集合里指定的 <option>标签**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //options属性，获取<select>元素里的<option>标签集合
        alert(xz.options);
        alert(xz.options[0]); //通过下标获取到指定的<option>标签
        alert(xz.options[0].value); //获取指定<option>标签里的value值
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
```



**type属性，获取 <select>元素是多选还是单选，返回元素标签的multiple属性值**  
 **使用方式：**  
 **select元素.type**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //type属性，获取<select>元素是多选还是单选，返回元素标签的multiple属性值
        alert(xz.type);
        //select-one  //表示multiple属性值是单选
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
```

**PS：选择框里的type属性有可能是：select-one，也有可能是：select-
multiple，这取决于HTML代码中有没有multiple属性。**



**获取选择框 <option>标签元素的value值和文本**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //options属性，获取<select>元素里的<option>标签集合
        //获取选择框<option>标签元素的value值和文本
        alert(xz.options[0].value + xz.options[0].text);
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
```

**PS：操作select时，最好使用HTML DOM，因为所有浏览器兼容的很好。而如果使用标准DOM，会因为不同的浏览器导致不同的结果。**

**PS：当选项没有value值的时候，IE会返回空字符串，其他浏览器会返回text值。**



**选择选项**  
 **onchange事件，当 <select>元素选择框发生改变时激发函数**  
 **使用方式：**  
 **< select>元素.onchange = 函数**

**selectedIndex属性，获取 <select>元素当前选项的索引位置，如果是多项选择，他始终返回的是第一个项。**  
 **使用方式：**  
 **< select>元素.selectedIndex**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //onchange事件，当<select>元素选择框发生改变时激发函数
        addEvent(xz, 'change', function () {
            //selectedIndex属性，获取<select>元素当前选项的索引位置
            alert(xz.selectedIndex);
            alert(this.options[this.selectedIndex].text);    //得到当前选项的text值
            alert(this.options[this.selectedIndex].value);    //得到当前选项的value值
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
```

**selectedIndex属性还有一个用法，就是给 **< select>元素定位一个选项 **

****使用方式：****

********< select>元素. **selectedIndex = 选项索引**********

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //selectedIndex属性还有一个用法，就是给<select>元素定位一个选项
        xz.selectedIndex = 2;  //将选择的第二个索引定位为默认选项
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
```



**selected属性，判断指定的 <option>标签是否是默认选项，返回布尔值，也可以通过selected = true
设置option当前元素为默认选项**  
 **使用方式：**  
 **option元素.selected**  
 **option元素.selected = true**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        var sy = xz.options[2]; //获取第二个<option>元素
        //selected属性，判断指定的<option>标签是否是默认选项，返回布尔值，也可以通过selected = true 设置option当前元素为默认选项
        alert(sy.selected); //查看当前<option>标签是否是默认选项，返回布尔值
        sy.selected = true; //设置当前<option>标签为默认选项
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
```

**而selected和selectedIndex在用途上最大的区别是，selected是返回的布尔值，所以一般用于判断上；而selectedIndex是数值，一般用于设置和获取。**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //给<select>标签添加一个事件，当选项改变时激发函数
        addEvent(xz, 'change', function () {
            //判断第3个选项被选中时
            if (this.options[2].selected == true) {
                alert('是默认选项！');
            }
        });
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
```



**添加选项**

**如需动态的添加选项我们有两种方案：DOM和Option构造函数。**

**DOM方式添加选项**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        var option = document.createElement('option');  //创建一个元素节点
        var text = document.createTextNode('北京t');  //创建一个文本节点
        option.appendChild(text); //将文本添加到新创建的元素节点中
        option.setAttribute('value', '北京v');  //设置元素的属性值
        xz.appendChild(option); //将新创建的元素节点添加到<select>标签的子元素末尾
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
```



**使用Option构造函数 **添加选项****

**Option()构造函数，构造一个\<option>标签元素节点，IE9以下不支持，IE9以下 **Option()函数构造的 **\<option>标签元素节点，不支持appendChild()添加，【不推荐appendChild()添加】******  
 **使用方式：**  
 **变量 = new Option( **'text值',** 'value值');**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //Option()构造函数，构造一个<option>标签元素节点
        var option = new Option('t', '北京v');
        //将构造的<option>标签元素节点，添加到<select>标签的子元素末尾
        xz.appendChild(option);     //IE出现bug
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
```



**add()方法,用来添加Option()函数构造的\<option>标签元素节点到<select>标签里,第一个参数Option()函数构造变量，参数二要添加的索引位置【推荐】IE9以下也支持**  
 **使用方式：**  
 **< select>标签.add(Option()函数构造变量，要添加的索引位置)**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
        //Option()构造函数，构造一个<option>标签元素节点
        var option = new Option('自贡t', '自贡v');
        //add()方法,用来添加Option()函数构造的<option>标签元素节点到<select>标签里
        xz.add(option,0); //0，表示添加到第一位
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
```

**PS：在DOM规定，add()中两个参数是必须的，如果不确定索引，那么第二个参数设置null即可，即默认移入最后一个选项。但这是IE中规定第二个参数是可选的，所以设置null表示放入不存在的位置，导致失踪，为了兼容性，我们传递undefined即可兼容。**

```

    xz.add(option,  null);                        //IE不显示了
    xz.add(option, undefined);                    //兼容了
```



**移除选项**

**有三种方式可以移除某一个选项：DOM移除、remove()方法移除和null移除。**

**remove()方法，移除 <select>标签里指定的<option>选项,参数<option>选项的索引位置【推荐】**  
 **使用方式：**  
 **select标签.remove( <option>选项的索引位置)**

```

    // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到<select>标签
    
        //removeChild删除节点里指定的子节点，获取<select>标签里的指定options传入方法
        //xz.removeChild(xz.options[0]);                //DOM移除
    
        //remove()方法，移除<select>标签里指定的<option>选项,参数<option>选项的索引位置【推荐】
        xz.remove(3);                            //remove()移除，推荐
    
        //获取到<option>选项设置为null
        //xz.options[0] = null;                        //null移除
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
```

**PS：当第一项移除后，下面的项，往上顶，所以不停的移除第一项，即可全部移除。**





**移动选项**

**如果有两个选择框，把第一个选择框里的第一项移到第二个选择框里，并且第一个选择框里的第一项被移除。**

```

     // <form id="get" name="rgj">
    //     <select name="xz" size="5">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option value="昆明v">昆明t</option>
    //     </select>
    //     <select name="xz2" size="5">
    //         <option>无</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到第一个<select>标签
        var xz2 = get.elements['xz2'];  //通过name值获取到第二个<select>标签
        //给第一个<select>标签添加一个点击事件，点击后激发函数
        addEvent(xz,'click',function () {
            //xz.selectedIndex获取到第一个<select>标签的当前选项的索引
            //xz.options[]通过索引获取到当前选项，将当前选项添加到第二个<select>标签里
            xz2.appendChild(xz.options[xz.selectedIndex]);
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
```



**排列选项**

**选择框提供了一个index属性，可以得到当前选项的索引值，和selectedIndex的区别是，一个是选择框对象的调用，一个是选项对象的调用。**

**index属性，获取 <option>标签当前元素的索引**  
 **使用方式**  
 **option元素.index**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option value="昆明v">昆明t</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到第一个<select>标签
        alert(xz.options[1].index);
        //返回1
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
```

**排序选项**

```

     // <form id="get" name="rgj">
    //     <select name="xz">
    //         <option value="上海v">上海t</option>
    //         <option value="杭州v">杭州t</option>
    //         <option value="南京v">南京t</option>
    //         <option value="昆明v">昆明t</option>
    //     </select>
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var xz = get.elements['xz'];  //通过name值获取到第一个<select>标签
        var option = xz.options[1];  //获取第二个option标签选项
        //insertBefore将一个节点添加到，指定节点的前面。第一个参数是要添加的节点，第二个参数是要在它之前添加节点的目标节点
        //将第二个节点移动添加到，第一个节点前
        xz.insertBefore(option, xz.options[option.index - 1]);        
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
```



**单选按钮和复选框**

**checked属性，判断指定单选框或复选框是否被选中，返回布尔值**  
 **使用方式**  
 **指定单选框或复选框元素.checked**

```

     // <form id="get" name="rgj">
    //     音乐：<input type="checkbox" name="yse" value="5">
    //     体育：<input type="checkbox" name="yse" value="6">
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var checkbox = get.elements['yse']; //通过name值获取到所有的单选框
        alert(checkbox[0].checked);  //判断指定点选框是否被选中，返回布尔值
    
        //循环所有单选框，打印出被选中表单的value值
        //根据所有单选框的长度循环次数
        for (var i = 0; i < checkbox.length; i++) {            //循环单选按钮
            //判断每次循环到的单选框checked属性等于true，就表示此单选框被选中
            if (checkbox[i].checked == true) {            //遍历每一个找出选中的那个
                //打印出被选中的单选框的value值
                alert(checkbox[i].value);                //得到值
            }
        }
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
```

**defaultChecked属性，判断指定单选框或复选框是否是被默认选中，它获取的是原本HTML的默认选中checked属性值，而不会因为点击而改变。**  
 **使用方式：**  
 **指定单选框或复选框元素.defaultChecked**

```

     // <form id="get" name="rgj">
    //     音乐：<input type="checkbox" name="yse" value="5">
    //     体育：<input type="checkbox" name="yse" value="6">
    // </form>
    
    //添加事件当页面加载完成后激发函数
    addEvent(window, 'load', function () {
        var get = document.getElementById('get');  //通过ID获取到form标签
        //elements属性，获取表单form元素里的表单字段，返回表单字段集合，后面可以跟字段下标，获取指定字段，也可以跟name值获取指定字段
        var checkbox = get.elements['yse']; //通过name值获取到所有的单选框
        alert(checkbox[0].defaultChecked); //判断单选框是否为默认选择
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
```



