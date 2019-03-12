
---
layout: post
title: " 第三百四十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—爬虫数据保存 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百四十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—爬虫数据保存**

**注意：数据保存的操作都是在 pipelines.py文件里操作的**



**将数据保存为json文件**

**spider 是一个信号检测**

[code]

    # -*- coding: utf-8 -*-
    
    # Define your item pipelines here
    #
    # Don't forget to add your pipeline to the ITEM_PIPELINES setting
    # See: http://doc.scrapy.org/en/latest/topics/item-pipeline.html
    from scrapy.pipelines.images import ImagesPipeline  #导入图片下载器模块
    import codecs
    import json
    
    
    class AdcPipeline(object):                      #定义数据处理类，必须继承object
        def __init__(self):
            self.file = codecs.open('shuju.json', 'w', encoding='utf-8')  #初始化时打开json文件
        def process_item(self, item, spider):       #process_item(item)为数据处理函数，接收一个item，item里就是爬虫最后yield item 来的数据对象
            # print('文章标题是：' + item['title'][0])
            # print('文章缩略图url是：' + item['img'][0])
            # print('文章缩略图保存路径是：' + item['img_tplj'])  #接收图片下载器填充的，图片下载后的路径
    
            #将数据保存为json文件
            lines = json.dumps(dict(item), ensure_ascii=False) + '\n'   #将数据对象转换成json格式
            self.file.write(lines)          #将json格式数据写入文件
            return item
    def spider_closed(self,spider):     #创建一个方法继承spider，spider是一个信号，当前数据操作完成后触发这个方法
            self.file.close()               #关闭打开文件
    
    class imgPipeline(ImagesPipeline):                      #自定义一个图片下载内，继承crapy内置的ImagesPipeline图片下载器类
        def item_completed(self, results, item, info):      #使用ImagesPipeline类里的item_completed()方法获取到图片下载后的保存路径
            for ok, value in results:
                img_lj = value['path']     #接收图片保存路径
                # print(ok)
                item['img_tplj'] = img_lj  #将图片保存路径填充到items.py里的字段里
            return item                    #将item给items.py 文件的容器函数
    
        #注意：自定义图片下载器设置好后，需要在
[/code]

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170805183224678-1268829778.png)





**将数据保存到数据库**

**我们使用一个ORM框架sqlalchemy模块，保存数据**

**数据库操作文件**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column
    from sqlalchemy import Integer, String, TIMESTAMP
    from sqlalchemy import ForeignKey, UniqueConstraint, Index
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    #配置数据库引擎信息
    ENGINE = create_engine("mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8", max_overflow=10, echo=True)
    
    Base = declarative_base()       #创建一个SQLORM基类
    
    class SendMsg(Base):            #设计表
        __tablename__ = 'sendmsg'
    
        id = Column(Integer, primary_key=True, autoincrement=True)
        title = Column(String(300))
        img_tplj = Column(String(300))
    
    
    
    def init_db():
        Base.metadata.create_all(ENGINE)        #向数据库创建指定表
    
    def drop_db():
        Base.metadata.drop_all(ENGINE)          #向数据库删除指定表
    
    def session():
        cls = sessionmaker(bind=ENGINE)         #创建sessionmaker类,操作表
        return cls()
    
    # drop_db()         #删除表
    # init_db()         #创建表
[/code]



**pipelines.py文件**

[code]

     # -*- coding: utf-8 -*-
    
    # Define your item pipelines here
    #
    # Don't forget to add your pipeline to the ITEM_PIPELINES setting
    # See: http://doc.scrapy.org/en/latest/topics/item-pipeline.html
    from scrapy.pipelines.images import ImagesPipeline  #导入图片下载器模块
    from adc import shujuku as ORM                      #导入数据库文件
    
    class AdcPipeline(object):                      #定义数据处理类，必须继承object
        def __init__(self):
            ORM.init_db()                           #创建数据库表
        def process_item(self, item, spider):       #process_item(item)为数据处理函数，接收一个item，item里就是爬虫最后yield item 来的数据对象
            print('文章标题是：' + item['title'][0])
            print('文章缩略图url是：' + item['img'][0])
            print('文章缩略图保存路径是：' + item['img_tplj'])  #接收图片下载器填充的，图片下载后的路径
    
            mysq = ORM.session()
            shuju = ORM.SendMsg(title=item['title'][0], img_tplj=item['img_tplj'])
            mysq.add(shuju)
            mysq.commit()
            return item
    
    
    
    
    
    
    class imgPipeline(ImagesPipeline):                      #自定义一个图片下载内，继承crapy内置的ImagesPipeline图片下载器类
        def item_completed(self, results, item, info):      #使用ImagesPipeline类里的item_completed()方法获取到图片下载后的保存路径
            for ok, value in results:
                img_lj = value['path']     #接收图片保存路径
                # print(ok)
                item['img_tplj'] = img_lj  #将图片保存路径填充到items.py里的字段里
            return item                    #将item给items.py 文件的容器函数
    
        #注意：自定义图片下载器设置好后，需要在
[/code]



