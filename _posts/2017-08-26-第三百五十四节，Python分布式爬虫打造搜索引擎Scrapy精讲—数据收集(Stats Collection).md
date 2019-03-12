
---
layout: post
title: " 第三百五十四节，Python分布式爬虫打造搜索引擎Scrapy精讲—数据收集(Stats Collection) "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百五十四节，Python分布式爬虫打造搜索引擎Scrapy精讲—数据收集(Stats Collection)**



Scrapy提供了方便的收集数据的机制。数据以key/value方式存储，值大多是计数值。 该机制叫做数据收集器(Stats Collector)，可以通过
Crawler API 的属性 stats 来使用  
无论数据收集(stats collection)开启或者关闭，数据收集器永远都是可用的。
因此您可以import进自己的模块并使用其API(增加值或者设置新的状态键(stat keys))。 该做法是为了简化数据收集的方法:
您不应该使用超过一行代码来收集您的spider，Scrpay扩展或任何您使用数据收集器代码里头的状态。

数据收集器的另一个特性是(在启用状态下)很高效，(在关闭情况下)非常高效(几乎察觉不到)。

数据收集器对每个spider保持一个状态表。当spider启动时，该表自动打开，当spider关闭时，自动关闭。

**数据收集各种函数**

**stats.set_value('数据名称', 数据值) 设置数据**  
 **stats.inc_value('数据名称') 增加数据值，自增1**  
 **stats.max_value('数据名称', value) 当新的值比原来的值大时设置数据**  
 **stats.min_value('数据名称', value) 当新的值比原来的值小时设置数据**  
 **stats.get_value('数据名称') 获取数据值**  
 **stats.get_stats() 获取所有数据**

**举例：**

[code]

     # -*- coding: utf-8 -*-
    import scrapy
    from scrapy.http import Request,FormRequest
    
    
    class PachSpider(scrapy.Spider):                            #定义爬虫类，必须继承scrapy.Spider
        name = 'pach'                                           #设置爬虫名称
        allowed_domains = ['www.dict.cn']                       #爬取域名
    
        def start_requests(self):    #起始url函数，会替换start_urls
            return [Request(
                url='http://www.dict.cn/9999998888',
                callback=self.parse
            )]
    
        # 利用数据收集器，收集所有404的url以及，404页面数量
        handle_httpstatus_list = [404]                                  # 设置不过滤404
    
        def __init__(self):
            self.fail_urls = []                                         # 创建一个变量来储存404URL
    
        def parse(self, response):                                      # 回调函数
            if response.status == 404:                                  # 判断返回状态码如果是404
                self.fail_urls.append(response.url)                     # 将URL追加到列表
                self.crawler.stats.inc_value('failed_url')              # 设置一个数据收集，值为自增，每执行一次自增1
                print(self.fail_urls)                                   # 打印404URL列表
                print(self.crawler.stats.get_value('failed_url'))       # 打印数据收集值
            else:
                title = response.css('title::text').extract()
                print(title)
[/code]

**  更多:http://scrapy-chs.readthedocs.io/zh_CN/latest/topics/stats.html**

