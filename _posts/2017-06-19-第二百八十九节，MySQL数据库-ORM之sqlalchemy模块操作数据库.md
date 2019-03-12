---
layout: post
title: " 第二百八十九节，MySQL数据库-ORM之sqlalchemy模块操作数据库 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL数据库-ORM之sqlalchemy模块操作数据库**

****sqlalchemy第三方模块****



**sqlalchemy**  
**sqlalchemy是Python编程语言下的一款ORM框架，该框架建立在数据库API之上，使用关系对象映射进行数据库操作，简言之便是：将对象转换成SQL，然后使用数据API执行SQL并获取执行结果。**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619172709960-896984567.png)







**SQLAlchemy本身无法操作数据库，其必须以pymsql等第三方插件，Dialect用于和数据API进行交流，根据配置文件的不同调用不同的数据库API，从而实现对数据库的操作，**

**如：下面是不同的 **第三方插件数据库链接插件pymysql是我们前面说过的****

[code]

     MySQL-Python
        mysql+mysqldb://<user>:<password>@<host>[:<port>]/<dbname>
      
    pymysql
        mysql+pymysql://<username>:<password>@<host>/<dbname>[?<options>]
      
    MySQL-Connector
        mysql+mysqlconnector://<user>:<password>@<host>[:<port>]/<dbname>
      
    cx_Oracle
        oracle+cx_oracle://user:pass@host:port/dbname[?key=value&key=value...]
[/code]



****一、底层处理****

**使用 Engine/ConnectionPooling/Dialect
进行数据库操作，Engine使用ConnectionPooling连接数据库，然后再通过Dialect执行SQL语句。**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from sqlalchemy import create_engine
     
     
    engine = create_engine("mysql+pymysql://root:123@127.0.0.1:3306/t1", max_overflow=5)
     
    # 执行SQL
    # cur = engine.execute(
    #     "INSERT INTO hosts (host, color_id) VALUES ('1.1.1.22', 3)"
    # )
     
    # 新插入行自增ID
    # cur.lastrowid
     
    # 执行SQL
    # cur = engine.execute(
    #     "INSERT INTO hosts (host, color_id) VALUES(%s, %s)",[('1.1.1.22', 3),('1.1.1.221', 3),]
    # )
     
     
    # 执行SQL
    # cur = engine.execute(
    #     "INSERT INTO hosts (host, color_id) VALUES (%(host)s, %(color_id)s)",
    #     host='1.1.1.99', color_id=3
    # )
     
    # 执行SQL
    # cur = engine.execute('select * from hosts')
    # 获取第一行数据
    # cur.fetchone()
    # 获取第n行数据
    # cur.fetchmany(3)
    # 获取所有数据
    # cur.fetchall()
[/code]

**注意：以上都是底层实现，因为我们操作的是上层，所以底层了解一下即可**





** **

**ORM:**

**ORM框架的作用就是把数据库表的一行记录与一个对象互相做自动转换。 正确使用ORM的前提是了解关系数据库的原理。
ORM就是把数据库表的行与相应的对象建立关联，互相转换。 由于关系数据库的多个表还可以用外键实现一对多、多对多等关联，相应地，
ORM框架也可以提供两个对象之间的一对多、多对多等功能。**







* * *



**  1、创建表**

**create_engine方法参数(
'使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称?charset=utf8',echo=True表示是否查看生成的sql语句,**
**max_overflow=5** **)**

**max_overflow=5 表示最大连接数**

**declarative_base()创建一个SQLORM基类**  
 **Column()设置字段属性**  
 **create_all()向数据库创建指定表**

**创建表数据类型**

**整数型： TINYINT，SMALLINT，INT，BIGINT**  
 **Boolean() 对应TINYINT**  
 **Integer() 对应INT**  
 **SMALLINT() 对应SMALLINT**  
 **BIGINT() 对应BIGINT**

**浮点型： FLOAT，DOUBLE，DECIMAL(M,D)**  
 **DECIMAL() 对应DECIMAL**  
 **Float() 对应FLOAT**  
 **REAL() 对应DOUBLE**

