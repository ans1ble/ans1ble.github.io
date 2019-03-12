
---
layout: post
title: " 第九十九节，JavaScript数据类型 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**JavaScript数据类型**





**学习要点：**

**1.typeof操作符**

**2.Undefined类型**

**3.Null类型**

**4.Boolean类型**

**5.Number类型**

**6.String类型**

**7.Object类型**



**ECMAScript中有5种简单数据类型：Undefined、Null、Boolean、Number和String。还有一种复杂数据类型——Object。ECMAScript不支持任何创建自定义类型的机制，所有值都成为以上6中数据类型之一。**



**一．typeof操作符，返回数据的类型**

**typeof操作符是用来检测变量的数据类型。对于值或变量使用typeof操作符会返回如下字符串。**

**返回的字符串**

|

**描述**  
  
---|---  
  
**undefined**

|

**未定义值的变量**  
  
**boolean**

|

**布尔值**  
  
**string**

|

**字符串**  
  
**number**

|

**数值**  
  
**object**

|

**对象或null(类型)**  
  
**function**

|

**函数**  
  
**使用方法：**

[code]

     var box = '李炎恢';
    alert(typeof box);  //typeof操作符打印类型，可以是变量
    alert(typeof '李炎恢'); //也可以直接是字面量，也就是直接写数据
    //返回string
[/code]

**typeof操作符可以操作变量，也可以操作字面量。虽然也可以这样使用：typeof(box)，但，typeof是操作符而非内置函数。PS：函数在ECMAScript中是对象，不是一种数据类型。所以，使用typeof来区分function和object是非常有必要的。**





**Undefined** **类型，声明定义了变量但没给变量赋值的类型**

**Undefined类型只有一个值，即特殊的undefined。在使用var声明变量，但没有对其初始化时，这个变量的值就是undefined。**

[code]

     var box;
    alert(box);
[/code]

**PS：我们没有必要显式的给一个变量赋值为undefined，因为没有赋值的变量会隐式的(自动的)赋值为undefined；而undefined主要的目的是为了用于比较，ECMAScript第3版之前并没有引入这个值，引入之后为了正式区分空对象与未经初始化的变量。**

**未初始化的变量与根本不存在的变量(未声明的变量)也是不一样的。**

[code]

     var box;
    alert(age);
[/code]

**PS：如果typeof box，typeof
age都返回的undefined。从逻辑上思考，他们的值，一个是undefined，一个报错；他们的类型，却都是undefined。所以，我们在定义变量的时候，尽可能的不要只声明，不赋值。**





**Null类型，空对象类型，一般用于初始化对象**

**Null类型是一个只有一个值的数据类型，即特殊的值null。它表示一个空对象引用(指针)，而typeof操作符检测null会返回object。**

[code]

     var box = null;
    alert(typeof box);
[/code]

**如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为null。这样，当检查null值就知道是否已经变量是否已经分配了对象引用了。**

[code]

     var box = null;if (box != null) {
        alert('box对象已存在！');
    }
[/code]

**有个要说明的是：undefined是派生自null的，因此ECMA-262规定对它们的相等性测试返回true。**

[code]

    alert(undefined ==  null);
[/code]

**由于undefined和null两个值的比较是相等的，所以，未初始化的变量和赋值为null的变量会相等。这时，可以采用typeof变量的类型进行比较。但，建议还是养成编码的规范，不要忘记初始化变量。**

[code]

     var box;
    var car = null;
    alert(typeof box == typeof car)
[/code]





**Boolean** **类型，布尔值类型**

**Boolean类型有两个值(字面量)：true和false。而true不一定等于1，false不一定等于0。JavaScript是区分大小写的，True和False或者其他都不是Boolean类型的值。**

[code]

     var box = true;
    alert(typeof box);
[/code]

****Boolean()函数，将其数据类型转换成布尔类型****

**虽然Boolean类型的字面量只有true和false两种，但ECMAScript中所有类型的值都有与这两个Boolean值等价的值。要将一个值转换为其对应的Boolean值，可以使用转型函数Boolean()。**

[code]

     var hello = 'Hello World!'; //字符串类型
    alert(typeof Boolean(hello)); //将字符串转换成布尔值
    //打印出boolean
[/code]

**上面是一种显示转换，属于强制性转换。而实际应用中，还有一种隐式转换。比如，在if条件语句里面的条件判断，就存在隐式转换。**

