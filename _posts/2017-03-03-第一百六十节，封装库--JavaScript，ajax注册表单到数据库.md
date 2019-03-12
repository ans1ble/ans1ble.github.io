---
layout: post
title: " 第一百六十节，封装库--JavaScript，ajax注册表单到数据库 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**封装库--JavaScript，ajax注册表单到数据库**

**效果图**

**![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170303172211548-1411739778.png)**





前台js

[code]

    var biaodan = $().xu_lie_biao_dan($('form').sh_jd());   //序列化获取表单数据，返回对象
            $().Ajax({                            //执行Ajax数据传输
                method:'post',                    //post方式发送
                url:'hj.php',                     //发送到hj.php
                data:biaodan,                     //发送内容，序列化获取到的表单对象
                success:function (text) {         //执行回调函数
                    if (text == 1){
                        alert('注册成功');         **//可以做注册成功的操作**
                    } else {
                        alert('注册失败');         **//可以做注册失败的操作**
                    }
                },
                async: true                        //异步模式
            });
[/code]

通讯PHP页面代码

[code]

    <?php
        header('Content-Type:text/html; charset=utf-8');
        //连接数据库
        define('DB_HOST', 'localhost');
        define('DB_USER', 'root');
        define('DB_PWD', '279819');
        define('DB_NAME', 'beke');
    
        $conn = @mysql_connect(DB_HOST, DB_USER, DB_PWD) or die('数据库链接失败：'.mysql_error());
    
        @mysql_select_db(DB_NAME) or die('数据库错误：'.mysql_error());
    
        @mysql_query('SET NAMES UTF8') or die('字符集错误：'.mysql_error());
    
    
        $_birthday = $_POST['year'].'-'.$_POST['month'].'-'.$_POST['day'];
    
        $query = "INSERT INTO huiyuan (user, pass, ques, ans, email, birthday, ps)
                                                    VALUES ('{$_POST['user']}', sha1('{$_POST['pass']}'), '{$_POST['ques']}', '{$_POST['ans']}', '{$_POST['email']}', '{$_birthday}', '{$_POST['ps']}')";
    
        mysql_query($query) or die('新增失败！'.mysql_error());
    
        echo mysql_affected_rows();  //注册成功返回值给Ajax
    
        mysql_close();
    
    
    ?>
[/code]

数据库数据

![](https://images2015.cnblogs.com/blog/955761/201703/955761-20170303172822532-400262640.png)

