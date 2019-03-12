---
layout: post
title: " 第二百四十七节，Bootstrap按钮和折叠插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap按钮和折叠插件**



**学习要点：**

**1.按钮**

**2.折叠**



**本节课我们主要学习一下 Bootstrap 中的按钮和折叠插件。**



**一．按钮**

**可以通过按钮插件创建不同状态的按钮，也就是点击后为选中状态颜色加深，需要再次点击后后取消选中状态，颜色还原**

**单个切换**



**data-toggle="button"绑定按钮事件，写在按钮button元素里，点击后选中或取消选中按钮(Bootstrap)**  
 **autocomplete="off"多次页面加载时按钮可能保持表单的禁用或选择状态。解决方案是：添加
autocomplete="off"。(Bootstrap)**

[code]

     <button class="btn btn-primary" data-toggle="button" autocomplete="off">单个切换</button>
[/code]

**点击前未选中颜色**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504162303101-708407259.png)**



**点击后选中颜色**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504162326070-1649975298.png)**



**再次点击后取消选中颜色**

**![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504162356820-1339463183.png)**





**单选按钮，也就是按钮式单选框**

**btn-group样式class类，写在包含多个按钮 <div>里，设置群组多个按钮为一组(Bootstrap)**  
 **data-toggle="buttons"按钮事件，写在群组div里，表示群组按钮事件，点击后选中当前按钮(Bootstrap)**  
 **label单选框或多选框按钮标签，设置群组单选框或多选框时用此标签代替button标签，转换成按钮(Bootstrap)**  
 **active样式class类，写在 <label>里，设置群组里的当前按钮为首选(Bootstrap)**  
 **for="nan"为当前元素所绑定的元素id(Bootstrap)**

[code]

     <div class="btn-group" data-toggle="buttons">
        <label for="nan" class="btn btn-primary active">
            <input id="nan" type="radio" name="sex" autocomplete="off" checked> 男
        </label>
        <label for="nv" class="btn btn-primary">
            <input id="nv" type="radio" name="sex" autocomplete="off"> 女
        </label>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504164710961-144430477.gif)





**按钮式复选框**

**复选框和单选框一样的只是type属性值不一样而已**

[code]

     <div class="btn-group" data-toggle="buttons">
        <label for="yy" class="btn btn-primary active">
            <input id="yy" type="checkbox" name="fa" autocomplete="off" checked>音乐
        </label>
        <label for="ty" class="btn btn-primary">
            <input id="ty" type="checkbox" name="fa" autocomplete="off"> 体育
        </label>
        <label for="msh" class="btn btn-primary">
            <input id="msh" type="checkbox" name="fa" autocomplete="off"> 美术
        </label>
        <label for="dl" class="btn btn-primary">
            <input id="dl" type="checkbox" name="fa" autocomplete="off"> 电脑
        </label>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504170109742-669087332.gif)







**加载状态 **按钮****

****加载状态按钮必须结合js****

****data-loading-text="上传中请稍后..."设置加载状态按钮点击后提示内容，按钮元素里，点击后提示的内容(Bootstrap)****



[code]

    <button id="myButton" type="button" data-loading-text="上传中请稍后..." class="btn btn-primary" autocomplete="off">
        上传文件
    </button>
[/code]



**js**

[code]

    $( function () {
        $("a,input,button").focus(function () {         //获取到所有的a,input,button标签执行聚集光标事件
            this.blur()                                 //当聚集光标时，去除虚线边框
        });
    
        $('#myButton').on('click', function () {        //获取到加载状态按钮，执行点击事件
            var btn = $(this).button('loading');        //点击后执行loading方法，即html里的data-loading-text="上传中请稍后..."
            setTimeout(function () {                    //计时器等待1秒
                btn.button('reset');                    //执行reset方法，还原初始状态
            }, 1000);
        });
    });
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504180731226-1134833543.gif)





**按钮方法中有三个参数：**

**button()按钮方法，将按钮元素执行按钮方法**

**toggle将按钮元素绑定按钮事件(Bootstrap)**  
 **reset将按钮元素还原初始状态(Bootstrap)**  
 **string自定义字符串，设置加载状态按钮提示内容(Bootstrap)**

