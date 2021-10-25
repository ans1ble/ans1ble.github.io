---
layout: post
title: " 第三百二十九节，web爬虫讲解2—urllib库爬虫—ip代理—用户代理和ip代理结合应用 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

  
**第三百二十九节，web爬虫讲解2—urllib库爬虫—ip代理**



**使用IP代理**

**ProxyHandler() 格式化IP，第一个参数，请求目标可能是http或者https,对应设置**  
 **build_opener() 初始化IP**  
 **install_opener() 将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP**

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib
    import urllib.request
    import random   #引入随机模块文件
    
    ip = "180.115.8.212:39109"
    proxy = urllib.request.ProxyHandler({"https":ip})                        #格式化IP,注意：第一个参数可能是http或者https，对应设置
    opener = urllib.request.build_opener(proxy,urllib.request.HTTPHandler)  #初始化IP
    urllib.request.install_opener(opener)       #将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP
    
    #请求
    url = "https://www.baidu.com/"
    data = urllib.request.urlopen(url).read().decode("utf-8")
    print(data)
[/code]



**ip代理池构建一**

**适合IP存活时间长，稳定性好的代理ip，随机调用列表里的ip**

[code]

     #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib
    from urllib import request
    import random   #引入随机模块文件
    def dai_li_ip():
        ip = [
            '110.73.8.103:8123',
            '115.46.151.100:8123',
            '42.233.187.147:19'
            ]
        shui = random.choice(ip)
        print(shui)
        proxy = urllib.request.ProxyHandler({"https": shui})  # 格式化IP,注意，第一个参数，请求目标可能是http或者https,对应设置
        opener = urllib.request.build_opener(proxy, urllib.request.HTTPHandler)  # 初始化IP
        urllib.request.install_opener(opener)  # 将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP
    
    #请求
    dai_li_ip() #执行代理IP函数
    url = "https://www.baidu.com/"
    data = urllib.request.urlopen(url).read().decode("utf-8")
    print(data)
[/code]



****ip代理池构建二，接口方式****

****每次调用第三方接口动态获取ip,适用于IP存活时间短的情况****

****我们用 http://http.zhimaruanjian.com/第三方接口测试****

[code]

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib
    from urllib import request
    import json
    def dai_li_ip():
        url = "http://http-webapi.zhimaruanjian.com/getip?num=1&type=2&pro=&city=0&yys=0&port=11&time=1&ts=0&ys=0&cs=0&lb=1&sb=0&pb=4&mr=1"
        data = urllib.request.urlopen(url).read().decode("utf-8")
        data2 = json.loads(data)  # 将字符串还原它本来的数据类型
    
        print(data2['data'][0])
        ip = str(data2['data'][0]['ip'])
        dkou = str(data2['data'][0]['port'])
        zh_ip = ip + ':' + dkou
        print(zh_ip)
    
    
        proxy = urllib.request.ProxyHandler({"https": zh_ip})  # 格式化IP,注意，第一个参数，请求目标可能是http或者https,对应设置
        opener = urllib.request.build_opener(proxy, urllib.request.HTTPHandler)  # 初始化IP
        urllib.request.install_opener(opener)  # 将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP
    
    #请求
    dai_li_ip() #执行代理IP函数
    url = "https://www.baidu.com/"
    data = urllib.request.urlopen(url).read().decode("utf-8")
    print(data)
[/code]



**用户代理和ip代理结合应用**

