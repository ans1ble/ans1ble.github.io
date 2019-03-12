---
layout: post
title: " 第一百零九节，JavaScript面向对象与原型 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**JavaScript面向对象与原型**



**学习要点：**

**1.学习条件**

**2.创建对象**

**3.原型**

**4.继承**



**ECMAScript有两种开发模式：1.函数式(过程化)，2.面向对象(OOP)。面向对象的语言有一个标志，那就是类的概念，而通过类可以创建任意多个具有相同属性和方法的对象。但是，ECMAScript没有类的概念，因此它的对象也与基于类的语言中的对象有所不同。**

** **

**一．学习条件**

**在JavaScript视频课程第一节课，就已经声明过，JavaScript课程需要大量的基础。这里，我们再详细探讨一下：**

**1.xhtml基础：JavaScript方方面面需要用到。**

**2.扣代码基础：比如XHTML,ASP,PHP课程中的项目都有JS扣代码的过程。**

**3.面向对象基础：JS的面向对象是非正统且怪异的，必须有正统面向对象基础。**

**4.以上三大基础，必须是基于项目中掌握的基础，只是学习基础知识不够牢固，必须在项目中掌握上面的基础即可。**



**二．创建对象**

**创建一个对象，然后给这个对象新建属性和方法。**

[code]

     var box = new Object();                    //创建一个Object对象
    box.name = 'Lee';                        //创建一个name属性并赋值
    box.age = 100;                            //创建一个age属性并赋值
    box.run = function () {                    //创建一个run()方法并返回值
        return this.name + this.age + '运行中...';
    };
    alert(box.run());                        //输出方法的值
    alert(box.name);                        //输出属性
[/code]

**上面创建了一个对象，并且创建属性和方法，在run()方法里的this，就是代表box对象本身。这种是JavaScript创建对象最基本的方法，但有个缺点，想创建一个类似的对象，就会产生大量的代码。**

[code]

     var box = new Object();                    //创建一个Object对象
    box.name = 'Lee';                        //创建一个name属性并赋值
    box.age = 100;                            //创建一个age属性并赋值
    box.run = function () {                    //创建一个run()方法并返回值
        return this.name + this.age + '运行中...';
    };
    alert(box.run());                        //输出方法的值
    alert(box.name);                        //输出属性
    
    var box2 = box;                        //得到box的引用
    box2.name = 'Jack';                        //直接改变了name属性
    alert(box2.run());                        //用box.run()发现name也改变了
    
    var box2 = new Object();
    box2.name = 'Jack';
    box2.age = 200;
    box2.run = function () {
        return this.name + this.age + '运行中...';
    };
    alert(box2.run());                        //这样才避免和box混淆，从而保持独立
[/code]



**工厂模式创建对象【推荐】**

**为了解决多个类似对象声明的问题，我们可以使用一种叫做工厂模式的方法，这种方法就是为了解决实例化对象产生大量重复的问题。**

[code]

     function createObject(name, age) {        //集中实例化的函数
        var obj = new Object();        //创建一个对象
        obj.name = name;               //追加一个属性
        obj.age = age;                  //追加一个属性
        obj.run = function () {        //追加一个方法
            return this.name + this.age + '运行中...';   //在对象里面的this代表对象本身，对象里的name属性加上age属性
        };
        return obj;    //返回对象
    }
    
    var box1 = createObject('Lee', 100);        //第一个实例
    var box2 = createObject('Jack', 200);        //第二个实例
    alert(box1.run());
    alert(box2.run());                        //保持独立
    //以后要构造不同数据的实例，只需要构造一个实例传入不同参数即可，这样减少了大量重复代码
[/code]

**工厂模式解决了重复实例化的问题，但还有一个问题，那就是识别问题，因为根本无法搞清楚他们到底是哪个对象的实例。所以就有了构造函数**



**构造函数(构造方法)创建对象【重点推荐】**

**ECMAScript中可以采用构造函数(构造方法)可用来创建特定的对象。类型于Object对象。**

[code]

     function Box(name, age) {                //构造函数模式创建对象
        this.name = name;             //构造函数后台会自动new Object()创建对象；数体内的this就代表new Object()出来的对象。
        this.age = age;               //向对象追加属性
        this.run = function () {     //向对象追加方法
            return this.name + this.age + '运行中...';
        };
    }
    
    var box1 = new Box('Lee', 100);            //注意：构造函数对象实列化必须使用new 运算符，构造函数传参初始化对象数据
    var box2 = new Box('Jack', 200);       //构造函数传参初始化对象数据
    alert(box1.run());                     //打印box1对象实列化下的run()方法，
    alert(box1 instanceof Box);                //很清晰的识别他从属于Box
[/code]

