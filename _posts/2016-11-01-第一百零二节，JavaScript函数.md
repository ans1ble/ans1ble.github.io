第一百零二节，JavaScript函数

**JavaScript函数**



**学习要点：**



**1.函数声明**



**2.return返回值**



**3.arguments对象**



**函数是定义一次但却可以调用或执行任意多次的一段JS代码。函数有时会有参数，即函数被调用时指定了值的局部变量。函数常常使用这些参数来计算一个返回值，这个值也成为函数调用表达式的值。**



**一．** **函数声明**

**函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方、任何时候调用执行。ECMAScript中的函数使用function关键字来声明，后跟一组参数以及函数体。**

****function关键字声明函数****

****无参函数：****

    
    
     function box() {                               //没有参数的函数
        alert('只有函数被调用，我才会被之执行');   
    }
    box();                                    //直接调用执行函数

**有参函数：**

**如果有参函数在调用时没有传参数，会自动赋值参数为undefined**

    
    
     function box(name, age) {                    //带参数的函数
        alert('你的姓名：'+name+'，年龄：'+age);
    }
    box('李炎恢',28);                            //调用函数，并传参



**二．** **return** **返回值，关键字，给函数定义返回值**

**带参和不带参的函数，都没有定义返回值，而是调用后直接执行的。实际上，任何函数都可以通过return语句跟后面的要返回的值来实现返回值。**

**无参定义返回值：**

    
    
     function box() {                            //没有参数的函数
        return '我被返回了！';                    //通过return把函数的最终值返回
    }            
    alert(box());                                //调用函数会得到返回值，然后外面输出

**有参定义返回值：**

    
    
     function box(name, age) {                    //有参数的函数
        return '你的姓名：'+name+'，年龄：'+age;//通过return 把函数的最终值返回
    }
    alert(box('李炎恢', 28));                        //调用函数得到返回值，然后外面输出

**我们还可以把函数的返回值赋给一个变量，然后通过变量进行操作。**

    
    
     function box(num1, num2) {
        return num1 * num2;
    }
    var num = box(10, 5);                        //函数得到的返回值赋给变量
    alert(num);   

**return语句还有一个功能就是退出当前函数，注意和break的区别。**

**PS：break用在循环和switch分支语句里。**

**注意：函数里一旦遇到 **return返回关键字后，下面还有代码就不会执行了****

    
    
     function box(num) {
        if (num < 5)  return num;            //满足条件，就返回num
        return 100;                            //返回之后，就不执行下面的语句了
    }
    alert(box(2));                          //打印函数变量



**三．** **arguments** **对象**

**ECMAScript函数不介意传递进来多少参数，也不会因为参数不统一而错误。实际上，函数体内可以通过arguments对象来接收传递进来的参数。**

**也就是函数可以不设置形式参数，在函数里可以用 **arguments来接收实际参数的传参，****

******arguments以数组下标方式类获取实际参数******

    
    
     function box() {
        return arguments[0]+' | '+arguments[1];        //arguments[0]，将调用函数时传的参数，当做数组索引下标的方式获取到
                                                    //arguments[0]，就是获取传参的第一个参数1
                                                    //arguments[1]，就是获取传参的第二个参数2
    }
    alert(box(1,2,3,4,5,6));                        //传递参数

**arguments对象的length属性可以得到参数的数量。**

**也就是 **arguments对象的length属性可以检查到，调用函数时传了多少个实际参数****

    
    
     function box() {
        return arguments.length;                    //得到6
    }
    alert(box(1,2,3,4,5,6));

**我们可以利用length这个属性，来智能的判断有多少参数，然后把参数进行合理的应用。比如，要实现一个加法运算，将所有传进来的数字累加，而数字的个数又不确定。**

    
    
     function box() {
        var sum = 0;
        if (arguments.length == 0) return sum;        //如果没有参数，返回sum变量
        for(var i = 0;i < arguments.length; i++) {    //如果有，就统计有多少位参数，循环对应次数，然后就累加
            sum = sum + arguments[i];
        }
        return sum;                            //返回累加结果26
    }
    alert(box(5,9,12));

**ECMAScript中的函数，没有像其他高级语言那种函数重载功能。**

    
    
     function box(num) {
        return num + 100;
    }
    function box (num) {                        //会执行这个函数
        return num + 200;
    }
    alert(box(50));                                //返回结果



**函数补充， **Function类型****

**学习要点：**

**1.函数的声明方式**

**2.作为值的函数**

**3.函数的内部属性**

**4.函数属性和方法**



