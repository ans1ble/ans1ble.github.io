
---
layout: post
title: " 第三百四十节，Python分布式爬虫打造搜索引擎Scrapy精讲—css选择器 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百四十节，Python分布式爬虫打造搜索引擎Scrapy精讲—css选择器**



****css选择器****

****1、****

****![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170803191436037-857086866.png)****



**2、**

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170803191508787-1715841890.png)



**3、**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170803191537147-2089179759.png)**

**  ::attr()获取元素属性，css选择器**

**::text获取标签文本**



**举例：**

**extract_first('') 获取过滤后的数据，返回字符串，有一个默认参数，也就是如果没有数据默认是什么，一般我们设置为空字符串**

**extract() **获取过滤后的数据，返回字符串列表****



[code]

    # -*- coding: utf-8 -*-
    import scrapy
    
    class PachSpider(scrapy.Spider):
        name = 'pach'
        allowed_domains = ['blog.jobbole.com']
        start_urls = ['http://blog.jobbole.com/all-posts/']
    
        def parse(self, response):
    
            asd = response.css('.archive-title::text').extract()  #这里也可以用extract_first('')获取返回字符串
            # print(asd)
    
            for i in asd:
                print(i)
[/code]

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170803191725709-1789476468.png)



