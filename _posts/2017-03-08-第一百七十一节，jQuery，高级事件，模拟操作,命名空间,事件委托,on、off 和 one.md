---
layout: post
title: " 第一百七十一节，jQuery，高级事件，模拟操作,命名空间,事件委托,on、off 和 one "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery，高级事件，模拟操作,命名空间,事件委托,on、off 和 one**



**学习要点：**

**1.模拟操作**

**2.命名空间**

**3.事件委托**

**4.on、off 和 one**



**jQuery 不但封装了大量常用的事件处理，还提供了不少高级事件方便开发者使用。比 如模拟用户触发事件、事件委托事件、和统一整合的 on 和
off，以及仅执行一次的 one 方 法。这些方法大大降低了开发者难度，提升了开发者的开发体验。**



**一．模拟操作**

**在事件触发的时候，有时我们需要一些模拟用户行为的操作。例如：当网页加载完毕后 自行点击一个按钮触发一个事件，而不是用户去点击。**

**trigger()方法，模拟事件操作，不阻止默认行为和冒泡，浏览器自动模拟用户行为，在要模拟的对象上使用，参数是要模拟的事件名称，还有可选参数，与原始事件对应**

[code]

     //点击按钮事件
        $('input').click(function () {
            alert('我的第一次点击来自模拟！');
        });
    //模拟用户点击行为
        $('input').trigger('click');
[/code]

[code]

    //可以合并两个方法
        $('input').click(function () {
            alert('我的第一次点击来自模拟！');
        }).trigger('click');
[/code]

**有时在模拟用户行为的时候，我们需要给事件执行传递参数，这个参数类似与 event.data 的额外数据，可以可以是数字、字符串、数组、对象。**

[code]

        $('input').click( function (e, data1, data2) {
            alert(data1 + ',' + data2);
        }).trigger('click', ['abc', '123']);
[/code]

**注意：当传递一个值的时候，直接传递即可。当两个值以上，需要在前后用中括号包含 起来。但不能认为是数组形式，下面给出一个复杂的说明。**

[code]

        $('input').click( function (e, data1, data2) {
            alert(data1.a + ',' + data2[1]);
        }).trigger('click', [{'a': '1', 'b': '2'}, ['123', '456']]);
[/code]



**模拟自定义事件**

**除了通过 JavaScript 事件名触发，也可以通过自定义的事件触发，所谓自定义事件其实 就是一个被.bind()绑定的任意函数。**

[code]

        $('input').bind('myEvent',  function () {
            alert('自定义事件！');
        }).trigger('myEvent');
[/code]



**trigger()方法提供了简写方案，只要想让某个事件执行模拟用户行为，直接再调用一个 空的同名事件即可。**

[code]

        $('input').click( function () {
            alert('我的第一次点击来自模拟！');
        }).click(); //空的 click()执行的是 trigger()
[/code]



**这种便捷的方法，jQuery 几乎所有常用的事件都提供了。**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170308151543797-1642099453.png)**



**triggerHandler()方法，模拟事件操作，阻止默认行为和阻止冒泡，浏览器自动模拟用户行为，在要模拟的对象上使用，参数是要模拟的事件名称，与原始事件对应**

**jQuery 还提供了另外一个模拟用户行为的方法：.triggerHandler()；这个方法的使用 和.trigger()方法一样。**

[code]

        $('input').click( function () {
            alert('我的第一次点击来自模拟！');
        }).triggerHandler('click');
[/code]

**在常规的使用情况下，两者几乎没有区别，都是模拟用户行为，也可以可以传递额外参 数。但在某些特殊情况下，就产生了差异：**

**1..triggerHandler()方法并不会触发事件的默认行为，而.trigger()会。**

[code]

        $('form').trigger('submit');  //模拟用户执行提交，并跳转到执行页面
        $('form').triggerHandler('submit'); //模拟用户执行提交，并阻止的默认行为
[/code]

**如果我们希望使用.trigger()来模拟用户提交，并且阻止事件的默认行为，则需要这么写：**

[code]

    $('form').submit( function (e) {
    　　e.preventDefault(); //阻止默认行为
    }).trigger('submit');
[/code]

**2..triggerHandler()方法只会影响第一个匹配到的元素，而.trigger()会影响所有。**



**3..triggerHandler()方法会返回当前事件执行的返回值，如果没有返回值，则返回
undefined；而.trigger()则返回当前包含事件触发元素的 jQuery 对象(方便链式连缀调用)。**

[code]

    alert($('input').click( function () {
    　　return 123;
    }).triggerHandler('click')); //返回 123，没有 return 返回
[/code]



**4..trigger()在创建事件的时候，会冒泡。但这种冒泡是自定义事件才能体现出来，是 jQuery 扩展于 DOM 的机制，并非 DOM
特性。而.triggerHandler()不会冒泡。**

[code]

     var index = 1;
    $('div').bind('myEvent',function(){
    　　alert('自定义事件' + index);
    　　index++;
    });
    $('.div3').trigger("myEvent");
[/code]



**二．命名空间**

**有时，我们想对事件进行移除。但对于同名同元素绑定的事件移除往往比较麻烦，这个 时候，可以使用事件的命名空间解决。**

[code]

        $('input').bind('click.abc',  function () {
            alert('abc');
        });
        $('input').bind('click.xyz', function () {
            alert('xyz');
        });
        $('input').unbind('click.abc'); //移除 click 实践中命名空间为 abc 的
[/code]

**注意：也可以直接使用('.abc')，这样的话，可以移除相同命名空间的不同事件。对于模
拟操作.trigger()和.triggerHandler()，用法也是一样的。**

[code]

    $('input').trigger('click.abc');
[/code]



**三．事件委托**

