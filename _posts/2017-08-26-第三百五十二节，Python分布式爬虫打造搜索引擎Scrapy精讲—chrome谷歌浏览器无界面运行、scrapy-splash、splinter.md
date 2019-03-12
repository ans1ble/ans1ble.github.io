
---
layout: post
title: " 第三百五十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—chrome谷歌浏览器无界面运行、scrapy-splash、splinter "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


  
**第三百五十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—chrome谷歌浏览器无界面运行、scrapy-splash、 splinter**



****1、chrome谷歌浏览器无界面运行****

******chrome谷歌浏览器无界面运行，主要运行在Linux系统， windows系统下不支持******

************chrome谷歌浏览器无界面运行需要一个模块，pyvirtualdisplay模块************

************需要先安装 ** ** ** ** ** **pyvirtualdisplay模块************************

************************Display(visible=0, size=(800, 600))
设置浏览器，visible=0表示不显示界面，size=(800, 600)表示浏览器尺寸************************

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
    
            from pyvirtualdisplay import Display
            display = Display(visible=0, size=(800, 600))
            display.start()
    
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

**  注意：Linux系统下会出现错误**

**报错：easyprocess.EasyProcessCheckInstalledError: cmd=['Xvfb', '-help']
OSError=[Errno 2] No such file or directory**

**需要两个步骤解决**

**1.执行命令：** **sudo apt-get install xvfb    安装 **xvfb软件****

****2.执行命令： pip install xvfbwrapper   安装 ** **xvfbwrapper模块********





**以下只是提到一下，前面讲的selenium模块操作浏览器已经够用了**

**2、scrapy-splash，也是 **scrapy获取动态网页的方案，这里就不介绍了，详情： https://github.com/scrapy-
plugins/scrapy-splash****

******3、splinter，是一个操作浏览器的模块 详情： https://github.com/cobrateam/splinter******