**使用构造函数的方法，即解决了重复实例化的问题，又解决了对象识别的问题，但问题是，这里并没有new
Object()，为什么可以实例化Box()，这个是哪里来的呢？**

**使用了构造函数的方法，和使用工厂模式的方法他们不同之处如下：**

**1.构造函数方法没有显示的创建对象(new Object())；**

**2.直接将属性和方法赋值给this对象；**

**3.没有renturn语句。**

**构造函数的方法有一些规范：**

**1.函数名和实例化构造名相同且大写，(PS：非强制，但这么写有助于区分构造函数和普通函数)；**

**2.通过构造函数创建对象，必须使用new运算符。**

**既然通过构造函数可以创建对象，那么这个对象是哪里来的，new Object()在什么地方执行了？执行的过程如下：**

**1.当使用了构造函数，并且new 构造函数()，那么就后台执行了new Object()；**

**2.将构造函数的作用域给新对象，(即new Object()创建出的对象)，而函数体内的this就代表new Object()出来的对象。**

**3.执行构造函数内的代码；**

**4.返回新对象(后台直接返回)。**



********this**** 关于this的使用****

**关于this的使用，this其实就是代表当前作用域对象的引用。如果在全局范围this就代表window对象，如果在构造函数体内，就代表当前的构造函数所声明的对象。如果是在对象内，就代表当前对象**

[code]

     var box = 2;
    alert(this.box);                            //全局，代表window
[/code]



**构造函数和普通函数的唯一区别，就是他们调用的方式不同。只不过，构造函数也是函数，必须用new运算符来调用，否则就是普通函数。**

[code]

     function Box(name, age) {                //构造函数模式创建对象
        this.name = name;             //构造函数后台会自动new Object()创建对象；数体内的this就代表new Object()出来的对象。
        this.age = age;               //向对象追加属性
        this.run = function () {     //向对象追加方法
            return this.name + this.age + '运行中...';
        };
    }
    
    var box1 = new Box('Lee', 100);            //注意：构造函数对象实列化必须使用new 运算符，构造函数传参初始化对象数据
    var box2 = new Box('Jack', 200);       //构造函数传参初始化对象数据
    alert(box1.run());                     //打印box1对象实列化下的run()方法，
    
    
    var box3 = new Box('Lee', 100);            //构造模式调用
    alert(box3.run());                      //打印box3对象实列化下的run()方法，
    
    Box('Lee', 20);                            //普通模式调用，无效
    
    var o = new Object();        //创建一个对象
    Box.call(o, '林贵秀', 200);                    //o对象冒充Box构造函数调用
    alert(o.run());           //打印Box构造函数里的run()方法
[/code]



**探讨构造函数内部的方法(或函数)的问题，首先看下两个实例化后的属性或方法是否相等。**

[code]

     function Box(name, age) {                //构造函数模式创建对象
        this.name = name;             //构造函数后台会自动new Object()创建对象；数体内的this就代表new Object()出来的对象。
        this.age = age;               //向对象追加属性
        this.run = function () {     //向对象追加方法
            return this.name + this.age + '运行中...';
        };
    }
    
    var box1 = new Box('Lee', 100);            //注意：构造函数对象实列化必须使用new 运算符，构造函数传参初始化对象数据
    var box2 = new Box('Lee', 100);       //构造函数传参初始化对象数据
    
    alert(box1.name == box2.name);            //true，属性的值相等
    alert(box1.run == box2.run);                //false，方法其实也是一种引用地址
    alert(box1.run() == box2.run());            //true，方法的值相等，因为传参一致
[/code]



**可以把构造函数里的方法(或函数)用new Function()方法来代替，得到一样的效果，更加证明，他们最终判断的是引用地址，唯一性。**

[code]

     function Box(name, age) {                //new Function()唯一性
        this.name = name;
        this.age = age;
        this.run = new Function("return this.name + this.age + '运行中...'");
    }
[/code]

**我们可以通过构造函数外面绑定同一个函数的方法来保证引用地址的一致性，但这种做法没什么必要，只是加深学习了解：**

[code]

     function Box(name, age) {
        this.name = name;
        this.age = age;
        this.run = run;
    }
    
    function run() {                        //通过外面调用，保证引用地址一致
        return this.name + this.age + '运行中...';
    }
[/code]

**虽然使用了全局的函数run()来解决了保证引用地址一致的问题，但这种方式又带来了一个新的问题，全局中的this在对象调用的时候是Box本身，而当作普通函数调用的时候，this又代表window。**



**三．prototype** **原型**

**我们
创建的每个函数都有一个prototype(原型)属性，这个属性是一个对象，它的用途是包含可以由特定类型的所有实例共享的属性和方法。逻辑上可以这么理解：prototype通过调用构造函数而创建的那个对象的原型对象。使用原型的好处可以让所有对象实例共享它所包含的属性和方法。也就是说，不必在构造函数中定义对象信息，而是可以直接将这些信息添加到原型中**

