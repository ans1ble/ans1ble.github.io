---
layout: post
title: " 第三百五十一节，Python分布式爬虫打造搜索引擎Scrapy精讲—将selenium操作谷歌浏览器集成到scrapy中 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百五十一节，Python分布式爬虫打造搜索引擎Scrapy精讲—将selenium操作谷歌浏览器集成到scrapy中**



**1、爬虫文件**

**dispatcher.connect() 信号分发器，第一个参数信号触发函数，第二个参数是触发信号，**  
 **signals.spider_closed 是爬虫结束信号**

[code]

    # -*- coding: utf-8 -*-
    import scrapy
    from scrapy.http import Request,FormRequest
    from selenium import webdriver                  # 导入selenium模块来操作浏览器软件
    from scrapy.xlib.pydispatch import dispatcher   # 信号分发器
    from scrapy import signals                      # 信号
    
    class PachSpider(scrapy.Spider):                            #定义爬虫类，必须继承scrapy.Spider
        name = 'pach'                                           #设置爬虫名称
        allowed_domains = ['www.taobao.com']                    #爬取域名
    
        def __init__(self):                                                                                 #初始化
            self.browser = webdriver.Chrome(executable_path='H:/py/16/adc/adc/Firefox/chromedriver.exe')    #创建谷歌浏览器对象
            super(PachSpider, self).__init__()                                                              #设置可以获取上一级父类基类的，__init__方法里的对象封装值
            dispatcher.connect(self.spider_closed, signals.spider_closed)       #dispatcher.connect()信号分发器，第一个参数信号触发函数，第二个参数是触发信号，signals.spider_closed是爬虫结束信号
    
            #运行到此处时，就会去中间件执行，RequestsChrometmiddware中间件了
    
        def spider_closed(self, spider):                                        #信号触发函数
            print('爬虫结束 停止爬虫')
            self.browser.quit()                                                 #关闭浏览器
    
        def start_requests(self):    #起始url函数，会替换start_urls
            return [Request(
                url='https://www.taobao.com/',
                callback=self.parse
            )]
    
    
        def parse(self, response):
            title = response.css('title::text').extract()
            print(title)
[/code]





**2、middlewares.py中间件文件**

[code]

     from scrapy.http import HtmlResponse
    
    
    class RequestsChrometmiddware(object):              # 浏览器访问中间件
    
        def process_request(self, request, spider):     # 重写process_request请求方法
            if spider.name == 'pach':                   # 判断爬虫名称为pach时执行
                spider.browser.get(request.url)         #用谷歌浏览器访问url
                import time
                time.sleep(3)
                print('访问：{0}'.format(request.url))  # 打印访问网址
                #设置响应信息，由浏览器响应信息返回
                return HtmlResponse(url=spider.browser.current_url, body=spider.browser.page_source, encoding='utf-8', request=request)
[/code]





**3、settings.py配置文件注册中间件**

[code]

    DOWNLOADER_MIDDLEWARES = {               #开启注册中间件
       'adc.middlewares.RequestsUserAgentmiddware': 543,
       'adc.middlewares.RequestsChrometmiddware': 542,
       'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None, #将默认的UserAgentMiddleware设置为None
    }
[/code]



