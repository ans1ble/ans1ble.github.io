python3+pyqt5+pyinstaller的各种问题

windows系统+python3+pyqt5+pyinstaller打包，经常会出现各种打包异常情况。
如果代码没有特别异常，那么综合原因，大抵都是这四个元素之间的匹配问题，引起的。

1.windows系统的版本和位数 （mac系统和linux 没有进行测试过）
2.python3的版本和位数
3.pyqt5的版本和位数 （如果pip安装，则位数同python3）
4.pyinstaller的版本和位数（一般pip安装，无需考虑位数）

坑1.pyinstaller打成的包，可以在64位操作系统使用，无法在32位操作系统使用
坑的成因：
python存在64位版本和32位版本。
64位版本打成的包，只能在64位操作系统使用。
32位版本打成的包，即可以在64位操作系统使用，也可以在32位操作系统使用。

解决方案：
重新安装32位版本的python，进行开发。

坑2.pyinstaller打成的包，可以在win7以上操作系统使用，无法在xp操作系统使用
坑的成因：
python3 从3.5版本开始，就已经不支持xp操作系统了。

解决方案：
重新安装3.4版本的python，进行开发。

坑3.pyqt5应用，开发运行时是正常，但pyinstaller打成的包，界面失真变丑。
坑的成因：
pyinstaller 不支持最新版本的pyqt5。

解决方案：
重新安装低版本的pyqt5，进行开发。（当前推荐：5.8.2版本）
命令
pip uninstall pyqt5
pip install pyqt5==5.8.2

坑4.pyqt5应用，开发运行时是正常，但pyinstaller打成的包，无法运行，提示failed to execute script xxx。
坑的成因：（同坑3）
pyinstaller 不支持最新版本的pyqt5。

解决方案：（同坑3）
重新安装低版本的pyqt5，进行开发。（当前推荐：5.8.2版本）
命令
pip uninstall pyqt5
pip install pyqt5==5.8.2

坑5.pyqt5应用，开发运行时是正常，但pyinstaller无法打包成功。
坑的成因：（同坑3）
pyinstaller 不支持最新版本的pyqt5。

解决方案：（同坑3）
重新安装低版本的pyqt5，进行开发。（当前推荐：5.8.2版本）
命令
pip uninstall pyqt5
pip install pyqt5==5.8.2

坑6.pip install pyqt5，安装不了pyqt5，提示找不到资源。
坑的成因：
你的python3可能是最新版本，pyqt5还不支持最新版本的python3

解决方案：
重新安装低版本的python3，进行开发。（当前推荐：3.6.6版本）

坑7.pip install pyqt5-tools，安装不了pyqt5-tools，提示找不到资源。
坑的成因：
你的python3可能是最新版本，pyqt5-tools还不支持最新版本的python3

解决方案：
重新安装低版本的python3，进行开发。（当前推荐：3.6.6版本）

坑8.pip install pyqtchart，但是安装不了pyqtchart。
坑的成因：
pyqtchart对pyqt5的版本有依赖需求。

解决方案：
针对pyqt5的版本进行安装。
命令如： pip install pyqtchart==5.8

坑9.pip install pyqtdatavisualization，但是安装不了pyqtdatavisualization。
坑的成因： （同坑8）
pyqtdatavisualization对pyqt5的版本有依赖需求。

解决方案：（同坑8）
针对pyqt5的版本进行安装。
命令如： pip install pyqtdatavisualization==5.8

坑10.python3的orm技术，使用sqlalchemy模块，开发运行时都是正常的，但pyinstaller打成的包，数据库执行异常。
坑的成因：
pyinstaller打成的包，在执行连表后的对象属性读取时，失败。

解决方案：
找不到好的解决方法，只能换回sql语言来完成。（如有好的解决方法，敬请留言告知）


坑11..32位XP打包环境，pyinstaller打包失败或异常    (2018年12月14日补充)
坑的成因：
最新版本3.3，3.3.1，3.4的pyinstaller ，不支持32位XP打包环境

解决方案：
重新安装低版本的pyinstaller ，进行打包。（当前推荐：3.2.1版本）
命令
pip uninstall pyinstaller
pip install pyinstaller ==3.2.1