**字符型： CHAR，VARCHAR**  
 **String(40) 对应VARCHAR**  
 **CHAR() 对应CHAR**

**日期型： DATETIME，DATE，TIMESTAMP**  
 **DATETIME() 对应DATETIME**  
 **DATE() 对应DATE**  
 **TIMESTAMP() 对应TIMESTAMP**

**备注型： TINYTEXT，TEXT，**  
 **Text() 对应TEXT**  
 **UnicodeText(10) 对应TINYTEXT**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619190708710-1158542965.png)





**创建一张表，并且创建索引**

**primary_key=True给当前字段创建主键索引**  
 **index=True给当前字段创建普通索引**  
 **unique=True给当前字段创建唯一索引**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #primary_key=True给当前字段创建主键索引
        name = Column(String(40),index=True)        #index=True给当前字段创建普通索引
        fullname = Column(String(40),unique=True)   #unique=True给当前字段创建唯一索引
        password = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619220148976-529606443.png)





**创建一张表，并且创建组合索引**

**UniqueConstraint('字段','字段',name='索引名称')创建唯一组合索引**  
 **Index('索引名称','字段','字段')创建普通组合索引**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #primary_key=True给当前字段创建主键索引
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
        __table_args__ = (
            UniqueConstraint('id', 'name', name='uix_id_name'),     #UniqueConstraint('字段','字段',name='索引名称')创建唯一组合索引
            Index('ix_id_name', 'name', 'password'),                #Index('索引名称','字段','字段')创建普通组合索引
        )
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619232449476-1518637654.png)





**创建两张表，并且创建外键链表，一对多**

**ForeignKey("连接表名称.连接表主键字段")外键链表一对多**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619234705898-375149270.png)

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619234713179-1421205519.png)









**创建三张表，并且创建外键链表，多对多**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    
    # 多对多
    class Group(Base):      #创建连接表
        __tablename__ = 'group' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #主键，自增
        name = Column(String(64), unique=True, nullable=False)      #唯一索引，不能为空
        port = Column(Integer, default=22)                          #默认值22
    
    
    class Server(Base):     #创建连接表
        __tablename__ = 'server' #表名称
    
        id = Column(Integer, primary_key=True, autoincrement=True) #主键，自增
        hostname = Column(String(64), unique=True, nullable=False) #唯一索引，不能为空
    
    
    class ServerToGroup(Base):  #创建关系表
        __tablename__ = 'servertogroup' #表名称
        nid = Column(Integer, primary_key=True, autoincrement=True) #主键，自增
        server_id = Column(Integer, ForeignKey('server.id'))        #外键server表的主键
        group_id = Column(Integer, ForeignKey('group.id'))          #外键group表的主键
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620010218116-1190908402.png)

**创建表字段属性【重点】**



**primary_key=True 主键索引**  
 **autoincrement=True 自增字段**  
 **index=True 给当前字段创建普通索引**  
 **unique=True 给当前字段创建唯一索引**  
 **UniqueConstraint('字段','字段',name='索引名称') 创建唯一组合索引**  
 **Index('索引名称','字段','字段') 创建普通组合索引**  
 **default='abc' 设置字段默认值，不怎么可靠**  
 **ForeignKey("连接表名称.连接表主键字段") 设置外键链表**  
 **nullable=False 类容不能为空**  
 **注：设置外检的另一种方式 ForeignKeyConstraint(['other_id'], ['othertable.other_id'])**





* * *



**2、删除表**

**drop_all(SQLORM基类)向数据库删除指定表**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'jif' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
    
    #Base.metadata.create_all(engine)  #向数据库创建指定表
    Base.metadata.drop_all(engine)  #向数据库删除指定表
[/code]



* * *





**3、向表添加 **一条** 数据**

