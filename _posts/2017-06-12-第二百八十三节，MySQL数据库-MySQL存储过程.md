---
layout: post
title: " 第二百八十三节，MySQL数据库-MySQL存储过程 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-MySQL存储过程**

****MySQL存储过程，也就是有点像 ** **MySQL函数，但是他与 ** ** **
**MySQL函数是有区别的，后面会讲到函数，所以注意区分****************

**注意：函数与存储过程的区别**

**存储过程是：CREATE PROCEDURE 创建的**

**函数时：create function 创建的**

**存储过程是：CALL  执行的**

**函数时：SELECT 执行的**

**函数里：不支持SQL语句【重点】**

**存储过程里：支持SQL语句【重点】**





********1、创建存储过程(函数)无参********

**delimiter设置数据库语句结束符，默认是遇到;表示语句结束，delimiter可以自定义语句结束符，后面跟结束符**  
 **create procedure创建存储过程(函数)，后面跟、函数名称()**  
 **BEGIN表示SQL语句开始，后面跟SQL语句**  
 **END表示SQL语句结束**

**举例：有这样一张表**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612185530900-1518766776.png)**

**创建一个usr_nl_20 ()函数，功能是查询 **usr表nl字段等于20的数据****

[code]

     -- delimiter设置数据库语句结束符，默认是遇到;表示语句结束，delimiter可以自定义语句结束符，后面跟结束符
    -- create procedure创建存储过程(函数)，后面跟、函数名称()
    -- BEGIN表示SQL语句开始，后面跟SQL语句
    -- END表示SQL语句结束
    
    -- 格式：
    -- delimiter $$                                        -- 将语句结束符改为$$
    -- create procedure 函数名称()
    -- BEGIN                                                    -- SQL语句开始
    --     SQL语句
    -- END $$                                                    -- SQL语句开始
    -- delimiter ;                                        -- 将语句结束符改为默认
    
    delimiter $$
    CREATE PROCEDURE usr_nl_20 ()
    BEGIN
        SELECT
            id,
            yhm,
            xb,
            nl
        FROM
            usr
        WHERE
            nl = 20 ;
    END $$
    delimiter ;
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612185835681-1700989268.png)







**2、执行存储过程(函数)**

**call执行存储过程(函数)，后面跟、函数名称()**

[code]

     -- call执行存储过程(函数)，后面跟、函数名称()
    CALL usr_nl_20();
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612190541634-84755468.png)





**3、删除存储过程(函数)**

**DROP PROCEDURE删除存储过程(函数)，后面跟要删除的函数名称**

[code]

     -- DROP PROCEDURE删除存储过程(函数)，后面跟要删除的函数名称
    DROP PROCEDURE usr_nl_20;
[/code]







**4、修改存储过程(函数)**

**一般 **函数都不用修改的办法，一般都是删除后重写****

**DROP PROCEDURE删除存储过程(函数)，后面跟要删除的函数名称**  
 **if EXISTS判断后面的变量或者函数是否存在，如果存在执行if EXISTS前面的语句**

[code]

     -- DROP PROCEDURE删除存储过程(函数)，后面跟要删除的函数名称
    -- if EXISTS判断后面的变量或者函数是否存在，如果存在执行if EXISTS前面的语句
    
    DROP PROCEDURE if EXISTS usr_nl_20;        -- 判断usr_nl_20函数是否存在，如果存在删除函数，如果不存在则不删除
    -- 如果存在函数删除后创建函数，不存在创建函数
    delimiter $$
    CREATE PROCEDURE usr_nl_20 ()
    BEGIN
        SELECT
            id,
            yhm,
            xb,
            nl
        FROM
            usr
        WHERE
            nl = 20 ;
    END $$
    delimiter ;
[/code]







**5、创建存储过程(函数)有参， **in  仅用于传入参数用****

**对于存储过程，可以接收参数， 其形式参数有三种用途类型：**  
 ** in 仅用于传入参数用**  
 ** out 仅用于返回值用**  
 ** inout 既可以传入又可以当作返回值**

**DECLARE 定义变量**  
 **DEFAULT 设置变量的默认值**  
 **SET 给变量赋值 要赋值的变量 值**  
 **定义变量的方式: DECLARE  变量名称  指定变量接收的数据类型  DEFAULT  设置变量的默认值**

