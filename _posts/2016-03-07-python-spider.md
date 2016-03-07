---
layout: default
title: python爬虫存档
---
# python爬虫存档
## 库的选择
  当然，我们可以使用原生的urllib,urllib2来编写爬虫程序，也可以`import re`来使用正则。当时，如果要快速的完成任务，引用别人已经写好的模块是必不可少的。
  如何发起http请求呢，我们使用`requests`，安装：`easy_install requests`。
  如何像`jQuery`那样匹配内容呢，安装:`easy_install pyquery`。
## 一个简单的例子
```
  from pyquery import PyQuery as jquery
  import requests
  
  def get_list(url,headers):
    r = requests.get(url=url,headers=headers)
    text = r.text#maybe you need t.text.encode("utf-8")
    d = jquery(text)
    lists = d(".list")
    if lists:
      for list in lists:
        print jqery(list).html()
```
