---
layout: post
title: " 第一百八十一节，jQuery-UI，知问前端--自动补全 UI--邮箱自动补全 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery-UI，知问前端--自动补全 UI-- **邮箱自动补全****



**学习要点：**

**1.调用 autocomplete()方法**

**2.修改 autocomplete()样式**

**3.autocomplete()方法的属性**

**4.autocomplete()方法的事件**

**5.autocomplete 中使用 on()**



**自动补全（autocomplete），是一个可以减少用户输入完整信息的 UI 工具。一般在输
入邮箱、搜索关键字等，然后提取出相应完整字符串供用户选择。**



**一．调用 autocomplete()方法**

****autocomplete()方法，输入框搜索数据源自动补全方法，有一个必填属性，参数是接收一个对象****

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
[/code]



**二．修改 autocomplete()样式**

**由于 autocomplete()方法是弹窗，然后鼠标悬停的样式。我们通过 Firebug 想获取到悬停 时背景的样式，可以直接通过
jquery.ui.css 里面找相应的 CSS。**

[code]

     //无须修改 ui 里的 CSS，直接用 style.css 替代掉
    .ui-menu-item a.ui-state-focus {
    　　background:url(../img/ui_header_bg.png);
    }
[/code]

**注意：其他修改方案类似。**



**三．autocomplete()方法的属性**

**自动补全方法有两种形式：1.autocomplete(options)，options 是以对象键值对的形式传参，
每个键值对表示一个选项；2.autocomplete('action', param)，action 是操作对话框方法的字符 串，param 则是
options 的某个选项。**



**autocomplete 外观选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313213221151-2004799170.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170313213226698-1078100618.png)**

**disabled false/布尔值 设置为 true，将禁止显示自动补全。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                disabled : true       //disabled false/布尔值 设置为 true，将禁止显示自动补全。
            });
[/code]



  
**source 无/数组 指定数据源，可以是本地的，也可以是远程的。，可以是各种数据类型**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                disabled : true       //disabled false/布尔值 设置为 true，将禁止显示自动补全。
            });
[/code]



  
**minLength 1/数值 默认为 1，触发补全列表最少输入字符数。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                minLength : 2       //minLength 1/数值 默认为 1，触发补全列表最少输入字符数。
            });
[/code]



**delay 300/数值 默认为 300 毫秒，延迟显示设置。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                delay : 0       //delay 300/数值 默认为 300 毫秒，延迟显示设置。
            });
[/code]



  
**autoFocus false/布尔值 设置为 true 时，第一个项目会自动被选定。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                autoFocus : true       //autoFocus false/布尔值 设置为 true 时，第一个项目会自动被选定。
            });
[/code]



**autocomplete 页面位置选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314120213729-1553317695.png)**



**position 无/对象使用对象的键值对赋值，有两个属性：my 和 at表示坐标。my 是以目标点左上角为基准，at 以目标点右下角为基准。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                position : {
                    // my : 'left top'  //设置提示框相当对于元素出现的横坐标，设置提示框相当对于元素出现的竖坐标
                    my : 'left center',
                    at : 'right+5 center'
                }
            });
[/code]



**四．autocomplete()方法的事件**

**除了属性设置外，autocomplete()方法也提供了大量的事件。这些事件可以给各种不同状 态时提供回调函数。这些回调函数中的 this
值等于对话框内容的 div 对象，不是整个对话框 的 div。**

**autocomplete 事件选项**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314120901823-82333024.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314120908041-1449526844.png)**

**create当自动补全被创建时会调用 create 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                create : function () {      //create当自动补全被创建时会调用 create 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。
                    alert('创建时');
                }
            });
[/code]



**open当自动补全被显示时，会调用 open 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**



**close 当自动补全被关闭时，会调用 close 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**



**focus当自动补全获取焦点时，会调用 focus 方法，该方法有两个参数(event, ui)。此事件中的 ui 有一个子属性对象
item，分别有两个属性：label，补全列表显示的文本；value，将要输入框的值。一般 label 和 value 值相同。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                focus : function (event, ui) {
                    alert(ui.item.value);
                }
            });
[/code]



**select 当自动补全获被选定时，会调用 select 方法，该方法有两个参数(event, ui)。此事件中的 ui 有一个子属性对象
item，分别有两个属性：label，补全列表显示的文本；value，将要输入框的值。一般 label 和 value 值相同。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                select : function (event, ui) {
                    alert(ui.item.value);
                }
            });
[/code]



**change当自动补全失去焦点且内容发生改变时，会调用 change方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**



**search 当自动补全搜索完成后，会调用 search 方法，该方法有两个参数(event, ui)。此事件中的 ui 参数为空。**



