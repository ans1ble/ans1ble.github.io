---
layout: post
title: " 第二百三十二节，Bootstrap排版样式 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap排版样式**



**学习要点：**

**1.页面排版**



**本节课我们主要学习一下 Bootstrap 全局 CSS 样式中的排版样式，包括了标题、页面 主体、对齐、列表等常规内容。**



**一．页面排版**

**Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。**

**1.页面主体**

**Bootstrap 将全局**

**font-size 设置为 14px，line-height 行高设置为 1.428(即 20px)；**

**< p>段落元素被设置等于 1/2 行高(即 10px)；颜色被设置为#333。**

**lead样式class类，语气加重，字体加粗大点(Bootstrap)**

[code]

     <p>Bootstrap 框架</p>
    <p class="lead">Bootstrap 框架</p>
    <p>Bootstrap 框架</p>
    <p>Bootstrap 框架</p>
    <p>Bootstrap 框架</p>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427162928850-1022523826.png)



**2.标题**

**我们从 Firebug 查看元素了解到，Bootstrap 分别对 h1 ~ h6 进行了 CSS 样式的重构，**

**< h1 ~ h6>标签样式(Bootstrap)**

[code]

    <h1>Bootstrap 框架</h1> //36px
    <h2>Bootstrap 框架</h2> //30px
    <h3>Bootstrap 框架</h3> //24px
    <h4>Bootstrap 框架</h4> //18px
    <h5>Bootstrap 框架</h5> //14px
    <h6>Bootstrap 框架</h6> //12px
[/code]

**并且还支持普通内联元素定义 class=(.h1 ~ h6)来实现相同的功能。**

[code]

     <span class="h1">Bootstrap</span>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427163826147-711883650.png)**

**注：通过 Firebug 查看元素还看到，字体颜色、字体样式、行高均被固定了，从而保
证了统一性，而原生的会根据系统内置的首选字体决定，颜色是最黑色。**



**在 h1 ~ h6 元素之间，还可以嵌入一个 small 元素作为副标题，**

**< small>标签样式，在 h1 ~ h6 元素之间，还可以嵌入一个 small 元素作为副标题(Bootstrap)**

[code]

    <h1>Bootstrap 框架 <small>Bootstrap 小标题</small></h1>
    <h2>Bootstrap 框架 <small>Bootstrap 小标题</small></h2>
    <h3>Bootstrap 框架 <small>Bootstrap 小标题</small></h3>
    <h4>Bootstrap 框架 <small>Bootstrap 小标题</small></h4>
    <h5>Bootstrap 框架 <small>Bootstrap 小标题</small></h5>
    <h6>Bootstrap 框架 <small>Bootstrap 小标题</small></h6>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427164048209-1535709070.png)**

**通过 Firebug 查看，我们发现 h1 ~ h3 下 small 元素的大小只占父元素的 65%，那么 通过计算(查看 Firebug
计算后的样式)，h1 ~ h3 下的 small 为 23.4px、19.5px、15.6px； h4 ~ h6 下 small 元素的大小只占父元素的
75% ,分别为：13.5px、10.5px、9px。 在 h1 ~ h6 下的 small 样式也进行了改变，颜色变成淡灰色：#777，行高为 1，粗度
为 400。**



**3.内联文本元素**

**添加标记，元素或.mark 类**

**< mark>标签样式，内联文本元素，添加标记，元素或.mark 类(Bootstrap)**

[code]

    <p>Bootstrap<mark>框架</mark></p>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427164342209-1239641075.png)**



**各种加线条的文本**



**< del>标签样式，内联文本元素，删除的文本(Bootstrap)**  
 **< s>标签样式，内联文本元素，无用的文本(Bootstrap)**  
 **< ins>标签样式，内联文本元素，插入的文本(Bootstrap)**  
 **< u>标签样式，内联文本元素，效果同上，下划线文本(Bootstrap)**



[code]

    <del>Bootstrap 框架</del>     //删除的文本
    <s>Bootstrap 框架</s>         //无用的文本
    <ins>Bootstrap 框架</ins>     //插入的文本
    <u>Bootstrap 框架</u>         //效果同上，下划线文本
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427164703787-1848037708.png)**



**各种强调的文本**



**< small>标签样式，内联文本元素，标准字号的 85%(Bootstrap)**  
 **< strong>标签样式，内联文本元素，加粗(Bootstrap)**  
 **< em>标签样式，内联文本元素，倾斜(Bootstrap)**



