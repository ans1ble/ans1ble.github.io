第一百一十节，JavaScript匿名函数和闭包

**JavaScript匿名函数和闭包**

**学习要点：**

**1.匿名函数**

**2.闭包**

**匿名函数就是没有名字的函数，闭包是可访问一个函数作用域里变量的函数。声明：本节内容需要有面向对象和少量设计模式基础，否则无法听懂.(所需基础15章的时候已经声明过了)。**



**一．** **匿名函数**

**普通函数**

    
    
     function box() {                            //函数名是box
        return 'Lee';
    }
    
    alert(box());//通过函数名称来执行函数



**匿名函数**

**就是没有名称的函数**

    
    
     //匿名函数
    function () {                                //匿名函数，会报错
        return 'Lee';
    }
    //匿名函数,因为没有名称所以无法执行，也就会报错



**通过表达式自我执行匿名函数**

    
    
     //通过表达式自我执行
    (function box() {                            //用括号将函数体，封装成表达式，就是用一对括号将函数体括起来，
        alert('Lee');
    })();                                        //最后用一个()表示执行函数，
    //返回：Lee



**用过变量执行匿名函数**

    
    
     //把匿名函数赋值给变量
    var box = function () {                        //将匿名函数赋给变量
        return 'Lee';
    };
    alert(box());                                //调用方式和函数调用相似，也就是通过变量名称加()执行函数



**函数里的匿名函数，产生闭包**



    
    
    //函数里的匿名函数
    function box () {
        return function () {                        //函数里的匿名函数，产生闭包
            return 'Lee';
        }
    }
    //执行方式1
    alert(box()());                                //通过执行函数，在加上一对括号执行匿名函数
    
    //执行方式2
    var asdf = box();   //将执行函数赋值给一个变量，
    alert(asdf());    //在通过变量在执行里面匿名函数





**二．** **闭包， 是在 **函数里返回匿名函数【重点】****

**闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包的常见的方式，就是在一个函数内部创建另一个函数，通过另一个函数访问这个函数的局部变量。**



**通过闭包可以返回局部变量**



    
    
    //通过闭包可以返回局部变量
    function box() {           //创建box函数
        var user = 'Lee';       //函数里有一个局部变量
        return function () {    //通过匿名函数返回box()局部变量
            return user;     //返回box()局部变量
        };
    }
    alert(box()());                                //通过box()()来直接调用匿名函数返回值
    
    var b = box();
    alert(b());                                    //另一种方式调用匿名函数返回值
    //返回Lee





**闭包优点和缺点**

**闭包可以把局部变量驻留在内存中**

**使用闭包有一个优点，也是它的缺点：就是可以把局部变量驻留在内存中，可以避免使用全局变量。(全局变量污染导致应用程序不可预测性，每个模块都可调用必将引来灾难，所以推荐使用私有的，封装的局部变量)。**  
    
    
    //通过全局变量来累加
    var age = 100;                                //全局变量
    function box1() {
        age ++;                                //模块级可以调用全局变量，进行累加
    }
    box1();                                    //执行函数，累加了
    alert(age);                                //输出全局变量
    //101
    box1();                                    //执行函数，累加了
    alert(age);                                //输出全局变量
    //102
    box1();                                    //执行函数，累加了
    alert(age);                                //输出全局变量
    //103
    
    //通过局部变量无法实现累加
    function box2() {
        var age = 100;                      //局部变量
        age ++;                                //累加
        return age;
    }
    
    alert(box2());                                //101
    alert(box2());                                //101，无法实现，因为又被初始化了
    
    //通过闭包可以实现局部变量的累加，闭包可以把局部变量驻留在内存中
    function box() {        //创建函数
        var age = 100;      //局部变量
        return function () {    //创建闭包匿名函数
            age ++;         //局部变量++
            return age;    //返回累加后的局部变量
        }
    }
    var b = box();                                //获得函数
    alert(b());                                    //调用匿名函数
    alert(b());                                    //第二次调用匿名函数，实现累加

**PS：由于闭包里作用域返回的局部变量资源不会被立刻销毁回收，所以可能会占用更多的内存。过度使用闭包会导致性能下降，建议在非常有必要的时候才使用闭包。**



**循环里包含匿名函数，出现问题**

