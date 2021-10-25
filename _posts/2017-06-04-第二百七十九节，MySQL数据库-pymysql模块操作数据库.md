---
layout: post
title: " 第二百七十九节，MySQL数据库-pymysql模块操作数据库 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-pymysql模块操作数据库**

****pymysql模块是python操作数据库的一个模块****



**connect()创建数据库链接,参数是连接数据库需要的连接参数**  
 **使用方式：**  
 **模块名称.connect()**  
 **参数：**  
 **host=数据库ip**  
 **port=数据库端口**  
 **user=数据库用户名**  
 **passwd=数据库密码**  
 **db=数据库名称**

**charset=数据库编码**

  
**cursor()创建数据库操作游标，无参**  
 **使用方式：**  
 **游标变量.cursor()**

  
**execute()操作数据库，参数1 sql语句，参数2 字符串占位符变量**  
 **使用方式：**  
 **游标变量.execute()**

****execute()操作数据库会返回，操作数据库后影响的行数，我们可以以此判断是否操作成功****

  
**commit()提交数据到数据库，无参**  
 **使用方式：**  
 **创建数据库链接变量.commit()**

  
**close()关闭游标**  
 **使用方式：**  
 **游标变量.close()**

  
**close()关闭数据库**  
 **使用方式：**  
 **创建数据库变量.close()**

**向数据库添加一条数据**



[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi')
    # 创建游标
    cursor = conn.cursor()
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("INSERT INTO db1(yhm,mim) VALUES('adc8868','279819')") #添加一条数据
    print(effect_row)   #返回影响行数
    
    # 提交，不然无法保存新建或者修改的数据
    conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]





**execute(sql语句%s,( **占位符变量** ))执行sql语句时的占位符使用**

****execute()** 操作一条数据**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi')
    # 创建游标
    cursor = conn.cursor()
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("INSERT INTO db1(yhm,mim) VALUES(%s,%s)",('adc279819',279819)) #添加一条数据
    print(effect_row)   #返回影响行数
    
    # 提交，不然无法保存新建或者修改的数据
    conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605142753747-667149964.png)





**executemany(sql语句,[(占位符变量),(占位符变量)])执行sql语句时的占位符使用**

**executemany()操作多条数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi')
    # 创建游标
    cursor = conn.cursor()
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.executemany("INSERT INTO db1(yhm,mim) VALUES(%s,%s)",[('a1',123),('a2',456),('a3',789)])
    print(effect_row)   #返回影响行数
    
    # 提交，不然无法保存新建或者修改的数据
    conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605143937028-1950767479.png)





**查询数据库数据**

**注意：操作数据库的增、删、改都需要commit()提交数据到数据库，而查询是不需要 **commit()的****

**fetchall()获取游标查询数据库里的数据，返回元祖**  
 **使用方式：**  
 **游标变量.fetchall()**



[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor()
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchall()   #获取游标里的数据
    print(shuju)
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]



![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605151027247-782227345.png)







**查询数据库内容时更改游标返回字典类型数据【推荐】**

**返回字典类型将数据库表的列(字段)作为键返回**

**默认查询数据时游标返回的元祖类型，如果想返回字典类型就需要设置游标**

**cursor=pymysql.cursors.DictCursor设置游标返回字典类型数据，当做参数写在execute()里，execute(cursor=pymysql.cursors.DictCursor)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchall()   #获取游标里的数据
    print(shuju)
    
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605152328997-543361306.png)





**fetchone()获取游标里第一条数据，如果多次执行fetchone()就依次获取数据**  
 **使用方式：**  
 **游标变量.fetchone()**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchone()   #获取游标里第一条数据
    print(shuju)
    
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605160021262-1032646579.png)





**fetchmany()获取游标里,指定条数据，参数是要获取数据的条数**  
 **使用方式：**  
 **游标变量.fetchmany(3)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchmany(3)   #获取游标里,指定条数据
    print(shuju)
    
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605160814793-1940863238.png)





**移动游标里数据指针获取对应数据**

**scroll(1,mode='relative')相对当前位置移动**  
 **使用方式：**  
 **游标变量.scroll(1,mode='relative')**  
 **第一个参数正数相对当前位置向下移动数值对应指针，第一个负数相对当前位置向上移动数值对应指针**

**scroll(2,mode='absolute')相对绝对位置移动**  
 **使用方式：**  
 **游标变量.scroll(2,mode='absolute')**  
 **将指针位置移动到第一个参数数值对应指针**

****相对当前位置移动获取数据 **mode='relative'******

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchone()   #获取游标里第一条数据,指针在第一个位置
    shuju = cursor.fetchone()   #指针在第二个位置
    shuju = cursor.fetchone()   #指针在第三个位置
    print(shuju)                #打印应该是第三条
    cursor.scroll(-2,mode='relative') #调整指针，相对当前位置向上移动2位
    shuju = cursor.fetchone()   #指针第二位
    print(shuju)
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605180955575-1863392574.png)



**相对绝对位置移动mode='absolute'**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("SELECT id,yhm,mim FROM db1")
    shuju = cursor.fetchone()   #获取游标里第一条数据,指针在第一个位置
    shuju = cursor.fetchone()   #指针在第二个位置
    shuju = cursor.fetchone()   #指针在第三个位置
    print(shuju)                #打印应该是第三条
    cursor.scroll(3,mode='absolute') #调整指针，相对绝对位置移动3位
    shuju = cursor.fetchone()   #指针第四位
    print(shuju)
    # 提交，不然无法保存新建或者修改的数据
    # conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605182019747-1307505324.png)





**添加数据库时获取到添加数据的自增id**

**lastrowid获取添加数据时的自增id**  
 **使用方式：**  
 **游标变量.lastrowid**  
 **注意：如果是添加的多条数据，获取到的自增id是最后一条的自增id**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import pymysql
    
    # 创建连接
    """
    host=数据库ip
    port=数据库端口
    user=数据库用户名
    passwd=数据库密码
    db=数据库名称
    charset=数据库编码
    """
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='279819', db='cshi',charset='utf8')
    # 创建游标
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    
    # 执行SQL，并返回收影响行数
    effect_row = cursor.execute("INSERT INTO db1 (yhm,mim) VALUES (%s,%s)",('bb3',8889))
    zzid = cursor.lastrowid  #获取添加数据时的自增id
    print(zzid) #打印自增id
    # 提交，不然无法保存新建或者修改的数据
    conn.commit()
    
    # 关闭游标
    cursor.close()
    # 关闭连接
    conn.close()
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170605184417512-916949215.png)