[code]

     #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib
    from urllib import request
    import json
    import random
    def yh_dl():    #创建用户代理池
        yhdl = [
            'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
            'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0',
            'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0)',
            'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.6; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
            'Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
            'Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; en) Presto/2.8.131 Version/11.11',
            'Opera/9.80 (Windows NT 6.1; U; en) Presto/2.8.131 Version/11.11',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Maxthon 2.0)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; TencentTraveler 4.0)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; The World)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; 360SE)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Avant Browser)',
            'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)',
            'Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
            'User-Agent:Mozilla/5.0 (iPod; U; CPU iPhone OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
            'Mozilla/5.0 (iPad; U; CPU OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
            'Mozilla/5.0 (Linux; U; Android 2.3.7; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1',
            'Opera/9.80 (Android 2.3.4; Linux; Opera Mobi/build-1107180945; U; en-GB) Presto/2.8.149 Version/11.10',
            'Mozilla/5.0 (Linux; U; Android 3.0; en-us; Xoom Build/HRI39) AppleWebKit/534.13 (KHTML, like Gecko) Version/4.0 Safari/534.13',
            'Mozilla/5.0 (BlackBerry; U; BlackBerry 9800; en) AppleWebKit/534.1+ (KHTML, like Gecko) Version/6.0.0.337 Mobile Safari/534.1+',
            'Mozilla/5.0 (compatible; MSIE 9.0; Windows Phone OS 7.5; Trident/5.0; IEMobile/9.0; HTC; Titan)',
            'UCWEB7.0.2.37/28/999',
            'NOKIA5700/ UCWEB7.0.2.37/28/999',
            'Openwave/ UCWEB7.0.2.37/28/999',
            'Mozilla/4.0 (compatible; MSIE 6.0; ) Opera/UCWEB7.0.2.37/28/999'
            ]
        thisua = random.choice(yhdl)                    #随机获取代理信息
        headers = ("User-Agent",thisua)                 #拼接报头信息
        opener = urllib.request.build_opener()          #创建请求对象
        opener.addheaders=[headers]                     #添加报头到请求对象
        urllib.request.install_opener(opener)           #将报头信息设置为全局，urlopen()方法请求时也会自动添加报头
    
    def dai_li_ip():    #创建ip代理池
        url = "http://http-webapi.zhimaruanjian.com/getip?num=1&type=2&pro=&city=0&yys=0&port=11&time=1&ts=0&ys=0&cs=0&lb=1&sb=0&pb=4&mr=1"
        data = urllib.request.urlopen(url).read().decode("utf-8")
        data2 = json.loads(data)  # 将字符串还原它本来的数据类型
    
        print(data2['data'][0])
        ip = str(data2['data'][0]['ip'])
        dkou = str(data2['data'][0]['port'])
        zh_ip = ip + ':' + dkou
        print(zh_ip)
    
    
        proxy = urllib.request.ProxyHandler({"https": zh_ip})  # 格式化IP,注意，第一个参数，请求目标可能是http或者https,对应设置
        opener = urllib.request.build_opener(proxy, urllib.request.HTTPHandler)  # 初始化IP
        urllib.request.install_opener(opener)  # 将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP
    
    #请求
    dai_li_ip() #执行代理IP函数
    yh_dl()     #执行用户代理池函数
    
    gjci = '连衣裙'
    zh_gjci = gjc = urllib.request.quote(gjci)         #将关键词转码成浏览器认识的字符，默认网站不能是中文
    url = "https://s.taobao.com/search?q=%s&s=0" %(zh_gjci)
    # print(url)
    data = urllib.request.urlopen(url).read().decode("utf-8")
    print(data)
[/code]



**用户代理和ip代理结合应用封装模块**

