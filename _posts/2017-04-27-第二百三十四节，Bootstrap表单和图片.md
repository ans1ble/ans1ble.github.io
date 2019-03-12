---
layout: post
title: " 第二百三十四节，Bootstrap表单和图片 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Bootstrap表单和图片**



**学习要点：**

**1.表单**

**2.图片**

**本节课我们主要学习一下 Bootstrap 表单和图片功能，通过内置的 CSS 定义，显示各 种丰富的效果。**



**一．表单**

**Bootstrap 提供了一些丰富的表单样式供开发者使用。**

**1.基本格式**

**实现基本的表单样式**

**form-control样式class类，写在 <input>里,设置输入框样式(Bootstrap)**  
 **form-group样式class类，写在输入框外面的 <div>里,设置输入框与输入框之间的样式(Bootstrap)**

[code]

    <form>
        <div class="form-group">
            <label>电子邮件</label>
            <input type="email" class="form-control" placeholder="请输入您的电子邮件">
        </div>
        <div class="form-group">
            <label>密码</label>
            <input type="password" class="form-control" placeholder="请输入您的密码">
        </div>
    </form>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427230245975-461433524.png)

**注：只有正确设置了输入框的 type 类型，才能被赋予正确的样式。支持的输入框控件
包括：text、password、datetime、datetime-local、date、month、time、week、
number、email、url、search、tel 和 color。**



**2.内联表单**

**让表单左对齐浮动，并表现为 inline-block 内联块结构，当小于 768px，会恢复独占样式**

**form-inline样式class类，写在 <form>里,让表单左对齐浮动，并表现为 inline-block 内联块结构，当小于
768px，会恢复独占样式(Bootstrap)**

[code]

    <form class="form-inline">
        <div class="form-group">
            <label>电子邮件</label>
            <input type="email" class="form-control" placeholder="请输入您的电子邮件">
        </div>
        <div class="form-group">
            <label>密码</label>
            <input type="password" class="form-control" placeholder="请输入您的密码">
        </div>
    </form>
[/code]

**大于768px**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427231132381-2025187424.png)

**小于768px**

**![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427231217319-33990857.png)**



**3.表单合组**

**前后增加片段，给输入框前后加上片段**

**input-group-addon样式class类，写在input同级的 <div>里,给输入框加一个片段(Bootstrap)**  
 **input-group样式class类，写在input父级的 <div>里,将输入框和片段合并(Bootstrap)**

[code]

    <form class="form-inline">
        <div class="form-group">
            <label>电子邮件</label>
            <input type="email" class="form-control" placeholder="请输入您的电子邮件">
        </div>
        <div class="form-group">
            <label>密码</label>
            <input type="password" class="form-control" placeholder="请输入您的密码">
        </div>
    
        <label>金额</label>
        <div class=" **input-group** ">
            <div class=" **input-group-addon** ">￥</div>
            <input type="text" class="form-control">
            <div class=" **input-group-addon** ">.00</div>
        </div>
    </form>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427232903584-1539085639.png)





**4.水平排列**

**让表单内的元素保持水平排列**

**form-horizontal样式class类，写在 <form>里,让表单内的元素保持水平排列(Bootstrap)**  
 **col-sm-2样式class类，写在 <label>里,给输入框的标题设置所占比例(Bootstrap)**  
 **col-sm-10样式class类，写在input的父级 <div>里,给输入框设置所占比例(Bootstrap)**  
 **control-label样式class类，写在 <label>里,让输入框标题和form元素同步(Bootstrap)**

[code]

    <form class=" **form-horizontal** ">
        <div class="form-group">
            <label class=" **col-sm-2** **control-label** ">电子邮件</label>
            <div class=" **col-sm-10** ">
                <input type="email" class="form-control" placeholder="请输入您的电子邮件">
            </div>
        </div>
    
        <div class="form-group">
            <label class=" **col-sm-2** **control-label** ">电子邮件</label>
            <div class=" **col-sm-10** ">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
    </form>
[/code]

**大屏**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427235403475-344762142.png)

**小屏**

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170427235431240-236563290.png)

**注：这里用到了 col-sm 栅格系统，后面章节会重点讲解，而 control-label 表示和 父元素样式同步。**



**5.复选框和单选框**

**设置复选框，为区块一行**

**checkbox样式class类，写在input外层 <div>里,设置复选框为区块一行样式(Bootstrap)**

[code]

        <div class=" **checkbox** ">
            <label>
                <input type="checkbox">体育
            </label>
        </div>
        <div class=" **checkbox** ">
            <label>
                <input type="checkbox">音乐
            </label>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428024453350-1595089145.png)



**设置禁用的复选框**

**disabled样式class类，写在input外层 <div>里,禁止复选框文字选择(Bootstrap)**

[code]

        <div class="checkbox **disabled** ">
            <label>
                <input type="checkbox" disabled>体育
            </label>
        </div>
        <div class="checkbox">
            <label>
                <input type="checkbox">音乐
            </label>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428030231225-286406598.png)



**设置内联一行显示的复选框**

**checkbox-inline样式class类，写在input外层 <label>里,设置内联一行显示的复选框(Bootstrap)**

[code]

        <label class=" **checkbox-inline** disabled" >
            <input type="checkbox" disabled>体育
        </label>
    
    
        <label class=" **checkbox-inline** ">
            <input type="checkbox">音乐
        </label>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428030829990-535455656.png)



**设置单选框区块一行显示**

**radio样式class类，写在input外层 <div>里,设置单选框区块一行显示(Bootstrap)**

[code]

        <div class=" **radio** ">
            <label>
                <input type="radio" name="sex">男
            </label>
        </div>
            <div class=" **radio** ">
            <label>
                <input type="radio" name="sex">女
            </label>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428120732709-418874763.png)