**prototype原型创建对象**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    var box1 = new Box();  //实列化对象
    alert(box1.run());    //打印执行对象里的run方法
[/code]

**比较一下原型内的方法地址是否一致：**



[code]

    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    var box1 = new Box();  //实列化对象1
    var box2 = new Box();  //实列化对象2
    alert(box1.run == box2.run);                    //true，方法的引用地址保持一致
[/code]

**ps:由此可以看出，构造对象函数的实列的方法地址是不一样的，而原型函数构造对象的实列的方法地址是一样的**



**为了更进一步了解构造函数的声明方式和原型模式的声明方式，我们通过图示来了解一下：**

**构造函数方式：原理图**



![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161111172917889-957745745.png)

**原型模式方式：原理图**

**![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161111173040452-1304134606.png)**



**原型模式的执行流程：**

**1.先查找构造函数实例里的属性或方法，如果有，立刻返回；**

**2.如果构造函数实例里没有，则去它的原型对象里找，如果有，就返回；**



**在原型模式声明中，多了两个属性，这两个属性都是创建对象时自动生成的。__proto__属性是实例指向原型对象的一个指针，它的作用就是指向构造函数的原型属性constructor。通过这两个属性，就可以访问到原型里的属性和方法了。**

**__proto__构造对象函数里内部指向原型的指针**

**PS：IE浏览器在脚本访问__proto__会不能识别，火狐和谷歌浏览器及其他某些浏览器均能识别。虽然可以输出，但无法获取内部信息。**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    var box1 = new Box();  //实列化对象1
    alert(box1.__proto__);                        //[object Object]，__proto__构造对象函数里内部指向原型的指针
[/code]

**constructor原型属性，指向的构造函数本身**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    var box1 = new Box();  //实列化对象1
    alert(box1.constructor);                        //constructor原型属性，指向的构造函数本身
    //返回构造函数本身
[/code]

**isPrototypeOf()方法测试判断一个对象的实列，是否指向了对象的原型【有参实列名称】返回布尔值**

**使用方法：**  
 **对象名称(对象构造函数).prototype.isPrototypeOf(实列名称)**

**一般只要实列化了会自动指向对象的原型**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    var box1 = new Box();  //实列化对象1
    alert(Box.prototype.isPrototypeOf(box1));//isPrototypeOf()方法测试判断一个对象的实列，是否指向了对象的原型
[/code]

**虽然我们可以通过对象实例访问保存在原型中的值，但却不能访问通过对象实例重写原型中的值。**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    var box1 = new Box();                      //实列化对象1
    alert(box1.name);                            //Lee，原型里的值
    box1.name = 'Jack';                         //在对象里追加一个相同的属性
    alert(box1.name);                            //Jack，就近原则，
    
    var box2 = new Box();                        //实列化对象2
    alert(box2.name);                            //Lee，原型里的值，没有被box1修改
[/code]

**构造函数实例属性和原型属性示意图**

**![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161111232626670-1617679811.png)**



**delete删除对象里的属性**

**如果想要box1也能在后面继续访问到原型里的值，可以把构造函数里的属性删除即可，具体如下：**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    var box1 = new Box();                      //实列化对象1
    alert(box1.name);                            //Lee，原型里的值
    box1.name = 'Jack';                         //在对象里追加一个相同的属性
    
    delete box1.name;                          //删除对象里添加的name属性
    
    alert(box1.name);                            //还是返回Lee，说明对象里新添加的属性被删除了
[/code]

**hasOwnProperty()函数，判断对象的属性或者方法，是在构造函数的实列里，还是在原型里，返回布尔值，实列里返回true，否则返回false**  
 **使用方法：**  
 **对象名称(构造对象函数名称).hasOwnProperty('对象属性');**

**如何判断属性是在构造函数的实例里，还是在原型里？可以使用hasOwnProperty()函数来验证：**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    var box1 = new Box();                      //实列化对象1
    alert(box1.name);                            //Lee，原型里的值
    
    alert(box1.hasOwnProperty('name'));        //返回false，说明name属性在原型里
    alert(box1.hasOwnProperty('run'));         //返回false，说明run方法在原型里
    
    box1.name = 'Jack';                         //在对象里追加一个相同的属性
    alert(box1.hasOwnProperty('name'));         //返回true，在对象里新追加了name属性，按照就近原则，此时判断的属性在构造函数的实列里
[/code]



**in判断对象的属性是否存在，只要存在不管是在实列中还是在原型中都返回true，实列和原型中都没有就返回false**

**使用方法：**  
 **'对象属性名称' in Box**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    alert('name' in Box);       //返回true，说明对象存在这个属性
[/code]



**自定义函数判断对象属性是否只存在原型中**

