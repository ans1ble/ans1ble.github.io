第一百零七节，JavaScript基本包装类型，数据类型的方法

**JavaScript基本包装类型，数据类型的方法**



**学习要点：**

**1.基本包装类型概述**

**2.Boolean类型**

**3.Number类型**

**4.String类型**



**为了便于操作基本类型值，ECMAScript提供了3个特殊的引用类型：Boolean、Number和String。这些类型与其他引用类型相似，但同时也具有与各自的基本类型相应的特殊行为。实际上，每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而能够调用一些方法来操作这些数据。**



一． **基本包装类型概述**

**substring()截取字符串指定索引后面的字符，有参截取开始位置**

    
    
     var box = 'Mr. Lee';                            //定义一个字符串
    var box2 = box.substring(2);                    //截掉字符串前两位,也就是从第二个索引开始截取后面的字符串
    alert(box2);                                //输出新字符串

**变量box是一个字符串类型，而box.substring(2)又说明它是一个对象(PS：只有对象才会调用方法)，最后把处理结果赋值给box2。'Mr.
Lee'是一个字符串类型的值， 按道理它不应该是对象，不应该会有自己的方法，但是它却有方法 **这就是基本包装类型** ，比如：**

    
    
    alert('Mr. Lee'.substring(2));                    //直接通过值来调用方法

** **

**1. **字面量方式创建的只能用内置的方法** ：**

    
    
    var box = 'Mr. Lee';                            //字面量
    box.name = 'Lee';                            //无效属性
    box.age = function () {                        //无效方法
        return 100;
    };
    alert(box);                                //Mr. Lee
    alert(box.substring(2));                        //. Lee
    alert(typeof box);                            //string
    alert(box.name);                            //undefined
    alert(box.age());                            //错误

**2.new运算创建的还可以自定义方法：**

    
    
     var box = new String('Mr. Lee');                //new运算符，创建字符串类型
    box.name = 'Lee';                            //有效属性
    box.age = function () {                        //有效方法
        return 100;
    };
    alert(box);                                //Mr. Lee
    alert(box.substring(2));                        //. Lee
    alert(typeof box);                            //object
    alert(box.name);                            //Lee
    alert(box.age());                            //100

****不管字面量形式还是new运算符形式，都可以使用它的内置方法****

**以上字面量声明和new运算符声明很好的展示了他们之间的区别。但有点定还是可以肯定的，那就是不管字面量形式还是new运算符形式，都可以使用它的内置方法。并且Boolean和Number特性与String相同，三种类型可以成为基本包装类型。**

**PS：在使用new运算符创建以上三种类型的对象时，可以给自己添加属性和方法，但我们建议不要这样使用，因为这样会导致根本分不清到底是基本类型值还是引用类型值。**



**二．** **Boolean** **类型，布尔值**

**Boolean类型没有特定的属性或者方法。**



**三．** **Number** **类型，数字**

**Number类型有一些静态属性(直接通过Number调用的属性，而无须new运算符)和方法。**

**Number静态属性**

**属   性**

|

**描述**  
  
---|---  
  
**MAX_VALUE**

|

**表示最大数**  
  
**MIN_VALUE**

|

**表示最小值**  
  
**NaN**

|

**非数值**  
  
**NEGATIVE_INFINITY**

|

**负无穷大，溢出返回该值**  
  
**POSITIVE_INFINITY**

|

**无穷大，溢出返回该值**  
  
**prototype**

|

**原型，用于增加新属性和方法**  
  
**Number静态属性，无需通过变量名称来调用，直接通过类型名称就可以调用**

**MAX_VALUE表示最大数**

    
    
     //MAX_VALUE表示最大数
    alert(Number.MAX_VALUE);

**MIN_VALUE表示最小值**

    
    
     //MIN_VALUE表示最小值
    alert(Number.MIN_VALUE);

