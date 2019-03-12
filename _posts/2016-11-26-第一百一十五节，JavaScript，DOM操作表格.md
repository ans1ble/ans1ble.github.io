
---
layout: post
title: " 第一百一十五节，JavaScript，DOM操作表格 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript，DOM操作表格**



**学习要点：**

**1.操作表格**

**DOM在操作生成HTML上，还是比较简明的。不过，由于浏览器总是存在兼容和陷阱，导致最终的操作就不是那么简单方便了。本章主要了解一下DOM操作表格和样式的一些知识。**

**一．操作表格**

**< table>标签是HTML中结构最为复杂的一个，我们可以通过DOM来创建生成它，或者HTML DOM来操作它。(PS：HTML
DOM提供了更加方便快捷的方式来操作HTML，有手册)。**

**使用DOM来创建个表格，很繁琐【不推荐】**

[code]

    window.onload =  function() { //window.onload事件，等待html执行完成后，执行匿名函数
        //使用DOM来创建这个表格
        var table = document.createElement('table'); //创建table元素节点
        table.border = 1;    //设置table元素节点边框宽度
        table.width = 300;   //设置table元素节点宽度
    
        var caption = document.createElement('caption');  //创建表格标题caption元素节点
        table.appendChild(caption);  //将标题caption元素节点，添加到table元素节点的子节点末尾
        caption.appendChild(document.createTextNode('人员表')); //创建一个文本将它添加到标题caption元素节点里
    
        var thead = document.createElement('thead');
        table.appendChild(thead);
    
        var tr = document.createElement('tr');
        thead.appendChild(tr);
    
        var th1 = document.createElement('th');
        var th2 = document.createElement('th');
        var th3 = document.createElement('th');
    
        tr.appendChild(th1);
        th1.appendChild(document.createTextNode('姓名'));
        tr.appendChild(th2);
        th2.appendChild(document.createTextNode('年龄'));
    
        document.body.appendChild(table);
    
    };
[/code]

**PS：使用DOM来创建表格其实已经没有什么难度，就是有点儿小烦而已。下面我们再使用HTML DOM来获取和创建这个相同的表格。**



**HTML DOM创建或者获取表格更清晰方便，比DOM好的多**



**HTML DOM中，给这些元素标签提供了一些属性和方法**

**属性或方法**

|

**说明**  
  
---|---  
  
**caption**

|

**保存着 <caption>元素的引用**  
  
**tBodies**

|

**保存着 <tbody>元素的HTMLCollection集合**  
  
**tFoot**

|

**保存着对 <tfoot>元素的引用**  
  
**tHead**

|

**保存着对 <thead>元素的引用**  
  
**rows**

|

**保存着对 <tr> 元素的HTMLCollection集合**  
  
**createTHead()**

|

**创建 <thead>元素，并返回引用**  
  
**createTFoot()**

|

**创建 <tfoot>元素，并返回引用**  
  
**createCaption()**

|

**创建 <caption>元素，并返回引用**  
  
**deleteTHead()**

|

**删除 <thead>元素**  
  
**deleteTFoot()**

|

**删除 <tfoot>元素**  
  
**deleteCaption()**

|

**删除 <caption>元素**  
  
**deleteRow(pos)**

|

**删除指定的行**  
  
**insertRow(pos)**

|

**向rows集合中的指定位置插入一行**  
  
** **

**< tbody>元素添加的属性和方法**

**属性或方法**

|

**说明**  
  
---|---  
  
**rows**

|

**保存着 <tbody>元素中行的HTMLCollection**  
  
**deleteRow(pos)**

|

**删除指定位置的行**  
  
**insertRow(pos)**

|

**向rows集合中的指定位置插入一行，并返回引用**  
  
** **

**< tr>元素添加的属性和方法**

**属性或方法**

|

**说明**  
  
---|---  
  
**cells**

|

**保存着 <tr>元素中单元格的HTMLCollection**  
  
**deleteCell(pos)**

|

**删除指定位置的单元格**  
  
**insertCell(pos)**

|

**向cells集合的指定位置插入一个单元格，并返回引用**  
  
**PS：因为表格较为繁杂，层次也多，在使用之前所学习的DOM只是来获取某个元素会非常难受，所以使用HTML DOM会清晰很多**

****HTML DOM获取表格****

****首先要通过id或者名称，获取到table节点****

