
---
layout: post
title: " 第三百五十五节，Python分布式爬虫打造搜索引擎Scrapy精讲—scrapy信号详解 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百五十五节，Python分布式爬虫打造搜索引擎Scrapy精讲—scrapy信号详解**

**信号一般使用信号分发器dispatcher.connect()，来设置信号，和信号触发函数，当捕获到信号时执行一个函数**

**dispatcher.connect() 信号分发器，第一个参数信号触发函数，第二个参数是触发信号，**



**以下是各种信号**

**signals.engine_started 当Scrapy引擎启动爬取时发送该信号。该信号支持返回deferreds。**  
 **signals.engine_stopped 当Scrapy引擎停止时发送该信号(例如，爬取结束)。该信号支持返回deferreds。**



**signals.item_scraped(item, response, spider) 当item被爬取，并通过所有 Item Pipeline
后(没有被丢弃(dropped)，发送该信号。该信号支持返回deferreds。**  
 **参数:**  
 **item (Item 对象) – 爬取到的item**  
 **spider (Spider 对象) – 爬取item的spider**  
 **response (Response 对象) – 提取item的response**

  
**signals.item_dropped(item, exception, spider) 当item通过 Item Pipeline
，有些pipeline抛出 DropItem 异常，丢弃item时，该信号被发送。该信号支持返回deferreds。**  
 **参数:**  
 **item (Item 对象) – Item Pipeline 丢弃的item**  
 **spider (Spider 对象) – 爬取item的spider**  
 **exception (DropItem 异常) – 导致item被丢弃的异常(必须是 DropItem 的子类)**

  
**signals.spider_closed(spider, reason)
当某个spider被关闭时，该信号被发送。该信号可以用来释放每个spider在 spider_opened
时占用的资源。该信号支持返回deferreds。**  
 **参数:**  
 **spider (Spider 对象) – 关闭的spider**  
 **reason (str) – 描述spider被关闭的原因的字符串。如果spider是由于完成爬取而被关闭，则其为 'finished'
。否则，如果spider是被引擎的 close_spider 方法所关闭，则其为调用该方法时传入的 reason 参数(默认为
'cancelled')。如果引擎被关闭(例如， 输入Ctrl-C)，则其为 'shutdown' 。**

  
**signals.spider_opened(spider)
当spider开始爬取时发送该信号。该信号一般用来分配spider的资源，不过其也能做任何事。该信号支持返回deferreds。**  
 **参数: spider (Spider 对象) – 开启的spider**

  
**signals.spider_idle(spider) 当spider进入空闲(idle)状态时该信号被发送。空闲意味着:**  
 **requests正在等待被下载**  
 **requests被调度**  
 **items正在item pipeline中被处理**  
 **当该信号的所有处理器(handler)被调用后，如果spider仍然保持空闲状态， 引擎将会关闭该spider。当spider被关闭后，
spider_closed 信号将被发送。您可以，比如，在 spider_idle 处理器中调度某些请求来避免spider被关闭。该信号 不支持
返回deferreds。**  
 **参数: spider (Spider 对象) – 空闲的spider**

  
**signals.spider_error(failure, response, spider)
当spider的回调函数产生错误时(例如，抛出异常)，该信号被发送**  
 **参数:**  
 **failure (Failure 对象) – 以Twisted Failure 对象抛出的异常**  
 **response (Response 对象) – 当异常被抛出时被处理的response**  
 **spider (Spider 对象) – 抛出异常的spider**

  
**signals.request_scheduled(request, spider) 当引擎调度一个 Request
对象用于下载时，该信号被发送。该信号 不支持 返回deferreds。**  
 **参数:**  
 **request (Request 对象) – 到达调度器的request**  
 **spider (Spider 对象) – 产生该request的spider**

  
**signals.response_received(response, request, spider) 当引擎从downloader获取到一个新的
Response 时发送该信号。该信号 不支持 返回deferreds。**  
 **参数:**  
 **response (Response 对象) – 接收到的response**  
 **request (Request 对象) – 生成response的request**  
 **spider (Spider 对象) – response所对应的spider**

  
**signals.response_downloaded(response, request, spider) 当一个 HTTPResponse
被下载时，由downloader发送该信号。该信号 不支持 返回deferreds。**  
 **参数:**  
 **response (Response 对象) – 下载的response**  
 **request (Request 对象) – 生成response的request**  
 **spider (Spider 对象) – response所对应的spider**



**我们以 **signals.spider_closed(spider, reason)信号举例其他信号同理：****

[code]

     # -*- coding: utf-8 -*-
    import scrapy
    from scrapy.http import Request,FormRequest
    from scrapy.xlib.pydispatch import dispatcher   # 信号分发器
    from scrapy import signals                      # 信号
    
    
    
    class PachSpider(scrapy.Spider):                            #定义爬虫类，必须继承scrapy.Spider
        name = 'pach'                                           #设置爬虫名称
        allowed_domains = ['www.dict.cn']                       #爬取域名
    
        def start_requests(self):    #起始url函数，会替换start_urls
            return [Request(
                url='http://www.dict.cn/9999998888',
                callback=self.parse
            )]
    
        # 利用数据收集器，收集所有404的url以及，404页面数量
        handle_httpstatus_list = [404]                                      # 设置不过滤404
    
        def __init__(self):
            self.fail_urls = []                                             # 创建一个变量来储存404URL
            dispatcher.connect(self.spider_closed, signals.spider_closed)   # dispatcher.connect()信号分发器，第一个参数信号触发函数，第二个参数是触发信号，signals.spider_closed是爬虫结束信号
    
        def spider_closed(self, spider, reason):  # 信号触发函数
            print('爬虫结束 停止爬虫')
            print(self.fail_urls)  # 打印404URL列表
            print(self.crawler.stats.get_value('failed_url'))  # 打印数据收集值
    
        def parse(self, response):                                          # 回调函数
            if response.status == 404:                                      # 判断返回状态码如果是404
                self.fail_urls.append(response.url)                         # 将URL追加到列表
                self.crawler.stats.inc_value('failed_url')                  # 设置一个数据收集，值为自增，每执行一次自增1
            else:
                title = response.css('title::text').extract()
                print(title)
[/code]