[code]

     <button id="myButton" type="button" data-zdyixx-text="上传中请稍后..." class="btn btn-primary" autocomplete="off">
        上传文件
    </button>
[/code]

**js**



[code]

    $(function () {
        $("a,input,button").focus(function () {         //获取到所有的a,input,button标签执行聚集光标事件
            this.blur();                                 //当聚集光标时，去除虚线边框
        });
    
        $('#myButton').on('click', function () {        //获取到按钮指定点击事件
            //$(this).button('toggle');                 //点击后执行按钮方法
            $(this).button('zdyixx');                   //执行自定义提示信息，即html里data-zdyixx-text="上传中请稍后..."
            setTimeout(function () {                    //计时器等待1秒
                $('#myButton').button('reset');         //执行reset方法，还原初始状态
            }, 1000);
        })
    
    });
[/code]



![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504183149773-432922686.gif)

** **





**二．折叠**

**通过点击可以折叠内容。**

**基本实例**

**data-toggle="collapse"设置按钮折叠事件，写在按钮元素里，点击后执行折叠事件(Bootstrap)**  
 **data-target="#content"指向折叠区块id，写在按钮元素里，将按钮与折叠内容区块关联(Bootstrap)**  
 **collapse样式class类，写在折叠区块 <div>里，设置折叠区块样式(Bootstrap)**  
 **well样式class类，写在折叠内容区块 <div>里，设置折叠内容区块嵌入样式(Bootstrap)**

[code]

    <button class="btn btn-primary" data-toggle="collapse" data-target="#content">
        Bootstrap
    </button>
    <div class="collapse" id="content">
        <div class="well">
            Bootstrap 是 Twitter 推出的一个用于前端开发的开源工具包。它由
            Twitter 的设计师 Mark Otto 和 Jacob Thornton 合作开发,是一个 CSS/HTML 框架。目
            前,Bootstrap 最新版本为 3.0 。
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504185723507-575096091.png)





**手风琴折叠**



**panel-group样式class类，面板容器 <div>里，设置一个面板容器区块(Bootstrap)**  
 **panel样式class类，写在面板组件 <div>元素里，声明面板组件div(Bootstrap)**  
 **panel-default样式class类，写在面板组件 <div>元素里，设置面板组件默认样式(Bootstrap)**  
 **panel-heading样式class类，写在面板组件里头部 <div>元素里，设置面板组件头部样式(Bootstrap)**  
 **panel-title样式class类，写在面板组件里头部 <h1-h4>元素里，设置面板组件头部标题样式(Bootstrap)**  
 **panel-collapse样式class类，写在面板组件里的内容区块 <div>元素里，设置折叠内容区域容器(Bootstrap)**  
 **collapse样式class类，写在面板组件里的内容区块 <div>元素里，设置折叠内容区域样式(Bootstrap)**  
 **in样式class类，写在面板组件里的内容区块 <div>元素里，设置当前折叠内容区域为默认展开效果(Bootstrap)**  
 **将标题里的a标签地址等于内容区域的id进行关联,(Bootstrap)**  
 **data-parent="#accordion"写在标题里的a标签里，值是折叠面板容器的id，将折叠面板容器与标题a标签关联(Bootstrap)**  
 **data-toggle="collapse"折叠事件，写在标题里的a标签，点击a标签后执行折叠事件(Bootstrap)**

[code]

     <div class="panel-group" id="accordion">
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseOne" data-toggle="collapse" data-parent="#accordion">点击我进行展示，再点击我进行折叠，第一部分</a>
                </h4>
            </div>
            <div id="collapseOne" class="panel-collapse collapse in">
                <div class="panel-body">
                    这里是第一部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseTwo" data-toggle="collapse" data-parent="#accordion">点击我进行展示，再点击我进行折叠，第二部分</a>
                </h4>
            </div>
            <div id="collapseTwo" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第二部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseThree" data-toggle="collapse" data-parent="#accordion">点击我进行展示，再点击我进行折叠，第三部分</a>
                </h4>
            </div>
            <div id="collapseThree" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第三部分。
                </div>
            </div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504202822242-1742765646.gif)





