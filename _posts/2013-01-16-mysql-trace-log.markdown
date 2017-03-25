---
layout: post
title:  "MySQL 设置跟踪查询语句"
date:   2013-01-16 20:00:00 +0800
categories: MySQL
tags: MySQL
---

本地开发环境  
Windows 2008 R2 + MySQL 5.0

修改 MySQL 的 my.ini 配置文件，在 [mysqld] 节点下添加如下记录

{% highlight ini %}
[mysqld]
# Query trace log
log="D:/opt/MySQL/data/query.log"
log-slow-queries="D:/opt/MySQL/data/query_slow.log"
{% endhighlight %}

然后，需要重新启动 My SQL 的服务，就可以实时看到当前正在执行的语句了。

**注:在linux中, my.ini 配置文件一般情况下命名为为 my.cnf**