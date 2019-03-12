
---
layout: post
title: " 第三百五十节，Python分布式爬虫打造搜索引擎Scrapy精讲—selenium模块是一个python操作浏览器软件的一个模块，可以实现js动态网页请求 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


  
**第三百五十节，Python分布式爬虫打造搜索引擎Scrapy精讲—selenium模块是一个python操作浏览器软件的一个模块，可以实现js动态网页请求**



****selenium模块****

******selenium模块为第三方模块需要安装， **selenium模块是一个操作各种浏览器对应软件的api接口模块********

****************selenium模块是一个操作各种浏览器对应软件的api接口模块，所以还得需要下载对应浏览器的操作软件****************

****************操作原理是： ** **selenium模块操作浏览器操作软件， ** ** ** ** ** ** ** ** **
**浏览器操作软件操作浏览器****************************************

**Selenium 2.0适用于以下浏览器**  
 **Google Chrome**  
 **Internet Explorer 7, 8, 9, 10, 11**  
 **Firefox**  
 **Safari**  
 **Opera**  
 **HtmlUnit**  
 **phantomjs**  
 **Android**  
 **iOS**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170824205035746-617336861.png)**





**Selenium 的核心，就是用js控制浏览器**

******************************************下载对应浏览器的 ** ** ** ** ** ** ** ** **
** ** ** ** ** ** ** ** ** **
**浏览器操作软件**********************************************************************************



**Chrome: https://sites.google.com/a/chromium.org/chromedriver/downloads**  
 **Edge: https://developer.microsoft.com/en-us/microsoft-
edge/tools/webdriver/**  
 **Firefox: https://github.com/mozilla/geckodriver/releases**  
 **Safari: https://webkit.org/blog/6900/webdriver-support-in-safari-10/**



**我们这里以火狐浏览器为列**

**首先将火狐浏览器的操作软件，geckodriver.exe文件放置到爬虫目录里**

**selenium模块可以模拟用户行为操作各种版本浏览器**

**webdriver.Firefox('操作浏览器软件路径') 实例化火狐浏览器对象**  
 **get('url') 访问网站**  
 **find_element_by_xpath('xpath表达式') 通过xpath表达式找对应元素**  
 **clear() 清空输入框里的内容**  
 **send_keys('内容') 将内容写入输入框**  
 **click() 点击事件**  
 **get_screenshot_as_file('截图保存路径名称') 将网页截图，保存到此目录**  
 **page_source 获取网页htnl源码**  
 **browser.close() 关闭浏览器**



[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from selenium import webdriver  # 导入selenium模块来操作浏览器软件
    import time
    
    browser = webdriver.Firefox(executable_path='H:/py/16/adc/adc/Firefox/geckodriver.exe')
    browser.get('https://www.tmall.com/?spm=a220o.1000855.a2226mz.1.5c90c3484bZCx6')
    
    # 模拟用户操作
    browser.find_element_by_xpath('//input[@id="mq"]').clear()                 # 通过xpath表达式找到输入框，clear()清空输入框里的内容
    browser.find_element_by_xpath('//input[@id="mq"]').send_keys('连衣裙')     # 通过xpath表达式找到输入框，send_keys()将内容写入输入框
    browser.find_element_by_xpath('//button[@type="submit"]').click()          # 通过xpath表达式找到搜索按钮,click()点击事件
    
    time.sleep(3)   # 等待3秒
    browser.get_screenshot_as_file('H:/py/17/img/123.jpg')  # 将网页截图，保存到此目录
    
    neir = browser.page_source   # 获取网页内容
    print(neir)
    
    browser.close()     # 关闭浏览器
[/code]





**利用scrapy的Selector方法。来过滤帅选数据**

**Selector()方法 ,过滤帅选数据,参数是得到的字符串html源码**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from selenium import webdriver  # 导入selenium模块来操作浏览器软件
    import time
    from scrapy.selector import Selector
    
    browser = webdriver.Firefox(executable_path='H:/py/16/adc/adc/Firefox/geckodriver.exe')
    browser.get('https://www.tmall.com/?spm=a220o.1000855.a2226mz.1.5c90c3484bZCx6')
    
    # 模拟用户操作
    browser.find_element_by_xpath('//input[@id="mq"]').clear()                 # 通过xpath表达式找到输入框，clear()清空输入框里的内容
    browser.find_element_by_xpath('//input[@id="mq"]').send_keys('连衣裙')     # 通过xpath表达式找到输入框，send_keys()将内容写入输入框
    browser.find_element_by_xpath('//button[@type="submit"]').click()          # 通过xpath表达式找到搜索按钮,click()点击事件
    
    time.sleep(3)   # 等待3秒
    browser.get_screenshot_as_file('H:/py/17/img/123.jpg')  # 将网页截图，保存到此目录
    
    neir = browser.page_source   # 获取网页内容
    # print(neir)
    gl_neir = Selector(text=neir)
    dedao = gl_neir.css('title::text').extract()
    print(dedao)
    
    browser.close()     # 关闭浏览器
[/code]





****selenium操作浏览器滚动滚动条****

****execute_script(js)**** ** **方法，执行原生态js脚本****

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from selenium import webdriver  # 导入selenium模块来操作浏览器软件
    import time
    from scrapy.selector import Selector
    
    browser = webdriver.Firefox(executable_path='H:/py/16/adc/adc/Firefox/geckodriver.exe')
    browser.get('https://www.oschina.net/blog')
    
    
    time.sleep(3)       # 等待3秒
    for i in range(3):  # 滚动3次滚动条
        js = 'window.scrollTo(0,document.body.scrollHeight); var lenofpage=document.body.scrollHeight; return lenofpage'
        browser.execute_script(js)  # 执行js语言滚动滚动条
        time.sleep(3)
    
    neir = browser.page_source   # 获取网页内容
    # print(neir)
    gl_neir = Selector(text=neir)
    dedao = gl_neir.css('title::text').extract()
    print(dedao)
    
    # browser.close()     # 关闭浏览器
[/code]





**设置请求网页不加载图片，提高请求效率**  
 **ChromeOptions() 方法，创建谷歌浏览器设置对象**  
 **Chrome() 方法，创建谷歌浏览器对象**

**下面以谷歌浏览器为列**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from selenium import webdriver  # 导入selenium模块来操作浏览器软件
    from scrapy.selector import Selector
    
    #设置请求网页不加载图片，提高请求效率
    chrome_options = webdriver.ChromeOptions()                          #创建谷歌浏览器设置对象
    prefs = {"profile.managed_default_content_settings.images": 2}      #设置谷歌浏览器不加载图片
    chrome_options.add_experimental_option('prefs', prefs)              #将不加载图片添加到浏览器
    
    browser = webdriver.Chrome(executable_path='H:/py/16/adc/adc/Firefox/chromedriver.exe', chrome_options=chrome_options)
    # browser.set_page_load_timeout(40) #设置页面最长加载时间为40s
    browser.get('https://www.taobao.com/')
    
    
    neir = browser.page_source   # 获取网页内容
    # print(neir)
    gl_neir = Selector(text=neir)
    dedao = gl_neir.css('title::text').extract()
    print(dedao)
    
    # browser.close()     # 关闭浏览器
[/code]



******selenium模块还可以操作**** PhantomJS浏览器，
**PhantomJS是一个无界面浏览器，比较清爽，但是多线程是性能会下降****



****重点：我们推荐使用chromedriver.exe，谷歌浏览器****