**我们可以通过 **hasOwnProperty()**
方法检测属性是否存在实例中，也可以通过in来判断实例或原型中是否存在属性。那么结合这两种方法，可以判断原型中是否存在属性。**

[code]

    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    
    Box.prototype.name = 'Lee';                    //在原型里添加属性
    Box.prototype.age = 100;                   //在原型里添加属性
    Box.prototype.run = function () {                //在原型里添加方法
        return this.name + this.age + '运行中...';
    };
    
    //自定义函数判断对象属性是否只存在原型中
    function panduan(shlh,mch){   //接收两个参数，第一个实列化对象名称，第二个要判断的对象属性
        return !shlh.hasOwnProperty(mch) && (mch in shlh); //当实列对象里不存在这个属性，并且原型中存在时返回
    }
    
    var box1 = new Box();
    alert(panduan(box1,'name')); //执行判断函数，返回true，说明属性在原型中
[/code]



**字面量方式创建原型**

**为了让属性和方法更好的体现封装的效果，并且减少不必要的输入，原型的创建可以使用字面量的方式：**

[code]

     function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    Box.prototype = {                        //使用字面量的方式创建原型
        name : 'Lee',
        age : 100,
        run : function () {
            return this.name + this.age + '运行中...';
        }
    };
    
    var box1 = new Box();   //实列化对象
    alert(box1.run());    //打印对象下面的run方法
[/code]



**字面量方式创建原型与追加原型的区别**

**使用构造函数创建原型对象和使用字面量创建对象在使用上基本相同，但还是有一些区别，字面量创建的方式使用constructor属性不会指向实例，而会指向Object，构造函数创建的方式则相反。**

[code]

     //字面量方式创建原型
    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    Box.prototype = {                        //使用字面量的方式创建原型，相当于新创建了一个Object对象
        name : 'Lee',
        age : 100,
        run : function () {
            return this.name + this.age + '运行中...';
        }
    };
    
    var box = new Box();   //实列化对象
    alert(box instanceof Box);   //判断box实列化是否是Box对象类型
    //返回true
    alert(box instanceof Object);   //判断box实列化是否是Object对象类型
    //返回true
    alert(box.constructor == Box);      //判断box实列化的原型constructor属性是否等于Box对象，也就是原型constructor属性是否指向Box对象
    //返回false
    alert(box.constructor == Object);  //判断box实列化的原型constructor属性是否等于Object对象，也就是原型constructor属性是否指向Object对象
    //返回true
    
    //由此可以说明：字面量方式创建原型，原型的constructor属性不是指向构造函数的，是指向构造函数里面，字面量新建的Object对象
[/code]

**PS：字面量方式为什么constructor会指向Object？因为Box.prototype={};这种写法其实就是创建了一个新对象。而每创建一个函数，就会同时创建它prototype，这个对象也会自动获取constructor属性。所以，新对象的constructor重写了Box原来的constructor，因此会指向新对象，那个新对象没有指定构造函数，那么就默认为Object。**



**字面量方式创建原型,将原型的constructor属性强制指向实列对象(构建对象函数)**

**如果想让字面量方式的constructor指向实例对象，那么可以这么做：**

[code]

     //字面量方式创建原型
    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    Box.prototype = {                        //使用字面量的方式创建原型，相当于新创建了一个Object对象
        constructor:Box,              //字面量方式创建原型,将原型的constructor属性强制指向实列对象(构建对象函数)
        name : 'Lee',
        age : 100,
        run : function () {
            return this.name + this.age + '运行中...';
        }
    };
    
    var box = new Box();   //实列化对象
    alert(box instanceof Box);   //判断box实列化是否是Box对象类型
    //返回true
    alert(box instanceof Object);   //判断box实列化是否是Object对象类型
    //返回true
    alert(box.constructor == Box);      //判断box实列化的原型constructor属性是否等于Box对象，也就是原型constructor属性是否指向Box对象
    //返回true
    alert(box.constructor == Object);  //判断box实列化的原型constructor属性是否等于Object对象，也就是原型constructor属性是否指向Object对象
    //返回false
    
    //由此可以说明：字面量方式创建原型，将原型的constructor属性强制指向实列对象(构建对象函数)，也就是原型constructor属性不在指向Object对象
[/code]

** **

**原型的声明是有先后顺序的，所以，重写的原型会切断之前的原型。**

[code]

     function Box() {};         //构造对象函数
    
    Box.prototype = {            //构造原型
        constructor : Box,      //将原型强制指向构造函数
        name : 'Lee',
        age : 100,
        run : function () {
            return this.name + this.age + '运行中...';
        }
    };
    
    //重写构造原型
    Box.prototype = {
        age : 200
    };                        //注意：只要重写了构造原型，就会截断原来的构造原型，下面的实列化就访问不了原来的原型了
    
    var box = new Box();                        //实列化对象
    alert(box.run());                            //打印实列化对象里的run方法，因为原型被重写了，重写的原型里没有run方法，报错