[code]

     var hello = 'Hello World!';
    if (hello) {
        alert('如果条件为true，就执行我这条！');
    } else {
        alert('如果条件为false，就执行我这条！');
    }
[/code]

**以下是其他类型转换成Boolean类型规则  **

**数据类型**

|

**转换为true的值**

|

**转换为false的值**  
  
---|---|---  
  
**Boolean（布尔类型）**

|

**true**

|

**false**  
  
**String（字符串类型）**

|

**任何非空字符串**

|

**空字符串**  
  
**Number（数字类型）**

|

**任何非零数字值(包括无穷大)**

|

**0和NaN**  
  
**Object（对象类型）**

|

**任何对象**

|

**null**  
  
**Undefined（没赋值变量）**

|

**没有   **true****

|

**undefined**  
  
** **

** **



**Number** **类型，数字类型包含整数和浮点数**

**Number类型包含两种数值：整型和浮点型。为了支持各种数值类型，ECMA-262定义了不同的数值字面量格式。**

**最基本的数值字面量是十进制整数。**

[code]

     var box = 100;            //十进制整数
[/code]

**八进制数值字面量，(以8为基数)，前导必须是0，八进制序列(0~7)。**

[code]

     var box = 070;            //八进制，56
    var box = 079;            //无效的八进制，自动解析为79
    var box = 08;            //无效的八进制，自动解析为8
[/code]

**十六进制字面量前面两位必须是0x，后面是(0~9及A~F)。**

[code]

     var box = 0xA;        //十六进制，10
    var box = 0x1f;        //十六进制，31
[/code]

**浮点类型，就是该数值中必须包含一个小数点，并且小数点后面必须至少有一位数字。**

[code]

     var box = 3.8;
    var box = 0.8;
    var box = .8;            //有效，但不推荐此写法
[/code]

**由于保存浮点数值需要的内存空间比整型数值大两倍，因此ECMAScript会自动将可以转换为整型的浮点数值转成为整型。**

[code]

     var box = 8.;            //小数点后面没有值，转换为8
    var box = 12.0;        //小数点后面是0，转成为12
[/code]

**对于那些过大或过小的数值，可以用科学技术法来表示(e表示法)。用e表示该数值的前面10的指数次幂**

[code]

     var box = 4.12e9;        //即4120000000
    var box = 0.00000000412;    //即4.12e-9
[/code]

**虽然浮点数值的最高精度是17位小数，但算术运算中可能会不精确。由于这个因素，做判断的时候一定要考虑到这个问题(比如使用整型判断)。**

[code]

    alert(0.1+0.2);             //0.30000000000000004
[/code]

**浮点数值的范围在：Number.MIN_VALUE ~ Number.MAX_VALUE之间。**

[code]

    alert(Number.MIN_VALUE);             //最小值
    alert(Number.MAX_VALUE);        //最大值
[/code]

**如果超过了浮点数值范围的最大值或最小值，那么就先出现Infinity(正无穷)或者-Infinity(负无穷)。**

[code]

     var box = 100e1000;                //超出范围，Infinity
    var box = -100e1000;                //超出范围，-Infinity
[/code]

**也可能通过Number.POSITIVE_INFINITY和Number.NEGATIVE_INFINITY得到Infinity(正无穷)及-Infinity(负无穷)的值。**

[code]

    alert(Number.POSITIVE_INFINITY);     //Infinity(正无穷)
    alert(Number.NEGATIVE_INFINITY);//-Infinity(负无穷)
[/code]

****isFinite()函数，判断一个数字是否超过规定的最大值或者最小值****

**要想确定一个数值到底是否超过了规定范围，可以使用isFinite()函数。如果没有超过，返回true，超过了返回false。**

[code]

     var box = 100e1000;
    alert(isFinite(box));                    //返回false或者true
[/code]

**NaN，即非数值(Not a
Number)是一个特殊的值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况(这样就不会抛出错误了)。比如，在其他语言中，任何数值除以0都会导致错误而终止程序执行。但在ECMAScript中，会返回出特殊的值，因此不会影响程序执行。**

[code]

     var box = 0 / 0;                //NaN
    var box = 12 / 0;                //Infinity
    var box = 12 / 0 * 0;            //NaN
[/code]

**可以通过Number.NaN得到NaN值，任何与NaN进行运算的结果均为NaN，NaN与自身不相等(NaN不与任何值相等)。**

