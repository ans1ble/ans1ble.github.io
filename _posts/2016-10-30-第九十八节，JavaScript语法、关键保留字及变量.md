---
layout: post
title: " 第九十八节，JavaScript语法、关键保留字及变量 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript语法、关键保留字及变量**





**学习要点：**

**1.语法构成**

**2.关键字保留字**

**3.变量**

**任何语言的核心都必然会描述这门语言最基本的工作原理。而JavaScript的语言核心就是ECMAScript，而目前用的最普遍的是第3版，我们就主要以这个版本来讲解。**



**一．** **语法构成**

**区分大小写**

**ECMAScript中的一切，包括变量、函数名和操作符都是区分大小写的。例如：text和Text表示两种不同的变量。**



**标识符**

**所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是下列格式规则组合起来的一或多个字符：**

**1.第一字符必须是一个字母 【f】、下划线【_】或一个美元符号【$】开头。**

**2.其他字符可以是字母、下划线、美元符号或数字。**

**3.不能把关键字、保留字、true、false和null作为标识符。**

**例如：myName、book123等**



**注释**

**ECMAScript使用C风格的注释，包括单行注释和块级注释。**

[code]

     // 单行注释
[/code]

[code]

    /*
    * 这是一个多行
    * 注释
    */
[/code]



**直接量(** **字面量literal)也就是数据类型**

**所有直接量(字面量)，就是程序中直接显示出来的数据值。 也就是数据类型**

**100                        //数字字面量**

**'林贵秀'                  //字符串字面量**

**false                      //布尔字面量**

**/js/gi                      //正则表达式字面量**

**null                        //对象字面量**

**在ECMAScript第3版中，像数组字面量和对象字面量的表达式也是支持的，如下：**

**{x:1, y:2}               //对象字面量表达式**

**[1,2,3,4,5]              //数组字面量表达式**



**二．** **关键字和保留字，也就是这些不能作为标识符**

**ECMAScript-262描述了一组具有特定用途的关键字，一般用于控制语句的开始或结束，或者用于执行特定的操作等。关键字也是语言保留的，不能用作标识符**

**ECMAScript全部关键字  **

**break**

|

**else**

|

**new**

|

**var**  
  
---|---|---|---  
  
**case**

|

**finally**

|

**return**

|

**void**  
  
**catch**

|

**for**

|

**switch**

|

**while**  
  
**continue**

|

**function**

|

**this**

|

**with**  
  
**default**

|

**if**

|

**throw**

|

** **  
  
**delete**

|

**in**

|

**try**

|

** **  
  
**do**

|

**instanceof**

|

**typeof**

|

** **  
  
**ECMAScript-262还描述了另一组不能用作标识符的保留字。尽管保留字在JavaScript中还没有特定的用途，但它们很有可能在将来被用作关键字**

**ECMAScript-262第3版定义的全部保留字  **

**abstract**

|

**enum**

|

**int**

|

**short**  
  
---|---|---|---  
  
**boolean**

|

**export**

|

**interface**

|

**static**  
  
**byte**

|

**extends**

|

**long**

|

**super**  
  
**char**

|

**final**

|

**native**

|

**synchronized**  
  
**class**

|

**float**

|

**package**

|

**throws**  
  
**const**

|

**goto**

|

**private**

|

**transient**  
  
**debugger**

|

**implements**

|

**protected**

|

**volatile**  
  
**double**

|

**import**

|

**public**

|

** **  
  
** **



**三．变量**

**ECMAScript的变量是松散类型的，所谓松散类型就是用来保存任何类型的数据。
定义变量时要使用var操作符（var是关键），后面跟一个变量名（变量名是标识符）。**

****var **关键字声明变量******

********定义变量的方法：********

**var(关键字声明变量) adc(标识符，就是变量名称) = 123（变量值）**

**alert()以弹窗的方式打印变量**

[code]

     var adc=123; //定义一个变量
    alert(adc) //打印出这个变量的值
[/code]



**undefined打印变量时输出 **undefined，表示打印的变量没有赋值****

**如果变量没有对它初始化，（也就是没有给变量赋值）。这时，系统会给它一个特殊的值 -- undefined（表示未定义）。**

[code]

     var box; 
    alert(box);
[/code]



**所谓变量，就是可以初始化后可以再次改变的量。ECMAScript属于弱类型(松散类型)的语言，可以同时改变不同类型的量。(PS：虽然可以改变不同类型的量，但这样做对于后期维护带来困难，而且性能也不高，导致成本很高！)**

[code]

     var boxString = '李炎恢';
    boxString = 100;    
    alert(boxString);
[/code]



**重复的使用var声明一个变量，只不过是一个赋值操作，并不会报错。但这样的操作是比较二的，没有任何必要。**

[code]

     var box= '李炎恢';
    var box= 'Lee';
[/code]



**还有一种变量不需要前面var关键字即可创建变量。这种变量和var的变量有一定的区别和作用范围，我们会在作用域那一节详细探讨**

[code]

    box= '李炎恢';
[/code]



**当你想声明多个变量的时候，可以在一行或者多行操作。**

[code]

     var box= '李炎恢';var age= 100;
[/code]



**而当你每条语句都在不同行的时候，你可以省略分号。(PS：这是ECMAScript支持的，但绝对是一个非常不好的编程习惯，切记不要)。**

[code]

     var box= '李炎恢'
    var age= 100
    alert(box)
[/code]



**可以使用一条语句定义多个变量，只要把每个变量(初始化或者不初始化均可)用逗号分隔开即可，为了可读性，每个变量，最好另起一行，并且第二变量和第一变量对齐(PS：这些都不是必须的)。**

[code]

     var box= '李炎恢',
       age = 28,
           height;
[/code]