**NaN非数值**

    
    
     //NaN非数值
    alert(Number.NaN);

**NEGATIVE_INFINITY负无穷大，溢出返回该值**

    
    
     //NEGATIVE_INFINITY负无穷大，溢出返回该值
    alert(Number.NEGATIVE_INFINITY);

**POSITIVE_INFINITY无穷大，溢出返回该值**

    
    
     //POSITIVE_INFINITY无穷大，溢出返回该值
    alert(Number.POSITIVE_INFINITY);



**Number内置对象的方法**



**方   法**

|

**描述**  
  
---|---  
  
**toString()**

|

**将数值转化为字符串，并且可以转换进制**  
  
**toLocaleString()**

|

**根据本地数字格式转换为字符串**  
  
**toFixed()**

|

**将数字保留小数点后指定位数并转化为字符串**  
  
**toExponential()**

|

**将数字以指数形式表示，保留小数点后指定位数并转化为字符串**  
  
**toPrecision()**

|

**指数形式或点形式表述数，保留小数点后面指定位数并转化为字符串**  
  
**toString()将数值转化为字符串，并且可以转换进制**

    
    
     var sdc = 123;
    alert(sdc.toString()); //toString()将数值转化为字符串，并且可以转换进制
    //返回'123'

**toLocaleString()根据本地数字格式转换为字符串，就像表示资金数字那样**

    
    
     var sdc = 1000;
    alert(sdc.toLocaleString()); //toLocaleString()根据本地数字格式转换为字符串
    //返回'1,000'

**toFixed()将数字保留小数点后指定位数并转化为字符串，【 **有参保留多少位** 】**

    
    
    var sdc = 12.5632;
    alert(sdc.toFixed(2)); //toFixed()将数字保留小数点后指定位数并转化为字符串
    //返回'12.56'

**toExponential()将数字以指数形式表示，保留小数点后指定位数并转化为字符串**

    
    
     var sdc = 12.5632;
    alert(sdc.toExponential()); //toExponential()将数字以指数形式表示，保留小数点后指定位数并转化为字符串
    //返回'1.25632e+1'

**toPrecision()指数形式或点形式表述数，保留小数点后面指定位数并转化为字符串，【有参小数点后保留多少位】根据传参来决定指数或者点数**

    
    
     var sdc = 12.356;
    alert(sdc.toPrecision(3)); //toPrecision()指数形式或点形式表述数，保留小数点后面指定位数并转化为字符串
    //返回'12.4'



**四．** **String** **类型，字符串**

**String类型包含了三个属性和大量的可用内置方法。**



**String对象属性**

**属   性**

|

**描述**  
  
---|---  
  
**length**

|

**返回字符串的字符长度**  
  
**constructor**

|

**返回创建String对象的函数**  
  
**prototype**

|

**通过添加属性和方法扩展字符串定义**  
  
**  length属性返回字符串的字符长度**

    
    
    var adc = "字符串";
    alert(adc.length); //length属性返回字符串的字符长度
    //返回3

**constructor属性返回创建String对象的函数**

    
    
     var adc = "字符串";
    alert(adc.constructor); //constructor属性返回创建String对象的函数
    /*返回
    function String() {
        [native code]
    }
    */

**prototype原型通过添加属性和方法扩展字符串定义**

**后面讲 **原型的时候专门讲解****

**String也包含对象的通用方法，比如valueOf()、toLocaleString()和toString()方法，但这些方法都返回字符串的基本值。**



**字符方法**

**方   法**

|

**描述**  
  
---|---  
  
**charAt(n)**

|

**返回指定索引位置的字符**  
  
**charCodeAt(n)**

|

**以Unicode编码形式返回指定索引位置的字符**  
  
** **

**  charAt()返回指定索引位置的字符，【 **有参索引位置数** 】**

    
    
    var adc = "字符串";
    alert(adc.charAt(1)); //charAt()返回指定索引位置的字符
    //返回-符

