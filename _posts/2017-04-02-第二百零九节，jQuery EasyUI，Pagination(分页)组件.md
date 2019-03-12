---
layout: post
title: " 第二百零九节，jQuery EasyUI，Pagination(分页)组件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**jQuery EasyUI，Pagination(分页)组件**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403182153582-1455730154.png)

**学习要点：**

**1.加载方式**

**2.属性列表**

**3.事件列表**

**4.方法列表**



**本节课重点了解 EasyUI 中 Pagination(分页)组件的使用方法，这个组件依赖于 LinkButton(按钮)组件。**



**一．加载方式**

**class 加载方式**

[code]

     <div id="box" class="easyui-pagination"
         data-options="total:2000,pageSize:10"
         style="background:#efefef;border:1px solid #ccc;">
    </div>
[/code]

**JS 加载调用**

**pagination()将元素执行分页方法**

[code]

    $('#box' ).pagination({
    　　total : 2000,
    　　pageSize : 10,
    });
[/code]

**实现一个 panel (面板)结合 pagination(分页)分页例子，需要一个 PHP 分页文件**

[code]

     <div id="content" class="easyui-panel" style="height:200px"
         data-options="href:'user.php?page=1'"></div>
    <div class="easyui-pagination" style="border:1px solid #ccc;"
         data-options="
        total : 5,
        pageSize : 1,
        pageNumber : 1,
        pageList : [1],
        onSelectPage : function (pageNumber, pageSize) {
            $('#content').panel('refresh', 'user.php?page='+pageNumber);
        }
    "></div>
[/code]



**二．属性列表**



**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403152206816-492720493.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403152235863-530773997.png)**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403152244113-1917971346.png)**



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403152257378-1512303560.png)

**total number 总记录数，在分页控件创建时初始的值。默认值1。 也就是数据库总条数**

[code]

    $(function () {
        $('#box').pagination({
            total:50,    //总记录数,也就是数据库总条数
            pageSize:5      //每页显示条数,就是每页显示多少条
        });
    });
[/code]



**pageSize number 每页显示条数。默认值10。 就是每页显示多少条**

[code]

    $(function () {
        $('#box').pagination({
            total:50,    //总记录数,也就是数据库总条数
            pageSize:5      //每页显示条数,就是每页显示多少条
        });
    });
[/code]



**pageNumber number 在分页控件 创建的时候显示的页数。默认值为1。**

[code]

    $(function () {
        $('#box').pagination({
            total:50,    //总记录数,也就是数据库总条数
            pageSize:5,      //每页显示条数,就是每页显示多少条
            pageNumber:1    //创建的时候显示的页数。默认值为1。
        });
    });
[/code]



**pageList array用户可以改变页面大小。pageList 属性定义了页 面 导 航 展 示 的 页 码 。 默 认 值
为[10,20,30,50]。 每页显示多少条的选择**

[code]

    $(function () {
        $('#box').pagination({
            total:50,    //总记录数,也就是数据库总条数
            pageSize:10,      //每页显示条数,就是每页显示多少条
            pageNumber:1,    //创建的时候显示的页数。默认值为1。
            pageList:[10,20]   //每页显示多少条的选择
        });
    });
[/code]



**loading boolean 定义数据是否正在载入。默认值为 false。， 有点异常**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            loading:false,          //义数据是否正在载入。默认值为 false。
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            }
        });
    });
[/code]



**buttons array自定义按钮，可用值有：， 新增按钮**  
 **1.每个按钮都有2个属性：**  
 **iconCls：显示背景图片的 CSS 类 ID**  
 **handler：当按钮被点击时调用的一个句柄函数。**  
 **2.页面已存在元素的选择器对象（例如：**  
 **buttons:'#btnDiv'）。默认值为 null。**

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            buttons:[{
                iconCls : 'icon-add',
                handler:function () {
                   alert('点击时操作')
                }
            },{
                iconCls : 'icon-edit',
                handler:function () {
                   alert('点击时操作')
                }
            }],
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            }
        });
    });
[/code]



**layout array 分页控件布局定义。布局选项可以包含一个或多个值：数组方式布局**  
 **1) list：页面显示条数列表。**  
 **2) sep：页面按钮分割线。**  
 **3) first：首页按钮。**  
 **4) prev：上一页按钮。**  
 **5) next：下一页按钮。**  
 **6) last：尾页按钮。**  
 **7) refresh：刷新按钮。**  
 **8) manual：手工输入当前页的输入框。**  
 **9) links：页面数链接。**

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            layout:['list','sep','first','prev','links','next','last','manual']
        });
    });
[/code]



**showPageList boolean 定义是否显示页面导航列表。 是否显示可选每页显示多少条**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            showPageList:false      //是否显示可选每页显示多少条
        });
    });
[/code]



**showRefresh boolean 定义是否显示刷新按钮。**

[code]

    $( function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            showRefresh:false      //定义是否显示刷新按钮。
        });
    });
[/code]



