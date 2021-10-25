---
layout: post
title: " 第二百八十六节，MySQL数据库-MySQL事务操作(回滚) "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-MySQL事务操作(回滚)  
  
**

**事务用于将某些操作的多个SQL作为原子性操作，一旦有某一个出现错误，即可回滚到原来的状态，从而保证数据库数据完整性。**



**举例：有这样一张表**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615180928587-1239485911.png)**



**从表里可以看出张三的资金里有850元，李四的资金有632元**

**假如张三向李四划款20元，那么张三的资金应该减20，李四的资金应该加20**

[code]

     UPDATE usr SET zij = zij - 20 WHERE yhm = '张三';
    UPDATE usr SET zij = zij + 20 WHERE yhm = '李四';
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615183139775-1399463760.png)

**可以看到张三的资金以减20，李四的资金以加20**



**但是如果在李四资金加的时候SQL语句出错，那么就会导致张三减少20成功，李四加上20失败，张三的资金减少了，李四资金没加上，钱就失踪了**

[code]

     UPDATE usr SET zij = zij - 20 WHERE yhm = '张三';
    UPDATE usr2 SET zij = zij + 20 WHERE yhm = '李四';
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615184205275-1229833586.png)





**定义一个存储过程来执行事务（回滚）**

**TRANSACTION表示事务**

[code]

     delimiter $$
    DROP PROCEDURE IF EXISTS p1;
    create PROCEDURE p1(  -- 创建存储过程
        OUT p_return_code tinyint   -- out类型参数，用于返回值
    )
    BEGIN 
      DECLARE exit handler for sqlexception  -- 捕捉错误，如果是sql错误就执行里面的
      BEGIN 
        -- ERROR 
        set p_return_code = 1;  -- 返回值1,说明sql错误
        rollback;   -- 回滚数据
      END; 
     
      DECLARE exit handler for sqlwarning   -- 捕捉错误，如果是sql警告就执行里面的
      BEGIN 
        -- WARNING 
        set p_return_code = 2;  -- 返回值2，说明出现sql警告
        rollback;  -- 回滚数据
      END; 
     
      START TRANSACTION;  -- 开始事务
            -- 执行sql语句
            UPDATE usr SET zij = zij - 20 WHERE yhm = '张三';
            UPDATE usr2 SET zij = zij + 20 WHERE yhm = '李四';
      COMMIT;  -- 提交
     
      -- SUCCESS 
      set p_return_code = 0; -- 返回0说明成功
     
    END $$
    delimiter ;
[/code]

**执行存储过程，执行事务**

[code]

    CALL p1( @u); -- 执行存储过程。传参接收返回值
    SELECT @u;  -- 查看返回值
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615194427462-634475271.png)

**可以看到返回1，说明sql错误，事务里的sql语句 **一旦有出现错误，将进行所有数据回滚，也就是无论成功的还是失败的语句都数据不变****

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615194956009-1135859424.png)**







**pymysql模块，默认开启了事务（回滚），也就是说 **pymysql模块自动实现了事务（回滚）** 【重点】**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615195235900-1218135870.png)**

**还是上面的列子，将一个sql语句写错**

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
    
            #获取存储过程(函数)的返回值
            effect_row = cursor.execute("UPDATE usr SET zij = zij - 20 WHERE yhm = '张三'")
            effect_row = cursor.execute("UPDATE usr2 SET zij = zij + 20 WHERE yhm = '李四'")
            fhuizhi = cursor.fetchone()
            print(fhuizhi)
    
    
            # 提交，不然无法保存新建或者修改的数据
            conn.commit()
    
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

**当执行时可以看到，提示第二个语句表名称是错误的，但是第一个应该是执行成功的**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615200329400-1968928041.png)**

**在这种情况下，可以看到 **pymysql模块自动实现了事务（回滚），数据库数据没有改变****

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170615200527728-873959481.png)**