**charCodeAt()以Unicode编码形式返回指定索引位置的字符 **【 **有参索引位置数** 】返回字符的acssii码****

    
    
    var adc = "字符串";
    alert(adc.charCodeAt(1)); //charCodeAt()以Unicode编码形式返回指定索引位置的字符
    //返回-31526

**通过索引获取字符串里指定的字符**

    
    
     var adc = "字符串";
    alert(adc[1]); //通过索引获取字符串里指定的字符
    //返回-符

**PS：box[1]在IE浏览器会显示undefined，所以使用时要慎重**



**字符串操作方法**

**方   法**

|

**描述**  
  
---|---  
  
**concat(str1...str2)**

|

**将字符串参数串联到调用该方法的字符串**  
  
**slice(n,m)**

|

**返回字符串n到m之间位置的字符串**  
  
**substring(n,m)**

|

**同上**  
  
**substr(n,m)**

|

**返回字符串n开始的m个字符串**  
  
**concat()将字符串联到调用该方法的字符串【有参要串联的字符串】**

    
    
     var adc = "字符串";
    var adc2 = "连接起来";
    var adc3 = "!";
    alert(adc.concat(adc2,adc3)); //concat()将字符串联到调用该方法的字符串
    //返回-字符串连接起来!

**slice()返回字符串n到m之间位置的字符串【有参索引范围】**

    
    
     var adc = "叫卖录音网";
    alert(adc.slice(2,4)); //slice()返回字符串n到m之间位置的字符串
    //返回-录音

****主意：如果只写了一个参数，这个参数就是开始参数，就会从这个参数位置开始向后全部获取，因为没有结束位置****

**如果传参为负数，先统计字符串所有字符数，所有字符数加上负数，等于开始位置**

    
    
     var adc = "叫卖录音网";
    alert(adc.slice(-2)); //5+(-2)=3位开始
    //返回-音网

**如果传参一个正数一个负数， **先统计字符串所有字符数，所有字符数加上负数，等于负数位置的正数****

    
    
     var adc = "叫卖录音网";
    alert(adc.slice(3,-1)); //5+(-1)=4, 等同于设置(3,4)
    //返回-音



**substring()返回字符串n到m之间位置的字符串【有参索引范围】**

    
    
     var adc = "叫卖录音网";
    alert(adc.substring(2,4)); //substring()返回字符串n到m之间位置的字符串
    //返回-录音

****主意：如果只写了一个参数，这个参数就是开始参数，就会从这个参数位置开始向后全部获取，因为没有结束位置****

******如果传参为负数，返回全部字符串******

    
    
     var adc = "叫卖录音网";
    alert(adc.substring(-1)); //如果传参为负数，返回全部字符串
    //返回-叫卖录音网

**如果传参一个正数一个负数，会将负数直接转换成0，并且将0提在前面**

    
    
     var adc = "叫卖录音网";
    alert(adc.substring(2,-1)); //会将负数直接转换成0，并且将0提在前面,等同于设置(0,2)
    //返回-叫卖



**substr()返回字符串n开始的m个字符串，就是从字符串第几个位置开始向后显示多少位字符【有参第一个参数从第几位开始，第二个参数向后显示几位】**

    
    
     var adc = "叫卖录音网";
    alert(adc.substr(2,4)); //substr()返回字符串n开始的m个字符串，就是从字符串第几个位置开始向后显示多少位字符
    //返回-录音网

**主意：如果只写了一个参数，这个参数就是开始参数，就会从这个参数位置开始向后全部获取，因为没有结束位置**  

**如果传参为负数，先统计字符串所有字符数，所有字符数加上负数，等于开始位置**

    
    
     var adc = "叫卖录音网";
    alert(adc.substr(-3)); //5+(-3)=2位开始
    //返回-录音网

