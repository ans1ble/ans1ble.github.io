---
layout: post
title: " 第三百四十八节，Python分布式爬虫打造搜索引擎Scrapy精讲—通过自定义中间件全局随机更换代理IP "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第三百四十八节，Python分布式爬虫打造搜索引擎Scrapy精讲—通过自定义中间件全局随机更换代理IP**



**设置代理ip只需要，自定义一个中间件，重写 process_request方法，**

**request.meta['proxy'] = "http://185.82.203.146:1080"    设置代理IP**

**中间件，注意将中间件注册到配置文件里去**

[code]

     from adc.daili_ip.sh_yong_ip.sh_yong_ip import sui_ji_hq_ip
    
    from fake_useragent import UserAgent    #导入浏览器用户代理模块
    
    class RequestsUserAgentmiddware(object):                                    #自定义浏览器代理中间件
        #中间件随机更换Requests请求头信息的User-Agent浏览器用户代理
        def __init__(self,crawler):
            super(RequestsUserAgentmiddware, self).__init__()                   #获取上一级父类基类的，__init__方法里的对象封装值
            self.ua = UserAgent()                                               #实例化浏览器用户代理模块类
            self.ua_type = crawler.settings.get('RANDOM_UA_TYPE','random')      #获取settings.py配置文件里的RANDOM_UA_TYPE配置的浏览器类型，如果没有，默认random，随机获取各种浏览器类型
    
        @classmethod                                                            #函数上面用上装饰符@classmethod，函数里有一个必写形式参数cls用来接收当前类名称
        def from_crawler(cls, crawler):                                         #重载from_crawler方法
            return cls(crawler)                                                 #将crawler爬虫返回给类
    
        def process_request(self, request, spider):                             #重载process_request方法
            def get_ua():                                                       #自定义函数，返回浏览器代理对象里指定类型的浏览器信息
                return getattr(self.ua, self.ua_type)
            sssf = get_ua()
            print('启用用户代理浏览器信息：{0}'.format(sssf))
            request.headers.setdefault('User-Agent', get_ua())                  #将浏览器代理信息添加到Requests请求
    
    
    class MyproxiesSpiderMiddleware(object):
        #中间件随机更换IP
    
        def process_request(self, request, spider):                             #重写process_request方法
            #到数据库随机获取一个IP
    
            xieyi = request._get_url()                                          #_get_url可以获取到请求URL，来判断是什么协议请求如https
            print(xieyi)
            dai_ip = sui_ji_hq_ip('http')                                       #到数据库随机获取一个代理IP
            request.meta['proxy'] = "http://{0}".format(dai_ip)                 #字符串格式化设置代理IP
    
            #request.meta['proxy'] = "http://185.82.203.146:1080"   设置代理IP
[/code]





