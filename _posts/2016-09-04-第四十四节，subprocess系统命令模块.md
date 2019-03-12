---
layout: post
title: " 第四十四节，subprocess系统命令模块 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

用python执行系命令的相关的模块和函数的功能均在 subprocess 模块中实现，并提供了丰富的功能



**call()模块函数**

**功能：输入系统命令，直接执行命令，返回状态码, 只能查看【有参】**

**使用方法1：模块名称. **call(["系统命令","系统命令"],shell=False)** **  
****

****使用方法2： **模块名称. **call("系统命令",shell=True)********

**格式如1：subprocess.call(["ls", "-l"],shell=False)**

****格式如2：subprocess.call("ls -lh",shell=True)****

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    subprocess.call(["ls", "-l"],shell=False)#输入系统命令，直接查看对应命令的功能【有参】
    subprocess.call("ls -lh",shell=True)#输入系统命令，直接查看对应命令的功能【有参】
[/code]



**check_call()模块函数**

**功能：输入系统命令，直接执行命令，返回状态码,如果状态码是 0 ，则返回执行结果，否则抛异常【有参】**

**使用方法1：模块名称.check_call **(["系统命令","系统命令"],shell=False)** **  
****

****使用方法2： **模块名称.check_call **("系统命令",shell=True)********

**格式如1：subprocess.check_call(["ls", "-l"],shell=False)**

**格式如2：subprocess.check_call("ls -lh",shell=True)**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    subprocess.check_call(["ls", "-l"],shell=False)#输入系统命令，直接执行命令，返回状态码,如果状态码是 0 ，则返回执行结果，否则抛异常
    subprocess.check_call("ls -lh",shell=True)#输入系统命令，直接执行命令，返回状态码,如果状态码是 0 ，则返回执行结果，否则抛异常
[/code]



**check_output()模块函数**

**功能：执行命令，如果状态码是 0 ，则返回执行结果，否则抛异常【有参】**

**使用方法1：模块名称. **check_output** **(["系统命令","系统命令"],shell=False)** **  
****

****使用方法2： **模块名称. **check_output** **("系统命令",shell=True)********

**格式如1：subprocess. **check_output** (["ls", "-l"],shell=False)**

**格式如2：subprocess. **check_output** ("ls -lh",shell=True)**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    a = subprocess.check_call(["ls", "-l"],shell=False)#执行命令，如果状态码是 0 ，则返回执行结果，否则抛异常【有参】
    print(a)
    b = subprocess.check_output("dir",shell=True)#执行命令，如果状态码是 0 ，则返回执行结果，否则抛异常【有参】
    print(b)
    # 输出
    # b' \xc7\xfd\xb6\xaf\xc6\xf7 H \xd6\xd0\xb5\xc4\xbe\xed\xc3\xbb\xd3\xd0\xb1\xea\xc7\xa9\xa1\xa3\r\n
[/code]



**Popen()模块函数**

**功能：用于执行复杂的系统命令【有参】**

参数：  
shell=命令，可以是字符串或者序列类型（如：list，元组）  
bufsize：指定缓冲。0 无缓冲,1 行缓冲,其他 缓冲区大小,负值 系统缓冲  
stdin, stdout, stderr：分别表示程序的标准输入、输出、错误句柄  
preexec_fn：只在Unix平台下有效，用于指定一个可执行对象（callable object），它将在子进程运行之前被调用  
close_sfs：在windows平台下，如果close_fds被设置为True，则新创建的子进程将不会继承父进程的输入、输出、错误管道。  
所以不能将close_fds设置为True同时重定向子进程的标准输入、输出与错误(stdin, stdout, stderr)。  
shell：同上  
cwd=用于设置子进程的当前目录  
env：用于指定子进程的环境变量。如果env = None，子进程的环境变量将从父进程中继承。  
universal_newlines：不同系统的换行符不同，True -> 同意使用 \n  
startupinfo与createionflags只在windows下有效  
将被传递给底层的CreateProcess()函数，用于设置子进程的一些属性，如：主窗口的外观，进程的优先级等等