**什么是事件委托？用现实中的理解就是：有 100 个学生同时在某天中午收到快递，但这 100
个学生不可能同时站在学校门口等，那么都会委托门卫去收取，然后再逐个交给学生。 而在 jQuery
中，我们通过事件冒泡的特性，让子元素绑定的事件冒泡到父元素(或祖先元素) 上，然后再进行相关处理即可。**



**如果一个企业级应用做报表处理，表格有 2000 行，每一行都有一个按钮处理。如果用 之前的.bind()处理，那么就需要绑定 2000 个事件，就好比
2000 个学生同时站在学校门口等 快递，不断会堵塞路口，还会发生各种意外。这种情况放到页面上也是一样，可能导致页面 极度变慢或直接异常。而且，2000
个按钮使用 ajax 分页的话，.bind()方法无法动态绑定尚 未存在的元素。就好比，新转学的学生，快递员无法验证他的身份，就可能收不到快递。**

**也就是说当很多元素需要绑定相同事件时，用传统的
**bind()方法，就需要一个一个的去绑定，新增的元素还无法实现，而是事件委托就只绑定父元素即可，而且还支持父元素下新添加的元素自动也绑定事件****

**传统事件绑定**

**HTML**

[code]

     <div style="background:red;width:200px;height:200px;" id="box">
        <input type="button" value="按钮" class="button"/>
        <input type="button" value="按钮" class="button"/>
        <input type="button" value="按钮" class="button"/>
    </div>
[/code]

**js**

[code]

        $('.button').bind('click', function () {
            $(this).clone().appendTo('#box');  //点击后克隆当前元素，添加到当前元素后面
        });
[/code]

**以上列子，只有原始的3个元素有效，后面克隆出来的，就无法再克隆了**



**delegate()方法，事件委托方法，绑定上级元素事件，上级元素会自动将事件传递给下级里所有指定的元素，而且还支持上级元素下新添加的指定元素也传递事件，支持连缀**  
 **在上级元素上使用，参数1下级要传递事件的元素，参数2事件名称，参数3事件函数**

[code]

        $('#box').delegate('.button', 'click',  function () {
            $(this).clone().appendTo('#box');
        });
[/code]

**以上列子，克隆出来的，也能再克隆了**



**undelegate()方法，解除事件委托方法，解除后不再执行事件委托**

[code]

        $('#box').delegate('.button', 'click',  function () {
            $(this).clone().appendTo('#box');
        });
        $('#box').undelegate('.button', 'click');
[/code]

**  注意：.delegate()需要指定父元素，然后第一个参数是当前元素，第二个参数是事件方
式，第三个参数是执行函数。和.bind()方法一样，可以传递额外参数。.undelegate()和.unbind()
方法一样可以直接删除所有事件，比如：.undelegate('click')。也可以删除命名空间的事件，
比如：.undelegate('click.abc')。**



**四．on(绑定事件)、off(删除事件) 和 one(绑定事件使用一次后自动删除)**

**目前绑定事件和解绑的方法有三组共六个。由于这三组的共存可能会造成一定的混乱， 为此 jQuery1.7
以后推出了.on()和.off()方法彻底摒弃前面三组。**



**on()方法绑定事件，替代.bind()方式，参数与 **bind()相同，增加了事件委托****

[code]

     //替代.bind()方式
        $('.button').on('click', function () {
            alert('替代.bind()');
        });
    //替代.bind()方式，并使用额外数据和事件对象
        $('.button').on('click', {user: 'Lee'}, function (e) {
            alert('替代.bind()' + e.data.user);
        });
    //替代.bind()方式，并绑定多个事件
        $('.button').on('mouseover mouseout', function () {
            alert('替代.bind()移入移出！');
        });
    //替代.bind()方式，以对象模式绑定多个事件
        $('.button').on({
            mouseover: function () {
                alert('替代.bind()移入！');
            },
            mouseout: function () {
                alert('替代.bind()移出！');
            }
        });
    //替代.bind()方式，阻止默认行为并取消冒泡
        $('form').on('submit', function () {
            return false;
        });
    //或
        $('form').on('submit', false);
    //替代.bind()方式，阻止默认行为
        $('form').on('submit', function (e) {
            e.preventDefault();
        });
    //替代.bind()方式，取消冒泡
        $('form').on('submit', function (e) {
            e.stopPropagation();
        });
[/code]

**on()方法 ** **事件委托，取代 **delegate()方法**
，被委托元素上使用，参数1事件名称，参数2是委托元素也就是要传递事件的元素，参数3是执行函数******

[code]

        $('#box').on('click', '.button', function () {
            $(this).clone().appendTo('#box');
        })
[/code]



**off()方法，替代.unbind()方式，移除事件**

[code]

    $('.button').off('click' );
    $('.button').off('click', fn);
    $('.button').off('click.abc');
[/code]



**off()方法取消委托，替代undelegate()事件，在被委托元素上使用，参数1事件名称，参数2委托元素、也就是要传递事件的元素**

[code]

    $('#box').off('click', '.button');
[/code]

**注意：和之前方式一样，事件委托和取消事件委托也有各种搭配方式，比如额外数据、 命名空间等等，这里不在赘述。**



**不管是.bind()还是.on()，绑定事件后都不是自动移除事件的，需要通过.unbind()和.off() 来手工移除。jQuery
提供了.one()方法，绑定元素执行完毕后自动移除事件，可以方法仅触 发一次的事件。**



**one()方法，绑定元素执行完毕后自动移除事件，只执行一次事件**

[code]

     //类似于.bind()只触发一次
        $('.button').one('click', function () {
            alert('one 仅触发一次！');
        });
[/code]

**one()方法事件委托，执行一次后自动移除，参数2是委托元素**

[code]

        $('#box').one('click', '.button',  function () {
            alert('one 仅触发一次！');
        });
[/code]



