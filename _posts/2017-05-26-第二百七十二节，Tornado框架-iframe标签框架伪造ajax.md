---
layout: post
title: " 第二百七十二节，Tornado框架-iframe标签框架伪造ajax "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**Tornado框架-iframe标签框架伪造ajax**

**html**

[code]

     <!DOCTYPE html>
    <html>
    
        <head lang="en">
            <meta charset="UTF-8">
            <title></title>
        </head>
    
        <body>
    
            <div>
                <p>请输入要加载的地址：<span id="currentTime"></span></p>
                <p>
                    <input id="url" type="text" />
                    <input type="button" value="刷新" onclick="LoadPage();">
                </p>
            </div>
    
    
            <div>
                <h3>加载页面位置：</h3>
                <iframe id="iframePosition" style="width: 100%;height: 500px;"></iframe>
            </div>
    
    
            <script type="text/javascript">
    
                window.onload= function(){                  //框架加载完毕后执行
                    var myDate = new Date();                //创建时间对象
                    document.getElementById('currentTime').innerText = myDate.getTime();  //获取时间戳写入到id为currentTime元素里
    
                };
    
                function LoadPage(){                        //函数
                    var targetUrl =  document.getElementById('url').value;      //获取id为url的value值
                    document.getElementById("iframePosition").src = targetUrl;  //将value值写入框架的src请求地址
                }
    
    </script>
    
        </body>
    </html>
[/code]

![](https://images2015.cnblogs.com/blog/955761/201705/955761-20170526111319357-1306690862.png)

