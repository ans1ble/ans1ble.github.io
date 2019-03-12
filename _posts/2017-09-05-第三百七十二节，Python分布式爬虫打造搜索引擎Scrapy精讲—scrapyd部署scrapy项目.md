
---
layout: post
title: " 第三百七十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—scrapyd部署scrapy项目 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十二节，Python分布式爬虫打造搜索引擎Scrapy精讲—scrapyd部署scrapy项目**



****scrapyd模块是专门用于部署 **scrapy项目的，可以部署和管理 ** ** **scrapy项目************

******下载地址：https://github.com/scrapy/scrapyd******

******建议安装******

[code]

    pip3 install scrapyd
[/code]

******首先安装 ** **scrapyd模块，安装后在
Python的安装目录下的Scripts文件夹里会生成scrapyd.exe启动文件，如果这个文件存在说明安装成功，我们就可以执行命令了**********

**********启动 ** ** ** ** **scrapyd服务********************

[code]

    在命令输入：scrapyd  
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170905235344569-1402976283.png)

**********如图说明启动成功，关闭或者退出命令窗口， 因为我们正真的使用是在指定的启动目录下启动服务的**********



**指定 **启动** 服务目录 ** **后**** **启动服务****

**重新打开命令， cd进入要指定服务的目录后，执行命令scrapyd启动服务**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906001602288-406819736.png)**

**此时可以看到启动目录里生成了dbs目录**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906001719663-1485332134.png)**



****dbs目录里是空的什么都没有****





****此时我们需要安装scrapyd-client模块****

********scrapyd-client模块是专门打包 ** **scrapy爬虫项目到 ** ** ** ** ** ** ** ** **
**scrapyd服务中的********************************

****下载目录：https://github.com/scrapy/scrapyd-client****

****建议安装****

[code]

    pip3 install scrapyd-client
[/code]

****安装后在Python的安装目录下的 Scripts文件夹里会生成scrapyd-deploy无后缀文件，如果有此文件说明安装成功****

****重点说明：这个 ** **scrapyd-deploy
无后缀文件是启动文件，在Linux系统下可以远行，在windows下是不能远行的，所以我们需要编辑一下使其在 ** ** **
**windows可以远行****************

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906193530163-344059436.png)

**在此目录里新建一个 scrapyd-deploy.bat文件，注意名称一定要和 ** **scrapyd-deploy相同，我们编辑这个bat文件 **
** ** **使其在 ** ** ** **windows可以远行**********************

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906194350304-948537913.png)



**scrapyd-deploy.bat文件编辑**

设置python执行文件路径和scrapyd-deploy无后缀文件路径

[code]

    @echo off
    "C:\Users\admin\AppData\Local\Programs\Python\Python35\python.exe" "C:\Users\admin\AppData\Local\Programs\Python\Python35\Scripts\scrapyd-deploy" %1 %2 %3 %4 %5 %6 %7 %8 %9
[/code]



**scrapyd-deploy.bat文件编辑好后，打开命令窗口cd 到 **scrapy项目中 有scrapy.cfg文件的目录，然后执行
**scrapyd-deploy 命令，看看我们编辑的 **scrapyd-deploy.bat 文件是否可以执行********

****如果下图表示可以执行****

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906203315757-465062445.png)



**设置scrapy项目中的scrapy.cfg文件，这个文件就是给 ** ** ** **scrapyd-deploy使用的**********

  **scrapy.cfg文件**

**注意：下面的中文备注不能写在里面，不然会报错，这写的备注只是方便知道怎么设置**

[code]

     # Automatically created by: scrapy startproject
    #
    # For more information about the [deploy] section see:
    # https://scrapyd.readthedocs.org/en/latest/deploy.html
    
    [settings]
    default = adc.settings
    
    [deploy:bobby]                      #设置部署名称bobby
    url = http://localhost:6800/        #开启url
    project = adc                       #项目名称
[/code]

**命令窗口输入：scrapyd-deploy -l     启动服务，可以看到我们设置的部署名称**

****
![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906204530710-768438109.png)****

**** ****

****开始打包前，执行一个命令： scrapy list   ，这个命令执行成功说明可以打包了，如果没执行成功说明还有工作没完成****

********注意执行   ** **scrapy list  命令的时候很有可能出现错误，如果是 ** **python无法找到 ** ** ** **
** ** ** **scrapy项目，需要在 ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**scrapy项目里的settings.py配置文件里设置成python可识别路径****************************************************************

[code]

     # 将当前项目的一级目录adc目录添加到python可以识别目录中
    BASE_DIR = os.path.dirname(os.path.abspath(os.path.dirname(__file__)))
    sys.path.insert(0, os.path.join(BASE_DIR, 'adc'))
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906222653085-325111114.png)