**作用域链的机制导致一个问题，在循环中里的匿名函数取得的任何变量都是最后一个值。**

    
    
     //循环里包含匿名函数
    function box() {      //创建函数
        var arr = [];    //创建一个空数组
    
        for (var i = 0; i < 5; i++) {    //循环5次
            arr[i] = function () {      //每次循环将匿名函数的返回值，通过数组下标方式添加到数组
                return i;
            };
        }
        return arr; //最后返回添加后的数组
    }
    
    var b = box();                                //得到函数返回的数组
    alert(b.length);                            //得到函数数组的长度
    for (var i = 0; i < b.length; i++) {        //根据数组的长度，循环次数
        alert(b[i]());                            //输出每个函数的值，都是最后一个值，因为在执行函数时就已经循环完了，最终得到的都是5
    }

**上面的例子输出的结果都是5，也就是循环后得到的最大的i值。因为b[i]调用的是匿名函数，匿名函数并没有自我执行，等到调用的时候，box()已执行完毕，i早已变成5，所以最终的结果就是5个5。**



**循环里包含匿名函数-改1，自我执行匿名函数**

    
    
     //循环里包含匿名函数-改1，自我执行匿名函数
    function box() {   //创建函数
        var arr = [];  //函数里创建一个空数组
    
        for (var i = 0; i < 5; i++) {    //循环5次
            arr[i] = (function (num) {        //每次循环自我执行匿名函数，得到匿名函数的返回值，将返回值通过数组下标添加到数组
                return num;
            })(i);                            //每次执行匿名函数，并且将每次循环的i传入匿名函数
        }
        return arr;  //最后返回数组
    }
    
    var b = box();      //执行函数得到，数组
    for (var i = 0; i < b.length; i++) {   //根据数组的长度来循环次数
        alert(b[i]);                            //每次循环通过数组下标，来打印数组里的元素
    }
    //返回
    //0
    //1
    //2
    //3
    //4

**改1中，我们让匿名函数进行自我执行，导致最终返回给a[i]的是数组而不是函数了。最终导致b[0]-b[4]中保留了0,1,2,3,4的值。**



**循环里包含匿名函数-改2，匿名函数下再做个匿名函数（ **闭包** ）**

    
    
    //循环里包含匿名函数-改2，匿名函数下再做个匿名函数
    function box() {     //创建函数
        var arr = [];    //函数里创建数组
    
        for (var i = 0; i < 5; i++) {   //循环5次
            arr[i] = (function (num) {    //自我执行匿名函数，将每次循环的i传到匿名函数1，
                return function () {      //匿名函数2直接返回值i的值，函数里的函数闭包，闭包可以将i驻留在内存
                    return num;                //原理和改1一样
                }
            })(i);                      //执行匿名函数，并将i传入匿名函数
        }
        return arr;  //返回数组
    }
    
    var b = box();  //执行函数，得到数组
    for (var i = 0; i < b.length; i++) {  //根据数组的长度来循环次数
        alert(b[i]());                    //通过数组的下标来获取数组的元素
    }
    //返回
    //0
    //1
    //2
    //3
    //4

**改1和改2中，我们通过匿名函数自我执行，立即把结果赋值给a[i]。每一个i，是调用方通过按值传递的，所以最终返回的都是指定的递增的i。而不是box()函数里的i。**



**关于this对象，也就是 **this作用域在对象闭包里的情况****

**在闭包中使用this对象也可能会导致一些问题，this对象是在运行时基于函数的执行环境绑定的，如果this在全局范围就是window，如果在对象内部就指向这个对象。
而闭包却在运行时指向window作用域的，因为闭包并不属于这个对象的属性或方法。**

******this作用域在对象闭包里，作用域指向的 **window全局********

    
    
     var user = 'The Window';  //全局变量创建字符串
    
    var obj = {    //创建对象
        user : 'The Object',  //添加一个对象属性
        getUserFunction : function () {  //添加一个对象方法
            return function () {                    //返回闭包，闭包不属于obj，里面的this指向window
                return this.user;   //这里的this指向window作用域，那么就是全局变量user
            };
        }
    };
    
    alert(obj.getUserFunction()());        //打印对象里的getUserFunction方法，返回的是全局变量user
    //返回：The Window
    
    //可以强制指向某个对象，用对象冒充，将自己传入冒充方法里，冒充自己，这样this就指向了对象本身
    alert(obj.getUserFunction().call(obj));            //The Object
    //返回：The Object



