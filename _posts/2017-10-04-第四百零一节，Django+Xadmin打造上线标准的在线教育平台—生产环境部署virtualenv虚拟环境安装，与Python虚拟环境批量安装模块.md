
---
layout: post
title: " 第四百零一节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署virtualenv虚拟环境安装，与Python虚拟环境批量安装模块 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第四百零一节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署virtualenv虚拟环境安装，与Python虚拟环境批量安装模块**



****virtualenv简介****

****![](https://images2017.cnblogs.com/blog/955761/201710/955761-20171004183901974-551509189.png)****







**1.安装virtualenv**

[code]

    [root@192 huan_jing] # pip3 install virtualenv
    Collecting virtualenv
      Downloading virtualenv-15.1.0-py2.py3-none-any.whl (1.8MB)
        100% |████████████████████████████████| 1.8MB 61kB/s 
    Installing collected packages: virtualenv
    Successfully installed virtualenv-15.1.0
    You are using pip version 7.1.2, however version 9.0.1 is available.
    You should consider upgrading via the 'pip install --upgrade pip' command.
    [root@192 huan_jing]# 
[/code]





**2.安装virtualenvwrapper**

****virtualenvwrapper是 **virtualenv的一个方便管理虚拟环境的管理器******

[code]

    pip3 install virtualenvwrapper
[/code]



**3.安装好virtualenvwrapper后编辑vim ~/.bashrc文件，这步很重要，不设置会导致下面的命令不可用**

[code]

    vim ~/.bashrc
[/code]

在文件加入

[code]

    export WORKON_HOME=/usr/xu_ni_huan_jing　　　　　　存放虚拟环境的目录
    source /usr/local/bin/virtualenvwrapper.sh　　　　指定virtualenvwrapper.sh文件路径
[/code]

使刚才修改的文件失效

[code]

    [root@192 xu_ni_huan_jing]# source ~/.bashrc
[/code]



**4.创建虚拟环境，创建后会自动进入虚拟环境**

**mkvirtualenv 虚拟环境名称**

[code]

    [root@192 xu_ni_huan_jing] # mkvirtualenv jxiou
    Using base prefix '/usr/local'
    New python executable in /usr/xu_ni_huan_jing/jxiou/bin/python3.5
    Also creating executable in /usr/xu_ni_huan_jing/jxiou/bin/python
    Installing setuptools, pip, wheel...done.
    virtualenvwrapper.user_scripts creating /usr/xu_ni_huan_jing/jxiou/bin/predeactivate
    virtualenvwrapper.user_scripts creating /usr/xu_ni_huan_jing/jxiou/bin/postdeactivate
    virtualenvwrapper.user_scripts creating /usr/xu_ni_huan_jing/jxiou/bin/preactivate
    virtualenvwrapper.user_scripts creating /usr/xu_ni_huan_jing/jxiou/bin/postactivate
    virtualenvwrapper.user_scripts creating /usr/xu_ni_huan_jing/jxiou/bin/get_env_details
    (jxiou) [root@192 xu_ni_huan_jing]# 
[/code]





**5.退出虚拟环境**

**deactivate**

[code]

    (jxiou) [root@192 xu_ni_huan_jing] # deactivate
    [root@192 xu_ni_huan_jing]# 
[/code]



**6.查看有哪些虚拟环境**

**workon**

[code]

    [root@192 /] # workon
    jxiou2
    jxiou
    [root@192 /]# 
[/code]



**7.进入一个指定的虚拟环境**

**workon jxiou(虚拟环境名称)**

[code]

    [root@192 /] # workon jxiou
    (jxiou) [root@192 /]#
[/code]



**8.在虚拟环境安装开发包**

**首先要进入虚拟环境**

[code]

    (jxiou) [root@192 /] # pip install requests
    Collecting requests
      Downloading requests-2.18.4-py2.py3-none-any.whl (88kB)
        100% |████████████████████████████████| 92kB 160kB/s 
    Collecting certifi>=2017.4.17 (from requests)
      Downloading certifi-2017.7.27.1-py2.py3-none-any.whl (349kB)
        100% |████████████████████████████████| 358kB 38kB/s 
    Collecting urllib3<1.23,>=1.21.1 (from requests)
      Downloading urllib3-1.22-py2.py3-none-any.whl (132kB)
        100% |████████████████████████████████| 133kB 23kB/s 
    Collecting idna<2.7,>=2.5 (from requests)
      Downloading idna-2.6-py2.py3-none-any.whl (56kB)
        100% |████████████████████████████████| 61kB 15kB/s 
    Collecting chardet<3.1.0,>=3.0.2 (from requests)
      Downloading chardet-3.0.4-py2.py3-none-any.whl (133kB)
        100% |████████████████████████████████| 143kB 24kB/s 
    Installing collected packages: certifi, urllib3, idna, chardet, requests
    Successfully installed certifi-2017.7.27.1 chardet-3.0.4 idna-2.6 requests-2.18.4 urllib3-1.22
    (jxiou) [root@192 /]# 
[/code]





**虚拟环境批量安装开发模块**

**1.首先在开发系统里cd进入一个目录，执行  pip freeze > chuaj.txt
命令，将开发环境里用到的第三方模块以txt文件方式导出模块安装文件**

**2.在生产环境里进入虚拟环境，将开发环境里导出的 **txt文件放到生产虚拟环境里，执行命令 pip install -r
/usr/xu_ni_huan_jing/jxiou/chuaj.txt  批量安装模块****

****如果遇到安装慢的可以ctrl+c停止安装，单独用加速镜像安装源，安装****



