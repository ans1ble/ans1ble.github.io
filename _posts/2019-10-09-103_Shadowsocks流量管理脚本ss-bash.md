### Shadowsocks流量管理脚本ss-bash

在分享自己搭建的Shadowsocks时，遇到一个问题。Shadowsocks python版虽然自带有多用户配置功能，但无法限制用户流量。而ss-panel+ss-manyuser的多用户分享方案偏商业用途，部署和配置都比较繁琐，数据库和web面板都有不小的资源占用。hellofwy所写的ss-bash的脚本则完美解决了这个问题，下面是这个脚本的简介、安装和注意事项说明：

### 简介
ss-bash无论是启动、停止，还是添加用户，修改流量限制，都是使用命令，十分简洁、方便。ss-bash原理是使用iptables规则获取各端口的流量，一个端口代表一个用户。脚本循环运行，在固定时间间隔根据iptables结果统计流量使用情况，并在流量超过限制时，添加对应端口的iptables reject规则以禁用端口。

系统要求为Linux Debian/Ubuntu，shadowsocks python版，iptables需要正常工作中。目前只支持统计ipv4流量。

github网址：https://github.com/hellofwy/ss-bash

### 安装更新

```bash
apt-get update
```
### 安装pip

```bash
apt-get install python-pip -y
```
### 安装shadowsocks

```bash
pip install shadowsocks
```
### 安装unzip和bc，bc是使用ss-bash的必备工具。

```bash
apt-get install unzip
apt-get install bc
```
### 下载ss-bash

```bash
wget https://github.com/hellofwy/ss-bash/archive/master.zip
unzip master.zip
```
### 使用查看帮助

```bash
cd ss-bash-master/
./ssadmin.sh h
```

### 添加用户，例如新增用户端口为8388，密码是123456，流量限制100G

```bash
./ssadmin.sh add 8388 123456 100G
```
### 启动

```bash
./ssadmin.sh start
```

更详细的说明文档，可以查看官方wiki：https://github.com/hellofwy/ss-bash/wiki

### 添加开机启动

编辑 /etc/rc.local

```bash
vim /etc/rc.local
```
在 exit 0 前面加入(路径请自行替换)

```bash
/home/ss-bash-master/ssadmin.sh start
```
常见问题
在使用之前确认已经关闭了原来的shadowsocks，并确保iptables正常。

1、无法连接上。确认本地shadowsocks客户端帐号无误，访问网站无法打开，客户端日志记录有大量的time out。解决方法：说明是服务器端口被封，尝试换一个端口。

2、日志记录远程计算机关闭或无法连接，说明shadowsocks没有启动。可能是vps宕机重启后shadowsocks没有启动。解决方法：启动shadowsocks，并为其添加开机启动。

3、修改加密方式。编辑配置文件 ssmlt.template 即可，例如加密方式改为chacha20

```bash
"server": "0.0.0.0",
"timeout": 60,
"method": "chacha20",
```