
---
layout: post
title: " 第四百节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署CentOS6.5安装python3.5.1 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第四百节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署CentOS6.5安装python3.5.1**



**1.检查系统是否安装了python**

[code]

    [root@192 ~] # rpm -qa python
    python-2.6.6-51.el6.x86_64
    [root@192 ~]# 
[/code]

**可以看到CentOS6.5系统默认安装了python2.6.6**



**2.检查一下Python安装在什么地方**

[code]

    [root@192 ~] # whereis python
    python: /usr/bin/python /usr/bin/python2.6 /usr/lib/python2.6 /usr/lib64/python2.6 /usr/include/python2.6 /usr/share/man/man1/python.1.gz
    [root@192 ~]#
[/code]

**可以看到Python启动文件在/usr/bin/python2.6里，有一个快速软连接在/usr/bin/python，那么我们就要安指定其他目录安装，防止默认安装到2.6.6的路径起冲突，
**2.6.6不能卸载掉，因为系统的yum命令是依赖Python2.6.6的****



**3.安装依赖库和编译器**

[code]

     # yum install gcc -y
    # yum install openssl-devel
[/code]

**如果没有安装openssl-devel，在安装过程中pip无法安装**



**4.下载对应版本的Python，并解压**

[code]

    wget https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tgz    下载python
    
     tar -xvf Python-3.5.1.tgz　　　　　　　　　　　　　　　　　　　　解压Python
[/code]



**5.进入Python解压目录，编译安装Python3.5.1**

[code]

    cd Python-3.5.1
[/code]

[code]

    ./configure --prefix=/usr/local 　　　　指定编译安装的目录
[/code]

[code]

    make && make install　　　　　　　　　　　　　　　　编译并且安装到指定目录
[/code]





**6.检查一下Python3.5安装的详情**

[code]

    [root@192 Python-3.5.1] # whereis python
    python: /usr/bin/python /usr/bin/python2.6 /usr/lib/python2.6 /usr/lib64/python2.6 /usr/local/bin/python3.5-config /usr/local/bin/python3.5m /usr/local/bin/python3.5m-config /usr/local/bin/python3.5 /usr/local/lib/python3.5 /usr/include/python2.6 /usr/share/man/man1/python.1.gz
[/code]

**可以看到Python3.5.1已经安装成功**





**7.将系统默认的python启动文件修改成别的名字**

**修改/usr/bin下的Python文件名字**

![](https://images2017.cnblogs.com/blog/955761/201710/955761-20171004150235661-32518584.png)





**8.将Python3.5.1安装目录下的Python3.5启动文件创建软连到，Python默认的启动目录**

[code]

    ln -s /usr/local/bin/python3.5 /usr/bin/python   创建Python3.5软连接到/usr/bin/目录，名字叫Python
[/code]

![](https://images2017.cnblogs.com/blog/955761/201710/955761-20171004151041708-1916846550.png)





**9.这样以后输入Python回车后就是执行的Python3.5.1的版本**

[code]

    [root@192 /] # python
    Python 3.5.1 (default, Oct  3 2017, 03:19:49) 
    [GCC 4.4.7 20120313 (Red Hat 4.4.7-18)] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> 
[/code]



**10.在安装python3.5.1时自动安装了pip3,测试一下pip3是否可用**

[code]

    [root@192 /] # pip3 list
    pip (7.1.2)
    setuptools (18.2)
    You are using pip version 7.1.2, however version 9.0.1 is available.
    You should consider upgrading via the 'pip install --upgrade pip' command.
    [root@192 /]# 
[/code]

**可以看到pip3能用**



**11.修改/usr/bin/yum文件**

**因为 **yum命令默认使用的Python文件名称调用的Python2.6.6，我们将Python软连接了python3.5.1所以现在
**yum命令不可以用了，我们要改一下 ** ** **yum配置文件，让它用回python2.6.6版本************

[code]

    vim /usr/bin/ yum  
    将第一行中的“#!/usr/bin/python”
    修改为“#!/usr/bin/python-2.6”，保存即可
[/code]

![](https://images2017.cnblogs.com/blog/955761/201710/955761-20171004180901818-929667522.png)

**测试**

[code]

    [root@192 /] # yum
    Loaded plugins: fastestmirror, refresh-packagekit, security
    You need to give some command
    Usage: yum [options] COMMAND
[/code]

**安装完成**



