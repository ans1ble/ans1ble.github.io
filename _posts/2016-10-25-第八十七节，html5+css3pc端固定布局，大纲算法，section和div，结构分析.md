第八十七节，html5+css3pc端固定布局，大纲算法，section和div，结构分析

**html5+css3pc端固定布局，大纲算法，section和div，结构分析**





**一．大纲算法**  
 **在HTML5中有一个很重要的概念，叫做HTML5
大纲算法(HTML5Outliner)，它的用途是为用户提供一份页面的信息结构目录。比如我们经常使用的手册就是一个非常好的大纲结构：**

**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161025110627187-582272179.png)**



**测试工具：[https://gsnedders.html5.org/outliner/
](https://gsnedders.html5.org/outliner/)**  
**这个工具可以上传本地html文件，也可以填写URL，或者直接在多行文本框上编写HTML5代码均可了解大纲。**  
 **通过我们将上一节课的代码编写，发现这个页面的大纲非常的难看，出现三个Untitled
Section，这个意思表示页面此处缺少大纲标题，不规范。如果你的页面在这里测试，大纲都比较清晰，那么HTML5页面是比较规范的。**



**需要大纲的标签**

**1.
<body>,是需要大纲标题的，注意：<body>里面的大纲标题的上级，如果是需要大纲标题的，大纲标题就归属于上级，如果上级是不需要大纲标题的，大纲标题就归属于<body>标签**

**语义标签一般就是拿来布局大纲，最好不要用于css样式，css样式用div，**



**语义标签说明**

**< body>      网页主体      需要大纲**

**< header>        表示首部
不需要要大纲             用于头部 **区域****

**< footer>         表示尾部
不需要要大纲             用于尾部区域**

**< nav>                   表示有意集中在一起的导航元素
需要大纲**

**< section>        表示重要概念或主题                                      需要大纲
**主题****

**< article>         表示一段独立的内容
需要大纲**

**< address>            表示文档或article的联系信息
不需要要大纲**

**< aside>            表示与周边内容少有牵涉的内容                             需要大纲**

**< hgroup>         将一组标题组织在一起
需要大纲,会自动变成下一个主大纲  需要定义大纲的地方**

**< details>              生成一个区域，用户将其展开可以获得更多细节               不需要要大纲**

**< summary>         用在details元素中，表示该元素内容的标题或说明            不需要要大纲**



****注意： <article>表示一段独立的内容，里面又可以添加 **< header>  ， **< nav> ， **< section> ，
**< footer>当上门的标签嵌套************





**二．section和div **  
**首先，我们暂不探讨怎么让html5页面大纲合乎规范。先探讨一下section和div的区别。div元素在html5之前就是非常常用的标签，它本身没有任何语义，用来页面布局和CSS样式以及JS调用。那么，div的用途已经说的很清楚了：**  
 **1.如果是页面布局，且不是header、footer之类的专属区域，都应该使用div；**  
 **2.如果只是单纯的对一个端内容进行CSS样式定义，那么也应该使用div;**  
 **3.如果想对一段内容进行JS控制，那么也应该使用div。**

**html5中，section并不是用来取代div的。在基础课程中已经简单的了解过，它是具有语义的文档标签。表示一段文档中的章节，比如包含一个标题和一个段落，而大纲规范中，至少要包含一个标题。**  
 **通过上诉说明，我们可以对section标签，增加一个h2即可实现大纲要求。**

****测试工具：<https://gsnedders.html5.org/outliner/>[
](https://gsnedders.html5.org/outliner/)****



**火狐插件：  HeadingsMap**



**三.完成大纲**

**![](https://images2015.cnblogs.com/blog/955761/201610/955761-20161025150846515-1917557211.png)**



**可以看出已经有很好的大纲结构了**



**html代码**

    
    
     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>瓢城旅行社</title>
        <link rel="stylesheet" href="css/index.css">
    </head>
    <body>
    <!--导航-->
    <header class="dao-hang">
        <div class="dao-hang2">
            <h1 class="log">瓢城旅行社</h1>
            <nav>
                <h2>网站导航</h2>
                <ul>
                    <h3>
                        <li class="dao-hang-lie-biao"><a href="index.html">首页</a></li>
                        <li class="dao-hang-lie-biao"><a href="#">旅游资讯</a></li>
                        <li class="dao-hang-lie-biao"><a href="#">机票订购</a></li>
                        <li class="dao-hang-lie-biao"><a href="#">风景欣赏</a></li>
                        <li class="dao-hang-lie-biao"><a href="#">公司简介</a></li>
                    </h3>
                </ul>
            </nav>
        </div>
    </header>
    
    
    <!--主体-->
    <section>section
    <h2>主题</h2>
    </section>
    
    
    <!--尾部-->
    <footer>footer</footer>
    
    </body>
    </html>



