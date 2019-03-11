第一百零八节，JavaScript，内置对象，Global对象字符串编码解码，Math对象数学公式

**JavaScript，内置对象，Global对象字符串编码解码，Math对象数学公式**



**学习要点：**



**1.Global对象**



**2.Math对象**



**ECMA-262对内置对象的定义是：“由ECMAScript实现提供的、不依赖宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在了。”意思就是说，开发人员不必显示地实例化内置对象；因为它们已经实例化了。ECMA-262只定义了两个内置对象：Global和Math。**

**一．** **Global** **对象**

**Global(全局)对象是ECMAScript中一个特别的对象，因为这个对象是不存在的。在ECMAScript中不属于任何其他对象的属性和方法，全局都属于它的属性和方法。所以，事实上，并不存在全局变量和全局函数；所有在全局作用域定义的变量和函数，都是Global对象的属性和方法。**

**PS：因为ECMAScript没有定义怎么调用Global对象，所以，Global.属性或者Global.方法()都是无效的。(Web浏览器将Global作为window对象的一部分加以实现)**



**Global对象有一些内置的属性和方法：**

**1.URI编码方法**

**URI编码可以对链接进行编码，以便发送给浏览器。 它们采用特殊的UTF-8编码替换所有无效字符，从而让浏览器能够接受和理解。**

**encodeURI()不会对本身属于URI的特殊字符进行编码，例如冒号、正斜杠、问号和#号；而encodeURIComponent()则会对它发现的任何非标准字符进行编码**

****encodeURI() **URI** 字符编码，不会对本身属于URI的特殊字符进行编码,有参要编码的 ** **
**URI字符**********

****比如浏览器地址输入框就采用了这个编码****

****注意： ** **encodeURI()编码的必须用 **decodeURI()解码**********

    
    
     var box = '//Lee李';
    alert(encodeURI(box));                        //只编码了中文
    //返回//Lee%E6%9D%8E

**decodeURI() ** ** **URI** 字符解码， ** **不会对本身属于URI的特殊字符进行解码， ** **有参要解码的 ** **
**URI字符******************  
**

    
    
     var box = '//Lee李';
    var box2 = encodeURI(box);                        //只编码了中文
    alert(box2);   //打印编码后的字符，//Lee%E6%9D%8E
    alert(decodeURI(box2));//打印解码后的字符，返回//Lee李
    
    var sdf = '//Lee%E6%9D%8E';
    alert(decodeURI(sdf));//打印解码后的字符，返回//Lee李

**encodeURIComponent()任何非标准URI字符进行编码，包括冒号、正斜杠、问号和#号，有参要编码的URI字符**

******注意： **encodeURIComponent()** ** **编码的必须用 **decodeURIComponent()**
**解码************

    
    
     var box = '//Lee李';
    var box2 = encodeURIComponent(box);                        //任何非标准URI字符进行编码，包括冒号、正斜杠、问号和#号
    alert(box2);   //打印编码后的字符，%2F%2FLee%E6%9D%8E

**decodeURIComponent()URI字符进行解码，有参要解码的URI字符**

    
    
     var box = '//Lee李';
    var box2 = encodeURIComponent(box);                        //任何非标准URI字符进行编码，包括冒号、正斜杠、问号和#号
    alert(box2);   //打印编码后的字符，%2F%2FLee%E6%9D%8E
    alert(decodeURIComponent(box2));//解码返回，//Lee李
    
    var sdf = '%2F%2FLee%E6%9D%8E';
    alert(decodeURIComponent(sdf));//解码返回，//Lee李

**PS：因为encodeURIComponent()编码比encodeURI()编码来的更加彻底，一般来说encodeURIComponent()使用频率要高一些。**

**PS：URI方法如上所述的四种，用于代替已经被ECMA-262第3版废弃的escape()和unescape()方法。URI方法能够编码所有的Unicode字符，而原来的只能正确地编码ASCII字符。所以建议不要再使用escape()和unescape()方法。**



**2.eval()方法**

**eval()方法主要担当一个字符串解析器的作用，他只接受一个参数，而这个参数就是字符串类型的js代码，也就是可以解析字符串类型的js代码**

    
    
    eval('var box = 100');                         //解析了字符串代码
    alert(box);
    eval('alert(100)');                            //同上
    
    eval('function box() {return 123}');            //函数也可以
    alert(box());

**eval()方法的功能非常强大，但也非常危险。因此使用的时候必须极为谨慎。特别是在用户输入数据的情况下，非常有可能导致程序的安全性，比如代码注入等等。**



**3.Global对象属性**

**Global对象包含了一些属性：undefined、NaN、Object、Array、Function等等。**

    
    
    alert(Array);                                 //返回构造函数



**1.window对象**