**在ECMAScript中，Function(函数)类型实际上是对象。每个函数都是Function类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此函数名实际上也是一个指向函数对象的指针。**



**一．** **函数的声明方式**

**1.普通的函数声明**

    
    
     function box(num1, num2) {
        return num1+ num2;
    }
    alert(box(1,2));

**2.使用变量初始化函数**

    
    
     var box= function(num1, num2) {
        return num1 + num2;
    };
    alert(box(1,2));

**3.使用Function构造函数【不推荐】**

    
    
     var box= new Function('num1', 'num2' ,'return num1 + num2');
    alert(box(1,2));

**PS：第三种方式我们不推荐，因为这种语法会导致解析两次代码（第一次解析常规ECMAScript代码，第二次是解析传入构造函数中的字符串），从而影响性能。但我们可以通过这种语法来理解"函数是对象，函数名是指针"的概念。**



**二．作为值的函数**

**ECMAScript中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。**

**将一个函数当做参数传给另外一个函数**

    
    
     function box(sumFunction, num) {              //定义函数box
        return sumFunction(num);                  //返回执行box函数，并传出参数10
    }
    
    function sum(num) {                          //定义函数sum
        return num + 10;                         //返回传入参数加10
    }
    
    var result = box(sum, 10);                    //执行函数box，将sum函数当做参数传入box函数
    alert(result);



**三．** **函数内部属性**

**在函数内部，有两个特殊的对象：arguments和this。arguments是一个类数组对象，包含着传入函数中的所有参数，主要用途是保存函数参数。但这个对象还有一个名叫callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数。**

**阶乘递归**

    
    
     function box(num) {
        if (num <= 1) {
            return 1;
        } else {
            return num * box(num-1);            //4 * 3 * 2 * 1=24阶乘，递归
        }
    }
    alert(box(4));



**对于阶乘函数一般要用到递归算法，所以函数内部一定会调用自身；如果函数名不改变是没有问题的，但一旦改变函数名，内部的自身调用需要逐一修改。为了解决这个问题，我们可以使用arguments.callee来代替。**

**callee属性， **该属性是一个指针，指向拥有这个arguments对象的函数****

    
    
     function box(num) {
        if (num <= 1) {
            return 1;
        } else {
            return num * arguments.callee(num-1);        //使用callee来执行box函数自身
        }
    }
    alert(box(4));



**this属性**

**函数内部另一个特殊对象是this，其行为与Java和C#中的this大致相似。换句话说，this引用的是函数，数据以执行操作的对象，或者说函数调用语句所处的那个作用域。PS：当在全局作用域中调用函数时，this对象引用的就是window。**

**window是一个对象，而且是js里面最大的对象，是最外围的对象**

    
    
    alert(window);          //打印对象，返回[object Window]
    alert(typeof window); //查看对象类型

**this在全局作用域中时 **this就是 **window对象******

    
    
    alert( this); //返回[object Window]

**全局变量都是Window的属性**

    
    
     //全局变量都是Window的属性
    var color = "红色的";   //声明一个变量
    alert(window.color);    //通过Window属性打印变量

**通过this打印全局变量**

    
    
     var color = "红色的";   //声明一个变量
    alert(this.color);    //通过this属性打印变量,全局变量也可以通过this来打印，也等同于通过Window打印

**window.color = "红色"; 相当于var color = "红色";**

    
    
    window.color = "红色";  //相当于var color = "红色";
    alert(color);
    var color = "红色";
    alert(color);



**this在对象里面的指向的对象本身**

**注意： **this在对象里面的指向的对象本身****

    
    
     var box = {                   //创建一个对象
        color:"蓝色",             //对象里的一个字段，等同于一个变量
        saycolor:function(){     //对象里的一个方法，也就是匿名函数
            alert(this.color);   //此时的this指向的是box对象本身，
        }
    };
    box.saycolor();              //执行对象里面的saycolor()方法



**this在函数与对象里面的区别**

    
    
    window.color = '红色的';                     //或者var color = '红色的';也行
    
    var box = {                                //创建一个对象
        color : '蓝色的'                       //定义一个字段
    };
    
    function sayColor() {                     //创建一个普通函数
        alert(this.color);                       //打印this下面的color
    }
    sayColor();                                //此时执行函数，函数里的this指向的window，所以打印的window.color
    //返回红色的
    
    box.sayColor = sayColor;                   //将sayColor()函数，追加到box对象里，此时sayColor()函数里的this就在对象里了，this在对象里指向的就是对象本身
    box.sayColor();                            //此时执行box对象里的sayColor()函数，打印的就是对象里面的color
    //返回蓝色的



