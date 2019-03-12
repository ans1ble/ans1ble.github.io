---
layout: post
title: " 第三百二十七节，web爬虫讲解2—urllib库爬虫—基础使用—超时设置—自动模拟http请求 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

  
**第三百二十七节，web爬虫讲解2—urllib库爬虫**



**利用python系统自带的 **urllib库写简单爬虫****

**urlopen() 获取一个URL的html源码**  
 **read() 读出html源码内容**  
 **decode("utf-8") 将字节转化成字符串**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html').read().decode("utf-8")
    print(html)
[/code]

[code]

    <!DOCTYPE html>
    <html lang="zh-CN">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta name="csrf-param" content="_csrf">
        <meta name="csrf-token" content="X1pZZnpKWnQAIGkLFisPFT4jLlJNIWMHHWM6HBBnbiwPbz4/LH1pWQ==">
[/code]



**正则获取页面指定内容**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    import re
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html').read().decode("utf-8")   #获取html源码
    pat = "51CTO学院Python实战群\((\d*?)\)"      #正则规则，获取到QQ号
    rst = re.compile(pat).findall(html)
    print(rst)
    
    #['325935753']
[/code]



**urlretrieve() 将网络文件下载保存到本地，参数1网络文件URL，参数2保存路径**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from urllib import request
    import re
    import os
    
    file_path = os.path.join(os.getcwd() + '/222.html')    #拼接文件保存路径
    # print(file_path)
    request.urlretrieve('http://edu.51cto.com/course/8360.html', file_path) #下载这个文件保存到指定路径
[/code]



**urlcleanup() 清除爬虫产生的内存**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from urllib import request
    import re
    import os
    
    file_path = os.path.join(os.getcwd() + '/222.html')    #拼接文件保存路径
    # print(file_path)
    request.urlretrieve('http://edu.51cto.com/course/8360.html', file_path) #下载这个文件保存到指定路径
    request.urlcleanup()
[/code]



**info() 查看抓取页面的简介**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    import re
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html')   #获取html源码
    a = html.info()
    print(a)
    
    # C:\Users\admin\AppData\Local\Programs\Python\Python35\python.exe H:/py/15/chshi.py
    # Date: Tue, 25 Jul 2017 16:08:17 GMT
    # Content-Type: text/html; charset=UTF-8
    # Transfer-Encoding: chunked
    # Connection: close
    # Set-Cookie: aliyungf_tc=AQAAALB8CzAikwwA9aReq63oa31pNIez; Path=/; HttpOnly
    # Server: Tengine
    # Vary: Accept-Encoding
    # Vary: Accept-Encoding
    # Vary: Accept-Encoding
[/code]



**getcode() 获取状态码**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    import re
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html')   #获取html源码
    a = html.getcode()  #获取状态码
    print(a)
    
    #200
[/code]





**geturl() 获取当前抓取页面的URL**

[code]

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    import re
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html')   #获取html源码
    a = html.geturl()  #获取当前抓取页面的URL
    print(a)
    
    #http://edu.51cto.com/course/8360.html
[/code]



**timeout 抓取超时设置，单位为秒**

**是指抓取一个页面时对方服务器响应太慢，或者很久没响应，设置一个超时时间，超过超时时间就不抓取了**

[code]

     #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    import urllib.request
    import re
    html = urllib.request.urlopen('http://edu.51cto.com/course/8360.html',timeout=30)   #获取html源码
    a = html.geturl()  #获取当前抓取页面的URL
    print(a)
    
    #http://edu.51cto.com/course/8360.html
[/code]





**自动模拟http请求**

**http请求一般常用的就是get请求和post请求**

****get请求****

**比如360搜索，就是通过get请求并且将用户的搜索关键词传入到服务器获取数据的**

**所以我们可以模拟百度http请求，构造关键词自动请求**

**quote() 将关键词转码成浏览器认识的字符，默认网站不能是中文**

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import urllib.request
    import re
    gjc = "手机"     #设置关键词
    gjc = urllib.request.quote(gjc)         #将关键词转码成浏览器认识的字符，默认网站不能是中文
    url = "https://www.so.com/s?q="+gjc     #构造url地址
    # print(url)
    html = urllib.request.urlopen(url).read().decode("utf-8")  #获取html源码
    pat = "(\w*<em>\w*</em>\w*)"            #正则获取相关标题
    rst = re.compile(pat).findall(html)
    # print(rst)
    for i in rst:
        print(i)                            #循环出获取的标题
    
        # 官网 < em > 手机 < / em >
        # 官网 < em > 手机 < / em >
        # 官网 < em > 手机 < / em > 这么低的价格
        # 大牌 < em > 手机 < / em > 低价抢
        # < em > 手机 < / em >
        # 淘宝网推荐 < em > 手机 < / em >
        # < em > 手机 < / em >
        # < em > 手机 < / em >
        # < em > 手机 < / em >
        # < em > 手机 < / em >
        # 苏宁易购买 < em > 手机 < / em >
        # 买 < em > 手机 < / em >
        # 买 < em > 手机 < / em >
[/code]

**  post请求**

**urlencode() 封装post请求提交的表单数据，参数是字典形式的键值对表单数据**  
 **Request() 提交post请求，参数1是url地址，参数2是封装的表单数据**

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import urllib.request
    import urllib.parse
    
    posturl = "http://www.iqianyue.com/mypost/"
    shuju = urllib.parse.urlencode({                #urlencode()封装post请求提交的表单数据，参数是字典形式的键值对表单数据
        'name': '123',
        'pass': '456'
        }).encode('utf-8')
    req = urllib.request.Request(posturl,shuju)     #Request()提交post请求，参数1是url地址，参数2是封装的表单数据
    html = urllib.request.urlopen(req).read().decode("utf-8")  #获取post请求返回的页面
    print(html)
[/code]



