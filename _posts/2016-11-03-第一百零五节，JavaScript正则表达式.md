第一百零五节，JavaScript正则表达式

**JavaScript正则表达式**



**学习要点：**

**1.什么是正则表达式**

**2.创建正则表达式**

**3.获取控制**

**4.常用的正则**



**假设用户需要在HTML表单中填写姓名、地址、出生日期等。那么在将表单提交到服务器进一步处理前，JavaScript程序会检查表单以确认用户确实输入了信息并且这些信息是符合要求的。**



**一．** **什么是正则表达式**

**正则表达式(regular
expression)是一个描述字符模式的对象。ECMAScript的RegExp类表示正则表达式，而String和RegExp都定义了使用正则表达式进行强大的模式匹配和文本检索与替换的函数。**

**正则表达式主要用来验证客户端的输入数据。用户填写完表单单击按钮之后，表单就会被发送到服务器，在服务器端通常会用PHP、ASP.NET等服务器脚本对其进行进一步处理。因为客户端验证，可以节约大量的服务器端的系统资源，并且提供更好的用户体验。**



**二．** **创建正则表达式**

**创建正则表达式和创建字符串类似，创建正则表达式提供了两种方法，一种是采用new运算符，另一个是采用字面量方式。**

**1.两种创建方式**

**通过new关键字和RegExp()创建表达式**

****RegExp()表达式对象，【有参，第一个参数是字符串，第二个参数是模式修饰符】****

    
    
     var asdc = "叫卖录音网";
    var asdc2 = new RegExp(asdc);  //创建正则对象，将字符串传入表达式
    alert(asdc2); //打印出表达式，返回/叫卖录音网/
    
    
    var asdc = "叫卖录音网";
    var asdc2 = new RegExp(asdc,'ig');  //创建正则对象，将字符串传入表达式,并且写了正则模式修饰符
    alert(asdc2); //打印出表达式，返回/叫卖录音网/gi

**模式修饰符的可选参数**

**参   数**

|

**含   义**  
  
---|---  
  
**i**

|

**忽略大小写**  
  
**g**

|

**全局匹配**  
  
**m**

|

**多行匹配**  
  












**字面量方式创建正则**

    
    
     var asdc2 = /叫卖录音网/;    //字面量方式创建正则
    var asdc3 = /叫卖录音网/ig;  //字面量方式创建正则，并且写入模式修饰符
    alert(asdc2);   //打印正则，返回/叫卖录音网/
    alert(asdc3);   ////打印正则，返回/叫卖录音网/gi



**2.测试正则表达式**

**RegExp对象包含两个方法：test()和exec()，功能基本相似，用于测试字符串匹配。test()方法在字符串中查找是否存在指定的正则表达式并返回布尔值，如果存在则返回true，不存在则返回false。exec()方法也用于在字符串中查找指定正则表达式，如果exec()方法执行成功，则返回包含该查找字符串的相关信息数组。如果执行失败，则返回null。**

**RegExp对象的方法**

**方   法**

|

**功   能**  
  
---|---  
  
**test**

|

**在字符串中测试模式匹配，返回true或false**  
  
**exec**

|

**在字符串中执行匹配搜索，返回结果数组**  
  










**test()方法在字符串中查找是否存在指定的正则表达式并返回布尔值，如果存在则返回true，不存在则返回false。**

**使用new运算符的test方法示例**

    
    
     /*使用new运算符的test方法示例*/
    var pattern = new RegExp('box', 'i');            //创建正则模式，不区分大小写
    var str = 'This is a Box!';                        //创建要比对的字符串
    alert(pattern.test(str));                        //通过test()方法验证是否匹配,返回true

**使用字面量方式的test方法示例**

    
    
     /*使用字面量方式的test方法示例*/
    var pattern = /box/i;                            //创建正则模式，不区分大小写
    var str = 'This is a Box!';                    //创建要匹配的字符串
    alert(pattern.test(str));                    //通过test()方法验证是否匹配，true

**使用一条语句实现正则匹配**

    
    
     /*使用一条语句实现正则匹配*/
    alert(/box/i.test('This is a Box!'));                //模式和字符串替换掉了两个变量



****exec()方法也用于在字符串中查找指定正则表达式，如果exec()方法执行成功，则返回包含该查找字符串的相关信息数组。如果执行失败，则返回null。****

****使用exec返回匹配数组****

    
    
     /*使用exec返回匹配数组*/
    var pattern = /录音/i;                          //创建正则匹配模式
    var str = '专业广告录音网站';                     //创建要匹配的字符串
    alert(pattern.exec(str));                        //匹配了返回数组，否则返回null