**beforePageText string 在输入组件之前显示一个 label 标签。 输入页前的文字**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            beforePageText:'目前第',      //输入页前的文字
            afterPageText:'一共{pages}页'  //输入页后的文字
        });
    });
[/code]



**afterPageText string 在输入组件之后显示一个 label 标签。 **输入页后的文字****

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            beforePageText:'目前第',      //输入页前的文字
            afterPageText:'一共{pages}页'  //输入页后的文字
        });
    });
[/code]



**displayMsg string 设置显示页面信息。**



[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            beforePageText:'目前第',      //输入页前的文字
            afterPageText:'一共{pages}页',  //输入页后的文字
            displayMsg:'显示{from}到{to}个会员,共{total}会员'
        });
    });
[/code]









**三．事件列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403171950316-1992674738.png)**

**onSelectPage   pageNumber,pageSize用户选择一个新页面的时候触发。回调函数包含2个参数：**  
 **pageNumber：新的页数。**  
 **pageSize: 每页显示的条数。**

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            }
        });
    });
[/code]



  
**onBeforeRefresh   pageNumber,pageSize在点击刷新按钮刷新之前触发，返回false 可以取消刷新动作。**

****pageNumber：新的页数。**  
 **pageSize: 每页显示的条数。****

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            onBeforeRefresh:function (pageNumber,pageSize) {
                alert('在点击刷新按钮刷新之前触发');
            }
        });
    });
[/code]



**onRefresh   pageNumber,pageSize 刷新之后触发。**

****pageNumber：新的页数。**  
 **pageSize: 每页显示的条数。****

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            onRefresh:function (pageNumber,pageSize) {
                alert('刷新之后触发');
            }
        });
    });
[/code]



**onChangePageSize   pageSize '改变每页显示条数触发。**

****pageSize: 每页显示的条数。****



[code]

    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
            onChangePageSize:function (pageSize) {
                alert('改变每页显示条数触发');
            }
        });
    });
[/code]







**三．方法列表**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170403175402035-824079678.png)**

**options none 返回参数对象。**

[code]

     /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //用户选择一个新页面的时候触发
                // pageNumber：新的页数。
                // pageSize: 每页显示的条数。
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);
            },
        });
        alert($('#box').pagination('options'));    //返回参数对象
    });
[/code]



**loading none 提醒分页控件正在加载中。 在加载分页时刷新按钮旋转**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //点击分页时触发
                $('#box').pagination('loading');    //在加载分页时刷新按钮旋转
                $('#content').panel('refresh','user.php?page=' + pageNumber + '&pagesize=' + pageSize);  //重新加载数据
                setTimeout(function () {
                    $('#box').pagination('loaded'); //分页加载完成时刷新按钮停止
                }, 1000);
            }
        });
    });
[/code]



**loaded none 提醒分页控件加载完成。 分页加载完成时刷新按钮停止**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //点击分页时触发
                $('#box').pagination('loading');    //在加载分页时刷新按钮旋转
                $('#content').panel('refresh','user.php?page=' + pageNumber + '&pagesize=' + pageSize);  //重新加载数据
                setTimeout(function () {
                    $('#box').pagination('loaded'); //分页加载完成时刷新按钮停止
                }, 1000);
            }
        });
    });
[/code]



**refresh options 刷新并显示分页栏信息。 值为一个对象里面写要改变的信息属性**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //点击分页时触发
                $('#box').pagination('loading');    //在加载分页时刷新按钮旋转
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);  //重新加载数据
                setTimeout(function () {
                    $('#box').pagination('loaded'); //分页加载完成时刷新按钮停止
                }, 1000);
            }
        });
        $(document).click(function () {
            $('#box').pagination('refresh', {
                pageSize: 20,
            });
        });
    });
[/code]



**select page 选择一个新页面，页面索引从1开始。 值为要改变的分页索引**

[code]

    /**
    <div id="content" class="easyui-panel" style="height:200px"
        data-options="href:'user.php?page=1&pagesize=1'"></div>     //传递数据，第一页，第一条
    <div id="box">
    </div>
     **/
    
    $(function () {
        $('#box').pagination({
            total: 50,    //总记录数,也就是数据库总条数
            pageSize: 10,      //每页显示条数,就是每页显示多少条
            pageNumber: 1,    //创建的时候显示的页数。默认值为1。
            pageList: [10, 20],   //每页显示多少条的选择
            onSelectPage: function (pageNumber, pageSize) {     //点击分页时触发
                $('#box').pagination('loading');    //在加载分页时刷新按钮旋转
                $('#content').panel('refresh', 'user.php?page=' + pageNumber + '&pagesize=' + pageSize);  //重新加载数据
                setTimeout(function () {
                    $('#box').pagination('loaded'); //分页加载完成时刷新按钮停止
                }, 1000);
            }
        });
        $(document).click(function () {
            $('#box').pagination('select', 2);
        });
    });
[/code]



**PS：我们可以使用$.fn.pagination.defaults 重写默认值对象。见前面章节**