[code]

    DROP PROCEDURE if EXISTS usr_nl_20;        -- 判断usr_nl_20函数是否存在，如果存在删除函数，如果不存在则不删除
    -- 如果存在函数删除后创建函数，不存在创建函数
    
    -- 对于存储过程，可以接收参数，其形式参数有三种用途类型：
    -- 　　in 仅用于传入参数用
    -- 　　out 仅用于返回值用
    -- 　　inout 既可以传入又可以当作返回值
    -- 
    -- 
    -- DECLARE定义变量
    -- DEFAULT设置变量的默认值
    -- SET给变量赋值 要赋值的变量 值
    -- 定义变量的方式:DECLARE  变量名称  指定变量接收的数据类型  DEFAULT  设置变量的默认值
    
    
    delimiter $$
    CREATE PROCEDURE usr_nl_20 (
        in canshu int
    )
    BEGIN
        DECLARE d1 int;
        DECLARE d2 int DEFAULT 3;
        SET d1 = canshu + d2;
    
        SELECT id,yhm,xb,nl FROM usr WHERE id > d1;
    END $$
    delimiter ;
[/code]

**运行有参函数**

[code]

     -- 运行有参函数
    CALL usr_nl_20(1);
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170613135417790-1326703875.png)







**6、创建存储过程(函数)有参， **in  仅用于传入参数用， **out  仅用于返回值用******

[code]

    delimiter $$
    DROP PROCEDURE if EXISTS usr_nl_20;
    CREATE PROCEDURE usr_nl_20 (
        in canshu int,  -- in 仅用于传入参数用
        OUT canshu2 INT  -- out 仅用于返回值用
    )
    BEGIN
        DECLARE d2 INT DEFAULT 3;  -- 设置变量d2等于3
        IF canshu = 1 THEN  -- 判断传入参数如果等于1
            SET canshu2 = 100 + d2;  -- 赋值返回参数等于100加d2
        ELSEIF canshu = 2 THEN  -- 判断传入参数等于2
            SET canshu2 = 200 + d2;  -- 返回参数等于200+d2
        ELSE  -- 否则
            SET canshu2 = 1000 + d2;  -- 返回参数等于1000+d2
        END IF;
    END $$
    delimiter ;
[/code]

**执行函数**

****执行函数，传入参数，和传入引用参数，也就是返回值参数****

****@定义引用参数，也就是返回值参数****

[code]

     -- 执行函数，传入参数，和传入引用参数，也就是返回值参数
    -- @定义引用参数，也就是返回值参数
    CALL usr_nl_20(1, @u);
    SELECT @u;    
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170613150600571-171072978.png)







**7、创建存储过程(函数)有参， **in  仅用于传入参数用， **out  仅用于返回值用， **inout
既可以传入又可以当作返回值********

[code]

    delimiter $$
    DROP PROCEDURE if EXISTS usr_nl_20;
    CREATE PROCEDURE usr_nl_20 (
        in canshu int,  -- in 仅用于传入参数用
        OUT canshu2 INT,  -- out 仅用于返回值用
        INOUT ii INT  -- inout 既可以传入又可以当作返回值
    )
    BEGIN
        DECLARE d2 INT DEFAULT 3;  -- 设置变量d2等于3
            SET ii = ii + 1;
        IF canshu = 1 THEN  -- 判断传入参数如果等于1
            SET canshu2 = 100 + d2;  -- 赋值返回参数等于100加d2
        ELSEIF canshu = 2 THEN  -- 判断传入参数等于2
            SET canshu2 = 200 + d2;  -- 返回参数等于200+d2
        ELSE  -- 否则
            SET canshu2 = 1000 + d2;  -- 返回参数等于1000+d2
        END IF;
    END $$
    delimiter ;
[/code]

**执行函数**

[code]

     SET @f = 5;  -- 定义inout类型变，可传入可返回变量
    CALL usr_nl_20(1, @u, @f);  -- 执行函数，参数in 仅用于传入参数用，参数out 仅用于返回值用，参数inout 既可以传入又可以当作返回值
    SELECT @u,@f;  -- 查看两个类型的返回值
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170613161607900-1797874915.png)





