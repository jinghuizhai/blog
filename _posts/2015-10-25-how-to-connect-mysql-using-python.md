---
layout: default
title: python连接mysql
---
#python连接mysql
python连接mysql的方法有很多，都需要了解一下，选择最合适自己的。
这里介绍了几个API，在官方的介绍[wiki](https://wiki.python.org/moin/MySQL)里：
第一个是mysql-python，就是通常大家说的MySQLdb。好处是参数化查询，这一特征有助于防止SQL注入，但是它的linux和windows平台的安装包是不同的。
然后是pymysql,和mysql-python的API一致，就是说怎么样使用mysql-python操作mysql，也就用pymysql。版本支持的跨度也大2.4 - 3.2.
再往后依次是：
*mxodbc
*pyodbc
*mysql-connector
等。