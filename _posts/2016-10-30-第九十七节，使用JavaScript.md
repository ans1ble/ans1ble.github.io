---
layout: post
title: " 第九十七节，使用JavaScript "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**使用JavaScript**



**学习要点：**

**1.创建一张HTML页面**

**2. <Script>标签解析**

**3.JS代码嵌入的一些问题**



**一．** **创建一张HTML** **页面**

**因为JavaScript是嵌套在html文档中的，所以要想创建一个html文档**

[code]

     <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>JavaScript讲解</title>
    </head>
    <body>
    
    </body>
    </html>
[/code]



**二．** **< Script>** **标签解析**

**< script>xxx</script>这组标签，是用于在html页面中插入js的主要方法。它主要有以下几个属性：**

1.charset：可选。表示通过src属性指定的字符集。由于大多数浏览器忽略它，所以很少有人用它。就是给js指定字符编码

如：

[code]

     <script type="text/javascript" src="1.js" charset="UTF-8"></script>
[/code]

2.defer：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。由于大多数浏览器不支持，故很少用。

3.language：已废弃。原来用于代码使用的脚本语言。由于大多数浏览器忽略它，所以不要用了。

4.src：可选。表示包含要执行代码的外部文件。

如：

[code]

    <script type="text/javascript" src="1.js" charset="UTF-8"></script>
[/code]

5.type：必需。可以看作是language的替代品。表示代码使用的脚本语言的内容类型。



**在HTML文档里写范例：type="text/javascript"。**

[code]

    <script type="text/javascript">
        alert( '欢迎来到JavaScript世界！');
    </script>
[/code]

[code]

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>JavaScript讲解</title>
        <script type="text/javascript">
            alert('欢迎来到JavaScript世界！')
        </script>
    </head>
    <body>
    
    </body>
    </html>
[/code]



**三．** **JS** **代码嵌入的一些问题**

**如果你想弹出一个
</script>标签的字符串，那么浏览器会误解成JS代码已经结束了。解决的方法，就是把字符串分成两个部分，通过连接符‘+’来连接。**

[code]

    <script type="text/javascript">
        alert('</scr'+'ipt>');
    </script>
[/code]



**一般来说，JS代码越来越庞大的时候，我们最好把他另存为一个.js文件，通过src引入即可。它还具有维护性高、可缓存(加载一次，无需加载)、方便未来扩展的特点**

[code]

     <script type="text/javascript" src="demo1.js"></script>
[/code]



**这样标签内就没有任何JS代码了。但，要注意的是，虽然没有任何代码，也不能用单标签：**

[code]

     <script type="text/javascript" src="demo1.js" />；
[/code]



**也不能在里面添加任何代码：**

[code]

     <script type="text/javascript" src="demo1.js">alert('我很可怜，执行不到！')</script>
[/code]



**按照常规，我们会把 <script>标签存放到<head>...</head>之间。但有时也会放在body之间。**

[code]

    <head>
        <meta charset="UTF-8">
        <title>JavaScript讲解</title>
        <script type="text/javascript">
            alert('欢迎来到JavaScript世界！')
        </script>
    </head>
[/code]



**平稳退化不支持JavaScript处理： <nosciprt>，现在浏览器都支持了，但有的浏览器关闭了js支持功能，我们可以用 **<
nosciprt>标签给予提示****

[code]

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>JavaScript讲解</title>
        <script type="text/javascript">
            alert('欢迎来到JavaScript世界！')
        </script>
    </head>
    <noscript>
        本站必须开启JavaScript支持，请将浏览器开启支持JavaScript
    </noscript>
    你好
    <body>
    
    </body>
    </html>
[/code]





