
---
layout: post
title: " 第三百五十九节，Python分布式爬虫打造搜索引擎Scrapy精讲—elasticsearch(搜索引擎)介绍以及安装 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百五十九节，Python分布式爬虫打造搜索引擎Scrapy精讲—elasticsearch(搜索引擎)介绍以及安装**



****elasticsearch(搜索引擎)介绍****

ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的 **全文搜索引擎** ，基于RESTful
web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是第二最流行的企业搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便。

我们建立一个网站或应用程序，并要添加搜索功能，令我们受打击的是:搜索工作是很难的。我们希望我们的搜索解决方案要快，我们希望有一个零配置和一个完全免费的搜索模式，我们希望能够简单地使用JSON通过HTTP的索引数据，我们希望我们的搜索服务器始终可用，我们希望能够一台开始并扩展到数百，我们要实时搜索，我们要简单的多租户，我们希望建立一个云的解决方案。Elasticsearch旨在解决所有这些问题和更多的问题。

![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828115425140-54992369.png)



**全文搜索引擎种类**

**1、 ** **elasticsearch******

**2、solr**

**3、sphinx**





**关系数据搜素缺点，也就是直接通过数据库搜索**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828121035796-1117471293.png)**

**  elasticsearch(搜索引擎)都能弥补以上缺点**



**elasticsearch安装**

** 1、 **elasticsearch是由Java开发的，所以首先要安装Java环境****

**** 注意： ** **elasticsearch所需要的 ** **Java环境必须大于或者等于1.8版本************

****下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html****

****我们下载Windows x64版本，jdk-8u144-windows-x64.exe文件，直接安装****

****安装好后，我们cmd命令输入：java -version  查看 ** **java版本********

********![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828125104999-718753945.png)********





**2、elasticsearch **-rtf** 安装**

** 下载地址：https://github.com/medcl/elasticsearch-rtf    集成了我们很多插件**

**运行系统可用内存 >2G** ****

**以下是集成安装的官方插件，个别插件需要配置才能使用，可根据需要删除 plugins 目录无关的插件，重启 elasticsearch 生效。**

[code]

    **bin/elasticsearch-plugin install discovery-multicast
    bin/elasticsearch-plugin install analysis-icu
    bin/elasticsearch-plugin install analysis-kuromoji
    bin/elasticsearch-plugin install analysis-phonetic
    bin/elasticsearch-plugin install analysis-smartcn
    bin/elasticsearch-plugin install analysis-stempel
    bin/elasticsearch-plugin install analysis-ukrainian
    bin/elasticsearch-plugin install discovery-file
    bin/elasticsearch-plugin install ingest-attachment
    bin/elasticsearch-plugin install ingest-geoip
    bin/elasticsearch-plugin install ingest-user-agent
    bin/elasticsearch-plugin install mapper-attachments
    bin/elasticsearch-plugin install mapper-size
    bin/elasticsearch-plugin install mapper-murmur3
    bin/elasticsearch-plugin install lang-javascript
    bin/elasticsearch-plugin install lang-python
    bin/elasticsearch-plugin install repository-hdfs
    bin/elasticsearch-plugin install repository-s3
    bin/elasticsearch-plugin install repository-azure
    bin/elasticsearch-plugin install repository-gcs
    bin/elasticsearch-plugin install store-smb
    bin/elasticsearch-plugin install discovery-ec2
    bin/elasticsearch-plugin install discovery-azure-classic
    bin/elasticsearch-plugin install discovery-gce**
[/code]

**  elasticsearch-rtf下载好解压后将文件夹复制到一个目录会得到以下文件**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828134229796-45967026.png)**

**双击进入bin文件夹里，按shlft+鼠标右键，在此处打开命令窗口，输入  elasticsearch.bat  回车运行**

**然后在浏览器输入http://127.0.0.1:9200/ 返回数据说明成功**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828135752312-1254891255.png)**





**3、安装 elasticsearch-rtf(搜索引擎)的可视化管理工具elasticsearch-head**

**注意： **(搜索引擎)的可视化管理工具elasticsearch-head，的安装要用到node.js的npm 插件管理器****

****所以要先安装 ** **node.js的npm 插件管理器********

****下载地址：https://nodejs.org/en/download/****

****我们下载windows版本即可，下载后安装即可****

****安装后cdm命令：npm      如下显示表示安装成功****

****![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828145639249-1165286909.png)****



****npm命令是 ** **node.js的npm 插件管理器，也就是下载插件安装插件的管理器，因为下载都是国外服务器很慢会掉线，我们需要使用淘宝的
** ** ** **npm镜像cnpm****************

****************执行命令： npm install -g cnpm
--registry=https://registry.npm.taobao.org   启用 ** ** ** **淘宝的 ** ** **
**npm镜像cnpm，注意：启用后当我们要输入 ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**npm命令时，就需要输入 ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**cnpm************************************************************************************************





**************(搜索引擎)的可视化管理工具elasticsearch-head的安装******

**下载地址：https://github.com/mobz/elasticsearch-head**

**下载后解压到指定目录，会得到以下文件**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828150039937-35946603.png)**

  **cd进入到解压的elasticsearch-head目录**

**执行命令：cnpm install   安装 **elasticsearch-head的依赖包****

****在执行命令：cnpm run start  启动 ** **elasticsearch-head ** **
**(搜索引擎)的可视化管理工具**************

********访问：<http://localhost:9100/>********

********访问后可以看到 ** ** ** ** ** ** **(搜索引擎)的可视化管理工具**********************

********![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828152914921-728440838.png)********



**我们看到显示未连接，我们需要配置 **elasticsearch-rtf(搜索引擎)** ** ** ** ** ** ** **连接，在
elasticsearch-rtf/config/elasticsearch.yml 这个文件里配置****************

****************在文件的最后面写入****************

[code]

     http.cors.enabled: true
    http.cors.allow-origin: "*"
    http.cors.allow-methods: OPTIONS, HEAD, GET, POST, PUT, DELETE
[/code]



**  重启elasticsearch-rtf(搜索引擎)后就可以连接了**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828173352577-996845305.png)**





**  安装Kibana 5.1.2版本**

** 注意： **Kibana的版本要对应 **elasticsearch-head里信息里的版本******

******![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828175434687-1506566569.png)******

  **下载地址：https://www.elastic.co/downloads/past-releases/kibana-5-1-2**

**我们下载windows版即可**

**将下载文件解压到指定目录，进入 kibana-5.1.2/bin文件夹**

**![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828182127343-83868257.png)**

**cd 进入 **kibana-5.1.2/bin 文件夹****

****执行命令：kibana.bat      运行 ** **kibana-5.1.2********

********![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828182446187-1401079506.png)********

********浏览器访问： http://localhost:5601  如下显示说明成功********

********![](https://images2017.cnblogs.com/blog/955761/201708/955761-20170828182932827-1047781150.png)********







** **