**caption属性，获取或设置表格的 <caption>标题标签**  
 **使用方式：**  
 **table节点.caption**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.caption);   //caption属性，获取表格的caption标题标签节点
        //返回：[object HTMLTableCaptionElement]
        alert(table.caption.innerHTML); //查看标题节点里的文本内容
        //返回：人员表
        table.caption.innerHTML = '标题修改了';
        alert(table.caption.innerHTML); //查看标题节点里的文本内容
        //返回：标题修改了
    
    };
[/code]

**tHead属性，获取表格的 <thead>表头标签节点**  
 **使用方式：**  
 **table节点.tHead**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tHead);  //tHead属性，获取表格的<thead>表头标签节点
        //返回：[object HTMLTableSectionElement]
    };
[/code]

**tFoot属性，获取表格的 <tfoot>表尾标签节点**  
 **使用方式：**  
 **table节点.tFoot**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tFoot);  //tFoot属性，获取表格的<tfoot>表尾标签节点
        //返回：[object HTMLTableSectionElement]
    };
[/code]

**tBodies属性，获取表格的 <tbody>表主体标签节点，因为主体可以有多个，所以tBodies属性返回的集合**  
 **使用方式：**  
 **table节点.tBodies**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tBodies);  //tBodies属性，获取表格的<tbody>表主体标签节点，因为主体可以有多个，所以tBodies属性返回的集合
        //返回：[object HTMLCollection]
        alert(table.tBodies[0]); //获取第一个<tbody>标签
        //返回：[object HTMLTableSectionElement]
    };
[/code]

**PS：在一个表格中
<thead>和<tfoot>是唯一的，只能有一个。而<tbody>不是唯一的可以有多个，这样导致最后返回的<thead>和<tfoot>是元素引用，而<tbody>返回的是元素集合。**

**rows属性，获取表格的行签节点，因为行可以有多个，所以rows属性返回的集合**  
 **使用方式：**  
 **table节点.rows**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.rows);  //rows属性，获取表格的<tr>主体里的行签节点，因为行可以有多个，所以rows属性返回的集合
        //返回：[object HTMLCollection]
        alert(table.rows.length); //获取<tr>标签长度
        //返回：4
    };
[/code]

**获取表格主体 <tbody>的<tr>里的行签节点**

[code]

    /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tBodies[0].rows);  //获取表格主体第一个<tbody>的<tr>里的行签节点
        //返回：[object HTMLCollection]
        alert(table.tBodies[0].rows.length); //获取<tr>标签长度
        //返回：2
    };
[/code]

**cells属性，获取表格的 <tr>里的<td>单元格节点，cells属性返回的集合**  
 **使用方式：**  
 **rows[0]行节点.cells**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tBodies[0].rows[0]);  //获取第一个表格主体里的第一个<tr>标签
        //返回：[object HTMLCollection]
        //cells属性，获取表格的<tr>里的<td>单元格节点，cells属性返回的集合
        alert(table.tBodies[0].rows[0].cells);  //获取第一个表格主体<tbody>里的第一个<tr>标签里的单元格<td>
        //返回;[object HTMLCollection]
        alert(table.tBodies[0].rows[0].cells.length); //查看单元格<td>的长度
        //返回;3
    };
[/code]

**获取 <td>单元格里的文本内容**

[code]

    /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        alert(table.tBodies[0].rows[0]);  //获取第一个表格主体里的第一个<tr>标签
        //返回：[object HTMLCollection]
        //cells属性，获取表格的<tr>里的<td>单元格节点，cells属性返回的集合
        alert(table.tBodies[0].rows[0].cells);  //获取第一个表格主体<tbody>里的第一个<tr>标签里的单元格<td>
        //返回;[object HTMLCollection]
        alert(table.tBodies[0].rows[0].cells[0].innerHTML); //查看第一个单元格<td>的文本内容
        //返回;张三
    };
[/code]



**按HTML DOM来删除标题、表头、表尾、行、单元格**



**deleteCaption()方法，删除表格的标题 <caption>节点**  
 **使用方式：**  
 **table节点.deleteCaption()**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        table.deleteCaption();  //deleteCaption()方法，删除表格的标题<caption>节点
    };
[/code]

**deleteTHead()方法，删除表格的表头 <thead>节点**  
 **使用方式：**  
 **table节点.deleteTHead()**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        table.deleteTHead();  //deleteTHead()方法，删除表格的表头<thead>节点
    };
[/code]

**deleteTFoot()方法，删除表格的表尾 <tfoot>节点**  
 **使用方式：**  
 **table节点.deleteTFoot()**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        table.deleteTFoot();  //deleteTFoot()方法，删除表格的表尾<tfoot>节点
    };