**如果传参一个正数一个负数，会将负数直接转换成0**

    
    
     var adc = "叫卖录音网";
    alert(adc.substr(2,-4)); //如果传参一个正数一个负数，会将负数直接转换成0,等同于(2,0)
    //返回

**PS：IE的JavaScript实现在处理向substr()方法传递负值的情况下存在问题，它会返回原始字符串，使用时要切记。**



**字符串位置方法**

**方   法**

|

**描述**  
  
---|---  
  
**indexOf(str, n)**

|

**从n开始搜索的第一个str，并将搜索的索引值返回**  
  
**lastIndexOf(str, n)**

|

**从n开始搜索的最后一个str，并将搜索的索引值返回**  
  
**  indexOf()从开始位置向后搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从前到后搜索开始位置】**

    
    
    var adc = "叫卖录音网专业广告录音";
    alert(adc.indexOf('录')); //从开始位置向后搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从前到后搜索开始位置】
    //返回-2

**设置第二个参数**

    
    
     var adc = "叫卖录音网专业广告录音";
    alert(adc.indexOf('录',3)); //从开始位置向后搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从前到后搜索开始位置】
    //返回-9

**lastIndexOf()从结尾位置向前搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从后到前搜索开始位置】**

    
    
     var adc = "叫卖录音网专业广告录音";
    alert(adc.lastIndexOf('录')); //lastIndexOf()从结尾位置向前搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从后到前搜索开始位置】
    //返回-9

**设置第二个参数**

    
    
     var adc = "叫卖录音网专业广告录音";
    alert(adc.lastIndexOf('录',2)); //lastIndexOf()从结尾位置向前搜索第一个str，并将搜索的索引值返回，【有参第一个要搜索的字符，第二个可选，从后到前搜索开始位置】
    //返回-2

**PS：如果没有找到想要的字符串，则返回-1。**

**示例：找出全部录**

    
    
     var box = '叫卖录音网专业广告录音';            //包含两个(录)的字符串
    var boxarr = [];                            //存放(录)位置的数组
    var pos = box.indexOf('录');                //先获取第一个(录)的位置
    while (pos > -1) {                            //如果位置大于-1，说明还存在(录)
        boxarr.push(pos);                        //添加到数组
        pos = box.indexOf('录', pos + 1);            //从新赋值pos目前的位置
    }
    alert(boxarr);                                //输出



**大小写转换方法**

**方   法**

|

**描述**  
  
---|---  
  
**toLowerCase(str)**

|

**将字符串全部转换为小写**  
  
**toUpperCase(str)**

|

**将字符串全部转换为大写**  
  
**toLocaleLowerCase(str)**

|

**将字符串全部转换为小写，并且本地化**  
  
**toLocaleupperCase(str)**

|

**将字符串全部转换为大写，并且本地化**  
  
**toLowerCase()将字符串全部转换为小写  【无参】**

    
    
    var box = 'JXIOU';
    alert(box.toLowerCase());            //toLowerCase()将字符串全部转换为小写
    //返回jxiou

**toUpperCase()将字符串全部转换为大写【无参】**

    
    
     var box = 'jxiou';
    alert(box.toUpperCase());            //toUpperCase()将字符串全部转换为大写【无参】
    //返回JXIOU

**toLocaleLowerCase()将字符串全部转换为小写，并且本地化**

    
    
     var box = 'JXIOU';
    alert(box.toLocaleLowerCase());            //toLocaleLowerCase()将字符串全部转换为小写，并且本地化
    //返回jxiou

**toLocaleUpperCase()将字符串全部转换为大写，并且本地化**

    
    
     var box = 'jxiou';
    alert(box.toLocaleUpperCase());            //toLocaleUpperCase()将字符串全部转换为大写，并且本地化
    //返回JXIOU

**PS：只有几种语言（如土耳其语）具有地方特有的大小写本地性，一般来说，是否本地化效果都是一致的。**



**字符串的模式匹配方法**

**方   法**

|

**描述**  
  