**将作用域在对象闭包里，强制指向对象**

    
    
     var user = 'The Window';  //全局变量创建字符串
    
    var obj = {    //创建对象
        user : 'The Object',  //添加一个对象属性
        getUserFunction : function () {  //添加一个对象方法
            var zyy = this;    //创建一个变量等于作用域，这里的作用域在闭包外，就是指向的对象本身
            return function () {                    //返回闭包，闭包不属于obj
                return zyy.user;   //这里使用zyy变量作用域，这样就强制将作用域指向对象
            };
        }
    };
    
    alert(obj.getUserFunction()());        //打印对象里的getUserFunction方法，返回的是对象里的user属性
    //返回：The Object



**内存泄漏，也就是无法销毁驻留在内存中的元素**

**也就是在使用完后用null; 解除引用，进行回收**

**由于IE的JScript对象和DOM对象使用不同的垃圾收集方式，因此闭包在IE中会导致一些问题。就是内存泄漏的问题，也就是无法销毁驻留在内存中的元素。以下代码有两个知识点还没有学习到，一个是DOM，一个是事件。**



    
    
    function box() {
        var oDiv = document.getElementById('oDiv');    //oDiv用完之后一直驻留在内存
        oDiv.onclick = function () {
            alert(oDiv.innerHTML);                    //这里用oDiv导致内存泄漏
        };
    }
    box();
    
    那么在最后应该将oDiv解除引用来避免内存泄漏。
    function box() {
        var oDiv = document.getElementById('oDiv');    
    var text = oDiv.innerHTML;
        oDiv.onclick = function () {
            alert(text);                    
        };
    oDiv = null;                                //解除引用
    }



**PS：如果并没有使用解除引用，那么需要等到浏览器关闭才得以释放。**

** **

**匿名函数私有化**

**模仿块级作用域**

**JavaScript没有块级作用域的概念。**

    
    
     function box1(count) {     //创建一个函数
        for (var i=0; i<count; i++) {} //根据传参进行循环次数
        alert(i);                    //打印i,i不会因为离开了for块就失效,
    }
    box1(2);
    //返回;2
    
    function box2(count) {  //创建一个函数
        for (var i=0; i<count; i++) {}  //根据传参进行循环次数
        var i;                                //就算重新声明一个i变量
        alert(i);                          //就算重新声明一个i变量，也能打印i
    }
    box2(2);
    //返回：2

**以上两个例子，说明JavaScript没有块级语句的作用域，if () {} for ()
{}等没有作用域，如果有，出了这个范围i就应该被销毁了。就算重新声明同一个变量也不会改变它的值。**

**JavaScript不会提醒你是否多次声明了同一个变量；遇到这种情况，它只会对后续的声明视而不见(如果初始化了，当然还会执行的)。使用模仿块级作用域可避免这个问题。**



**模仿块级作用域(私有作用域)**

**就是将要私有的变量或者函数写在匿名函数里，这样就私有了**

**列1**

    
    
    ( function () {
        //这里是块级作用域
    })();

**列2**

    
    
     //使用块级作用域(私有作用域)改写
    function box(count) {
        (function () {
            for (var i = 0; i<count; i++) {}
        })();
        alert(i);                                //报错，无法访问
    }
    box(2);

**使用了块级作用域(私有作用域)后，匿名函数中定义的任何变量，都会在执行结束时被销毁。这种技术经常在全局作用域中被用在函数外部，从而限制向全局作用域中添加过多的变量和函数。一般来说，我们都应该尽可能少向全局作用域中添加变量和函数。在大型项目中，多人开发的时候，过多的全局变量和函数很容易导致命名冲突，引起灾难性的后果。如果采用块级作用域(私有作用域)，每个开发者既可以使用自己的变量，又不必担心搞乱全局作用域。**

    
    
    ( function () {
        var box = [1,2,3,4];
        alert(box);                            //box出来就不认识了
    })();

**在全局作用域中使用块级作用域可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。只要函数执行完毕，就可以立即销毁其作用域链了。**



**私有变量**

**JavaScript没有私有属性的概念；所有的对象属性都是公有的。不过，却有一个私有变量的概念。任何在函数中定义的变量，都可以认为是私有变量，因为不能在函数的外部访问这些变量。**

    
    
     function box() {
        var age = 100;                            //私有变量，外部无法访问
    }