**response当自动补全搜索完成后，在菜单显示之前，会调用response 方法，该方法有两个参数(event, ui)。此事件中的 ui
参数有一个子对象 content[数组]，他会返回 label 和 value值，可通过遍历了解。**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq,
                response : function (event, ui) {
                    alert(ui.content[0].value);
                }
            });
[/code]

**注意：其他事件选项使用相同**



**autocomplete('action', param)方法**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314123559291-421632286.png)**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314123609182-1223959269.png)**

**autocomplete('close') jQuery 对象 关闭自动补齐**



**autocomplete('disable') jQuery 对象 禁用自动补齐**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
            $('#reg #email').autocomplete('disable');  //禁用自动补齐
[/code]



**autocomplete('enable') jQuery 对象 启用自动补齐**



**autocomplete('destroy') jQuery 对象 删除自动补齐，直接阻断。**



**autocomplete('widget') jQuery 对象 获取工具提示的 jQuery 对象**



**autocomplete('search',value) jQuery 对象 在数据源获取匹配的字符串。
**value值会代替输入框输入字符补全****

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
            $('#reg #email').autocomplete('search','a');  //value值会代替输入框输入字符补全,不输入内容也会按照a补全
[/code]



**autocomplete('option', param) 一般值 获取 options 属性的值，获取方法属性，第二个参数要获取的属性名称**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
            alert($('#reg #email').autocomplete('option', 'source'));
[/code]



**autocomplete('option', param,value)jQuery 对象 设置 options
属性的值，设置属性值，第二个参数是要设置的属性名称，第三个参数是要设置的属性值**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
            alert($('#reg #email').autocomplete('option', 'source','aaaaa'));
[/code]

**注意：其他使用相同**



**五．autocomplete 中使用 on()**

**在 autocomplete 的事件中，提供了使用 on()方法处理的事件方法。**

**on()方法触发的自动补全事件**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170314125724182-363158672.png)**

**autocompleteopen 显示时触发**

[code]

             var buq = ['aaa@163.com', 'bbb@163.com', 'ccc@163.com']; //自动补全数据源
            $('#reg #email').autocomplete({        //将邮箱执行自动补全方法
                source : buq
            });
            $('#reg #email').on('autocompleteopen',function () {
                alert('显示时触发');
            });
[/code]



**autocompleteclose 关闭时触发**



**autocompletesearch 查找时触发**



**autocompletefocus 获得焦点时触发**



**autocompleteselect 选定时触发**



**autocompletechange 改变时触发**



**autocompleteresponse 搜索完毕后，显示之前**





**邮箱自动补全**

**学习要点：**

**1.数据源 function**

**2.邮箱自动补全**

**本节课，我们通过自动补全 source 属性的 function 回调函数，来动态的设置我们的数 据源，以达到可以实现邮箱补全功能。**



**一．数据源 function**

**自动补全 UI 的 source 不但可以是数组，也可以是 function 回调函数。提供了自带的两 个参数设置动态的数据源。**

**数据源回调函数参数request, response**



[code]

            $('#email').autocomplete({
                source: function (request, response) {
                    alert(request.term); //可以获取你输入的值
                    response(['aa', 'aaaa', 'aaaaaa', 'bb']); //展示补全结果
                }
            });
[/code]



**注意：这里的 response 不会根据你搜索关键字而过滤无关结果，而是把整个结果全部呈 现出来。因为 source
数据源，本身就是给你动态改变的，就由你自定义，从而放弃系统内 置的搜索能力。**



**二．邮箱自动补全**

[code]

    $('#email' ).autocomplete({
                autoFocus: true,
                delay: 0,
                source: function (request, response) {
                    var hosts = ['qq.com', '163.com', '263.com', 'gmail.com', 'hotmail.com'], //起始
                        term = request.term,        //获取输入值
                        ix = term.indexOf('@'),     //@
                        name = term,                //用户名
                        host = '',                  //域名
                        result = [];                //结果
                    //结果第一条是自己输入
                    result.push(term);
                    if (ix > -1) { //如果有@的时候
                        name = term.slice(0, ix); //得到用户名
                        host = term.slice(ix + 1); //得到域名
                    }
                    if (name) {
                        //得到找到的域名
                        var findedHosts = (host ? $.grep(hosts, function (value, index) {
                                return value.indexOf(host) > -1;
                            }) : hosts),
                            //最终列表的邮箱
                            findedResults = $.map(findedHosts, function (value, index) {
                                return name + '@' + value;
                            });
                        //增加一个自我输入
                        result = result.concat(findedResults);
                    }
                    response(result);
                }
            });
[/code]