**sessionmaker()创建sessionmaker类**  
 **add()将创建的数据添加到sessionmaker类**  
 **commit()向数据库提交写入添加到sessionmaker类的数据， 注意:只要是向数据库添加或者删除都需要 **commit()提交****

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
    Base.metadata.create_all(engine)  #向数据库创建指定表，如果表存在忽略创建
    
    ed_user = User(name='xiaoyu', fullname='Xiaoyu Liu', password='123') #执行自定义类，创建一行数据
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    session.add(ed_user)    #执行sessionmaker类下的add方法，add(创建数据变量)，将创建的数据添加到sessionmaker类
    
    session.commit()        #向数据库提交数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619203455585-1655573434.png)





**4、向表添加 **多条** 数据**

**add_all()添加多条数据，参数是一个列表，列表元素是自定义类创建数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi', echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
    Base.metadata.create_all(engine)  #向数据库创建指定表，如果表存在忽略创建
    
    
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    session.add_all([
        User(name='alex', fullname='Alex Li', password='456'),
        User(name='alex', fullname='Alex old', password='789'),
        User(name='peiqi', fullname='Peiqi Wu', password='sxsxsx')])
    
    
    session.commit()        #向数据库提交数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170619203359960-2124181906.png)





**向外键表添加数据并且设置外键值**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    session.add_all([
        User(name='林贵秀1',password='123456',fullname=1), #fullname=1添加数据设置外键字段值为连接表的主键id
        User(name='林贵秀2',password='123456',fullname=2), #fullname=1添加数据设置外键字段值为连接表的主键id
        User(name='林贵秀3',password='123456',fullname=3)  #fullname=1添加数据设置外键字段值为连接表的主键id
    ])
    
    
    session.commit()        #向数据库提交数据
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620164126070-524173165.png)



* * *

**  5、删除数据**

**delete()删除指定表数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    session.query(User).filter(User.id > 2).delete()  #删除User类对应表的id大于2的数据
    
    
    session.commit()        #向数据库提交数据
[/code]





* * *



**6、修改数据**

**synchronize_session参数详解**  
 **synchronize_session用于query 在进行删除或者修改数据操作时，对session的同步策略。**

**False \- 不对session进行同步，直接进行 **删除或者修改** 操作。**  
 **'fetch' \- 在删除或者修改数据操作之前，先发一条sql到数据库获取符合条件的记录。**  
 **'evaluate' \-
在删除或者修改数据操作之前，用query中的条件直接对session的identity_map中的objects进行eval操作，将符合条件的记录下来。**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
        shu = Column(Integer)
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    session.query(User).filter(User.id == 2).update({"name":"099"})   #将User类对应的表里id等于2的数据，name字段的值修改为"099"
    session.query(User).filter(User.id == 13).update({User.name: User.name + ",会员"}, synchronize_session=False) #在原有值后面追加值，不对session进行同步
    session.query(User).filter(User.id == 19).update({"name": User.name + 1}, synchronize_session="evaluate")  #将指定字段的值加1，注意：字段必须为数字类型
    
    
    session.commit()        #向数据库提交数据
[/code]



* * *



**7、查询**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class User(Base):           #自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)
        name = Column(String(40))
        fullname = Column(String(40))
        password = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表，如果表存在忽略创建
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    print(session.query(User))          #session.query(操作表类名称)，执行对指定表的查询语句，得到表的所有字段集合
    print(session.query(User).all())    #session.query(操作表类名称).all(),得到列表形式表的所有字段集合对象
    print(session.query(User.id, User.name, User.fullname, User.password).all())  #查询指定表里的指定字段
    print(session.query(User.id, User.name, User.fullname, User.password).order_by(User.id.desc()).all())  #查询指定表里的指定字段，以id排序desc()降序，asc()升序
    for row in session.query(User).order_by(User.id.desc()):  #以id排序desc()降序循环表里的内容
        print(row.id, row.name, row.fullname, row.password)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620140435913-1780987930.png)



**  __repr__将表返回对象的数据转化为解释器可读取的数据，默认返回的数据对象**

