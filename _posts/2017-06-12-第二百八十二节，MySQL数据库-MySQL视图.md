---
layout: post
title: " 第二百八十二节，MySQL数据库-MySQL视图 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-MySQL视图**

**1、视图是一个虚拟表（非真实存在），其本质是【根据SQL语句获取动态的数据集，并为其命名】，用户使用时只需使用【名称】即可获取结果集，并可以将其当作表来使用。**

**2、也就是说视图是 **SQL语句查询到的数据动态组合的临时虚拟表，
**创建视图，以后如果要查询视图里的相同数据，就不必在写查询语句了，直接将视图当做表来使用，解决重复写语句问题******

****举例：有这样一张表****

****![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612153035306-492903438.png)****



**查询到年龄20岁的数据**

[code]

     -- 查询到年龄20岁的数据
    SELECT id,yhm,xb,nl FROM usr WHERE nl = 20;
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612153614587-805234626.png)



**这个查询结果，就可以创建成视图，以后如果要这个查询，就不必在写查询语句了，直接将视图当做表来使用**





**1、创建视图**

**CREATE VIEW 视图名称 AS  SQL语句**

[code]

    -- CREATE VIEW 视图名称 AS  SQL语句
    -- 查询表里nl字段等于20的数据创建视图
    CREATE VIEW usr_nl AS
    SELECT
        id,
        yhm,
        xb,
        nl
    FROM
        usr
    WHERE
        nl = '20';
[/code]

**视图虚拟表，也就是SQL语句的查询结果**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612160602025-1746294491.png)





**2、使用视图**

**使用视图时，将其当作表进行操作即可，由于视图是虚拟表，所以无法使用其对真实表进行创建、更新和删除操作，仅能做查询用。**

[code]

     SELECT * FROM `usr_nl`;
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170612161024165-1718661024.png)





**3、修改视图**

**ALTER VIEW 视图名称 AS SQL语句**

[code]

     -- ALTER VIEW 视图名称 AS SQL语句
    ALTER VIEW usr_nl AS
    SELECT
        id,
        yhm,
        xb,
        nl
    FROM
        usr
    WHERE
        nl = '21';
[/code]





**4、删除视图**

**DROP VIEW 视图名称**

[code]

     -- DROP VIEW 视图名称
    DROP VIEW usr_nl;
[/code]