[/code]



****内置的引用类型都可以使用原型，**
也就是说js的各种数据类型就是一个对象，所以数据类型对象也是可以使用原型的，比如：String字符串类型，Array数组类型等，这些类型的方法就是它本身对象的原型方法**

****原型对象不仅仅可以在自定义对象的情况下使用，而ECMAScript内置的引用类型都可以使用这种方式，并且内置的引用类型本身也使用了原型。****

**prototype查看一个方法是否是一个类型对象的原型，**

**使用方式：**  
 **类型对象名称.prototype.要查询的方法**

[code]

    alert(Array.prototype.sort);                     //sort就是Array类型的原型方法
    alert(String.prototype.substring);                //substring就是String类型的原型方法
[/code]

**使用对象原型给内置数据类型拓展方法，比如字符串类型对象**

[code]

     //给字符串对象添加一个原型方法
    String.prototype.addstring = function () {        //给String字符串类型添加一个addstring方法
        return this + '，被添加了！';                //this代表调用的字符串
    };
    
    alert('Lee'.addstring());                        //使用这个方法
[/code]

**PS：尽管给原生的内置引用类型添加方法使用起来特别方便，但我们不推荐使用这种方法。因为它可能会导致命名冲突，不利于代码维护。**



**原型的缺点和优点**

**原型模式创建对象也有自己的缺点，它省略了构造函数传参初始化这一过程，带来的缺点就是初始化的值都是一致的。而原型最大的缺点就是它最大的优点，那就是共享。**

**原型中所有属性是被很多实例共享的，共享对于函数非常合适，对于包含基本值的属性也还可以。但如果属性包含引用类型，就存在一定的问题：**

****原型的优点****

**原型的优点就是数据共享，只要在原型里设置一次数据，其他的实列化都共享原型里的数据**

[code]

     //字面量方式创建原型
    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    Box.prototype = {                        //使用字面量的方式创建原型，相当于新创建了一个Object对象
        constructor:Box,              //字面量方式创建原型,将原型的constructor属性强制指向实列对象(构建对象函数)
        name : 'Lee',
        age : 100,
        asdc : ['哥哥','姐姐','妹妹']  //原型里添加一个数组
    };
    
    var a1 = new Box();  //实列化对象1
    alert(a1.asdc); //打印实列化1对里的数字
    //返回：哥哥,姐姐,妹妹
    
    var a2 = new Box();//实列化对象2
    alert(a2.asdc);//打印实列化2对里的数字
    
    //由此可见，原型的优点就是数据共享，只要在原型里设置一次数据，其他的实列化都共享原型里的数据
[/code]

****原型的缺点****

****原型数据是共享的无法保证每个实列化的数据独立，因为原型是共享的，有一个实列改变了原型数据，后面的实列也随之共享了改变后的数据****

[code]

     //字面量方式创建原型
    function Box() {}                            //声明一个构造对象函数，没有初始化数据
                                                //每一个函数都有一个原型对象prototype，向原型对象添加数据时，构造对象函数会调用原型对象数据
    Box.prototype = {                        //使用字面量的方式创建原型，相当于新创建了一个Object对象
        constructor:Box,              //字面量方式创建原型,将原型的constructor属性强制指向实列对象(构建对象函数)
        name : 'Lee',
        age : 100,
        asdc : ['哥哥','姐姐','妹妹']  //原型里添加一个数组
    };
    
    var a1 = new Box();  //实列化对象1
    alert(a1.asdc); //打印实列化1对里的数字
    //返回：哥哥,姐姐,妹妹
    
    var a2 = new Box();//实列化对象2
    a2.asdc.push('弟弟');//向原型里的数组添加一个元素
    alert(a2.asdc);//打印实列化2对里的数字
    //返回：哥哥,姐姐,妹妹,弟弟
    
    alert(a1.asdc);//此时打印实列化1也添加了数据了，因为原型是共享的，有一个实列改变了原型数据，后面的实列也随之共享了改变后的数据
    
    //由此可见，实列化1也添加了数据了，因为原型是共享的，有一个实列改变了原型数据，后面的实列也随之共享了改变后的数据
[/code]

**PS：数据共享的缘故，导致很多开发者放弃使用原型，因为每次实例化出的数据需要保留自己的特性，而不能共享。**



****组合构造函数+原型模式** ： **也就是不共享的数据使用构造函数，共享的数据使用原型****

**为了解决构造传参和共享问题，可以组合构造函数+原型模式：**