**之前已经说明，Global没有办法直接访问，而Web浏览器可以使用window对象来实现一全局访问。**

    
    
    alert(window.Array);                         //同上



**二．** **Math** **对象**

**ECMAScript还为保存数学公式和信息提供了一个对象，即Math对象。与我们在JavaScript直接编写计算功能相比，Math对象提供的计算功能执行起来要快得多。**

**1.Math对象的属性**

**Math对象包含的属性大都是数学计算中可能会用到的一些特殊值。**



**属   性**

|

**说   明**  
  
---|---  
  
**Math.E**

|

**自然对数的底数，即常量e的值**  
  
**Math.LN10**

|

**10的自然对数**  
  
**Math.LN2**

|

**2的自然对数**  
  
**Math.LOG2E**

|

**以2为底e的对数**  
  
**Math.LOG10E**

|

**以10为底e的对数**  
  
**Math.PI**

|

**∏的值**  
  
**Math.SQRT1_2**

|

**1/2的平方根**  
  
**Math.SQRT2**

|

**2的平方根**  
  


    
    
    alert(Math.E);                                //
    alert(Math.LN10);
    alert(Math.LN2);
    alert(Math.LOG2E);
    alert(Math.LOG10E);
    alert(Math.PI);
    alert(Math.SQRT1_2);
    alert(Math.SQRT2);                        //



**2.min()和max()方法**

**min()用于确定一组数值中的最小值**

    
    
    alert(Math.min(2,4,3,6,3,8,0,1,3));                 //最小值

**max()用于确定一组数值中的最大值。**

    
    
    alert(Math.max(4,7,8,3,1,9,6,0,3,2));             //最大值



**3.舍入方法**

**ceil()执行向上舍入，即它总是将数值向上舍入为最接近的整数；**

    
    
    alert(Math.ceil(25.9));                         //26
    alert(Math.ceil(25.5));                        //26
    alert(Math.ceil(25.1));                        //26

**floor()执行向下舍入，即它总是将数值向下舍入为最接近的整数；**

    
    
    alert(Math.floor(25.9));                         //25
    alert(Math.floor(25.5));                        //25
    alert(Math.floor(25.1));                        //25

**round()执行标准舍入，即它总是将数值四舍五入为最接近的整数；**

    
    
    alert(Math.round(25.9));                         //26
    alert(Math.round(25.5));                        //26
    alert(Math.round(25.1));                        //25



**4.random()方法**

**random()方法返回介于0到1之间一个随机数，不包括0和1。如果想大于这个范围的话，可以套用一下公式：**

**值 = Math.floor(Math.random() * 结束范围数 + 开始范围数 - 1) =正真的结束范围数，开始范围数还是原来的**

****结束范围数 + 开始范围数 - 1 =正真的结束范围数，开始范围数还是原来的****

    
    
    alert(Math.floor(Math.random() * 10 + 1));         //结束范围数为10+开始范围数1=11，11-1=10 （1-10）的随机范围
    
    
    for (var i = 0; i<10;i ++) {
        document.write(Math.floor(Math.random() * 10 + 5));        //结束范围数为10+开始范围数5=15，15-1=14 （5-14）的随机范围
        document.write('<br />');
    }

**为了更加方便的传递想要范围，可以写成函数【推荐】**

    
    
     function selectFrom(lower, upper) {  //自定义随机函数，接收开始范围数和结束范围数
        var sum = upper - lower + 1;                    //结束范围数10减去开始范围数5=5,5+1=6
        return Math.floor(Math.random() * sum + lower);//（* 6 + 5）,6+5-1=10，范围就是5-10
    }
    
    //调用上面的随机函数即可
    for (var i=0 ;i<10;i++) {
        document.write(selectFrom(5,10));                    //直接传递范围即可
        document.write('<br />');
    }



**5.其他方法**

**方   法**

|

**说   明**  
  
---|---  
  
**Math.abs(num)**

|

**返回num的绝对值**  
  
**Math.exp(num)**

|

**返回Math.E的num次幂**  
  
**Math.log(num)**

|

**返回num的自然对数**  
  
**Math.pow(num,power)**

|

**返回num的power次幂**  
  
**Math.sqrt(num)**

|

**返回num的平方根**  
  
**Math.acos(x)**

|

**返回x的反余弦值**  
  
**Math.asin(x)**

|

**返回x的反正弦值**  
  
**Math.atan(x)**

|

**返回x的反正切值**  
  
**Math.atan2(y,x)**

|

**返回y/x的反正切值**  
  
**Math.cos(x)**

|

**返回x的余弦值**  
  
**Math.sin(x)**

|

**返回x的正弦值**  
  
**Math.tan(x)**

|

**返回x的正切值**  
  


    
    
    alert(Math.abs(5));//返回num的绝对值

**其他相同**