**设置单选框内联一行显示**

**radio-inline样式class类，写在input外层 <div>里,设置单选框内联一行显示(Bootstrap)**

[code]

        <div class=" **radio-inline** ">
            <label>
                <input type="radio" name="sex">男
            </label>
        </div>
            <div class=" **radio-inline** ">
            <label>
                <input type="radio" name="sex">女
            </label>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428121224740-345791060.png)

**注意：禁用单选框和禁用复选框一样**



**6.下拉列表**

**设置下拉列表**

**form-control样式class类，写在 <select>里,设置下拉列表(Bootstrap)**

[code]

        <select class=" **form-control** ">
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
            <option>5</option>
        </select>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428122339615-92310151.png)



**7.校验状态**

**设置 **校验状态，也就是设置输入框的 **校验状态样式，******

**has-error样式class类，写在input最外层 <div>里,设置校验状态，也就是设置输入框的校验状态样式，错误状态(Bootstrap)**  
 **has-success样式class类，写在input最外层
<div>里,设置校验状态，也就是设置输入框的校验状态样式，成功状态(Bootstrap)**  
 **has-warning样式class类，写在input最外层
<div>里,设置校验状态，也就是设置输入框的校验状态样式，警告状态(Bootstrap)**

[code]

        <div class="form-group **has-error** ">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
        <div class="form-group **has-success** ">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
        <div class="form-group **has-warning** ">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428123534115-1393443513.png)

**label 标签同步相应状态，如果标题名字没有同步校验状态可以在 **label标签加class="control-label"同步****

**control-label样式class类，写在要同步样式的标签里,将当前元素与最外层div样式同步，也就共用样式(Bootstrap)**

[code]

         <div class="form-group has-error">
            <label class="col-sm-2 **control-label** ">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
        <div class="form-group has-success">
            <label class="col-sm-2 **control-label** ">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
        <div class="form-group has-warning">
            <label class="col-sm-2 **control-label** ">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
            </div>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428125120115-1725934379.png)



**8.给输入框添加额外的文字图标**

**文本框右侧内置文本图标**

**glyphicon样式class类，写在input同级的 <span>里,设置文本图标基础样式(Bootstrap)**  
 **glyphicon-ok样式class类，写在input同级的 <span>里,设置文本图标(Bootstrap)**  
 **form-control-feedback样式class类，写在input同级的 <span>里,设置文本图标的位置(Bootstrap)**  
 **has-feedback样式class类，写在input最外层的 <div>里,将文本图标位置应用到输入框(Bootstrap)**

[code]

        <div class="form-group has-warning has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
                <span class="glyphicon glyphicon-ok form-control-feedback"></span>
            </div>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428130656412-888622427.png)

**图标样式**

**glyphicon-ok样式class类，写在input同级的 <span>里,成功状态图标(Bootstrap)**  
 **glyphicon-warning-sign样式class类，写在input同级的 <span>里,警告状态图标(Bootstrap)**  
 **glyphicon-remove样式class类，写在input同级的 <span>里,错误状态图标(Bootstrap)**

[code]

        <div class="form-group has-success has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
                <span class="glyphicon glyphicon-ok form-control-feedback"></span>
            </div>
        </div>
        <div class="form-group has-warning has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
                <span class="glyphicon glyphicon-warning-sign form-control-feedback"></span>
            </div>
        </div>
        <div class="form-group has-error has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
                <span class="glyphicon glyphicon-remove form-control-feedback"></span>
            </div>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428132412819-342463196.png)



**9.输入框控制尺寸**

**从大到小**

**input-lg样式class类，写在 <input>里,大尺寸输入框(Bootstrap)**  
 **input-sm样式class类，写在 <input>里,小尺寸输入框(Bootstrap)**

[code]

        <div class="form-group has-success has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control input-lg" placeholder="请输入名称">
                <span class="glyphicon glyphicon-ok form-control-feedback"></span>
            </div>
        </div>
        <div class="form-group has-warning has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" placeholder="请输入名称">
                <span class="glyphicon glyphicon-warning-sign form-control-feedback"></span>
            </div>
        </div>
        <div class="form-group has-error has-feedback">
            <label class="col-sm-2 control-label">电子邮件</label>
            <div class="col-sm-10">
                <input type="text" class="form-control input-sm" placeholder="请输入名称">
                <span class="glyphicon glyphicon-remove form-control-feedback"></span>
            </div>
        </div>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428133040600-1338076639.png)

**注：也可以设置父元素 form-group-lg、form-group-sm，来调整。**





**二．图片**

**Bootstrap 提供了一些丰富的图片样式供开发者使用。**

**1.图片形状**



**img-rounded样式class类，写在 <img>里,设置图片圆角样式(Bootstrap)**  
 **img-circle样式class类，写在 <img>里,设置图片圆形，图片时正方形的就是圆形，图片时长方形的就是椭圆(Bootstrap)**  
 **img-thumbnail样式class类，写在 <img>里,设置图片缩略图样式(Bootstrap)**

[code]

    <img src="img/pic.png" alt="图片" class="img-rounded">
    <img src="img/pic.png" alt="图片" class="img-circle">
    <img src="img/pic.png" alt="图片" class="img-thumbnail">
[/code]

![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428134554272-912499626.png)





**  2响应式图片**

**img-responsive样式class类，写在 <img>里,设置图片响应式(Bootstrap)**



[code]

    <img src="img/pic.png" alt="图片" class="img-thumbnail img-responsive">
    <img src="img/pic.png" alt="图片" class="img-thumbnail img-responsive">
    <img src="img/pic.png" alt="图片" class="img-thumbnail img-responsive">
[/code]



![](https://images2015.cnblogs.com/blog/955761/201704/955761-20170428135444850-1360716248.png)