[/code]

**deleteRow()方法，删除表格的行 <tr>节点，参数是要删除第几个tr标签**  
 **使用方式：**  
 **tr父节点.deleteRow(要删除第几个tr)**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        table.tBodies[0].deleteRow(0);  //deleteRow()方法，删除表格的行<tr>节点
    };
[/code]

**deleteCell()方法，删除表格的单元格 <td>节点，参数是要删除第几个td标签**  
 **使用方式：**  
 **td父节点.deleteCell(要删除第几个td标签)**

[code]

     /*
    <table border="1" width="300">
        <caption>人员表</caption>
        <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>20</td>
            </tr>
            <tr>
                <td>李四</td>
                <td>女</td>
                <td>22</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">合计：N</td>
            </tr>
        </tfoot>
    </table>
    */
    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.getElementsByTagName('table')[0]; //通过名称获取到table标签节点
        table.tBodies[0].rows[1].deleteCell(1);  //deleteCell()方法，删除表格的单元格<td>节点，参数是要删除第几个td标签
    };
[/code]

**  添加表格**

**  给<body>添加<table>标签**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.createElement('table');  //创建一个元素table标签节点
        table.width = 300; //设置table标签宽度
        table.border = 1;  //table标签边框宽度
        document.body.appendChild(table); //将table标签添加到body的子节点里
    };
[/code]

**createCaption()方法，给表格 <table>，添加标题标签<caption>**  
 **使用方式：**  
 **< caption>父节点.createCaption()**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.createElement('table');  //创建一个元素table标签节点
        table.width = 300; //设置table标签宽度
        table.border = 1;  //table标签边框宽度
    
        table.createCaption().innerHTML = '人员表';  //createCaption()方法，给表格<table>，添加标题标签<caption>
        document.body.appendChild(table); //将table标签添加到body的子节点里
    };
[/code]

**createTHead()方法，给表格 <table>，添加表头标签<thead>，返回引用**  
 **使用方式：**  
 **< thead>父节点.createTHead()**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.createElement('table');  //创建一个元素table标签节点
        table.width = 300; //设置table标签宽度
        table.border = 1;  //table标签边框宽度
        document.body.appendChild(table); //将table标签添加到body的子节点里
    
        table.createCaption().innerHTML = '人员表';  //createCaption()方法，给表格<table>，添加标题标签<caption>
        var thead = table.createTHead();  //createTHead()方法，给表格<table>，添加表头标签<thead>
    };
[/code]

**insertRow()方法，给表格添加行标签 <tr>，参数添加第几行， **返回引用****  
 **使用方式：**  
 **< tr>父节点.insertRow()**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.createElement('table');  //创建一个元素table标签节点
        table.width = 300; //设置table标签宽度
        table.border = 1;  //table标签边框宽度
        document.body.appendChild(table); //将table标签添加到body的子节点里
    
        table.createCaption().innerHTML = '人员表';  //createCaption()方法，给表格<table>，添加标题标签<caption>
        var thead = table.createTHead();  //createTHead()方法，给表格<table>，添加表头标签<thead>
        thead.insertRow(0);  //insertRow()方法，给表格添加行标签<tr>
    };
[/code]

**insertCell()方法，给表格添加单元格标签 <td>,参数创建第几个td**  
 **使用方式：**  
 **< td>父节点.insertCell()**

[code]

    window.onload = function() { //window.onload事件，等待html执行完成后，执行匿名函数
        var table = document.createElement('table');  //创建一个元素table标签节点
        table.width = 300; //设置table标签宽度
        table.border = 1;  //table标签边框宽度
        document.body.appendChild(table); //将table标签添加到body的子节点里
    
        table.createCaption().innerHTML = '人员表';  //createCaption()方法，给表格<table>，添加标题标签<caption>
        var thead = table.createTHead();  //createTHead()方法，给表格<table>，添加表头标签<thead>
        var tr = thead.insertRow(0);  //insertRow()方法，给表格添加行标签<tr>
        tr.insertCell(0).innerHTML = '数据1';  //insertCell()方法，给表格添加单元格标签<td>,参数创建第几个td
        tr.insertCell(1).innerHTML = '数据2';
        tr.insertCell(2).innerHTML = '数据3';
    };
[/code]

**在创建表格的时候
<table>、<tbody>、<th>没有特定的方法，需要使用document来创建。也可以模拟已有的方法编写特定的函数即可，例如：insertTH()之类的。**