**PS：exec方法还有其他具体应用，我们在获取控制学完后再看。**



**3.使用字符串的正则表达式方法**

**除了test()和exec()方法，String对象也提供了4个使用正则表达式的方法。**

**String对象中的正则表达式方法**

**方   法**

|

**含   义**  
  
---|---  
  
**match(pattern)**

|

**返回pattern中的子串或null**  
  
**replace(pattern, replacement)**

|

**用replacement替换pattern**  
  
**search(pattern)**

|

**返回字符串中pattern开始位置**  
  
**split(pattern)**

|

**返回字符串按指定pattern拆分的数组**  
  


















**match()返回匹配到的字符串以数组形式，加上length属性还可以返回匹配到的数组长度**

    
    
     /*使用match方法获取获取匹配数组*/
    var pattern = /box/ig;                        //全局搜索
    var str = 'This is a Box!，That is a Box too';
    alert(str.match(pattern));                        //匹配到两个Box,Box
    alert(str.match(pattern).length);                //获取数组的长度

**search()返回匹配字符串的开始位置**

    
    
     /*使用search来查找匹配数据*/
    var pattern = /box/ig;
    var str = 'This is a Box!，That is a Box too';
    alert(str.search(pattern));                        //查找到返回位置，否则返回-1

**PS：因为search方法查找到即返回，也就是说无需g全局**



**replace()将匹配到的字符串替换成别的字符串**

    
    
     /*使用replace替换匹配到的数据*/
    var pattern = /box/ig;
    var str = 'This is a Box!，That is a Box too';
    alert(str.replace(pattern, 'Tom'));                //将Box替换成了Tom

**split()返回字符串按指定匹配拆分的数组  **

    
    
    /*使用split拆分成字符串数组*/
    var pattern = /！/ig;
    var str = 'This is a Box!，That is a Box too';
    alert(str.split(pattern));                        //将空格拆开分组成数组

**RegExp** **对象的静态属性**

**属   性**

|

**短   名**

|

**含   义**  
  
---|---|---  
  
**input**

|

**$_**

|

**当前被匹配的字符串**  
  
**lastMatch**

|

**$ &**

|

**最后一个匹配字符串**  
  
**lastParen**

|

**$+**

|

**最后一对圆括号内的匹配子串**  
  
**leftContext**

|

