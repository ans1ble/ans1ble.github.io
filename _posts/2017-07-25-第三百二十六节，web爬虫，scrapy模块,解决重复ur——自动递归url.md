---
layout: post
title: " 第三百二十六节，web爬虫，scrapy模块,解决重复ur——自动递归url "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

  
**第三百二十六节，web爬虫，scrapy模块,解决重复url——自动递归url**



**一般抓取过的url不重复抓取，那么就需要记录url，判断当前URL如果在记录里说明已经抓取过了，如果不存在说明没抓取过**

**记录url可以是缓存，或者数据库，如果保存数据库按照以下方式：**

**id URL加密(建索引以便查询) 原始URL**

**保存URL表里应该至少有以上3个字段**  
 **1、URL加密(建索引以便查询)字段：用来查询这样速度快，**  
 **2、原始URL，用来给加密url做对比，防止加密不同的URL出现同样的加密值**



**自动递归url**

[code]

     # -*- coding: utf-8 -*-
    import scrapy       #导入爬虫模块
    from scrapy.selector import HtmlXPathSelector  #导入HtmlXPathSelector模块
    from scrapy.selector import Selector
    
    
    class AdcSpider(scrapy.Spider):
        name = 'adc'                                        #设置爬虫名称
        allowed_domains = ['hao.360.cn']
        start_urls = ['https://hao.360.cn/']
    
        def parse(self, response):
    
            #这里做页面的各种获取以及处理
    
            #递归查找url循环执行
            hq_url = Selector(response=response).xpath('//a/@href')   #查找到当前页面的所有a标签的href，也就是url
            for url in hq_url:                                        #循环url
                yield scrapy.Request(url=url, callback=self.parse)    #每次循环将url传入Request方法进行继续抓取，callback执行parse回调函数，递归循环
    
            #这样就会递归抓取url并且自动执行了，但是需要在settings.py 配置文件中设置递归深度，DEPTH_LIMIT=3表示递归3层 
[/code]

**这样就会递归抓取url并且自动执行了，但是需要在 settings.py 配置文件中设置递归深度，DEPTH_LIMIT=3表示递归3层**

**![](https://images2015.cnblogs.com/blog/955761/201707/955761-20170725134811974-426130734.png)**