[code]

    class UserInfo(Base):                                               #定义一个类操作数据库userinfo表
        __tablename__ = 'userinfo'
    
        nid = Column(Integer, primary_key=True, autoincrement=True)
        username = Column(String(32))
        password = Column(String(32))
        email = Column(String(32))
        ctime = Column(TIMESTAMP)
    
        __table_args__ = (                                              #创建索引
            Index('ix_user_pwd', 'username', 'password'),               #创建普通组合索引
            Index('ix_email_pwd', 'email', 'password'),                 #创建普通组合索引
        )
    
        def __repr__(self):                                             #将表返回的数据转化为解释器可读取的数据，默认返回的数据对象
            return "%s-%s-%s" %(self.nid, self.username, self.email)    #转换的字段字符串格式化
[/code]



**relationship()表关联**

[code]

     class News(Base):                                                   #定义一个类操作数据库news表
    
        __tablename__ = 'news'
    
        nid = Column(Integer, primary_key=True, autoincrement=True)
        user_info_id = Column(Integer, ForeignKey("userinfo.nid"))
        news_type_id = Column(Integer, ForeignKey("newstype.nid"))
        ctime = Column(TIMESTAMP)
        title = Column(String(32))
        url = Column(String(128))
        content = Column(String(150))
        favor_count = Column(Integer, default=0)
    
        comment_count = Column(Integer, default=0)
    
        ##与生成表结构无关，仅用于查询方便
        f = relationship('Favor',backref='n')                           #表示在Favor建一个n字段关联news表的id
[/code]



**查询说明**

**query(要取的字段) 查询数据库数据**  
 **all() 显示数据，返回列表加元祖，查询多条数据使用**  
 **first() 显示数据，返回元祖，查询一条数据使用**  
 **filter(多条件) 过滤数据**  
 **filter_by(a=xxx) 过滤数据，只能使用条件等于**  
 **from_statement(sql语句) 过滤数据**  
 **order_by(排序字段.desc()) 排序，desc()降序，asc()升序**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8',echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    
    ret = session.query(User.id,User.name, User.password,User.fullname).all()  #指定表里的所有字段
    print(ret)
    
    ret = session.query(User.id,User.name, User.password,User.fullname).filter_by(id = 13).all()  #查询表里的id字段等于指定值的数据,返回列表加元祖
    print(ret)
    
    ret = session.query(User.id,User.name, User.password,User.fullname).filter_by(id=15).first()  #查询表里的id字段等于指定值的数据，返回元祖
    print(ret)
    
    ret = session.query(User.id,User.name, User.password,User.fullname).filter(User.id > 15).order_by(User.id.desc()).all()  #查找表里id大于15的数据，以id排序desc()降序
    print(ret)
    
    
    ret = session.query(User.id,User.name, User.password,User.fullname).from_statement(text("SELECT * FROM users where name = '林贵秀2'")).all() #查询表里ame = '林贵秀2'的数据
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620193901585-472104256.png)





**查询条件**

**between(1, 16) 之间**  
 **in_([1,3,4]) 里为1,3,4的**  
 **~ 取反，非的意思**

**from sqlalchemy import and_, or_  #注意：在条件里如果要使用and_(并且)，or_(或者),必须先引入这两个方法**

**and_ (并且)，**  
 **or_ (或者)**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter_by(name='林贵秀2').all()    #查询表里name字段等于林贵秀2的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(User.id > 20, User.name == '林贵秀1').all()   #查询表里id大于20，name等于林贵秀1的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(User.id.between(1, 16), User.name == '林贵秀1').all() #查询表里id为1至16之间，name等于林贵秀1的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(User.id.in_([1,3,4])).all()    #查询表里id为1,3,4的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(~User.id.in_([1,3,4])).all()   #查询表里id不为1,3,4的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(User.id.in_(session.query(User.id).filter_by(name='林贵秀1'))).all()  #查找一张表里的id作为参数，再次查找数据
    print(ret)
    
    
    from sqlalchemy import and_, or_  #注意：在条件里如果要使用and_(并且)，or_(或者),必须先引入这两个方法
    
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(and_(User.id > 3, User.name == '林贵秀1')).all()  #查找表里id大于3，并且name等于林贵秀1的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(or_(User.id < 3, User.name == '林贵秀1')).all()   #查找表里id小于3或者name等于林贵秀1的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(
        or_(
            User.id < 2,    #id小于2
            and_(User.name == '林贵秀1', User.id > 3), #name等于林贵秀1并且id大于3
            User.password != "" #password不为空
        )).all()
    
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620212624132-214941670.png)





