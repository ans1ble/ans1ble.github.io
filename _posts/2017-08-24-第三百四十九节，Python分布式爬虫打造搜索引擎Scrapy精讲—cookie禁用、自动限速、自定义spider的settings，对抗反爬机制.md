---
layout: post
title: " 第三百四十九节，Python分布式爬虫打造搜索引擎Scrapy精讲—cookie禁用、自动限速、自定义spider的settings，对抗反爬机制 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百四十九节，Python分布式爬虫打造搜索引擎Scrapy精讲—cookie禁用、自动限速、自定义spider的settings，对抗反爬机制**



****cookie禁用****

****就是在 **Scrapy的配置文件settings.py里禁用掉 ** **cookie禁用，可以防止被通过 **
**cookie禁用识别到是爬虫，注意，只适用于不需要登录的网页， ** **cookie禁用后是无法登录的******************

**settings.py里禁用掉cookie禁用**

**COOKIES_ENABLED = False 禁用cookie**

[code]

     # Disable cookies (enabled by default)
    COOKIES_ENABLED = False
[/code]



**自动限速**

****Scrapy默认没有限速的，只要遇到URL就访问，没有间隙****

****自动限速(AutoThrottle)扩展****

**********settings.py里设置**********

****DOWNLOAD_DELAY = 下载器在下载同一个网站下一个页面前需要等待的时间。该选项可以用来限制爬取速度，
减轻服务器压力。同时也支持小数（单位秒）****

[code]

     # Configure a delay for requests for the same website (default: 0)
    # See http://scrapy.readthedocs.org/en/latest/topics/settings.html#download-delay
    # See also autothrottle settings and docs
    DOWNLOAD_DELAY = 10
[/code]

**AUTOTHROTTLE_ENABLED = True   开启限速， **启用AutoThrottle扩展****

[code]

     # Enable and configure the AutoThrottle extension (disabled by default)
    # See http://doc.scrapy.org/en/latest/topics/autothrottle.html
    AUTOTHROTTLE_ENABLED = True
[/code]





******自定义spider的settings，也就是为每一个爬虫单独设置配置文件里的值，将覆盖掉 ** ** ** **
**settings.py里的相同设置****************

**custom_settings = {键值对} 为每一个爬虫单独设置配置文件里的值，将覆盖掉settings.py里的相同设置，在爬虫文件里设置**

**举例：**

[code]

     # -*- coding: utf-8 -*-
    import scrapy
    from scrapy.http import Request,FormRequest
    
    class PachSpider(scrapy.Spider):                            #定义爬虫类，必须继承scrapy.Spider
        name = 'pach'                                           #设置爬虫名称
        allowed_domains = ['www.kuaidaili.com']                 #爬取域名
    
        custom_settings = {
            "COOKIES_ENABLED": True                             #覆盖掉settings.py里的相同设置，开启COOKIES
        }
    
        def start_requests(self):    #起始url函数，会替换start_urls
            """第一次请求一下登录页面，设置开启cookie使其得到cookie，设置回调函数"""
            return [Request(
                url='http://www.kuaidaili.com/free/inha/2/',
                meta={'cookiejar':1},       #开启Cookies记录，将Cookies传给回调函数
                callback=self.parse
            )]
    
    
        def parse(self, response):
            title = response.xpath('//*[@id="list"]/table/tbody/tr')
[/code]