**终端输入的命令分为两种：**

**1.输入即可得到输出，如：dir 命令**

**方法1：模块名称.Popen(["系统命令", "系统命令"],shell=命令模式)**

****方法2：模块名称.Popen("系统命令",shell=命令模式)****

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    a = subprocess.Popen(["ls", "-l"],shell=False)#执行命令，   
    b = subprocess.Popen("ls -l",shell=True)#执行命令，
[/code]

cwd=用于设置子进程的当前目录

**方法： ** **模块名称.Popen("系统命令",shell=命令模式,cwd="系统目标目录")  比如要先进入目录后再执行命令的情况******

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    obj = subprocess.Popen("mkdir t3", shell=True, cwd='/home/dev',)#执行命令,为先执行的目录
[/code]

**2.输入进行某环境，依赖再输入，如：python**

Popen()参数

stdin输入通道  
stdout输出通道  
stderr错误输出通道  
universal_newlines启用换行符

**方法：模块名称.Popen("系统命令", shell=命令模式, 输入通道, 输出通道, 错误通道, 启用换行符)**

**格式：subprocess.Popen("python", shell=True, stdin=subprocess.PIPE,
stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)**

**write()模块函数**

****功能：** 向输入通道写入命令【有参】**

****使用方法：对象变量.输入通道名称. **write("系统命令")******

********格式如：obj.stdin.write("print(1)\n")********

********close()模块函数********

****功能：关闭通道，关闭输入通道，关闭输出通道，关闭错误通道【无参】****

****使用方法： ** **对象变量.要关闭通道名称. ** ** ** **close()****************

**格式如：obj.stdin.close()**

**read()模块函数**

****功能：1.输出通道获取结果，2.错误通道获取出错信息【无参】**  
**

****使用方法： ** **对象变量.输出通道或错误通道名称. **read()**********

**格式如1：obj.stdout.read()**

****格式如2：obj.stderr.read()****

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess #导入模块
    obj = subprocess.Popen("python", shell=True, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)#创建命令对象
    obj.stdin.write("print(1)\n")#输入通道写入命令
    obj.stdin.write("print(2)")#输入通道写入命令
    obj.stdin.close()#关闭输入通道
    
    cmd_out = obj.stdout.read()#输出通道获取结果
    obj.stdout.close()#关闭输出通道
    cmd_error = obj.stderr.read()#错误通道获取出错信息
    obj.stderr.close()#关闭错误通道
    
    print(cmd_out)#打印出输出通道信息
    print(cmd_error)#打印错误通道信息
    # 输出
    # 1
    # 2
[/code]



**communicate()模块函数**

****功能：自动选择通道，可以自动获取通道信息，如果传值将自动写入输入通道，然后自动获取输出通道信息【有参可选】**  
**

****使用方法1： ** **对象变量. **communicate()**********

**************使用方法2： ** **对象变量. **communicate('输入通道命令')********************

**格式如1：obj.stdout.read()**

**格式如2：obj.stderr.read('print("hello")')**

列1

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess
    obj = subprocess.Popen("python", shell=True, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)#创建对象
    obj.stdin.write("print(1)\n")#输入通道写入命令
    obj.stdin.write("print(2)")#输入通道写入命令
    obj.stdin.close()#关闭输入通道
    
    out_error_list = obj.communicate()#自动选择通道，可以自动获取通道信息，如果传值将自动写入输入通道，然后自动获取输出通道信息
    print(out_error_list)
    # 输出
    # ('1\n2\n', '')
[/code]

列2

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import subprocess
    obj = subprocess.Popen("python", shell=True, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)#创建对象
    out_error_list = obj.communicate('print("hello")')#自动选择通道，可以自动获取通道信息，如果传值将自动写入输入通道，然后自动获取输出通道信息
    print(out_error_list)
    # 输出
    # ('hello\n', '')
[/code]