**8、pymysql模块，执行存储过程(函数)，获取SQL语句查询结果、和返回值**

**举例：创建了一个 **存储过程(函数)有参，函数里既有返回值、又有 **SQL语句查询结果，怎么通过 **pymysql模块 **
**既拿到返回结果，又拿到 ** ** **SQL语句查询结果******************

******************表******************

******************![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170613165948868-1498764433.png)******************

********************执行存储过程(函数)********************

[code]

     delimiter $$
    DROP PROCEDURE if EXISTS usr_nl_20;
    CREATE PROCEDURE usr_nl_20 (
        in canshu int,  -- in 仅用于传入参数用
        OUT canshu2 INT,  -- out 仅用于返回值用
        INOUT ii INT  -- inout 既可以传入又可以当作返回值
    )
    BEGIN
        DECLARE d2 INT DEFAULT 3;  -- 设置变量d2等于3
            SET ii = ii + 1;
            SELECT * FROM usr; -- SQL查询语句
        IF canshu = 1 THEN  -- 判断传入参数如果等于1
            SET canshu2 = 100 + d2;  -- 赋值返回参数等于100加d2
        ELSEIF canshu = 2 THEN  -- 判断传入参数等于2
            SET canshu2 = 200 + d2;  -- 返回参数等于200+d2
        ELSE  -- 否则
            SET canshu2 = 1000 + d2;  -- 返回参数等于1000+d2
        END IF;
    END $$
    delimiter ;
[/code]

** **

**pymysql模块，执行存储过程(函数)，获取SQL语句查询结果、和返回值**

**callproc()执行存储过程(函数),两个参数**  
 **使用方式：**  
 **游标变量.callproc('存储过程(函数)名称',(函数参数多个参数,号隔开))**



**fetchall()获取存储过程(函数)里的SQL语句查询结果**  
 **使用方式：**  
 **游标变量.fetchall()**



**execute()获取存储过程(函数)的返回值,参数是要获取返回值的形式参数索引**  
 **使用方式：**  
 **游标变量.execute("select @_存储过程(函数)名称_0,@_存储过程(函数)名称_1,@_存储过程(函数)名称_2")**



**fetchone()拿到存储过程(函数)的返回值**  
 **使用方式：**  
 **游标变量.fetchone()**

[code]

     #!/usr/bin/env python
    #coding:utf-8
    
    import tornado.ioloop
    import tornado.web                                              #导入tornado模块下的web文件
    import pymysql                                                  #导入数据库模块
    
    class khdHandler(tornado.web.RequestHandler):
        def get(self):
    
            #连接数据库
            conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
            # 创建游标
            cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    
            #执行存储过程(函数)
            row = cursor.callproc('usr_nl_20',(1,2,3))
    
    
            #获取存储过程(函数)里的SQL语句查询结果
            chaxjieg = cursor.fetchall()
            print(chaxjieg) #打印SQL语句查询结果
    
            #获取存储过程(函数)的返回值
            effect_row = cursor.execute("select @_usr_nl_20_0,@_usr_nl_20_1,@_usr_nl_20_2")
            fhuizhi = cursor.fetchone()
            print(fhuizhi)
    
    
            # 提交，不然无法保存新建或者修改的数据
            # conn.commit()
    
            # 关闭游标
            cursor.close()
            # 关闭连接
            conn.close()
    
            self.write("欢迎访问")
    
    
    settings = {                                            #html文件归类配置，设置一个字典
        "template_path":"views",                            #键为template_path固定的，值为要存放HTML的文件夹名称
        "static_path":"statics",                            #键为static_path固定的，值为要存放js和css的文件夹名称
    }
    
    #路由映射
    application = tornado.web.Application([                 #创建一个变量等于tornado.web下的Application方法
        (r"/khd", khdHandler),
    ],**settings)                                           #将html文件归类配置字典，写在路由映射的第二个参数里
    
    if __name__ == "__main__":
        #内部socket运行起来
        application.listen(8002)                            #设置端口
        tornado.ioloop.IOLoop.instance().start()
[/code]

**原理图**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170613175529743-281724386.png)