[code]

    function Box(name, age) {                     //不共享的使用构造函数
        this.name = name;               //将传参添加到对象属性
        this.age = age;                 //将传参添加到对象属性
        this. family = ['父亲', '母亲', '妹妹'];
    }
    //字面量方式创建原型
    Box.prototype = {                            //共享的使用原型模式
        constructor : Box,
        run : function () {
            return this.name + ',' +this.age + ',' + '家庭成员' + ',' + this.family;
        }
    };
    
    var a1 = new Box('小明',20); //传参实列化对象1
    alert(a1.run()); //打印实列对象1里的原型方法
    //返回：小明,20,家庭成员,父亲,母亲,妹妹
    
    var a2 = new Box('小张',30);//传参实列化对象2
    alert(a2.run());//打印实列对象2里的原型方法
    //返回：小张,30,家庭成员,父亲,母亲,妹妹
[/code]

**PS：这种混合模式很好的解决了传参和引用共享的大难题。是创建对象比较好的方法。**

** **

****动态原型模式** 。也就是将原型封装到构造函数里【重点推荐】**

**构造函数+原型部分让人感觉又很怪异，最好就是把构造函数和原型封装到一起。为了解决这个问题，我们可以使用 **动态原型模式** 。**

[code]

    function Box(name ,age) {                    //将所有信息封装到函数体内
        this.name = name;                 //添加对象属性
        this.age = age;                   //添加对象属性
    
          //将原型封装到构造函数里
        if (typeof this.run != 'function') {            //仅在第一次调用的初始化，判断run不等于方法的时候，才创建原型方法，避免每次实列都创建方法
            Box.prototype.run = function () {
                return this.name + this.age + '运行中...';
            };
        }
    }
    
    var box = new Box('Lee', 100); //实列化对象
    alert(box.run()); //打印对象里的原型方法
    //返回：Lee100运行中...
[/code]

**当第一次调用构造函数时，run()方法发现不存在，然后初始化原型。当第二次调用，就不会初始化，并且第二次创建新对象，原型也不会再初始化了。这样及得到了封装，又实现了原型方法共享，并且属性都保持独立。**

**PS：使用动态原型模式，要注意一点，不可以再使用字面量的方式重写原型，因为会切断实例和新原型之间的联系。**



**寄生构造函数**

**以上讲解了各种方式对象创建的方法，如果这几种方式都不能满足需求，可以使用一开始那种模式：寄生构造函数。**

[code]

     function Box(name, age) {    //创建构建对象函数
        var obj = new Object();  //创建对象
        obj.name = name;         //给对象添加属性
        obj.age = age;           //给对象添加属性
        obj.run = function () {  //给对象添加方法
            return this.name + this.age + '运行中...';
        };
        return obj; //返回对象
    }
    var asdf = Box('NIH',200);
    alert(asdf.run());
[/code]

**寄生构造函数，其实就是工厂模式+构造函数模式。这种模式比较通用，但不能确定对象关系，所以，在可以使用之前所说的模式时，不建议使用此模式。**



****寄生构造数据类型对象的额外方法****

**在什么情况下使用寄生构造函数比较合适呢？假设要创建一个具有额外方法的引用类型。由于之前说明不建议直接String.prototype.addstring，可以通过寄生构造的方式添加。**

[code]

     function myString(string) {             //构造对象拓展函数
        var str = new String(string);   //实列化一个字符串对象
        str.addstring = function () {   //向字符串对象里添加一个方法
            return this + '，被添加了！';
        };
        return str; //返回实列化的字符串
    }
    
    var box = new myString('Lee');            //实列化拓展函数传参
    alert(box.addstring());                 //打印实列化拓展对象里的addstring()方法
    //返回：Lee，被添加了！
[/code]



**稳妥构造函数**

**在一些安全的环境中，比如禁止使用this和new，这里的this是构造函数里不使用this，这里的new是在外部实例化构造函数时不使用new。这种创建方式叫做稳妥构造函数。**

[code]

     function Box(name , age) {   //构造函数
        var obj = new Object();  //创建一个对象
        obj.run = function () {  //给对象添加一个方法
            return name + age + '运行中...';        //直接接受函数参数name和age
        };
        return obj; //返回对象
    }
    
    var box = Box('Lee', 100);                    //直接调用函数
    alert(box.run());   //打印构造函数里的run方法
[/code]

**PS：稳妥构造函数和寄生类似。**



**四．** **继承**

**prototype继承的方式依靠原型链完成**

**继承是面向对象中一个比较核心的概念。其他正统面向对象语言都会用两种方式实现继承：一个是接口实现，一个是继承。而ECMAScript只支持继承，不支持接口实现，而实现继承的方式依靠原型链完成。**

