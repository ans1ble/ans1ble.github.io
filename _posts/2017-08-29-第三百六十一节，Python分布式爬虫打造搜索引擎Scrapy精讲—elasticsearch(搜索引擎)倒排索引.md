
---
layout: post
title: " 第三百六十一节，Python分布式爬虫打造搜索引擎Scrapy精讲—elasticsearch(搜索引擎)倒排索引 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百六十一节，Python分布式爬虫打造搜索引擎Scrapy精讲— **elasticsearch(搜索引擎)** 倒排索引**



**倒排索引**

**倒排索引源于实际应用中需要根据属性的值来查找记录。这种索引表中的每一项都包括一个属性值和具有该属性值的各记录的地址。由于不是由记录来确定属性值，而是由属性值来确定记录的位置，因而称为倒排索引(inverted
index)。带有倒排索引的文件我们称为倒排索引文件，简称倒排文件(inverted file)。**





**倒排索引原理**

**就是将一句话进行分词并记录分词所存在的文章，当用户搜索词时可以直接查找到当前词所存在的文章**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170829190633624-647857318.png)**







**倒排索引分词权重记录(词瓶)**

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170829192416062-1717824951.png)

**  分词权重记录，是通过(TF-IDF)来实现的，详情https://baike.so.com/doc/433640-459181.html**





**倒排索引待解决的问题**

**这些问题elasticsearch(搜索引擎)已经解决**

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170829193359046-144498846.png)