[code]

    alert(Number.NaN);             //NaN
    alert(NaN+1);                    //NaN
    alert(NaN == NaN)                //false
[/code]

****isNaN()函数， **用来判断一个值到底是不是NaN******

**ECMAScript提供了isNaN()函数，用来判断这个值到底是不是NaN。isNaN()函数在接收到一个值之后，会尝试将这个值转换为数值。**

[code]

    alert(isNaN(NaN));                 //true
    alert(isNaN(25));                //false，25是一个数值
    alert(isNaN('25'));                //false，'25'是一个字符串数值，可以转成数值
    alert(isNaN('Lee'));                //true，'Lee'不能转换为数值
    alert(isNaN(true));                //false    true可以转成成1
[/code]

**isNaN()函数也适用于对象。在调用isNaN()函数过程中，首先会调用valueOf()方法，然后确定返回值是否能够转换成数值。如果不能，则基于这个返回值再调用toString()方法，再测试返回值。**

[code]

     var box = {
        toString : function () {
            return '123';            //可以改成return 'Lee'查看效果
        }
    };
    alert(isNaN(box));                //false
[/code]



********Number() **函数， **转型函数，可以用于任何数据类型转换成数值************

**有3个函数可以把非数值转换为数值：Number()、parseInt()和parseFloat()。
Number()函数是转型函数，可以用于任何数据类型，而另外两个则专门用于把字符串转成数值。**

[code]

    alert(Number(true));            //1，Boolean类型的true和false分别转换成1和0
    alert(Number(25));                //25，数值型直接返回
    alert(Number(null));            //0，空对象返回0
    alert(Number(undefined));        //NaN，undefined返回NaN
[/code]



**如果是字符串，应该遵循一下规则：**

1.只包含数值的字符串，会直接转成成十进制数值，如果包含前导0，即自动去掉。

[code]

    alert(Number('456'));            //456
    alert(Number('070'));            //70
[/code]

2.只包含浮点数值的字符串，会直接转成浮点数值，如果包含前导和后导0，即自动去掉。

[code]

    alert(Number('08.90'));            //8.9
[/code]

3.如果字符串是空，那么直接转成成0

[code]

    alert(Number(''));                //0
[/code]

4.如果不是以上三种字符串类型，则返回NaN。

[code]

    alert('Lee123');                //NaN
[/code]

5.如果是对象，首先会调用valueOf()方法，然后确定返回值是否能够转换成数值。如果转换的结果是NaN，则基于这个返回值再调用toString()方法，再测试返回值。

[code]

    var box = {
        toString : function () {
            return '123';            //可以改成return 'Lee'查看效果
        }
    };
    alert(Number(box));            //123
[/code]

******parseInt() **函数， ** ** **
**把字符串转换成数值【有参可选】第二个参数是以什么进制方式，如16****************

**由于Number()函数在转换字符串时比较复杂且不够合理，因此在处理整数的时候更常用的是parseInt()。**

[code]

    alert(parsetInt('456Lee'));         //456，会返回整数部分
    alert(parsetInt('Lee456Lee'));        //NaN，如果第一个不是数值，就返回NaN
    alert(parseInt('12Lee56Lee'));        //12，从第一数值开始取，到最后一个连续数值结束
    alert(parseInt('56.12'));            //56，小数点不是数值，会被去掉
    alert(parseInt(''));                //NaN，空返回NaN
[/code]

**parseInt()除了能够识别十进制数值，也可以识别八进制和十六进制。**

[code]

    alert(parseInt('0xA'));             //10，十六进制
    alert(parseInt('070'));            //56，八进制
    alert(parseInt('0xALee'));        //100，十六进制，Lee被自动过滤掉
[/code]

**ECMAScript为parseInt()提供了第二个参数，用于解决各种进制的转换**

[code]

    alert(parseInt('0xAF'));             //175，十六进制
    alert(parseInt('AF', **16** ));            //175，第二参数指定十六进制，可以去掉0x前导
    alert(parseInt('AF'));            //NaN，理所当然
    alert(parseInt('101010101',2));    //314，二进制转换
    alert(parseInt('70',8))            //56，八进制转换
[/code]

******parseFloat() **函数， ** ** ** ** ** ** ** ** ** **
**把字符串转换成数值******************************

**parseFloat()是用于浮点数值转换的，和parseInt()一样，从第一位解析到非浮点数值位置。**