[code]

     function Box() {                            //Box构造对象函数(父类)
        this.name = 'Lee';                     //向对象里添加一个name属性
    }
    
    function Desk() {                            //Desk构造对象函数（子类）
        this.age = 100;                         //向对象里添加一个age属性
    }
    
    Desk.prototype = new Box();                    //Desc继承了Box，通过原型，形成链条，子类的原型等于实列化父类
    
    var desk = new Desk();
    alert(desk.age);
    alert(desk.name);                            //得到被继承的name属
    //以此让子类继承父类
    
    function Table() {                            //Table构造对象函数（孙类）
    this.level = 'AAAAA';                       //向对象里添加一个age属性
    }
    
    Table.prototype = new Desk();                //Table继承了Desk，通过原型，形成链条，孙类的原型等于实列化子类
    
    var table = new Table();
    alert(table.name);                            //继承了Box的name属性
    alert(table.age);                           //继承了Desk的age属性
[/code]

![](https://images2015.cnblogs.com/blog/955761/201611/955761-20161113211925764-1365917034.png)

**ps如果一个对象的实列和原型里都有相同的一个属性，按照就近原则，先到实列中查找，实列中没有在到原型中**



**以上原型链继承还缺少一环，那就是Obejct，所有的构造函数都继承自Obejct。而继承Object是自动完成的，并不需要程序员手动继承。**

**经过继承后的实例，他们的从属关系会怎样呢？**

[code]

     function Box() {                            //Box构造对象函数(父类)
        this.name = 'Lee';                     //向对象里添加一个name属性
    }
    
    function Desk() {                            //Desk构造对象函数（子类）
        this.age = 100;                         //向对象里添加一个age属性
    }
    
    Desk.prototype = new Box();                    //Desc继承了Box，通过原型，形成链条，子类的原型等于实列化父类
    
    function Table() {                            //Table构造对象函数（孙类）
    this.level = 'AAAAA';                       //向对象里添加一个age属性
    }
    
    Table.prototype = new Desk();                //Table继承了Desk，通过原型，形成链条，孙类的原型等于实列化子类
    
    var table = new Table(); //实列化Table对象
    var desk = new Desk();   //实列化Desk对象
    
    alert(table instanceof Object);                //true，判断table实列化是否从属于Object对象
    alert(desk instanceof Table);                    //false，判断desk实列化是否从属于Table对象，因为desk是Table的父类不从属
    alert(table instanceof Desk);                    //true，判断table实列化是否从属于Desk对象
    alert(table instanceof Box);                    //true，判断table实列化是否从属于Box对象
[/code]

**在JavaScript里，被继承的函数称为超类型(父类，基类也行，其他语言叫法)，继承的函数称为子类型(子类，派生类)。继承也有之前问题，比如字面量重写原型会中断关系，使用引用类型的原型，并且子类型还无法给超类型传递参数。**



**借用构造函数（ **对象冒充** ）继承**

**为了解决引用共享和超类型无法传参的问题，我们采用一种叫借用构造函数的技术，或者称为对象冒充(伪造对象、经典继承)的技术来解决这两种问题。**

[code]

     function Box(age) {   //构造对象函数
        this.name = ['Lee', 'Jack', 'Hello']; //向对象添加一个数组
        this.age = age; //向对象添加一个属性
    }
    
    function Desk(age) {  //构造对象函数
        Box.call(this, age);                        //对象冒充，给超类型传参
    }
    
    var desk = new Desk(200);  //实列化冒充Box对象传参
    alert(desk.age);
    alert(desk.name);
    desk.name.push('AAA');                        //添加的新数据，只给desk
    alert(desk.name);
[/code]



**原型链+借用构造函数（对象冒充）组合继承【重点推荐】**

**借用构造函数虽然解决了刚才两种问题，但没有原型，复用则无从谈起。所以，我们需要原型链+借用构造函数的模式，这种模式成为组合继承** 。

[code]

    function Box(age) { //构造对象函数
        this.name = ['Lee', 'Jack', 'Hello']; //给对象添加一个数组
        this.age = age; //给对象添加一个方法
    }
    
    Box.prototype.run = function () {    //给Box对象添加一个原型方法            
        return this.name + this.age;
    };
    
    function Desk(age) {  //对象冒充函数传参
        Box.call(this, age);                        //将Desk对象冒充Box对象
    }
    
    Desk.prototype = new Box();                    //原型链继承，Desk对象继承Box对象的数据
    
    var desk = new Desk(100);    //实列化冒充对象传参100
    alert(desk.run()); //打印冒充对象里的原型run()方法，也就是Box的原型方法，因为Desk对象冒充的Box对象
[/code]



**原型式继承**

**还有一种继承模式叫做：原型式继承；这种继承借助原型并基于已有的对象创建新对象，同时还不必因此创建自定义类型。**

[code]

     function obj(o) {                        //创建一个普通函数，接收一个参数
        function F() {}                        //创建一个构造函数
        F.prototype = o;                    //把普通函数的传参，赋值给构造对象的原型
        return new F();                        //最终返回出实例化的构造函数
    }
    
    var box = {                                //字面量创建对象
        name : 'Lee',                      //创建对象属性
        arr : ['哥哥','妹妹','姐姐']        //创建对象数组
    };
    
    var box1 = obj(box);        //将box对象当做参数传给obj函数
    alert(box1.name);      //打印对象原型的name属性
    //返回：Lee
    box1.name = 'Jack';    //向构造对象实列里添加一个属性
    alert(box1.name);      //打印构造对象实列里的name
    //返回：Jack
    
    alert(box1.arr);      //打印对象原型的arr属性
    //返回：哥哥,妹妹,姐姐
    box1.arr.push('父母'); //向对象原型里的数字追加一个元素
    alert(box1.arr);       //打印对象原型里追加后的数字
    //返回：哥哥,妹妹,姐姐,父母
    
    var box2 = obj(box);    //将box对象当做参数传给obj函数
    alert(box2.name);       //打印构造对象原型里的name属性
    //返回：Lee
    alert(box2.arr);        //引用类型共享了
    //返回：哥哥,妹妹,姐姐,父母
[/code]



**寄生式继承，把原型式+工厂模式结合而来，目的是为了封装创建对象的过程。**

[code]

     //临时函数
    function obj(o) {                        //创建一个普通函数，接收一个参数
        function F() {}                        //创建一个构造函数
        F.prototype = o;                    //把普通函数的传参，赋值给构造对象的原型
        return new F();                        //最终返回出实例化的构造函数
    }
    
    //创建对象
    var box = {                                //字面量创建对象
        name : 'Lee',                      //创建对象属性
        arr : ['哥哥','妹妹','姐姐']        //创建对象数组
    };
    
    //寄生函数
    function create(o) {                    //创建寄生函数，将对象当做参数传进来
        var f= obj(o);                    //又将对象当做参数传给obj函数执行，得到的是构造对象原型实列化后的对象
        f.run = function () {            //向构造对象里添加一个实列方法
            return this.arr;                //同样，会共享引用，因为还是调用的对象原型
        };
        return f;                   //返回最后实列后的对象
    }
    var box1 = create(box); //实列化对象，将box对象传到寄生函数，在由寄生函数传到临时函数添加成构造对象的原型
    alert(box1.run());//打印对象实列里的run方法
[/code]



**组合式继承**

**组合式继承是JavaScript最常用的继承模式；但，组合式继承也有一点小问题，就是超类型在使用过程中会被调用两次：一次是创建子类型的时候，另一次是在子类型构造函数的内部。**

[code]

     function Box(name) {     //构造对象函数
        this.name = name;    //添加对象实列属性
        this.arr = ['哥哥','妹妹','父母']; //添加对象实列数组
    }
    
    Box.prototype.run = function () {  //添加对象原型方法
        return this.name;
    };
    
    function Desk(name, age) {    //创建冒充对象，将Desk冒充Box对象
        Box.call(this, name);  //第二次调用Box
        this.age = age;
    }
    
    Desk.prototype = new Box();                //    Desk的原型等于new Box()，也就是Desk继承 Box对象
    //第一次调用Box
    
    var asdf = new Desk('LII',200);  //实列化对象
    alert(asdf.run());    //打印对象里原型方法
    
    //超类型在使用过程中会被调用两次：一次是创建子类型的时候，另一次是在子类型构造函数的内部。
[/code]



**寄生组合继承【重点推荐】**

**以上代码是之前的组合继承，那么寄生组合继承，解决了两次调用的问题。**

[code]

     function obj(o) {   //创建一个中转函数
        function F() {}   //创建一个对象
        F.prototype = o;   //将函数接收到的参数添加到对象原型
        return new F();   //返回实列对象
    }
    
    function create(box, desk) {     //创建寄生函数，接收box, desk对象
        var f = obj(box.prototype);   //将box对象的原型传入obj函数，得到obj实列对象
        f.constructor = desk;  //将obj实列对象的原型指向desk
        desk.prototype = f;  //将desk的原型指向f对象
    }
    
    function Box(name) {      //创建Box对象
        this.name = name;
        this.arr = ['哥哥','妹妹','父母'];
    }
    
    Box.prototype.run = function () {   //添加Box原型方法
        return this.name;
    };
    
    function Desk(name, age) {   //定义冒充对象
        Box.call(this, name);
        this.age = age;
    }
    
    create(Box, Desk);                        //通过这里实现继承
    
    var desk = new Desk('Lee',100);
    desk.arr.push('姐姐');
    alert(desk.arr);
    alert(desk.run());                            //只共享了方法
    
    var desk2 = new Desk('Jack', 200);
    alert(desk2.arr);                            //引用问题解决
[/code]



