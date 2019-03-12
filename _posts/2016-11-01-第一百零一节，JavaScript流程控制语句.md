---
layout: post
title: " 第一百零一节，JavaScript流程控制语句 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript流程控制语句**



**学习要点：**

**1.语句的定义**

**2.if 语句**

**3.switch语句**

**4.do...while语句**

**5.while语句**

**6.for语句**

**7.for...in语句**

**8.break和continue语句**

**9.with语句**



**ECMA-262规定了一组流程控制语句。语句定义了ECMAScript中的主要语法，语句通常由一个或者多个关键字来完成给定的任务。诸如：判断、循环、退出等**



**一．** **语句的定义** ** **

**在ECMAScript中，所有的代码都是由语句来构成的。语句表明执行过程中的流程、限定与约定，形式上可以是单行语句，或者由一对大括号“｛｝”括起来的复合语句，在语法描述中，复合语句整体可以作为一个单行语句处理。如下：**

[code]

     var box = 100; //单行语句
    var age = 20; //另一条单行语句
    
    {
        //用花括号包含的语句集合，叫做复合语句，单位一个
        //一对花括号，表示一个复合语句，处理时候，可以当做一条单行语句来对待
        //复合语句我们一般叫做代码块
        var height = 200;
        var width = 300;
    }
[/code]

**语句的种类**

**类型**

|

**子类型**

|

**语法**  
  
---|---|---  
  
**声明语句**

|

**变量声明语句**

|

**var box = 100;**  
  
**标签声明语句**

|

**label : box;**  
  
**表达式语句**

|

**变量赋值语句**

|

**box = 100;**  
  
**函数调用语句**

|

**box();**  
  
**属性赋值语句**

|

**box.property = 100;**  
  
**方法调用语句**

|

**box.method();**  
  
**分支语句**

|

**条件分支语句**

|

**if () {} else {}**  
  
**多重分支语句**

|

**switch () { case n : ...};**  
  


**语句的种类(** **续)**



**类型**

|

**子类型**

|

**语法**  
  
---|---|---  
  
**循环语句**

|

**for**

|

**for (;;;) {}**  
  
**for ... in**

|

**for ( x in x) {}**  
  
**while**

|

**while () {};**  
  
**do ... while**

|

**do {} while ();**  
  
**控制结构**

|

**继续执行子句**

|

**continue ;**  
  
**终端执行子句**

|

**break ;**  
  
**函数返回子句**

|

**return ;**  
  
**异常触发子句**

|

**throw ;**  
  
**异常捕获与处理**

|

**try {} catch () {} finally {}**  
  
**其他**

|

**空语句**

|

**;**  
  
**with语句**

|

**with () {}**  
  




**二．if语句**

**if 语句即条件判断语句，一共有三种格式：**

**1\. if (条件表达式) 语句;**

**判断条件返回布尔值，返回true(真)就执行里面的语句，反之返回假，则不执行里面的语句**

[code]

     var box = 100;
    if (box > 50) alert('box大于50');    //if里面的括号(box > 50)返回的结果转换成布尔值是
                                        //true(真)的时候，则执行后面的一条语句，否则不执行
    
    var box = 100;
    if (box > 50)
        alert('box大于50');     //两行的if语句，判断后也执行一条语句
    
    alert('不管怎样，我都能被执行到！'); //这条会被执行，可以看出这个打印已经给if语句没关系了
    
    var box = 100;
    if (box < 50) {
        alert('box大于50');   //用复合语句包含，判断后执行一条复合语句
        alert('我被执行到！'); //复合语句就是一个代码块，判断后执行的代码块
    }
[/code]

**对于if语句括号里的表达式，ECMAScript会自动调用Boolean()转型函数将这个表达式的结果转换成一个布尔值。如果值为true，执行后面的一条语句，否则不执行。**

**PS：if语句括号里的表达式如果为true，只会执行后面一条语句，如果有多条语句，那么就必须使用复合语句把多条语句包含在内。**

**PS2：推荐使用第一种或者第三种格式，一行的if语句，或者多行的if复合语句。这样就不会因为多条语句而造成混乱。**

**PS3：复合语句我们一般喜欢称作为：代码块。**

**2\. if (条件表达式) {语句;} else {语句;}**

****判断条件返回布尔值，返回true(真)就执行里面的语句，反之返回假，则执行 **else** 里面的语句****

