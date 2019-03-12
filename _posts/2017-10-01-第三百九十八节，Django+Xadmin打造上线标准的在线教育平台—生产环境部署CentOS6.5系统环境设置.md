
---
layout: post
title: " 第三百九十八节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署CentOS6.5系统环境设置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十八节，Django+Xadmin打造上线标准的在线教育平台—生产环境部署CentOS6.5系统环境设置**



**1、Linux安装配置**  
 **注意事项：**  
 **虚拟机网卡桥接模式**  
 **不要拨VPN**

如果，网络怎么都不同，可以删除这个文件  
 **/etc/udev/rules.d/70-persistent-net.rules （ 6.2版本和ubuntu 会有这个文件，这个文件是记录网口和
MAC地址关系的）**  
 **su root**





**基本配置:**  
 **ip**  
 **[root@localhost ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0**  
 **DEVICE=eth0 # 网卡名**  
 **BOOTPROTO=static # 静态指定IP地址，也可以动态，但是建议是静态。**  
 **ONBOOT=yes # 是否是开机启动**  
 **TYPE=Ethernet # 类型(默认即可)**  
 **IPADDR=192.168.31.123 # IP地址**  
 **NETMASK=255.255.255.0 # 掩码**  
 **GATEWAY=192.168.31.1 # 网关**





**ssh DNS解析 (为了安全-判断IP是否有效IP) #**  
 **/etc/ssh/sshd_config # UseDNS no**





**iptables 防火墙关闭**  
 **/etc/init.d/iptables stop # 关闭iptables**  
 **[root@localhost ~]# chkconfig iptables off # 关闭机起动级别(开机不启动)**  
 **[root@localhost ~]# chkconfig --list iptables**  
 **iptables 0:off 1:off 2:off 3:off 4:off 5:off 6:off**





**selinux 安全模块-用不到关闭**  
 **vim /etc/selinux/config # SELINUX=disabled**



  
**dns**  
 **[root@localhost ~]# cat /etc/resolv.conf**  
 **nameserver 192.168.31.1 # nameserver Dns地址和真机保持一致即可**





**vim**  
 **光标：j 下 k 上 H 左 L右**

**i --当前光标下进入编辑模式**  
 **ESC --退出编辑模式**  
 **a --当前光标下一个字符进入编辑模式**  
 **A --尾行进入编辑模式**  
 **dd --删除整行**  
 **dG --删除光标所在行到文件最后一行所有内容**  
 **dgg --删除光标所在行到文件第一行所有内容**  
 **u --返回上一次修改状态**  
 **wq --保存退出**  
 **q! --放弃打开文件后的所有修改退出**





**yum**  
 **类似于python pip包管理 # 快速安装软件的一个工具**





**weget 下载**

  
**\-------如果有基础并且Linux已经部署好可以访问外网了直接掉过第一部分的视频-----**



**2、Linux 下Python安装[用是升级不影响现有Python/多版本共存]**  
 **下载Python**

**安装**  
 **安装Python依赖包**  
 **yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-
devel readline-devel tk-devel gcc make**  
 **解压和安装软件包**  
 **tar -xzvf /opt/Python-3.6.1.tgz -C /usr/local/src/ #
src目录是存放源码的目录解压到src目录**  
 **cd /usr/local/src/Python-3.6.1**  
 **./configure --prefix=/usr/local/python3**  
 **make && make install**



  
**添加环境变量**  
 **cd /etc/profile.d/**  
 **export PATH="$PATH:/usr/local/python3/bin"**  
 **source ../profile # 重载文件**  
 **echo $PATH # 查看当前环境变量是否添加**



**3、代码上传 xshell / Git 简单的Git命令**  
 **yum -y install git**  
 **git clone 你的git url**  