[code]

    alert(parseFloat('123Lee'));         //123，去掉不是别的部分
    alert(parseFloat('0xA'));            //0，不认十六进制
    alert(parseFloat('123.4.5'));        //123.4，只认一个小数点
    alert(parseFloat('0123.400'));        //123.4，去掉前后导
    alert(parseFloat('1.234e7'));        //12340000，把科学技术法转成普通数值
[/code]





**String** **类型，字符串类型**

**String类型用于表示由于零或多个16位Unicode字符组成的字符序列，即字符串。字符串可以由双引号(")或单引号(')表示。**

[code]

     var box = 'Lee';
    var box = "Lee";
[/code]

**PS：在某些其他语言(PHP)中，单引号和双引号表示的字符串解析方式不同，而ECMAScript中，这两种表示方法没有任何区别。但要记住的是，必须成对出现，不能穿插使用，否则会出错。**

[code]

     var box = '李炎恢";                //出错
[/code]

**String类型包含了一些特殊的字符字面量，也叫转义序列。**

**字面量**

|

**含义**  
  
---|---  
  
**\n**

|

**换行**  
  
**\t**

|

**制表**  
  
**\b**

|

**空格**  
  
**\r**

|

**回车**  
  
**\f**

|

**进纸**  
  
**\\\**

|

**斜杠**  
  
**\'**

|

**单引号，转义字符**  
  
**\"**

|

**双引号，转义字符**  
  
**\xnn**

|

**以十六进制代码nn表示的一个字符(0~F)。例：\x41**  
  
**\unnn**

|

**以十六进制代码nnn表示的一个Unicode字符(0~F)。例：\u03a3**  
  


[code]

    var sdf = "林\n贵秀"
    alert(sdf)
    //打印出来就会换行
[/code]

**
ECMAScript中的字符串是不可变的，也就是说，字符串一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的**

**字符串填充该变量。**

[code]

     var box = 'Mr.';
    box = box + ' Lee';
    alert(box)
    //打印出Mr.Lee
[/code]

**toString()方法可以把值转换成字符串。【有参可选】**

**注意：null或者undefined的情况下 **toString()是无法转换的****

[code]

     var dsaf = 11; //数字类型
        dsaf = dsaf.toString(); //将数字类型转换成字符串类型
    alert(typeof dsaf); //打印出string
[/code]

[code]

    var box = true;
    alert(box.toString());//将布尔类型转换成字符串类型
[/code]

**toString()方法一般是不需要传参的，但在数值转成字符串的时候，可以传递进制参数。**

[code]

     var box = 10;
    alert(box.toString());                //10，默认输出
    alert(box.toString(2));                //1010，二进制输出
    alert(box.toString(8));                //12，八进制输出
    alert(box.toString(10));                //10，十进制输出
    alert(box.toString(16));                //a，十六进制输出
[/code]

****String() **函数， **将任何类型的值转换为字符串********

**如果在转型之前不知道变量是否是null或者undefined的情况下，我们还可以使用转型函数String()，这个函数能够将任何类型的值转换为字符串。**

[code]

     var box = null;
    alert(typeof String(box));//转换成字符串类型
[/code]

**PS：如果值有toString()方法，则调用该方法并返回相应的结果；如果是null或者undefined，则返回"null"或者"undeinfed"。**





**Object** **类型，对象类型， **其实就是一组数据和功能的集合****

****new操作符****

**ECMAScript中的对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。**

[code]

     var box = {}; //简单创建方法
    var boxf = new Object(); //通过new操作符创建对象
[/code]

**Object()是对象构造，如果对象初始化时不需要传递参数，可以不用写括号，但这种方式我们是不推荐的。**

[code]

     var box = new Object;
[/code]

**Object()里可以任意传参，可以传数值、字符串、布尔值等。而且，还可以进行相应的计算。**

[code]

     var box = new Object(2);            //Object类型，值是2
    var age = box + 2;                    //可以和普通变量运算
    alert(age);                        //输出结果，转型成Number数字类型了
[/code]

**既然可以使用new Object()来表示一个对象，那么我们也可以使用这种new操作符来创建其他类型的对象。**

[code]

     var box = new Number(5);            //new String('Lee')、new Boolean(true)
    alert(typeof box);                    //Object类型
[/code]

**既然可以使用new Object()来表示一个对象，那么我们也可以使用这种new操作符来创建其他类型的对象。**

[code]

     var box = new Number(5);            //new String('Lee')、new Boolean(true)
    alert(typeof box);                    //Object类型
[/code]