**如果错误提示，什么远程计算机拒绝，说明你的 ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**scrapy项目有链接远程计算机，如链接数据库或者elasticsearch(搜索引擎)之类的，需要先将链接服务器启动**********************************

  ** ** ** **执行   ** **scrapy list  命令返回了爬虫名称说明一切ok了，如下图************

************![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170906223321882-1731244839.png)************



********到此我们就可以开始打包 **scrapy项目到 **scrapyd了，用命令结合
**scrapy项目中的scrapy.cfg文件设置来打包**************

****************************scrapy.cfg文件****************************

[code]

     # Automatically created by: scrapy startproject
    #
    # For more information about the [deploy] section see:
    # https://scrapyd.readthedocs.org/en/latest/deploy.html
    
    [settings]
    default = adc.settings
    
    [deploy:bobby]                      #设置部署名称bobby
    url = http://localhost:6800/        #开启url
    project = adc                       #项目名称
[/code]

**执行打包命令：  scrapyd-deploy 部署名称 -p 项目名称**

**如：scrapyd-deploy bobby -p adc**

**如下显示表示 **scrapy项目打包成功****

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907182640476-1712934607.png)**



****scrapy项目打包成功后说明****

******scrapy项目打包成功后会在 **scrapyd启动服务的目录生成相应的文件，如下：********

********1、会在 **scrapyd 启动服务的目录下的dbs文件夹生成 **scrapy项目名称.db************

****![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907183643101-421660620.png)****

**2、会在 scrapyd启动服务的目录下的eggs文件夹生成 ** ** ** ** **scrapy项目名称的文件夹 ，里面是一个
**scrapyd-deploy打包生成的名称.egg**************

****![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907184407741-1629609170.png)****



**3、会将 **scrapy爬虫项目打包 ，在 ** **scrapy项目里 会生成两个文件夹，build文件夹和project.egg-
info文件夹********

****************build文件夹里是打包后的爬虫项目， **scrapyd以后远行的就是这个打包后的项目******************

**************************project.egg-
info文件夹里是打包时的一些配置**************************

**************************说明： **scrapyd-deploy 只负责将 **scrapy爬虫项目打包给
**scrapyd部署 ，只需要打包一次，打包后，以后的启动爬虫，停止爬虫等 **scrapy项目管理由
**scrapyd来完成************************************



****************************************scrapyd ** ** ** ** ** ** ** ** ** **
** ** ** ** ** **管理 ** ** ** ** ** ** ** ** ** ** ** ** ** ** **
**scrapy项目********************************************************************************************************

********************************************************************************************************注意：
** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** ** **scrapyd ** ** ** **
** ** ** ** ** ** ** ** ** ** ** **管理用的  curl
命令，curl命令不支持windows系统，只支持Linux系统，所以在 **windows系统下我们用
cmder来执行命令**********************************************************************************************************************************************************************************



********1、远行爬虫，远行指定 **scrapy下面的指定爬虫**********

[code]

    curl http://localhost:6800/schedule.json -d project= scrapy项目名称 -d spider=爬虫名称
    如：
    curl http://localhost:6800/schedule.json -d project=adc -d spider=lagou
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907192832460-309819801.png)

********![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907194434882-1819820825.png)********



****************2、停止爬虫****************

[code]

    curl http://localhost:6800/cancel.json -d project= scrapy项目名称 -d job=远行ID
    如：
    curl http://localhost:6800/cancel.json -d project=adc -d job=5454948c93bf11e7af0040167eb10a7b
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907195339647-1850485079.png)

********![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907195410476-1973483969.png)********



********3、删除scrapy项目********

********注意：一般删除 **scrapy项目，需要先执行命令停止项目下在远行的爬虫**********

**********删除项目后会删除 **scrapyd启动服务的目录下的eggs文件夹生成egg文件，需要重新用 **scrapyd-
deploy打包后才能再次运行**************

[code]

    curl http://localhost:6800/delproject.json -d project= scrapy项目名称
    如果：
    curl http://localhost:6800/delproject.json -d project=adc
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907200352319-1076917567.png)



**4、查看有多少个scrapy项目在api中**

[code]

    curl http://localhost:6800/listprojects.json
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907203840194-977118711.png)



****5、查看指定的scrapy项目中有多少个爬虫****

[code]

    curl http://localhost:6800/listspiders.json?project= scrapy项目名称
    如：
    curl http://localhost:6800/listspiders.json?project=adc
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170907204324226-1076300126.png)



### scrapyd支持的API 介绍

 scrapyd支持一系列api，下面用一个py文件来介绍

