**使用系统文件检查器工具修复丢失或损坏的系统文件**

如果某些 Windows 功能不工作或 Windows 崩溃，请使用系统文件检查器扫描
Windows 并还原文件。  \
 \
虽然下面的步骤初步看上去可能比较复杂，但只要按顺序逐步操作，我们会让你重新步入正轨。

**运行系统文件检查器工具 (SFC.exe)**

为此，请按照下列步骤操作：

1.  打开权限提升的命令提示符。 为此，请根据你的具体情况执行以下操作：

> [[全部隐藏]{.underline}](https://support.microsoft.com/)
>
> [**Windows 8.1 或 Windows 8**](https://support.microsoft.com/)
>
>  
>
> 从屏幕右边缘滑入，然后点击"搜索"。
> 或者，如果你使用的是鼠标，请指向屏幕的右下角，然后单击"搜索"。
> 在"搜索"框中键入命令提示符，右键单击"命令提示符"，然后单击"以管理员身份运行"。
> 如果系统提示你输入管理员密码或进行确认，则键入密码或单击"允许"。
>
> ![Command prompt - Run as administrator (Windows 8 or
> 8.1)](img/image1.png){width="3.375in" height="4.53125in"}
>
>  
>
> [**Windows 10、Windows 7 或 Windows
> Vista**](https://support.microsoft.com/)
>
>  
>
> 为此，请单击"启动"，在"搜索"框中键入命令提示符或 cmd，右键单击"命令提示符"，然后单击"以管理员身份运行"。
> 如果系统提示你输入管理员密码或进行确认，则键入密码或单击"允许"。
>
> ![命令提示-以管理员身份运行](img/image2.png){width="3.8854166666666665in"
> height="5.364583333333333in"}
>
>  

2.  如果运行的是 Windows 10、Windows 8.1 或 Windows
    > 8，在运行系统文件检查器之前，请先运行收件箱部署映像服务和管理
    > (DISM) 工具。  （如果运行的是 Windows 7 或 Windows
    > Vista，请跳到步骤 3。） 

> 键入以下命令，然后按 Enter 键。  命令操作可能需要几分钟才能完成。

DISM.exe /Online /Cleanup-image /Restorehealth

> **重要说明：** 当运行此命令时，DISM 通过 Windows
> 更新提供修复损坏所需的文件。 但是，如果 Windows
> 更新客户端已断开，则会将正在运行的 Windows
> 安装用作修复来源，或者将来自网络共享或可移动媒体（例如 Windows DVD）的
> Windows 并行文件夹用作文件来源。 为此，请改为运行以下命令：

DISM.exe /Online /Cleanup-Image /RestoreHealth
/Source:**C:\\RepairSource\\Windows** /LimitAccess

> **注意：** 请使用修复来源的位置替换 **C:\\RepairSource\\Windows** 占位符。
> 有关使用 DISM 工具修复 Windows 的更多信息，请参考[修复 Windows
> 映像]{.underline}。

3.  在命令提示符处，键入以下命令，然后按 Enter 键：

sfc /scannow

![具有管理员权限的 sfc /scannow
命令提示符](img/image3.png){width="5.122047244094488in"
height="2.677165354330709in"}

 \
 

> sfc
> /scannow 命令将扫描所有受保护的系统文件，并用位于 **%WinDir%**\\System32\\dllcache
> 的压缩文件夹中的缓存副本替换损坏的文件。\
> %WinDir% 占位符代表 Windows 操作系统文件夹。 例如：C:\\Windows。\
> \
> 注意 在验证 100％ 完成之前，请勿关闭此命令提示符窗口。
> 此流程完成后将显示扫描结果。

4.  流程结束后，你可能收到以下消息之一：

    -   Windows 资源保护找不到任何完整性冲突。

> 这表示您没有任何丢失或损坏的系统文件。

-   Windows 资源保护无法执行请求的操作。

> 要解决此问题，请[[在安全模式中]{.underline}](http://windows.microsoft.com/zh-cn/windows/start-computer-safe-mode)执行系统文件检查器，并确保
> PendingDeletes 和 PendingRenames
> 文件夹存在于 **%WinDir%**\\WinSxS\\Temp 下。

-   Windows 资源保护找到了损坏的文件并已成功将其修复。 详细信息包含在
    > CBS.Log（路径为 **%WinDir%**\\Logs\\CBS\\CBS.log）中。

> 若要查看有关系统文件扫描和还原的详细信息，请转到[[如何查看系统文件检查器进程的详细信息]{.underline}](https://support.microsoft.com/zh-cn/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system#cbs log)。

-   Windows 资源保护找到了损坏的文件但无法修复其中的某些文件。
    > 详细信息包含在
    > CBS.Log（路径为 **%WinDir%**\\Logs\\CBS\\CBS.log）中。

> 若要手动修复损坏的文件，请查看[[系统文件检查器进程的详细信息]{.underline}](https://support.microsoft.com/zh-cn/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system#cbs log)查找损坏的文件，然后[[手动将损坏的文件替换为已知完好的文件副本]{.underline}](https://support.microsoft.com/zh-cn/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system#manually repair)。

**更多信息**

**如何查看系统文件检查器进程的详细信息**

若要查看 CBS.Log 文件中包含的详细信息，可以使用 Findstr 命令将信息复制到
Sfcdetails.txt 文件，然后查看 Sfcdetails.txt 中的详细信息。
为此，请按照下列步骤操作：

1.  打开上文步骤 1 所述的提升的命令提示符。

2.  在命令提示符处，键入以下命令，然后按 Enter 键：

> findstr /c:\"\[SR\]\" %windir%\\Logs\\CBS\\CBS.log
> \>\"%userprofile%\\Desktop\\sfcdetails.txt\"
>
> 注意 Sfcdetails.txt
> 文件包含每次系统文件检查器工具在计算机上运行时的详细信息。
> 文件包括有关系统文件检查器工具未修复文件的信息。
> 验证日期和时间项以确定该问题文件为你上次运行系统文件检查器工具时找到的文件。

3.  从你的桌面打开 Sfcdetails.txt 文件。

4.  Sfcdetails.txt 文件使用以下格式：

> 日期/时间 SFC 详细信息
>
> 以下示例日志文件包含无法修复的文件项：
>
> 2007-01-12 12:10:42, Info CSI 00000008 \[SR\] Cannot
>
> repair member file \[l:34{17}\]\"Accessibility.dll\" of Accessibility,
> Version =
>
> 6.0.6000.16386, pA = PROCESSOR\_ARCHITECTURE\_MSIL (8), Culture
> neutral,
>
> VersionScope neutral, PublicKeyToken = {l:8 b:b03f5f7f11d50a3a}, Type
>
> neutral, TypeName neutral, PublicKey neutral in the store, file is
> missing

**\
如何手动将损坏的系统文件替换为已知完好的文件副本**

当你确定哪个系统文件已损坏且无法通过 Sfcdetails.txt
文件中的详细信息修复之后，查找损坏文件所在的位置，然后手动将损坏的文件替换为已知完好的文件副本。
为此，请按照下列步骤操作：\
\
注意 你可能可以从与你的计算机运行相同版本的 Windows
的另一台计算机获取系统文件的已知完好副本。
你可以在该计算机上执行系统文件检查器进程，以确保要复制的系统文件是完好的副本。

1.  获得损坏的系统文件的管理所有权。
    > 为此，在提升的命令提示符处，复制并粘贴（或键入）以下命令，然后按
    > Enter 键：

> takeown /f **Path\_And\_File\_Name**
>
> 注意 **Path\_And\_File\_Name** 占位符代表损坏文件的路径和文件名。
> 例如，键入 takeown /f C:\\windows\\system32\\jscript.dll。 
>
> ![命令提示符下，使用管理员权限的命令成功](img/image4.png){width="5.110236220472441in"
> height="2.673228346456693in"}
>
>  

2.  授予管理员完全访问损坏的系统文件的权限。
    > 为此，复制并粘贴（或键入）以下命令，然后按 Enter 键：

> icacls **Path\_And\_File\_Name** /GRANT ADMINISTRATORS:F
>
> 注意 **Path\_And\_File\_Name** 占位符代表损坏文件的路径和文件名。
> 例如，键入 icacls C:\\windows\\system32\\jscript.dll /grant
> administrators:F。
>
> ![具有管理员权限的命令提示符](img/image5.png){width="5.106299212598425in"
> height="2.677165354330709in"}
>
>  

3.  将损坏的系统文件替换为已知完好的文件副本。
    > 为此，复制并粘贴（或键入）以下命令，然后按 Enter 键：

> 复制 **Source\_File Destination**
>
> 注意 **Source\_File** 占位符代表计算机上已知完好的文件副本的路径和文件名，**Destination** 占位符代表损坏文件的路径和文件名。
> 例如，键入 copy E:\\temp\\jscript.dll
> C:\\windows\\system32\\jscript.dll。

如果上述步骤不起作用，则可能需要重新安装
Windows。 有关详细信息，请参阅 [Windows 10
恢复选项](https://support.microsoft.com/zh-cn/help/12415)。