**$`**

|

**最后一次匹配前的子串**  
  
**multiline**

|

**$***

|

**用于指定是否所有的表达式都用于多行的布尔值**  
  
**rightContext**

|

**$'**

|

**在上次匹配之后的子串**  
      
    
    **使用静态属性**
    
    
     /*使用静态属性*/
    var pattern = /(g)oogle/;
    var str = 'This is google！';
    pattern.test(str);                            //必须执行一下
    alert(RegExp.input);                        //This is google！
    alert(RegExp.leftContext);                    //This is
    alert(RegExp.rightContext);                    //！
    alert(RegExp.lastMatch);                    //google
    alert(RegExp.lastParen);                    //g
    alert(RegExp.multiline);                    //false

**PS：Opera不支持input、lastMatch、lastParen和multiline属性。IE不支持multiline属性。**

**所有的属性可以使用短名来操作**

**RegExp.input可以改写成RegExp['$_']，依次类推。但RegExp.input比较特殊，它还可以写成RegExp.$_。**



**RegExp** **对象的实例属性**

**属   性**

|

**含   义**  
  
---|---  
  
**global**

|

**Boolean值，表示g是否已设置**  
  
**ignoreCase**

|

**Boolean值，表示i是否已设置**  
  
**lastIndex**

|

**整数，代表下次匹配将从哪里字符位置开始**  
  
**multiline**

|

**Boolean值，表示m是否已设置**  
  
**Source**

|

**正则表达式的源字符串形式**  
  


**使用实例属性**



    
    
    /*使用实例属性*/
    var pattern = /google/ig;
    alert(pattern.global);                        //true，是否全局了
    alert(pattern.ignoreCase);                    //true，是否忽略大小写
    alert(pattern.multiline);                        //false，是否支持换行
    alert(pattern.lastIndex);                        //0，下次的匹配位置
    alert(pattern.source);                        //google，正则表达式的源字符串
    
    var pattern = /google/g;
    var str = 'google google google';
    pattern.test(str);                            //google，匹配第一次
    alert(pattern.lastIndex);                        //6，第二次匹配的位



**PS：以上基本没什么用。并且lastIndex在获取下次匹配位置上IE和其他浏览器有偏差，主要表现在非全局匹配上。lastIndex还支持手动设置，直接赋值操作**



**三．** **获取控制**

**正则表达式元字符是包含特殊含义的字符。它们有一些特殊功能，可以控制匹配模式的方式。反斜杠后的元字符将失去其特殊含义。**

**字符类：单个字符和数字**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**.**

|

**匹配除换行符外的任意字符**  
  
**[a-z0-9]**

|

**匹配括号中的字符集中的任意字符**  
  
**[^a-z0-9]**

|

**匹配任意不在括号中的字符集中的字符**  
  
**\d**

|

**匹配数字**  
  
**\D**

|

**匹配非数字，同[^0-9]相同**  
  
**\w**

|

**匹配字母和数字及_**  
  
**\W**

|

**匹配非字母和数字及_**  
  
** **

**字符类：空白字符**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**\0**

|

**匹配null字符**  
  
**\b**

|

**匹配空格字符**  
  
**\f**

|

**匹配进纸字符**  
  
**\n**

|

**匹配换行符**  
  
**\r**

|

**匹配回车字符**  
  
**\t**

|

**匹配制表符**  
  
**\s**

|

**匹配空白字符、空格、制表符和换行符**  
  
**\S**

|

**匹配非空白字符**  
  
** **

**字符类：锚字符**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**^**

|

**行首匹配**  
  
**$**

|

**行尾匹配**  
  
**\A**

|

**只有匹配字符串开始处**  
  
**\b**

|

**匹配单词边界，词在[]内时无效**  
  
**\B**

|

**匹配非单词边界**  
  
**\G**

|

**匹配当前搜索的开始位置**  
  
**\Z**

|

**匹配字符串结束处或行尾**  
  
**\z**

|

**只匹配字符串结束处**  
  
** **

**字符类：重复字符**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**x?**

|

**匹配0个或1个x**  
  
**x***

|

**匹配0个或任意多个x**  
  
**x+**

|

**匹配至少一个x**  
  
**(xyz)+**

|

**匹配至少一个(xyz)**  
  
**x{m,n}**

|

**匹配最少m个、最多n个x**  
  
** **

**字符类：替代字符**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**this|where|logo**

|

**匹配this或where或logo中任意一个**  
  
** **

**字符类：记录字符**

**元字符/元符号**

|

**匹配情况**  
  
---|---  
  
**(string)**

|

**用于反向引用的分组**  
  
**\1或$1**

|

**匹配第一个分组中的内容**  
  
**\2或$2**

|

**匹配第二个分组中的内容**  
  
**\3或$3**

|

**匹配第三个分组中的内容**  
  
** **

** .匹配除换行符以外的任意字符**

    
    
     /*使用点元字符*/
    var pattern = /g.gle/;                        //.匹配一个任意字符
    var str = 'g@gle';
    alert(pattern.test(str));                   //返回true

**  *匹配0个一个或者多个前导字符**



    
    
    /*重复匹配*/
    var pattern = /g.*gle/;                        //*匹配0个一个或者多个前导字符
    var str = 'g2456gle';
    alert(pattern.test(str));
    
    var pattern2 = /gi*gle/;                    //*匹配0个一个或者多个前导字符
    var str2 = 'giigle';
    alert(pattern2.test(str2));



**  +匹配至少一个前导字符**

    
    
    var pattern2 = /gi+gle/;                    // +匹配至少一个前导字符
    var str2 = 'giigle';
    alert(pattern2.test(str2));

**？匹配0个或一个前导字符**

    
    
     var pattern2 = /gi?gle/;                    //？匹配0个或一个前导字符
    var str2 = 'gigle';
    alert(pattern2.test(str2));

**{}匹配指定数量范围的前导字符**

    
    
     var pattern2 = /gi{2,4}gle/;                    //{}匹配指定数量范围的前导字符
    var str2 = 'giiiigle';
    alert(pattern2.test(str2));



**[a-z]匹配小写字母a到z之间的任意一个字母**

    
    
     var pattern2 = /gi[a-z]gle/;                    //[a-z]匹配小写字母a到z之间的任意一个字母
    var str2 = 'gixgle';
    alert(pattern2.test(str2));

**[0-9]匹配数字0到9之间的任意一个数字**

    
    
     var pattern2 = /gi[0-9]gle/;                    //[0-9]匹配数字0到9之间的任意一个数字
    var str2 = 'gi5gle';
    alert(pattern2.test(str2));

**[a-zA-Z0-9]匹配小写字母或者大写字母a到z之间数字0到9之间的任意一个字母或者数字**

    
    
     var pattern2 = /gi[a-zA-Z0-9]gle/;                    //[a-zA-Z0-9]匹配小写字母或者大写字母a到z之间数字0到9之间的任意一个字母或者数字
    var str2 = 'giFgle';
    alert(pattern2.test(str2));

****[^]** 非，后导字符不相同或者不在范围就匹配，反向匹配**

**^如果不是写在元字符里的，是另外一个意思**

    
    
     var pattern2 = /gi[^a-zA-Z0-9]gle/;                    //[^]非，后导字符不相同或者不在范围就匹配，反向匹配
    var str2 = 'gi!gle';
    alert(pattern2.test(str2));

**\d匹配数字等同于[0-9]**

    
    
     var pattern2 = /\digle/;                    //\d匹配数字等同于[0-9]
    var str2 = '5555555igle';
    alert(pattern2.test(str2));

**\D匹配非数字，等同于[^0-9]**

    
    
     var pattern2 = /\Digle/;                    //\D匹配非数字，等同于[^0-9]
    var str2 = 'Tigle';
    alert(pattern2.test(str2));

**\w匹配字母及数字和_下划线**

    
    
     var pattern2 = /\wigle/;                    //\w匹配字母及数字和_下划线
    var str2 = '5igle';
    alert(pattern2.test(str2));

**\W匹配非字母及数字和_下划线**

    
    
     var pattern2 = /\Wigle/;                    //\W匹配非字母及数字和_下划线
    var str2 = '!igle';
    alert(pattern2.test(str2));

**^行 **首** 匹配**

    
    
    var pattern2 = /^[0-9]igle/;                    //^首行匹配
    var str2 = '5igle';
    alert(pattern2.test(str2));

**$行尾匹配**

    
    
     var pattern2 = /igle$/;                    //$行尾匹配
    var str2 = '1121555igle';
    alert(pattern2.test(str2));

**\s匹配空白字符、空格、制表符和换行符**

    
    
     var pattern2 = /ig\sle/;                    //\s匹配空白字符、空格、制表符和换行符
    var str2 = 'ig le';
    alert(pattern2.test(str2));

**\b匹配是否到达了边际**

    
    
     var pattern2 = /igle\b/;                    //\b匹配是否到达了边际
    var str2 = 'igle';
    alert(pattern2.test(str2));

**|或模式匹配，其中任意一个符合就匹配**

    
    
     var pattern2 = /igle|adc|varjk/;                    //|或模式匹配，其中任意一个符合就匹配
    var str2 = 'adc';
    alert(pattern2.test(str2));

**()分组，组里的可以看做一个整体**

    
    
     var pattern2 = /(igle)45(adc)/;                    //()分组，组里的可以看做一个整体
    var str2 = 'igle45adc';
    alert(pattern2.test(str2));

**  $获取匹配内容里分组部分，后面跟要获取第几个分组如$1**

    
    
    var pattern2 = /(igle)45(adc)/;                    //()分组，组里的可以看做一个整体
    var str2 = 'igle45adc';                        //执行一次
    str2.match(pattern2);
    alert(RegExp.$1);                               //打印匹配内容里分组部分

**替换匹配内容里分组部分**

    
    
     var pattern1 = /8(.*)8/;
    var str1 = 'This is 8google8';
    var result1 = str1.replace(pattern1,'<strong>$1</strong>');        //得到替换的字符串输出
    document.write(result1);
    
    var pattern2 = /(.*)\s(.*)/;
    var str2 = 'google baidu';
    var result2 = str2.replace(pattern2, '$2 $1');            //将两个分组的值替换输出
    document.write(result2);



**  贪婪和惰性**

**贪   婪**

|

**惰   性**  
  
---|---  
  
**+**

|

**+?**  
  
**?**

|

**??**  
  
*****

|

***?**  
  
**{n}**

|

**{n}?**  
  
**{n,}**

|

**{n,}?**  
  
**{n,m}**

|

**{n,m}?**  
  


**  关于贪婪和惰性**

    
    
    var pattern = /[a-z]+?/;                        //?号关闭了贪婪匹配，只替换了第一个
    var str = 'abcdefjhijklmnopqrstuvwxyz';
    var result = str.replace(pattern, 'xxx');
    alert(result);

**禁止了贪婪，开启的全局**

    
    
     var pattern = /8(.+?)8/g;                        //禁止了贪婪，开启的全局
    var str = 'This is 8google8, That is 8google8, There is 8google8';
    var result = str.replace(pattern,'<strong>$1</strong>');
    document.write(result);

**另一种禁止贪婪**

    
    
     var pattern = /8([^8]*)8/g;                    //另一种禁止贪婪
    var str = 'This is 8google8, That is 8google8, There is 8google8';
    var result = str.replace(pattern,'<strong>$1</strong>');
    document.write(result);    

**使用exec返回数组，也就是可以用 **exec()方法将匹配到的内容输出****

    
    
     var pattern = /^[a-z]+\s[0-9]{4}$/i;
    var str = 'google 2012';
    alert(pattern.exec(str));                        //返回包含字符串的数组
    
    
    **只匹配字母  
    **
    
    
     var pattern = /^[a-z]+/i;                        //只匹配字母
    var str = 'google 2012';
    alert(pattern.exec(str));                        //返回google

**使用分组**

    
    
     var pattern = /^([a-z]+)\s([0-9]{4})$/i;            //使用分组
    var str = 'google 2012';
    alert(pattern.exec(str)[0]);                    //google 2012
    alert(pattern.exec(str)[1]);                    //google
    alert(pattern.exec(str)[2]);                    //2012

**捕获性分组和非捕获性分组，就是所有分组都 **捕获****

******捕获性分组******

    
    
     var pattern = /(\d+)([a-z])/;                    //捕获性分组
    var str = '123abc';
    alert(pattern.exec(str));                       //返回数组类型的123a,123,a

**非捕获性分组**

    
    
     var pattern = /(\d+)(?:[a-z])/;                    //非捕获性分组
    var str = '123abc';
    alert(pattern.exec(str));                //返回数组123a,123

**使用分组嵌套**

    
    
     /*使用分组嵌套*/
    var pattern = /(A?(B?(C?)))/;                    //从外往内获取
    var str = 'ABC';
    alert(pattern.exec(str));          //返回分组ABC,ABC,BC,C

**使用前瞻捕获**

    
    
     /*使用前瞻捕获*/
    var pattern = /(goo(?=gle))/;                    //goo后面必须跟着gle才能捕获
    var str = 'google';
    alert(pattern.exec(str));                    //返回数组goo,goo

**使用特殊字符匹配**

    
    
     /*使用特殊字符匹配*/
    var pattern = /\.\[\/b\]/;                        //特殊字符，用\符号转义即可
    var str = '.[/b]';
    alert(pattern.test(str));                    //返回true

**使用换行模式**

    
    
     /*使用换行模式*/
    var pattern = /^\d+/mg;                        //启用了换行模式
    var str = '1.baidu\n2.google\n3.bing';
    var result = str.replace(pattern, '#');
    alert(result);
    //返回
    //#.baidu
    //#.google
    //#.bing



**四．** **常用的正则**

**1.检查邮政编码**

    
    
     var pattern = /[1-9][0-9]{5}/;                    //共6位数字，第一位不能为0
    var str = '224000';
    alert(pattern.test(str));

**2.检查文件压缩包和文件格式**



    
    
    var pattern = /^[\w]+\.(zip|rar|gz)&/;                //\w表示所有数字和字母加下划线
    var str = '123.zip';                            //\.表示匹配.，后面是一个选择
    alert(pattern.test(str));



**3.删除多余空格**

    
    
     var pattern = /\s/g;                            //g必须全局，才能全部匹配
    var str = '111 222 333';
    var result = str.replace(pattern,'');                //把空格匹配成无空格
    alert(result);

**4.删除首尾空格**

    
    
     var pattern = /^\s+/;                            //强制首
    var str = '          goo  gle            ';
    var result = str.replace(pattern, '');
    pattern = /\s+$/;                            //强制尾
    result = result.replace(pattern, '');
    alert('|' + result + '|');
    
    
    **使用了非贪婪捕获**





    
    
    var pattern = /^\s*(.+?)\s*$/;                    //使用了非贪婪捕获
    var str = '            google          ';
    alert('|' + pattern.exec(str)[1] + '|');



    
    
    **使用了分组获取  
    **
    
    
     var pattern = /^\s*(.+?)\s*$/;
    var str = '            google          ';
    alert('|' + str.replace(pattern, '$1') + '|');            //使用了分组获取

**5.简单的电子邮件验证**

    
    
     var pattern = /^([a-zA-Z0-9_\.\-]+)@([a-zA-Z0-9_\.\-]+)\.([a-zA-Z]{2,4})$/;
    var str = 'yc60.com@gmail.com';
    alert(pattern.test(str));
    
    
    var pattern = /^([\w\.\-]+)@([\w\.\-]+)\.([\w]{2,4})$/;
    var str = 'yc60.com@gmail.com';
    alert(pattern.test(str));

**PS：以上是简单电子邮件验证，复杂的要比这个复杂很多，大家可以搜一下。**

    
    
    ** **



    
    
    ** **

