
---
layout: post
title: " 第四十二节，configparser特定格式的ini配置文件模块 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


configparser用于处理特定格式的文件，其本质上是利用open来操作文件。

特定格式的ini配置文件模块，用于处理ini配置文件，注意：这个ini配置文件，只是ini文件名称的文本文件，不是后缀为.ini的文件，也就是ini文件，不是ini.ini文件

**ini配置文件格式**

**每个标签称之为节点**

[code]

     # 注释1
    ;  注释2
     
    [section1] # 节点
    k1 = v1    # 第一种键值对
    k2:v2       # 第二种键值对
     
    [section2] # 第一种键值对
    k1 = v1    # 第二种键值对
[/code]



**ConfigParser()模块函数**

**功能：创建ConfigParser对象，对象用来操作文件【无参】**

**使用方法：模块名称. **ConfigParser()** **  
****

**格式如：config = configparser.ConfigParser()**

**read()模块函数**

**功能：打开文件【有参】**

**使用方法：对象变量. **read("文件路径文件名称",encoding='字符编码')** **  
****

**格式如：config.read("ini", encoding='utf-8')**

**sections()模块函数**

**功能： **获取对象里的所有节点名称，以列表形式返回，列表里的元素就是节点名称【有参】****

**使用方法：对象变量. **sections()** **  
****

**格式如：ret = config.sections()**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    ret = config.sections() #获取对象里的节点名称，以列表形式返回，列表里的元素就是节点名称
    print(ret)
    # 输出
    # ['section1', 'section2']
[/code]



**items()模块函数**

**功能：获取指定节点下所有的键值对,返回的一个列表，列表里的元素是元祖，每个元祖的元素是键值对【有参】 **  
****

**使用方法：对象变量. **items("要获取的节点名称")** **  
****

**格式如：ret = config.items("section2")**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    ret = config.items("section2") #获取指定节点下所有的键值对,返回的一个列表，列表里的元素是元祖，每个元祖的元素是键值对
    print(ret)
    # 输出
    # [('k1', 'v1'), ('k2', 'v2')]
[/code]



**options()模块函数**

**功能：获取指定节点下所有的建，返回列表，列表里的元素是指定节点下所有的建【有参】 **  
****

**使用方法：对象变量. **options("要获取的节点名称")** **  
****

**格式如：ret = config.options("section2")**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    ret = config.options("section2") #获取指定节点下所有的建，返回列表，列表里的元素是指定节点下所有的建
    print(ret)
    # 输出
    # ['k1', 'k2']
[/code]



**get()模块函数**

**功能：获取指定节点下指定key的值,返回对应字符串【有参】 **  
****

**使用方法：对象变量. **get("要获取的节点名称","要获取的key键名称")** **  
****

**格式如：ret = config.get("section2","k2")**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    ret = config.get("section2","k2") #获取指定节点下指定key的值,返回对应字符串
    print(ret)
    # 输出
    # v2
[/code]



**has_section()模块函数**

**功能：检查指定的节点是否存在，存在返回True，不存在返回False【有参】 **  
****

**使用方法：对象变量. **has_section("要检查的节点名称")** **  
****

**格式如：ret = config.has_section("section2")**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    ret = config.has_section("section2") #检查指定的节点是否存在，存在返回True，不存在返回False
    print(ret)
    # 输出
    # True
[/code]



**add_section()模块函数**

**功能：在文件里追加节点【有参】 **  
****

**使用方法：对象变量. **add_section("要追加的节点名称")** **  
****

**格式如：config.add_section("section5")**

**write()模块函数**

**功能：文件对象改变后将对象重新写入文件【有参】参数是打开要写入的文件 **  
****

**注意：对文件的，增，删，改，操作后都要用 **write()写入一下文件保存****

**使用方法：对象变量. **write(open("文件路径或名称","文件打开方式",encoding='字符编码'))** **  
****

**格式如：config.write(open("ini","w",encoding='utf-8'))**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    config.add_section("section5") #在文件里追加节点
    config.write(open("ini","w",encoding='utf-8')) #文件对象改变后将对象重新写入文件
[/code]



**remove_section()模块函数**

**功能：删除指定的节点【有参】 **  
****

**使用方法：对象变量. **remove_section("要删除的节点名称")** **  
****

**格式如：config.remove_section("section3")**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    config.remove_section("section3") #删除指定的节点
    config.write(open("ini","w",encoding='utf-8')) #文件对象改变后将对象重新写入文件
[/code]



**has_option()模块函数  **

**功能：检查指定节点下面的指定键是否存在，存在返回True，不存在返回False【有参】 **  
****

**使用方法：对象变量. **has_option("要检查节点名称","键名称")** **  
****

**格式如：sf = config.has_option("section2","k2")**

[code]

     # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    sf = config.has_option("section2","k2") #检查指定节点下面的指定键是否存在，存在返回True，不存在返回False
    print(sf)
    # 输出
    # True
[/code]



**remove_option()模块函数**

**功能：删除指定节点下的指定键值对 **  
****

**使用方法：对象变量. **remove_option("指定节点名称","节点下要删除的键名称")** **  
****

**格式如：config.remove_option("section2","k1")**

[code]

     # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    config.remove_option("section2","k1") #删除指定节点下的键值对
    config.write(open("ini","w",encoding='utf-8')) #文件对象改变后将对象重新写入文件
[/code]



**set()模块函数**

**功能：设置指定节点下的指定键值对 **  
****

**使用方法：对象变量. **set("指定节点","键名称","值")** **  
****

**格式如：config.set("section2","k1","v1")**

**说明**

**根据键来判断如果键不存则创建定义的键值对**

**如果存在则更改成定义的值**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("ini", encoding='utf-8') #以utf-8的编码打开ini文件
    config.set("section2","k1","v1") #设置指定节点下的指定键值对
    config.write(open("ini","w",encoding='utf-8')) #文件对象改变后将对象重新写入文件
[/code]



**创建一个配置文件**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import configparser #导入configparser模块
    wjian = open("des","a",encoding='utf-8') #以a模式创建打开des文件
    wjian.close() #关闭打开的文件
    """上面的open只用于创建des文件"""
    
    config = configparser.ConfigParser() #创建ConfigParser对象
    config.read("des", encoding='utf-8') #以utf-8的编码打开des文件
    config.add_section("section1")  #追加指定节点
    config.set("section1","k1","v1") #指定节点下设置键值对
    config.set("section1","k2","v2") #指定节点下设置键值对
    config.set("section1","k3","v3") #指定节点下设置键值对
    
    config.add_section("section2") #追加指定节点
    config.set("section2","a1","s1") #指定节点下设置键值对
    config.set("section2","a2","s2") #指定节点下设置键值对
    config.set("section2","a3","s3") #指定节点下设置键值对
    
    config.add_section("section3") #追加指定节点
    config.set("section3","f1","k1") #指定节点下设置键值对
    config.set("section3","f2","k2") #指定节点下设置键值对
    config.set("section3","f3","k3") #指定节点下设置键值对
    
    config.write(open("des","w",encoding='utf-8'))  #将改变后的对象写入des文件
[/code]



**重点总结： **注意：对文件的，增，删，改，操作后都要用 **write()写入一下文件保存******