[code]

    # -*- coding: utf-8 -*-
    
    import requests
    import json 
    
    baseUrl ='http://127.0.0.1:6800/'
    daemUrl ='http://127.0.0.1:6800/daemonstatus.json'
    listproUrl ='http://127.0.0.1:6800/listprojects.json'
    listspdUrl ='http://127.0.0.1:6800/listspiders.json?project=%s'
    listspdvUrl= 'http://127.0.0.1:6800/listversions.json?project=%s'
    listjobUrl ='http://127.0.0.1:6800/listjobs.json?project=%s'
    delspdvUrl= 'http://127.0.0.1:6800/delversion.json'
    
    #http://127.0.0.1:6800/daemonstatus.json
    #查看scrapyd服务器运行状态
    r= requests.get(daemUrl)
    print '1.stats :\n %s \n\n'  %r.text  
    
    #http://127.0.0.1:6800/listprojects.json
    #获取scrapyd服务器上已经发布的工程列表
    r= requests.get(listproUrl)
    print '1.1.listprojects : [%s]\n\n'  %r.text
    if len(json.loads(r.text)["projects"])>0 :
        project = json.loads(r.text)["projects"][0]
    
    #http://127.0.0.1:6800/listspiders.json?project=myproject
    #获取scrapyd服务器上名为myproject的工程下的爬虫清单
    listspd=listspd % project
    r= requests.get(listspdUrl)
    print '2.listspiders : [%s]\n\n'  %r.text 
    if json.loads(r.text).has_key("spiders")>0 :
        spider =json.loads(r.text)["spiders"][0]
    
    
    #http://127.0.0.1:6800/listversions.json?project=myproject
    ##获取scrapyd服务器上名为myproject的工程下的各爬虫的版本
    listspdvUrl=listspdvUrl % project
    r = requests.get(listspdvUrl)
    print '3.listversions : [%s]\n\n'  %rtext 
    if len(json.loads(r.text)["versions"])>0 :
        version = json.loads(r.text)["versions"][0]
    
    #http://127.0.0.1:6800/listjobs.json?project=myproject
    #获取scrapyd服务器上的所有任务清单，包括已结束，正在运行的，准备启动的。
    listjobUrl=listjobUrl % proName
    r=requests.get(listjobUrl)
    print '4.listjobs : [%s]\n\n'  %r.text 
    
    
    #schedule.json
    #http://127.0.0.1:6800/schedule.json -d project=myproject -d spider=myspider
    #启动scrapyd服务器上myproject工程下的myspider爬虫，使myspider立刻开始运行，注意必须以post方式
    schUrl = baseurl + 'schedule.json'
    dictdata ={ "project":project,"spider":spider}
    r= reqeusts.post(schUrl, json= dictdata)
    print '5.1.delversion : [%s]\n\n'  %r.text 
    
    
    #http://127.0.0.1:6800/delversion.json -d project=myproject -d version=r99'
    #删除scrapyd服务器上myproject的工程下的版本名为version的爬虫，注意必须以post方式
    delverUrl = baseurl + 'delversion.json'
    dictdata={"project":project ,"version": version }
    r= reqeusts.post(delverUrl, json= dictdata)
    print '6.1.delversion : [%s]\n\n'  %r.text 
    
    #http://127.0.0.1:6800/delproject.json -d project=myproject
    #删除scrapyd服务器上myproject工程，注意该命令会自动删除该工程下所有的spider，注意必须以post方式
    delProUrl = baseurl + 'delproject.json'
    dictdata={"project":project  }
    r= reqeusts.post(delverUrl, json= dictdata)
    print '6.2.delproject : [%s]\n\n'  %r.text 
[/code]



### 总结一下：

1、获取状态  

http://127.0.0.1:6800/daemonstatus.json

2、获取项目列表  
http://127.0.0.1:6800/listprojects.json

3、获取项目下已发布的爬虫列表  

http://127.0.0.1:6800/listspiders.json?project=myproject

4、获取项目下已发布的爬虫版本列表  

http://127.0.0.1:6800/listversions.json?project=myproject

5、获取爬虫运行状态  

http://127.0.0.1:6800/listjobs.json?project=myproject  
 6、启动服务器上某一爬虫（必须是已发布到服务器的爬虫）  
http://localhost:6800/schedule.json
（post方式，data={"project":myproject,"spider":myspider}）

7、删除某一版本爬虫  

http://127.0.0.1:6800/delversion.json
（post方式，data={"project":myproject,"version":myversion}）

8、删除某一工程，包括该工程下的各版本爬虫

  

http://127.0.0.1:6800/delproject.json（post方式，data={"project":myproject}）



 到此，基于scrapyd的爬虫发布教程就写完了。

可能有人会说，我直接用scrapy cwal 命令也可以执行爬虫，个人理解用scrapyd服务器管理爬虫，至少有以下几个优势：

1、可以避免爬虫源码被看到。

2、有版本控制。

3、可以远程启动、停止、删除，正是因为这一点，所以scrapyd也是分布式爬虫的解决方案之一。