**查询通配符**

**like() 通配符**  
 **e% 开头的所有（%表示多个字符串,表示查询开头为e后面可以是多个字符的数据）**  
 **%e% 表示查询中间为e前后可以是多个字符的数据**  
 **e_ 开头的所有（_表示一个字符,表示查询开头为e后面可以是一个字符的数据）**  
 **_e_ 表示查询中间为e前后可以是一个字符的数据**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 通配符
    """
    e%  开头的所有（%表示多个字符串,表示查询开头为e后面可以是多个字符的数据）
    %e% 表示查询中间为e前后可以是多个字符的数据
    e_  e开头的所有（_表示一个字符,表示查询开头为e后面可以是一个字符的数据）
    _e_ 表示查询中间为e前后可以是一个字符的数据
    """
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(User.name.like('林贵秀%')).all()  #查找表里name字段开头为林贵秀后面可以是多个字符的数据
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).filter(~User.name.like('林贵秀%')).all() #查找表里name字段开头不为林贵秀后面可以是多个字符的数据
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170620220651460-1687447733.png)





**查询限制**

****限制一般做分页****

**[13:18]从第13行开始到18行结束，也就是取5行**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 限制
    ret = session.query(User.id, User.name, User.password, User.fullname)[13:18]    #从第13行开始到18行结束，也就是取5行
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170621094513116-1386765666.png)





**查询排序**

****一般默认是从第一列id排序的****

**order_by(排序字段.asc()) 排序,desc()降序，asc()升序**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 排序
    ret = session.query(User.id, User.name, User.password, User.fullname).order_by(User.id.desc()).all()    #根据 “列” 从大到小排列
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).order_by(User.id.asc()).all()     #根据 “列” 从小到大排列
    print(ret)
    
    ret = session.query(User.id, User.name, User.password, User.fullname).order_by(User.id.desc(), User.name.asc()).all()   #根据 “列1” 从大到小排列，如果排序列1数据有相同，则按列2从小到大排序
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170621095811976-196678309.png)







**查询分组**

****分组一般就是一个分组列记录每条数据所属什么类型如：普通会员、超级会员、黄金会员****

******注意：group by 必须在where之后，order by之前******

**from sqlalchemy.sql import func 注意：分组必须sqlalchemy.sql模块里的func方法**  
 **group_by(分组字段) 分组**  
 **func.count() 统计所属当前分组的数据列数**  
 **func.max() 显示当前组里指定列最大的数据**  
 **func.min() 显示当前组里指定列最小的数据**  
 **func.sum() 显示当前组指定列相加的和**  
 **func.avg() 显示当前组指定列的平均数**  
 **having (条件)帅选统计**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8')
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
        fzu = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 分组
    from sqlalchemy.sql import func
    
    ret = session.query(User.fzu).group_by(User.fzu).all()  #查看分组类容
    print(ret)
    
    #查看分组所有统计信息
    ret = session.query(
        User.fzu,               #显示当前分组
        func.count(User.fzu),   #统计所属当前分组的数据,统计当前分组的列数
        func.max(User.id),      #显示当前组里指定列最大的数据
        func.min(User.id),      #显示当前组里指定列最小的数据
        func.sum(User.id),      #显示当前组指定列相加的和
        func.avg(User.id)       #显示当前组指定列的平均数
    ).group_by(User.fzu).all()  #查看分组所有统计信息
    print(ret)
    
    #查看分组指定统计值大于3的信息
    ret = session.query(
        User.fzu,               #显示当前分组
        func.count(User.fzu),   #统计所属当前分组的数据,统计当前分组的列数
        func.max(User.id),      #显示当前组里指定列最大的数据
        func.min(User.id),      #显示当前组里指定列最小的数据
        func.sum(User.id),      #显示当前组指定列相加的和
        func.avg(User.id)       #显示当前组指定列的平均数
    ).group_by(User.fzu).having(func.min(User.id) > 3).all()    #查看分组指定统计值大于3的信息
    print(ret)
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170621120454679-1153561585.png)