**折叠属性**

**data-parent 默认值为 false，设置需指定父元素选择器。也就是说，选定其中一个折叠区，其他折叠将隐藏，实现手风琴效果。**

**data-toggle 如果前面加 data-*，设置' collapse'表示实现折叠；如果是 JavaScript 中的属性，默认为
true，实现反转**

[code]

    <div class="panel-group" id="accordion">
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseOne" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第一部分</a>
                </h4>
            </div>
            <div id="collapseOne" class="panel-collapse collapse in">
                <div class="panel-body">
                    这里是第一部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseTwo" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第二部分</a>
                </h4>
            </div>
            <div id="collapseTwo" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第二部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseThree" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第三部分</a>
                </h4>
            </div>
            <div id="collapseThree" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第三部分。
                </div>
            </div>
        </div>
    </div>
[/code]

**js**



[code]

    $(function () {
        $("a,input,button").focus(function () {         //获取到所有的a,input,button标签执行聚集光标事件
            this.blur();                                 //当聚集光标时，去除虚线边框
        });
    
        $('#collapseOne,#collapseTwo,#collapseThree').collapse({        //获取所有标题a标签id执行折叠方法
            parent: '#accordion',       //将a标签与折叠容器id关联
            toggle: false,              //false默认项展开，true默认项折叠
        });
    });
[/code]









**折叠方法，方法还提供了三个参数：hide、show、toggle。**

**collapse()折叠方法，将折叠容器里的折叠内容区块执行折叠方法(Bootstrap)**

**hide折叠方法参数，将内容折叠(Bootstrap)**  
 **show折叠方法参数，将内容展开(Bootstrap)**  
 **toggle折叠方法参数，反转折叠和展开(Bootstrap)**

[code]

    $( function () {
        $("a,input,button").focus(function () {         //获取到所有的a,input,button标签执行聚集光标事件
            this.blur();                                 //当聚集光标时，去除虚线边框
        });
    
        $('#collapseOne').collapse('hide');
        $('#collapseTwo').collapse('show');
        $('button').on('click', function () {
            $('#collapseOne').collapse('toggle');
        });
    });
[/code]





**折叠事件，Collapse 插件中事件有四种。**

**show.bs.collapse 在 show 方法调用时立即触发(Bootstrap)**  
 **shown.bs.collapse 折叠区完全显示出来是触发(Bootstrap)**  
 **hide.bs.collapse 在 hide 方法调用时触发(Bootstrap)**  
 **hidden.bs.collapse 该事件在折叠区域完全隐藏之后触发(Bootstrap)**

**js**

[code]

    $( function () {
        $("a,input,button").focus(function () {         //获取到所有的a,input,button标签执行聚集光标事件
            this.blur();                                 //当聚集光标时，去除虚线边框
        });
    
        $('#collapseOne').on('show.bs.collapse', function () {      //获取到折叠内容区块执行事件
            alert('在 show 方法调用时立即触发');
        });
        $('#collapseOne').on('shown.bs.collapse', function () {
            alert('折叠区完全显示出来是触发');
        });
        $('#collapseOne').on('hide.bs.collapse', function () {
            alert('在 hide 方法调用时触发');
        });
        $('#collapseOne').on('hidden.bs.collapse', function () {
            alert('该事件在折叠区域完全隐藏之后触发');
        });
    });
[/code]

**HTML**

[code]

     <div class="panel-group" id="accordion">
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseOne" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第一部分</a>
                </h4>
            </div>
            <div id="collapseOne" class="panel-collapse collapse in">
                <div class="panel-body">
                    这里是第一部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseTwo" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第二部分</a>
                </h4>
            </div>
            <div id="collapseTwo" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第二部分。
                </div>
            </div>
        </div>
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4 class="panel-title">
                    <a href="#collapseThree" data-toggle="collapse">点击我进行展示，再点击我进行折叠，第三部分</a>
                </h4>
            </div>
            <div id="collapseThree" class="panel-collapse collapse">
                <div class="panel-body">
                    这里是第三部分。
                </div>
            </div>
        </div>
    </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170504213345820-572705633.png)