**而通过函数内部创建一个闭包，那么闭包通过自己的作用域链也可以访问这些变量。而利用这一点，可以创建用于访问私有变量的公有方法。**

    
    
     function Box() {
        var age = 100;                            //私有变量
        function run() {                        //私有函数
            return '运行中...';
        }
        this.get = function () {                    //对外公共的特权方法
            return age + run();
        };
    }
    
    var box = new Box();
    alert(box.get());

**可以通过构造方法传参来访问私有变量。**

    
    
     function Person(value) {   //构造对象函数
        var user = value;                        //这句其实可以省略
        this.getUser = function () {  //添加对象方法
            return user;   //返回user对象
        };
        this.setUser = function (value) {  //添加对象方法接收一个参数
            user = value;  //返回传参
        };
    }
    var person = new Person('变量'); //实列化对象
    alert(person.getUser()); //打印对象里的getUser()方法
    //返回：变量

**但是对象的方法，在多次调用的时候，会多次创建。可以使用静态私有变量来避免这个问题。**



**静态私有变量**

**通过块级作用域(私有作用域)中定义私有变量或函数，同样可以创建对外公共的特权方法。**

    
    
    ( function () {   //创建一个自我执行匿名函数
        var age = 100;   //私有变量
        function run() {   //私有函数
            return '运行中...';
        }
        Box = function () {};                    //构造方法
        Box.prototype.go = function () {            //原型方法
            return age + run();  //返回私有变量加私有函数
        };
    })();
    
    
    var box = new Box(); //实列化对象
    alert(box.go()); //打印对象里的go方法

**上面的对象声明，采用的是Box = function () {} 而不是function Box() {}
因为如果用后面这种，就变成私有函数了，无法在全局访问到了，所以使用了前面这种。**



**使用了prototype导致方法共享了，而user也就变成静态属性了。(所谓静态属性，即共享于不同对象中的属性)。**

    
    
    ( function () {  //创建自我执行匿名函数
        var user = '';   //创建私有变量等于空字符串
        Person = function (value) {      //创建全局构造对象函数
            user = value;   //将对象传参重新赋值给私有变量
        };
        Person.prototype.getUser = function () { //创建原型方法
            return user; //返回私有变量
        };
        Person.prototype.setUser2 = function (value) {  //创建原型方法接收一个参数
            user = value;  //将传参赋值给私有变量
            return user;
        }
    })();
    
    var abdc = new Person('变量');//实列化对象
    alert(abdc.getUser()); //打印对象里的方法
    alert(abdc.setUser2('变量2'));

**使用了prototype导致方法共享了，而user也就变成静态属性了。(所谓静态属性，即共享于不同对象中的属性)。**



**模块模式**

**之前采用的都是构造函数的方式来创建私有变量和特权方法。那么对象字面量方式就采用模块模式来创建。**

**列1**

    
    
     var box = {                                //字面量对象，也是单例对象
        age : 100,                             //这是公有属性，将要改成私有
        run : function () {                    //这是公有函数，将要改成私有
            return '运行中...';
        }
    };

**列2**

    
    
     //私有化变量和函数：
    var box = function () {  //创建一个自我执行函数
        var age = 100;  //私有变量
        function run() {  //私有函数
            return '运行中...';
        }
        return {                                //直接返回对象
            go : function () {     //创建一个对象方法
                return age + run();  //返回私有变量加私有函数
            }
        };
    }();
    
    alert(box.go());  //打印box函数里的go方法

**上面的直接返回对象的例子，也可以这么写：**

    
    
     var box = function () {  //自我执行函数
        var age = 100;   //私有变量
        function run() {  //私有函数
            return '运行中...';
        }
        var obj =  {                            //创建字面量对象
            go : function () {   //创建对象方法
                return age + run();  //返回私有变量加私有方法
            }
        };
        return obj;                            //最后返回这个对象
    }();
    
    alert(box.go());

**字面量的对象声明，其实在设计模式中可以看作是一种单例模式，所谓单例模式，就是永远保持对象的一个实例。**



**增强的模块模式，这种模式适合返回自定义对象，也就是构造函数。**

    
    
     function Desk(){};   //创建一个对象函数
    var box = function () {  //创建一个自我执行函数
        var age = 100;  //创建私有变量
        function run() {  //创建私有函数
        return '运行中...';
        }
        var desk = new Desk();        //实列化构造对象函数
        desk.go = function () {   //向对象添加一个方法
            return age + run(); //返回私有变量加私有函数
        };
        return desk; //最后返回这个对象实列
    }();
    alert(box.go()); //打印对象里go()方法