**随机数据库获取IP**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import time
    
    import requests
    
    from adc.daili_ip.mysq import shujuku as ORM
    
    
    def suiji_ip(rst):
        """
        调用此函数随机到数据库获取代理IP返回IP，如果IP不可用会自动删除返回False
        """
        atime = time.localtime(time.time()-240)          #设置获取多少时间以内检测过的IP(单位秒)
        sudu = '00:00:03'                               #设置获取访问速度小于等于多少的IP，单位(时分秒)默认3秒
        dqatime = "{0}-{1}-{2} {3}:{4}:{5}".format(
            atime.tm_year,
            atime.tm_mon,
            atime.tm_mday,
            atime.tm_hour,
            atime.tm_min,
            atime.tm_sec
        )  # 将格式化时间日期，单独取出来拼接成一个完整日期
    
        try:
            mysq = ORM.session()
            shuju = mysq.query(
                ORM.daili_ip.ip,
                ORM.daili_ip.port,
                ORM.daili_ip.xtype,
                ORM.daili_ip.seshi_ri_qi,
                ORM.daili_ip.connectTimeMs
            ).from_statement(
                "SELECT ip,port,xtype,seshi_ri_qi,connectTimeMs FROM daili_ip WHERE xtype='{0}' AND ce_shi='{1}' AND seshi_ri_qi>='{2}' AND connectTimeMs<='{3}' ORDER BY RAND() LIMIT 1".format(rst, '1', dqatime, sudu)
            ).all()
            mysq.close()
            if shuju:
                print('获取到IP')
            else:
                print('获取IP失败，请检查获取条件')
        except Exception as e:
            print('查询代理IP数据出错')
            return True
        ip = shuju[0][0]
        duan_kou = shuju[0][1]
        print('启用代理IP，数据库获取到IP：{0}'.format(shuju))
    
        http_url = '{0}://image.baidu.com/'.format(rst)
        proxy_url = '{0}://{1}:{2}'.format(rst, ip, duan_kou)
        headers = {
            'Referer': http_url,
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:54.0) Gecko/20100101 Firefox/54.0',
        }
    
        print('启用代理IP，测试网址：{0}'.format(http_url))
        print('启用代理IP，测试头：{0}'.format(proxy_url))
        try:
            proxy_dict = {
                'http': proxy_url
            }
            response = requests.get(http_url, proxies=proxy_dict, headers=headers)
        except Exception as e:
            print('启用代理IP，测速连接失败{0}'.format(e))
            print('启用代理IP，测速连接失败，当前IP不可用，删除当前ip！')
            fanhui = mysq.query(ORM.daili_ip).filter(ORM.daili_ip.ip == ip).delete()  # 删除不可以数据
            mysq.commit()
            mysq.close()
            if fanhui == 1:
                print("成功删除当前IP")
            else:
                print('删除当前IP失败')
            return False
        else:
            code = response.status_code  # 获取状态吗
            sudu = str(response.elapsed)  # 获取响应时间
            if code >= 200 and code < 300:
                atime = time.localtime()
                dqatime = "{0}-{1}-{2} {3}:{4}:{5}".format(
                    atime.tm_year,
                    atime.tm_mon,
                    atime.tm_mday,
                    atime.tm_hour,
                    atime.tm_min,
                    atime.tm_sec
                )  # 将格式化时间日期，单独取出来拼接成一个完整日期
    
                print('启用代理IP，测试代理ip--{0}{1}--状态可用--状态码--{2}'.format(ip, duan_kou, code))
                print('启用代理IP，当前IP可以，正在向数据库标记')
                fanhui = mysq.query(ORM.daili_ip).filter(ORM.daili_ip.ip == ip).update({
                    "ce_shi": "1",
                    "seshi_ri_qi": dqatime,
                    "connectTimeMs": sudu
                })
                mysq.commit()
                mysq.close()
                if fanhui == 1:
                    print('向数据库成功标记可用IP！')
                else:
                    print('向数据库标记可用IP失败！！！')
                print('向爬虫返回IP：{0}:{1}'.format(ip, duan_kou))
                return ip + ':' + duan_kou
            else:
                print('启用代理IP，测试代理ip--{0}{1}--状态不可用--状态码--{2}'.format(ip, duan_kou, code))
                print('返回状态码不可以，正在向数据库删除当前IP')
                fanhui = mysq.query(ORM.daili_ip).filter(ORM.daili_ip.ip == ip).delete()  # 删除不可以数据
                mysq.commit()
                mysq.close()
                if fanhui == 1:
                    print('删除当前IP成功')
                else:
                    print('删除当前IP失败')
                return False
    
    
    def sui_ji_hq_ip(rst):
        """
        正式使用：调用此函数，接收一个参数协议，如http
        循环到数据库获取IP，IP如果不可用删除后继续获取，直到ip可以后返回ip
        值循环获取测试30分钟内有效的IP
        """
        n = True
        h = None
        while n:
            youxiao_ip = suiji_ip(rst)
            if youxiao_ip:
                h = youxiao_ip
                n = False
        return h
    
    # print(sui_ji_hq_ip('http'))
[/code]





**数据库模块文件**

[code]

     import sqlalchemy
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy import Column, Integer, String, ForeignKey, UniqueConstraint, Index,text,DATETIME,TIME
    from sqlalchemy.orm import sessionmaker, relationship
    from sqlalchemy import create_engine
    
    import requests
    import json
    import time
    import datetime
    
    
    #配置数据库引擎信息
    ENGINE = create_engine("mysql+pymysql://root:279819@127.0.0.1:3306/cshi?charset=utf8", max_overflow=500, echo=True)
    
    Base = declarative_base()       #创建一个SQLORM基类
    
    class daili_ip(Base):            #ip池设计表
        __tablename__ = 'daili_ip'
    
        id = Column(Integer, primary_key=True, autoincrement=True)
        ip = Column(String(300), unique=True)       #IP
        port = Column(String(300))                  #端口
        city = Column(String(300))                  #城市
        isp = Column(String(300))                   #运营商
        connectTimeMs = Column(TIME())              #速度
        anonymity = Column(String(300))             #匿名方式
        country = Column(String(300))               #国家
        xtype = Column(String(300))                 #协议
        zhuang_tai_ma = Column(String(300))         #状态码
        ruku_riqi = Column(DATETIME())             #入库日期
        ce_shi = Column(String(300))                #测试状态
        seshi_ri_qi = Column(DATETIME())           #测试日期
        shi_xiao_riqi = Column(DATETIME())         # 失效日期
    
    
    def init_db():
        Base.metadata.create_all(ENGINE)        #向数据库创建指定表
    
    def drop_db():
        Base.metadata.drop_all(ENGINE)          #向数据库删除指定表
    
    def session():
        cls = sessionmaker(bind=ENGINE)         #创建sessionmaker类,操作表
        return cls()
    
    
    # drop_db()         #删除表
    # init_db()
[/code]



