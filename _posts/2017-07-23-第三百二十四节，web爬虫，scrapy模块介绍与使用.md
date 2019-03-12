---
layout: post
title: " 第三百二十四节，web爬虫，scrapy模块介绍与使用 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百二十四节，web爬虫，scrapy模块介绍与使用**

Scrapy是一个为了爬取网站数据，提取结构性数据而编写的应用框架。 其可以应用在数据挖掘，信息处理或存储历史数据等一系列的程序中。  
其最初是为了页面抓取 (更确切来说, 网络抓取 )所设计的， 也可以应用在获取API所返回的数据(例如 Amazon Associates Web
Services ) 或者通用的网络爬虫。Scrapy用途广泛，可以用于数据挖掘、监测和自动化测试。

Scrapy 使用了 Twisted异步网络库来处理网络通讯。整体架构大致如下

![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170723212038159-992324312.png)



**Scrapy主要包括了以下组件：**

  * **引擎(Scrapy)**  
用来处理整个系统的数据流处理, 触发事务(框架核心)

  * **调度器(Scheduler)**  
用来接受引擎发过来的请求, 压入队列中, 并在引擎再次请求的时候返回. 可以想像成一个URL（抓取网页的网址或者说是链接）的优先队列,
由它来决定下一个要抓取的网址是什么, 同时去除重复的网址

  * **下载器(Downloader)**  
用于下载网页内容, 并将网页内容返回给蜘蛛(Scrapy下载器是建立在twisted这个高效的异步模型上的)

  * **爬虫(Spiders)**  
爬虫是主要干活的, 用于从特定的网页中提取自己需要的信息, 即所谓的实体(Item)。用户也可以从中提取出链接,让Scrapy继续抓取下一个页面

  * **项目管道(Pipeline)**  
负责处理爬虫从网页中抽取的实体，主要的功能是持久化实体、验证实体的有效性、清除不需要的信息。当页面被爬虫解析后，将被发送到项目管道，并经过几个特定的次序处理数据。

  * **下载器中间件(Downloader Middlewares)**  
位于Scrapy引擎和下载器之间的框架，主要是处理Scrapy引擎与下载器之间的请求及响应。

  * **爬虫中间件(Spider Middlewares)**  
介于Scrapy引擎和爬虫之间的框架，主要工作是处理蜘蛛的响应输入和请求输出。

  * **调度中间件(Scheduler Middewares)**  
介于Scrapy引擎和调度之间的中间件，从Scrapy引擎发送到调度的请求和响应。



**Scrapy运行流程大概如下：**

  1. 引擎从调度器中取出一个链接(URL)用于接下来的抓取
  2. 引擎把URL封装成一个请求(Request)传给下载器
  3. 下载器把资源下载下来，并封装成应答包(Response)
  4. 爬虫解析Response
  5. 解析出实体（Item）,则交给实体管道进行进一步的处理
  6. 解析出的是链接（URL）,则把URL交给调度器等待抓取



**创建Scrapy框架项目**

****Scrapy框架项目是有python安装目录里的Scripts文件夹里scrapy.exe文件创建的，所以python安装目录下的 **
**Scripts文件夹要配置到系统环境变量里，才能运行命令生成项目********

********创建项目********

********首先运行cmd终端，然后cd 进入要创建项目的目录，如：cd H:\py\14********

********进入要创建项目的目录后执行命令 scrapy startproject 项目名称********

[code]

    scrapy startproject pach1
[/code]

**项目创建成功**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170723214011705-1505671017.png)**



**项目说明**

目录结构如下：

├── firstCrawler

│   ├── __init__.py

│   ├── items.py

│   ├── middlewares.py

│   ├── pipelines.py

│   ├── settings.py

│   └── spiders

│       └── __init__.py

└── scrapy.cfg

    * `scrapy.cfg`: 项目的配置文件
    * `tems.py`: 项目中的item文件，用来定义解析对象对应的属性或字段。
    * `pipelines.py`: 负责处理被spider提取出来的item。典型的处理有清理、 验证及持久化(例如存取到数据库）[  
](http://lib.csdn.net/base/mysql "MySQL知识库")

    * `settings.py`: 项目的设置文件.
    * spiders：实现自定义爬虫的目录
    * middlewares.py：Spider中间件是在引擎及Spider之间的特定钩子(specific hook)，处理spider的输入(response)和输出(items及requests)。 其提供了一个简便的机制，通过插入自定义代码来扩展Scrapy功能。

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170723220140619-2067789450.png)**



**创建第一个爬虫**

**创建爬虫文件在spiders文件夹里创建**

**1、创建一个类必须继承scrapy.Spider类，类名称自定义**

**类里的属性和方法：**

**name属性 ，设置爬虫名称**  
 **allowed_domains属性 ，设置爬取的域名，不带http**  
 **start_urls属性 ，设置爬取的URL，带http**  
 **parse()方法 ，爬取页面后的回调方法，response参数是一个对象，封装了所有的爬取信息**

****response对象的方法和属性****

**response.url 获取抓取的rul**  
 **response.body 获取网页内容字节类型**  
 **response.body_as_unicode() 获取网站内容字符串类型**

[code]

    # -*- coding: utf-8 -*-
    import scrapy
    
    
    class AdcSpider(scrapy.Spider):
        name = 'adc'                                        #设置爬虫名称
        allowed_domains = ['www.shaimn.com']
        start_urls = ['http://www.shaimn.com/xinggan/']
    
        def parse(self, response):
            current_url = response.url                      #获取抓取的rul
            body = response.body                            #获取网页内容字节类型
            unicode_body = response.body_as_unicode()       #获取网站内容字符串类型
            print(unicode_body)
[/code]

**爬虫写好后执行爬虫，cd到爬虫目录里执行 scrapy crawl adc --nolog命令，说明： **scrapy crawl adc ( **
**adc表示**** 爬虫名称) \--nolog( ** **\--nolog表示不显示日志**** )****

****也可以在PyCharm执行命令****

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170724171121590-563261664.png)**