四． **函数属性和方法**

**ECMAScript中的函数是对象，因此函数也有属性和方法。每个函数都包含两个属性：length和prototype。其中，length属性表示函数希望接收的命名参数的个数。**

****length属性表示函数希望接收的命名参数的个数。****

    
    
     function box(name,age){
        alert(name + age);
    }
    box(5,6); //执行函数
    
    alert(box.length); //查看函数希望接收的命名参数的个数
    //返回2



**prototype属性**



**PS：对于prototype属性，它是保存所有实例方法的真正所在，也就是原型。这个属性，我们将在面向对象一章详细介绍。而prototype下有两个方法：apply()和call()，每个函数都包含这两个非继承而来的方法。这两个方法的用途都在特定的作用域中调用函数，实际上等于设置函数体内this对象的值。
简单一句话理解就是 **apply()和call()方法可以冒充一个函数执行****

**  apply()方法冒充另外一个函数，第一个参数是要冒充的函数的作用域,第二个参数是数组类型的形式参数，用于接收函数的形式参数**

****冒充一个函数，实际上就是将要冒充的函数指向指定的作用域去执行****

    
    
     function box(num1,num2){       //原函数
        return num1 + num2;
    }
    alert(box(1,2));  //执行打印返回数据
    
    function saybox(num1,num2){                     //冒充box函数执行，实际就是调用了box函数
        return box.apply(this,[num1,num2]);         //用apply方法冒充另外一个函数，第一个参数是要冒充的函数的作用域，此时this就是box函数的作用域，this就是window
                                                     //第二个参数是数组类型的形式参数，用于接收函数的形式参数
    }
    alert(saybox(3,4)); //执行冒充函数
    
    
    **第二个参也可以用arguments属性类接收实际参数  
    **
    
    
     function box(num1,num2){       //原函数
        return num1 + num2;
    }
    alert(box(1,2));  //执行打印返回数据
    
    function saybox(num1,num2){                     //冒充box函数执行，实际就是调用了box函数
        return box.apply(this,arguments);         //用apply方法冒充另外一个函数，第一个参数是要冒充的函数的作用域，此时this就是box函数的作用域，this就是window
                                                     //第二个参也可以用arguments属性类接收实际参数
    }
    alert(saybox(3,4)); //执行冒充函数



**call()方法于apply()方法相同，他们的区别仅仅在于接收参数的方式不同。对于call()方法而言，第一个参数是作用域，没有变化，变化只是其余的参数都是直接传递给函数的。**

****冒充一个函数，实际上就是将要冒充的函数指向指定的作用域去执行****

**和apply区别在于后面的传参**

    
    
     function box(num1,num2){       //原函数
        return num1 + num2;
    }
    alert(box(1,2));  //执行打印返回数据
    
    function saybox(num1,num2){                     //冒充box函数执行，实际就是调用了box函数
        return box.call(this,num1,num2);            //用call方法冒充另外一个函数，第一个参数是要冒充的函数的作用域，此时this就是box函数的作用域，this就是window
                                                     //作用域后面的参数是形式参数，原函数有多少个形式参数，就需要写多少个形式参数
    }
    alert(saybox(3,4)); //执行冒充函数

**事实上，传递参数并不是apply()和call()方法真正的用武之地；它们经常使用的地方是能够扩展函数赖以运行的作用域。**

    
    
     var color = '红色的';                    //或者window.color = '红色的';也行
    
    var box = {
        color : '蓝色的'
    };
    
    function sayColor() {
        alert(this.color);
    }
    sayColor();                            //执行sayColor()函数，此时函数里的this作用域是window，所以打印的是红色
    
    sayColor.call(this);                        //这句话的意思是冒充this下的sayColor函数执行，作用域在window
    sayColor.call(window);                        //这句话的意思是冒充window下的sayColor函数执行，作用域在window
    sayColor.call(box);                            //这句话的意思是冒充box对象下的sayColor函数执行，作用域在box，

**冒充一个函数，实际上就是将要冒充的函数指向指定的作用域去执行**

**这个例子是之前作用域理解的例子修改而成，我们可以发现当我们使用call(box)方法的时候，sayColor()方法的运行环境已经变成了box对象里了。**

**使用call()或者apply()来扩充作用域的最大好处，就是对象不需要与方法发生任何耦合关系(耦合，就是互相关联的意思，扩展和维护会发生连锁反应)。也就是说，box对象和sayColor()方法之间不会有多余的关联操作，比如
box.sayColor = sayColor;也就是不需要将方法追加到对象里**

    
    
    ** **