---|---  
  
**match(pattern)**

|

**返回pattern 中的子串或null**  
  
**replace(pattern, replacement)**

|

**用replacement 替换pattern**  
  
**search(pattern)**

|

**返回字符串中pattern 开始位置**  
  
**split(pattern)**

|

**返回字符串按指定pattern 拆分的数组**  
  
**正则表达式在字符串中的应用，在前面的章节已经详细探讨过，这里就不再赘述了。以上中match()、replace()、serach()、split()在普通字符串中也可以使用。**

**match()查找字符串里的指定字符，找到返回找到的字符，没找到返回null【有参要查找的字符串】**

    
    
     var box = '叫卖录音网';
    alert(box.match('录'));            //match()查找字符串里的指定字符，找到返回找到的字符，没找到返回null【有参要查找的字符串】
    //返回录

**search()返回要查找的字符在字符串里的开始位置，【有参要查找的字符】**

    
    
     var box = '叫卖录音网';
    alert(box.search('录'));            //search()返回要查找的字符在字符串里的开始位置，【有参要查找的字符】
    //返回2

**replace()替换指定的字符【有参第一个被替换的字符，第二个要替换的字符】**

    
    
     var box = '叫卖录音网';
    alert(box.replace('录','广'));            //replace()替换指定的字符【有参第一个被替换的字符，第二个要替换的字符】
    //返回叫卖广音网

**split()按照指定字符分割，返回数组【有参要分割的字符】**

    
    
     var box = '叫卖录音网';
    alert(box.split('录'));            //split()按照指定字符分割，返回数组
    //返回叫卖,音网



**其他方法**

**方   法**

|

**描述**  
  
---|---  
  
**fromCharCode(ascii)**

|

**静态方法，输出Ascii码对应值**  
  
**localeCompare(str1,str2)**

|

**比较两个字符串，并返回相应的值**  
  
**  fromCharCode()静态方法，输出Ascii码对应值，静态方法直接用数据类型名称调用【有参Ascii码】**

    
    
    alert(String.fromCharCode(76)); //fromCharCode()静态方法，输出Ascii码对应值
    //返回L

**localeCompare()比较两个字符串，并返回相应的值【有参要比较的字符】**

**localeCompare()方法详解：比较两个字符串并返回以下值中的一个；**

**1.如果字符串在字母表中应该排在字符串参数之前，则返回一个负数。(多数-1)**

**2.如果字符串等于字符串参数，则返回0。**

**3.如果字符串在自附表中应该排在字符串参数之后，则返回一个正数。(多数1)**

    
    
     var box = 'Lee';
    alert(box.localeCompare('apple'));                //1
    alert(box.localeCompare('Lee'));                //0
    alert(box.localeCompare('zoo'));                //-1



**HTML方法**

**方   法**

|

**描述**  
  
---|---  
  
**anchor(name)**

|

**< a name="name">str</a>**  
  
**big()**

|

**< big>str</big>**  
  
**blink()**

|

**< blink>str</blink>**  
  
**bold()**

|

**< b>Str</b>**  
  
**fixed()**

|

**< tt>Str</tt>**  
  
**fontcolor(color)**

|

**< font color="color">str</font>**  
  
**fontsize(size)**

|

**< font size="size">str</font>**  
  
**link(URL)**

|

**< a href="URL">str</a>**  
  
**small()**

|

**< small>str</small>**  
  
**strike()**

|

**< strike>str</strike>**  
  
**italics()**

|

**< i>italics</i>**  
  
**sub()**

|

**< sub>str</sub>**  
  
**sup()**

|

**< sup>str</sup>**  
  
** **

**以上是通过JS生成一个html标签，根据经验，没什么太大用处，做个了解。**

    
    
     var box = '百度';
    alert(box.link('http://www.baidu.com'));
    //返回<a href="http://www.baidu.com">百度</a>

**其他相同**

** **

