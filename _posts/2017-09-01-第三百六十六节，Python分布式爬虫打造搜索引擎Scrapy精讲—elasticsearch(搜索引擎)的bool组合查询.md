
---
layout: post
title: " 第三百六十六节，Python分布式爬虫打造搜索引擎Scrapy精讲—elasticsearch(搜索引擎)的bool组合查询 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百六十六节，Python分布式爬虫打造搜索引擎Scrapy精讲—elasticsearch(搜索引擎)的bool组合查询**



**bool查询说明**

**filter:[],字段的过滤，不参与打分**  
 **must:[],如果有多个查询，都必须满足【并且】**  
 **should:[],如果有多个查询，满足一个或者多个都匹配【或者】**  
 **must_not:[],相反查询词一个都不满足的就匹配【取反，非】**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足【并且】
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配【或者】
    #     "must_not":[],    相反查询词一个都不满足的就匹配【取反，非】
    #}
[/code]





**建立测试数据**

[code]

     #建立测试数据
    POST jobbole/job/_bulk
    {"index":{"_id":1}}
    {"salary":10,"title":"python"}
    {"index":{"_id":2}}
    {"salary":20,"title":"Scrapy"}
    {"index":{"_id":3}}
    {"salary":30,"title":"Django"}
    {"index":{"_id":4}}
    {"salary":40,"title":"Elasticsearch"}
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170901205834155-1675554306.png)





**bool组合查询——最简单的filter过滤查询之term查询，相当于等于**

****过滤查询到salary字段等于20的数据****

**可以看出执行两个两个步骤，先查到所有数据，然后在查到的所有数据过滤查询到salary字段等于20的数据**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配
    #     "must_not":[],    相反查询词一个都不满足的就匹配
    #}
    
    
    
    #简单过滤查询
    #最简单的filter过滤查询
    #如果我们要查salary字段等于20的数据
    GET jobbole/job/_search
    {
      "query": {
        "bool": {                   #bool组合查询
          "must":{                  #如果有多个查询词，都必须满足
            "match_all":{}          #查询所有字段
          },
          "filter": {               #filter过滤
            "term": {               #term查询，不会将我们的搜索词进行分词，将搜索词完全匹配的查询
              "salary": 20          #查询salary字段值为20
            }
          }
        }
      }
    }
    
    
    
    #简单过滤查询
    #最简单的filter过滤查询
    #如果我们要查salary字段等于20的数据
    GET jobbole/job/_search
    {
      "query": {
        "bool": {
          "must":{
            "match_all":{}
          },
          "filter": {
            "term": {
              "salary": 20
            }
          }
        }
      }
    }
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170901213239390-548772234.png)





**bool组合查询——最简单的filter过滤查询之terms查询，相当于或**

**过滤查询到salary字段等于10或20的数据**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配
    #     "must_not":[],    相反查询词一个都不满足的就匹配
    #}
    
    
    
    
    #简单过滤查询
    #最简单的filter过滤查询
    #如果我们要查salary字段等于20的数据
    #过滤salary字段值为10或者20的数据
    GET jobbole/job/_search
    {
      "query": {
        "bool": {
          "must":{
            "match_all":{}
          },
          "filter": {
            "terms": {
              "salary":[10,20]
            }
          }
        }
      }
    }
[/code]

**注意：filter过滤里也可以用其他基本查询的**





**_analyze测试查看分词器解析的结果**  
 **analyzer设置分词器类型ik_max_word精细化分词，ik_smart非精细化分词**  
 **text设置词**

[code]

     #_analyze测试查看分词器解析的结果
    #analyzer设置分词器类型ik_max_word精细化分词，ik_smart非精细化分词
    #text设置词
    GET _analyze
    {
      "analyzer": "ik_max_word",
      "text": "Python网络开发工程师"
    }
    
    GET _analyze
    {
      "analyzer": "ik_smart",
      "text": "Python网络开发工程师"
    }
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170901221416249-700237337.png)





**bool组合查询——组合复杂查询1**  
 **查询salary字段等于20或者title字段等于python、salary字段不等于30、并且salary字段不等于10的数据**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足【并且】
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配【或者】
    #     "must_not":[],    相反查询词一个都不满足的就匹配【取反，非】
    #}
    
    # 查询salary字段等于20或者title字段等于python、salary字段不等于30、并且salary字段不等于10的数据
    GET jobbole/job/_search
    {
      "query": {
        "bool": {
          "should": [
            {"term":{"salary":20}},
            {"term":{"title":"python"}}
          ],
          "must_not": [
            {"term": {"salary":30}},
            {"term": {"salary":10}}]
        }
      }
    }
[/code]





**bool组合查询——组合复杂查询2**  
 **查询salary字段等于20或者title字段等于python、salary字段不等于30、并且salary字段不等于10的数据**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足【并且】
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配【或者】
    #     "must_not":[],    相反查询词一个都不满足的就匹配【取反，非】
    #}
    
    # 查询title字段等于python、或者、(title字段等于elasticsearch并且salary等于30)的数据
    GET jobbole/job/_search
    {
      "query": {
        "bool": {
          "should":[
            {"term":{"title":"python"}},
            {"bool": {
              "must": [
                {"term": {"title":"elasticsearch"}},
                {"term":{"salary":30}}
              ]
            }}
          ]
        }
      }
    }
[/code]





**bool组合查询——过滤空和非空**

[code]

     #建立数据
    POST bbole/jo/_bulk
    {"index":{"_id":"1"}}
    {"tags":["search"]}
    {"index":{"_id":"2"}}
    {"tags":["search","python"]}
    {"index":{"_id":"3"}}
    {"other_field":["some data"]}
    {"index":{"_id":"4"}}
    {"tags":null}
    {"index":{"_id":"1"}}
    {"tags":["search",null]}
[/code]



**处理null空值的方法**

**获取tags字段，值不为空并且值不为null的数据**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足【并且】
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配【或者】
    #     "must_not":[],    相反查询词一个都不满足的就匹配【取反，非】
    #}
    
    
    #处理null空值的方法
    #获取tags字段，值不为空并且值不为null的数据
    GET bbole/jo/_search
    {
      "query": {
        "bool": {
          "filter": {
            "exists": {
              "field": "tags"
            }
          }
        }
      }
    }
[/code]

**获取tags字段值为空或者为null的数据，如果数据没有tags字段也会获取**

[code]

     # bool查询
    # 老版本的filtered已经被bool替换
    #用 bool 包括 must should must_not filter 来完成
    #格式如下：
    
    #bool:{
    #     "filter":[],      字段的过滤，不参与打分
    #     "must":[],        如果有多个查询，都必须满足【并且】
    #     "should":[],      如果有多个查询，满足一个或者多个都匹配【或者】
    #     "must_not":[],    相反查询词一个都不满足的就匹配【取反，非】
    #}
    
    
    #获取tags字段值为空或者为null的数据，如果数据没有tags字段也会获取
    GET bbole/jo/_search
    {
      "query": {
        "bool": {
          "must_not": {
            "exists": {
              "field": "tags"
            }
          }
        }
      }
    }
[/code]