[code]

    var box = 100;
    if (box > 50) {
        alert('box大于50');                //条件为true，执行这个代码块
    } else {
        alert('box小于50');                //条件为false，执行这个代码块
    } 
[/code]

**3.if (条件表达式) {语句;} else if (条件表达式) {语句;} ... else {语句;}  **

**多个条件判断，那个条件 ** **返回true(真)就执行那个里面的语句、下面的就不执行了，所有的条件都返回假，就执行
**else里面的语句********

[code]

     var box = 100;
    if (box >= 100) {                        //如果满足条件，不会执行下面任何分支
        alert('甲');
    } else if (box >= 90) {
        alert('乙');
    } else if (box >= 80) {
        alert('丙');
    } else if (box >= 70) {
        alert('丁');
    } else if (box >= 60) {
        alert('及格');
    } else {                                //如果以上都不满足，则输出不及格
        alert('不及格');
    }
[/code]



**三．** **switch** **语句**

**switch语句是多重条件判断，用于多个值相等的比较。被判断变量与那条判断相等就执行那条里面的语句**

**break关键字，中途退出当**

[code]

     var box = 1;
    switch (box) {                        //用于判断box相等的多个值
        case 1 :                       //case 1 相当于如果box==1，会执行alert('one');
            alert('one');
            break;                        //break;遇到break会退出判断语句，用于防止语句的穿透
        case 2 :
            alert('two');
            break;
        case 3 :
            alert('three');
            break;
    
        default :                        //相当于if语句里的else，否则的意思
            alert('error');
    }
[/code]



**四．** **do...while循环** **语句**

**do...while语句是一种先运行，后判断的循环语句。也就是说，不管条件是否满足，至少先运行一次循环体。**

[code]

     var box = 1;                            
    do {                                    //先运行一次，再判断
        alert(box);                         //第一步打印box
        box++;                              //第二步累加，box等于2
    } while (box <= 5);                        //第三步判断box是否小于或者等于5，此时box等于2，条件成立开始循环
[/code]



**五．** **while循环** **语句**

**while语句是一种先判断，后运行的循环语句。也就是说，必须满足条件了之后，方可运行循环体。**

[code]

     var box = 1;                            //如果是1，执行五次，如果是10，不执行
    while (box <= 5) {                        //先判断，再执行
        alert(box);
        box++;
    }
[/code]



六． **for循环** **语句**

**for语句也是一种先判断，后运行的循环语句。但它具有在执行循环之前初始变量和定义循环后要执行代码的能力。**

[code]

     for (var box = 1; box <= 5 ; box++) {        //第一步，声明变量var box = 1;
        alert(box);                        //第二步，判断box <=5
    }                                    //第三步，alert(box)
    //第四步，box++
    //第五步，从第二步再来，直到判断为false
[/code]



**七．** **for...in循环** **语句，迭代循环语句，可以循环出对象里的数据**

[code]

     var duix = {             //创建对象，对象有点像python里的字典，由键值对组成
        'xm':'林贵秀',
        'nl':'32',
        'xb':'男'
    };
    for(var i in duix){     //循环出对象里面的元素名称，定义变量i,将每次循环到的数据赋值给i
        alert(i);            //循环打印出i
    };
[/code]



** **

**八．** **break** **和continue** **语句**

**break和continue语句用于在循环中精确地控制代码的执行。其中，break语句会立即退出循环，强制继续执行循环体后面的语句。而continue语句退出当前循环，继续后面的循环**

****break关键字， **立即退出循环******

******document.write()打印数据显示到网页上******

[code]

     for (var box = 1; box <= 10; box++) {
        if (box == 5) break;                        //如果box是5，就退出循环
        document.write(box);
        document.write('<br />');
    }
[/code]

****continue关键字， **退出当前循环继续后面的循环******

[code]

     for (var box = 1; box <= 10; box++) {
        if (box == 5) continue;                    //如果box是5，就退出当前循环
        document.write(box);
        document.write('<br />');
    }
[/code]



**九．** **with()** **语句，对象作用域设置**

**with语句的作用是将代码的作用域设置到一个特定的对象中。**

[code]

     var box = {                                //创建一个对象
        'name' : '李炎恢',                        //键值对
        'age' : 28,
        'height' : 178
    };
    
    var n = box.name;                            //从对象里取值赋给变量
    var a = box.age;
    var h = box.height;
    
    //可以将上面的三段赋值操作改写成：
    with (box) {                                //省略了box对象名
        var n = name;
        var a = age;
        var h = height;
    }
[/code]