[code]

    <small>Bootstrap 框架</small>     //标准字号的 85%
    <strong>Bootstrap 框架</strong>   //加粗 700
    <em>Bootstrap 框架</em>           //倾斜
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427164958147-38591171.png)



**4.对齐**

**设置文本对齐**



**text-left样式class类，居左(Bootstrap)**  
 **text-center样式class类，居中(Bootstrap)**  
 **text-right样式class类，居右(Bootstrap)**  
 **text-justify样式class类，两端对齐，支持度不佳(Bootstrap)**  
 **text-nowrap样式class类，不换行(Bootstrap)**



[code]

    <p class="text-left">Bootstrap 框架</p>       //居左
    <p class="text-center">Bootstrap 框架</p>     //居中
    <p class="text-right">Bootstrap 框架</p>      //居右
    <p class="text-justify">Bootstrap 框架</p>    //两端对齐，支持度不佳
    <p class="text-nowrap">Bootstrap 框架</p>     //不换行
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427165430803-798890723.png)



**5.大小写**

**设置英文文本大小写**



**text-lowercase样式class类，小写(Bootstrap)**  
 **text-uppercase样式class类，大写(Bootstrap)**  
 **text-capitalize样式class类，首字母大写(Bootstrap)**



[code]

    <p class="text-lowercase">Bootstrap 框架</p> //小写
    <p class="text-uppercase">Bootstrap 框架</p> //大写
    <p class="text-capitalize">Bootstrap 框架</p>//首字母大写
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427165748303-1565466519.png)



**6.缩略语**

**< abbr>标签样式，缩略语，文字下虚线(Bootstrap)**

**initialism样式class类，文字上鼠标放上去显示title文本和一个？图标(Bootstrap)**

[code]

    Bootstrap <abbr title="Bootstrap" class="initialism">框架</abbr>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427170255365-1864053699.png)



**7.地址文本**

**设置地址，去掉了倾斜，设置了行高，底部 20px**

[code]

     <address>
        <strong>Twitter, Inc.</strong>
        <br>
        795 Folsom Ave, Suite 600
        <br>
        San Francisco, CA 94107<br>
        <abbr title="Phone">P:</abbr> (123) 456-7890
    </address>
[/code]



**8.引用文本**

**默认样式引用，增加了做边线，设定了字体大小和内外边距**

**< blockquote>标签样式，默认样式引用，增加了做边线，设定了字体大小和内外边距(Bootstrap)**

[code]

    <blockquote>
        Bootstrap 框架
    </blockquote>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427170620444-850644182.png)**

**反向引用**

**blockquote-reverse样式class类，反向引用(Bootstrap)**

[code]

     <blockquote class="blockquote-reverse ">
        Bootstrap 框架
    </blockquote>
[/code]



**9.列表排版**

**移出默认样式**

**list-unstyled样式class类，列表排版，移出默认样式(Bootstrap)**

[code]

     <ul class="list-unstyled">
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
    </ul>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427170942162-1826394189.png)**

**设置成内联**

**list-inline样式class类，列表排版，设置成内联(Bootstrap)**

[code]

     <ul class="list-inline">
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
        <li>Bootstrap 框架</li>
    </ul>
[/code]

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427171038475-2111666557.png)**



**水平排列描述列表**

**  dl-horizontal样式class类，列表排版，水平排列描述列表(Bootstrap)**

[code]

    <dl class="dl-horizontal">
        <dt>Bootstrap</dt>
        <dd>Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。Bootstrap 提供了一些常规设计好的页面排版的样式供开发者使用。</dd>
    </dl>
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427161624725-1601062976.png)



**10.代码**



**内联代码**

**< code>标签样式，内联代码(Bootstrap)**

[code]

    <code>&lt;section&gt;</code>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427161827990-634463343.png)

**用户输入**

**< kbd>标签样式，用户输入(Bootstrap)**

[code]

    press <kbd>ctrl + ,</kbd>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427162008350-751983198.png)



**代码块**

**< pre>标签样式，代码块(Bootstrap)**

[code]

    <pre>&lt;p&gt;Please input...&lt;/p&gt;</pre>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427162131256-465025296.png)



**Bootstrap 还列举了 <var>表示标记变量，<samp>表示程序输出，只不过没有重新复** _ **写 CSS。**_

  