**** ****

****外键链表查询****

**外键链表数据类型必须一致**  
 **a表里创建外键连接b表的主键，首先检查a表里要设置外键的字段、和b表里的主键字段数据类型是否一致，两者数据类型必须一致，不然无法建立索引【重点】**

**外键链表约束**  
**a表和b表链表后，两表之间建立了链表关系，a表受b表约束，也就是当a表添加或者修改一条数据时、这条数据的外键字段值如果是b表主键字段不存在的，将无法添加，会报错【重点】**

**外键连表查询**  
 **query(外键表, 连接表).filter(外键表.外键字段 == 连接表.主键字段)**

**join()外键连表查询【推荐】**  
 **query(外键表, 连接表).join(连接表)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8',echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
        fzu = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 外键连表查询
    # query(外键表, 连接表).filter(外键表.外键字段 == 连接表.主键字段)，
    ret = session.query(User.id, User.name, User.password, User.fullname, Favor.id, Favor.caption).filter(User.fullname == Favor.id).all()
    print(ret)  #查看外键表和连接表组合后的信息
    
    # join()外键连表查询
    # query(外键表, 连接表).join(连接表)，只显示有关联的数据[推荐]
    ret = session.query(User.id, User.name, User.password, User.fullname,Favor.id, Favor.caption).join(Favor).all()
    print(ret)    #查看join()外键连表后的信息
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170621142449945-1213005680.png)





**查询组合**

**组合就是将两张表数据显示出来，注意两张表显示的列数量要是一样的**  
 **union() 组合表，对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；**  
 **union_all() 组合表，对两个结果集进行并集操作，包括重复行，不进行排序；**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    
    #create_engine方法，创建数据库链接，
    #create_engine方法参数('使用数据库+数据库链接模块://数据库用户名:密码@ip地址:端口/要连接的数据库名称',echo=True表示是否查看生成的sql语句)
    engine = create_engine('mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8',echo=True)
    
    Base = declarative_base()   #创建一个SQLORM基类
    
    class Favor(Base):          #创建连接表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'favor' #表名称
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        caption = Column(String(50), default='red', unique=True)    #设置字段默认值，设置字段唯一索引
    
    class User(Base):           #创建外键表，自定义类，功能生成一张表，参数必须继承SQLORM基类
        __tablename__ = 'users' #表名称
    
        #创建字段
        #字段名称 = Column(字段属性...)
        id = Column(Integer, primary_key=True, autoincrement=True)  #设置主键，自增
        name = Column(String(40))
        password = Column(String(40))
        fullname = Column(Integer,ForeignKey("favor.id"))           #ForeignKey("连接表名称.连接表主键字段")外键链表一对多
        fzu = Column(String(40))
    
    
    Base.metadata.create_all(engine)  #向数据库创建指定表
    
    #创建sessionmaker类，sessionmaker(bind=数据库链接变量)
    MySession = sessionmaker(bind=engine)
    session = MySession()   #执行sessionmaker类
    
    # 组合
    q1 = session.query(User.id, User.name).filter(User.id > 1)
    q2 = session.query(Favor.id, Favor.caption).filter(Favor.id > 1)
    ret = q1.union(q2).all()
    print(ret)  #将表1和表2组合后查看
    
    q1 = session.query(User.id, User.name).filter(User.id > 1)
    q2 = session.query(Favor.id, Favor.caption).filter(Favor.id > 1)
    ret = q1.union_all(q2).all()
    print(ret)  #将表1里id大于1的数据和，表2里id大于1的数据组合查看
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170621150138195-1282617648.png)



