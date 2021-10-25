---
layout: post
title: " 第三百三十六节，web爬虫讲解2—urllib库中使用xpath表达式—BeautifulSoup基础 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百三十六节，web爬虫讲解2—urllib库中使用xpath表达式—BeautifulSoup基础**



**在urllib中，我们一样可以使用xpath表达式进行信息提取，此时，你需要首先安装lxml模块，然后将网页数据通过lxml下的etree转化为treedata的形式**



**urllib库中使用xpath表达式**

**etree.HTML() 将获取到的html字符串，转换成树形结构，也就是xpath表达式可以获取的格式**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import urllib.request
    from lxml import etree  #导入html树形结构转换模块
    
    wye = urllib.request.urlopen('http://sh.qihoo.com/pc/home').read().decode("utf-8",'ignore')
    zhuanh = etree.HTML(wye)  #将获取到的html字符串，转换成树形结构，也就是xpath表达式可以获取的格式
    print(zhuanh)
    hqq = zhuanh.xpath('/html/head/title/text()') #通过xpath表达式获取标题
    
    #注意，xpath表达式获取到数据，有时候是列表，有时候不是列表所以要做如下处理
    if str(type(hqq)) == "<class 'list'>":  #判断获取到的是否是列表
        print(hqq)
    else:
        xh_hqq = [i for i in hqq]       #如果不是列表，循环数据组合成列表
        print(xh_hqq)
    
    
    #返回 ：['【今日爆点】你的专属资讯平台']
[/code]





**BeautifulSoup基础  
**

****BeautifulSoup是获取thml元素的模块****

**BeautifulSoup-3.2.1版本**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170801212137349-637858141.png)**