[code]

     #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib
    from urllib import request
    import json
    import random
    import re
    import urllib.error
    def hq_html(hq_url):
        """
        hq_html()封装的爬虫函数，自动启用了用户代理和ip代理
        接收一个参数url,要爬取页面的url，返回html源码
        """
        def yh_dl():    #创建用户代理池
            yhdl = [
                'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
                'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0',
                'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0)',
                'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.6; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
                'Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
                'Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; en) Presto/2.8.131 Version/11.11',
                'Opera/9.80 (Windows NT 6.1; U; en) Presto/2.8.131 Version/11.11',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Maxthon 2.0)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; TencentTraveler 4.0)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; The World)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; 360SE)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Avant Browser)',
                'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)',
                'Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
                'User-Agent:Mozilla/5.0 (iPod; U; CPU iPhone OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
                'Mozilla/5.0 (iPad; U; CPU OS 4_3_3 like Mac OS X; en-us) AppleWebKit/533.17.9 (KHTML, like Gecko) Version/5.0.2 Mobile/8J2 Safari/6533.18.5',
                'Mozilla/5.0 (Linux; U; Android 2.3.7; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1',
                'Opera/9.80 (Android 2.3.4; Linux; Opera Mobi/build-1107180945; U; en-GB) Presto/2.8.149 Version/11.10',
                'Mozilla/5.0 (Linux; U; Android 3.0; en-us; Xoom Build/HRI39) AppleWebKit/534.13 (KHTML, like Gecko) Version/4.0 Safari/534.13',
                'Mozilla/5.0 (BlackBerry; U; BlackBerry 9800; en) AppleWebKit/534.1+ (KHTML, like Gecko) Version/6.0.0.337 Mobile Safari/534.1+',
                'Mozilla/5.0 (compatible; MSIE 9.0; Windows Phone OS 7.5; Trident/5.0; IEMobile/9.0; HTC; Titan)',
                'UCWEB7.0.2.37/28/999',
                'NOKIA5700/ UCWEB7.0.2.37/28/999',
                'Openwave/ UCWEB7.0.2.37/28/999',
                'Mozilla/4.0 (compatible; MSIE 6.0; ) Opera/UCWEB7.0.2.37/28/999'
                ]
            thisua = random.choice(yhdl)                    #随机获取代理信息
            headers = ("User-Agent",thisua)                 #拼接报头信息
            opener = urllib.request.build_opener()          #创建请求对象
            opener.addheaders=[headers]                     #添加报头到请求对象
            urllib.request.install_opener(opener)           #将报头信息设置为全局，urlopen()方法请求时也会自动添加报头
    
        def dai_li_ip(hq_url):    #创建ip代理池
            url = "http://http-webapi.zhimaruanjian.com/getip?num=1&type=2&pro=&city=0&yys=0&port=11&time=1&ts=0&ys=0&cs=0&lb=1&sb=0&pb=4&mr=1"
            if url:
                data = urllib.request.urlopen(url).read().decode("utf-8")
                data2 = json.loads(data)  # 将字符串还原它本来的数据类型
                # print(data2['data'][0])
                ip = str(data2['data'][0]['ip'])
                dkou = str(data2['data'][0]['port'])
                zh_ip = ip + ':' + dkou
                pat = "(\w*):\w*"
                rst = re.compile(pat).findall(hq_url)  #正则匹配获取是http协议还是https协议
                rst2 = rst[0]
                proxy = urllib.request.ProxyHandler({rst2: zh_ip})  # 格式化IP,注意，第一个参数，请求目标可能是http或者https,对应设置
                opener = urllib.request.build_opener(proxy, urllib.request.HTTPHandler)  # 初始化IP
                urllib.request.install_opener(opener)  # 将代理IP设置成全局,当使用urlopen()请求时自动使用代理IP
            else:
                pass
    
        #请求
        try:
            dai_li_ip(hq_url) #执行代理IP函数
            yh_dl()     #执行用户代理池函数
    
            data = urllib.request.urlopen(hq_url).read().decode("utf-8")
            return data
        except urllib.error.URLError as e:  # 如果出现错误
            if hasattr(e, "code"):  # 如果有错误代码
                # print(e.code)  # 打印错误代码
                pass
            if hasattr(e, "reason"):  # 如果有错误信息
                # print(e.reason)  # 打印错误信息
                pass
    
    # a = hq_html('http://www.baid.com/')
    # print(a)
[/code]



**模块使用**

[code]

     #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import urllib.request
    import fzhpach
    gjc = '广告录音'
    gjc = urllib.request.quote(gjc)                 #将关键词转码成浏览器认识的字符，默认网站不能是中文
    url = 'https://www.baidu.com/s?wd=%s&pn=0' %(gjc)
    a = fzhpach.hq_html(url)
    print(a)
[/code]



