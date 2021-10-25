---
layout: post
title: " 第二百九十节，MySQL数据库-MySQL命令行导出导入数据库，数据库备份还原 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**MySQL命令行导出导入数据库，数据库备份还原**



**MySQL命令行导出数据库：**  
 **1，进入MySQL目录下的bin文件夹：cd MySQL中到bin文件夹的目录**  
 **如我输入的命令行：cd C:\Program Files\MySQL\MySQL Server 4.1\bin**  
 **(或者直接将windows的环境变量path中添加该目录)**

  
**2，导出数据库：mysqldump -u 用户名 -p 数据库名 > 导出的文件名 **  
**如我输入的命令行:mysqldump -u root -p news > news.sql (输入后会让你输入进入MySQL的密码)**  
 **（如果导出单张表的话在数据库名后面输入表名即可）**

**3、会看到文件news.sql自动生成到bin文件下**  
 **命令行导入数据库：**



**MySQL命令行导入数据库：**

**1，将要导入的.sql文件移至bin文件下，这样的路径比较方便**  
 **2，同上面导出的第1步**  
 **3，进入MySQL：mysql -u 用户名 -p**  
 **如我输入的命令行:mysql -u root -p (输入同样后会让你输入MySQL的密码)**  
 **4，在MySQL-Front中新建你要建的数据库，这时是空数据库，如新建一个名为news的目标数据库**  
 **5，输入：mysql >use 目标数据库名**  
 **如我输入的命令行:mysql >use news;**  
 **6，导入文件：mysql >source 导入的文件名; **  
**如我输入的命令行：mysql >source news.sql;**



**备份数据库**



**MySQL备份和还原,都是利用mysqldump、mysql和source命令来完成的。**  
 **1.Win32下MySQL的备份与还原**  
 **1.1 备份**  
 **开始菜单 | 运行 | cmd |利用“cd \Program Files\MySQL\MySQL Server 5.0\bin”命令进入bin文件夹
| 利用“mysqldump -u 用户名 -p databasename >exportfilename”导出数据库到文件，如mysqldump -u
root -p voice>voice.sql，然后输入密码即可开始导出。 **  



**还原数据库**  
 **1.2 还原**  
 **进入MySQL Command Line Client，输入密码，进入到“mysql >”，输入命令"show
databases；"，回车，看看有些什么数据库；建立你要还原的数据库，输入"create database
voice；"，回车；切换到刚建立的数据库，输入"use voice；"，回车；导入数据，输入"source
voice.sql；"，回车，开始导入，再次出现"mysql>"并且没有提示错误即还原成功。 **  
  
**Linux下MySQL的备份与还原 **  
**2.1 备份**  
 **[root@localhost ~]# cd /var/lib/mysql (进入到MySQL库目录，根据自己的MySQL的安装情况调整目录)**  
 **[root@localhost mysql]# mysqldump -u root -p voice >voice.sql，输入密码即可。**  
 **2.2 还原**  
 **法一：**  
 **[root@localhost ~]# mysql -u root -p 回车，输入密码，进入MySQL的控制台"mysql >"，同1.2还原。**  
 **法二：**  
 **[root@localhost ~]# cd /var/lib/mysql (进入到MySQL库目录，根据自己的MySQL的安装情况调整目录)**  
 **[root@localhost mysql]# mysql -u root -p voice <voice.sql，输入密码即可。 **

** **

