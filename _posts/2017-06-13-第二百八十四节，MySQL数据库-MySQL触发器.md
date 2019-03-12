---
layout: post
title: " 第二百八十四节，MySQL数据库-MySQL触发器 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-MySQL触发器**

**对某个表进行【增/删/改】操作的前后如果希望触发某个特定的行为时，可以使用触发器，触发器用于定制用户对表的行进行【增/删/改】前后的行为。**



**1、创建触发器基本语法**



**TRIGGER触发器**  
 **BEFORE之前**  
 **AFTER之后**  
 **INSERT插入**  
 **DELETE删除**  
 **UPDATE更新**

[code]

     # 插入前
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) INSERT(插入) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_before_insert_tb1 BEFORE INSERT ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
    
    # 插入后
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 AFTER(之后) INSERT(插入) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_after_insert_tb1 AFTER INSERT ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
    
    # 删除前
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) DELETE(删除) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_before_delete_tb1 BEFORE DELETE ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
    
    # 删除后
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 AFTER(之后) DELETE(删除) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_after_delete_tb1 AFTER DELETE ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
    
    # 更新前
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) UPDATE(更新) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_before_update_tb1 BEFORE UPDATE ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
    
    # 更新后
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 AFTER(之后) UPDATE(更新) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    CREATE TRIGGER tri_after_update_tb1 AFTER UPDATE ON tb1 FOR EACH ROW
    BEGIN
        ...
    END
[/code]





**2、实列，创建一张表插入之前的触发器**

**当向指定的一张表插入一条数据时，触发器自动向另外一张表插入一条数据**

**有这样两个表**

**usr表**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614175831462-1917275817.png)**

**jif表**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614175946493-756182514.png)**



**创建一个触发器，当向usr表插入一条数据之前，触发器自动向jif表插入一条数据**

[code]

     # 插入前
    -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) INSERT(插入) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    
    delimiter $$ -- 因为可能有多条触发行为，所有需要修改语句结束符
    DROP TRIGGER if EXISTS chufa_qi_usr; -- 判断这个触发器如果存在删除
    
    CREATE TRIGGER chufa_qi_usr BEFORE INSERT ON usr FOR EACH ROW -- 给usr表创建一个插入数据之前的触发器
    BEGIN
        INSERT INTO jif (jif) VALUES ('123'); -- 向jif表的jif字段插入值123
    END $$
    delimiter ;
[/code]

**  可以看到usr表的触发器已经创建**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614183018259-649907483.png)**

**当向usr表插入一条数据之前，触发器会自动向 **jif表的jif字段插入一条数据****

[code]

     INSERT INTO usr (yhm,xb,nl) VALUES ('张无忌','男','30'); -- 向usr表插入数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614183440696-408399702.png)

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614183448087-935278904.png)

**  注意：其他的、增、删、改、之前或者之后触发器原理相同**







**3、在触发器里获取到，触发器表指定字段的插入值**

**NEW 获取触发器表指定字段的插入值，后面跟要获取值的字段名称，如：NEW.nl**

**获取触发器表指定字段的插入值，可以做判断和传值写入等操作**

**举例：判断触发表插入数据时，如果nl字段值等于30将nl字段值写入另外一张表**

[code]

     -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) INSERT(插入) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    
    delimiter $$ -- 因为可能有多条触发行为，所有需要修改语句结束符
    DROP TRIGGER if EXISTS chufa_qi_usr; -- 判断这个触发器如果存在删除
    
    CREATE TRIGGER chufa_qi_usr BEFORE INSERT ON usr FOR EACH ROW -- 给usr表创建一个插入数据之前的触发器
    BEGIN
            IF NEW.nl = '30' THEN  -- 判断插入数据时触发表的nl字段的值如果等于30
                INSERT INTO jif (jif) VALUES (NEW.nl); -- 获取触发器表插入数据时的nl字段值，插入到jif表的jif字段里
            END IF;
    END $$
    delimiter ;
[/code]

**插入数据**

[code]

     INSERT INTO usr (yhm,xb,nl) VALUES ('东方不败','男','30'); -- 向usr表插入数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614192520853-249543203.png)

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614192545962-1004478913.png)**









**4、在触发器里获取到，触发器表指定字段的删除值**

**OLD 获取触发器表指定字段的删除值，后面跟要获取值的字段名称，如：OLD.nl**

**获取触发器表指定字段的删除值，可以做判断和传值写入等操作**

**举例：判断触发表删除数据时，如果nl字段值等于30将nl字段值写入另外一张表**

[code]

     -- CREATE(创建) TRIGGER(触发器) 触发器名称 BEFORE(之前) DELETE(删除) ON 表名称 FOR(为) EACH(每一) ROW(行)
    -- BEGIN(触发器开始)
    --     触发器行为......
    -- END(触发器结束)
    
    delimiter $$ -- 因为可能有多条触发行为，所有需要修改语句结束符
    DROP TRIGGER if EXISTS chufa_qi_usr; -- 判断这个触发器如果存在删除
    
    CREATE TRIGGER chufa_qi_usr BEFORE DELETE ON usr FOR EACH ROW -- 给usr表创建一个插入数据之前的触发器
    BEGIN
            IF OLD.nl = '30' THEN  -- 判断删除数据时触发表的nl字段的值如果等于30
                INSERT INTO jif (jif) VALUES (OLD.nl); -- 获取触发器表删除数据时的nl字段值，插入到jif表的jif字段里
            END IF;
    END $$
    delimiter ;
[/code]

**删除数据**

[code]

     DELETE FROM usr WHERE id=15; -- 删除usr表id等于15的数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614201940134-95308671.png)

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614201948587-2049357466.png)





**5、触发器获取触发表操作字段值重点：**

****NEW 获取触发表 ** **插入数据时，**** 指定字段的插入值（插入数据使用）****

******OLD ** **获取触发表 ** **删除数据时，**** 指定字段的删除值 ** **（删除数据使用）**************

**************NEW、 ** ** **OLD ** ** ** ** **更新数据时********** 都可以使用 ** ** ** **
** ** **（更新数据使用）**********************************



