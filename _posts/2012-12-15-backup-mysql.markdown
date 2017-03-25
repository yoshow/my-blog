---
layout: post
title:  "备份 MySQL 数据库"
date:   2012-12-15 20:00:00 +0800
tags: ["SQL","MySQL"]
---

备份 MySQL 数据库的命令  
{% highlight BASH %}
mysqldump -h{hostname} -u{username} -p{password} {databasename} > backupfile.sql
{% endhighlight %} 

备份 MySQL 数据库为带删除表的命令  
{% highlight BASH %}
mysqldump -–add-drop-table -u{username} -p{password} {databasename} > backupfile.sql
{% endhighlight %} 

直接将 MySQL 数据库压缩备份(适用于 Linux)  
{% highlight BASH %}
mysql -h{hostname} -u{username} -p{password} {databasename} | gzip > backupfile.sql.gz
{% endhighlight %} 

备份 MySQL 数据库某个(些)表的命令  
{% highlight BASH %}
mysqldump -h{hostname} -u{username} -p{password} {databasename} {table1} {table2} > backupfile.sql
{% endhighlight %} 

同时备份多个 MySQL 数据库的命令  
{% highlight BASH %}
mysqldump -h{hostname} -u{username} -p{password} –databases {databasename1} {databasename2} > backupfile.sql
{% endhighlight %} 

仅备份数据库结构的命令  
{% highlight BASH %}
mysqldump –no-data –databases {databasename1} {databasename2} {databasename3} > backupfile.sql
{% endhighlight %} 

备份服务器上所有数据库的命令  
{% highlight BASH %}
mysqldump –all-databases > backupfile.sql
{% endhighlight %} 

将数据库转移到新服务器的命令(适用于 Linux)  
{% highlight BASH %}
mysqldump -u{username} -p{password} {databasename} | mysql –host=*.*.*.* -C {databasename}
{% endhighlight %} 

还原 MySQL 数据库的命令  
{% highlight BASH %}
mysql -h{hostname} -u{username} -p{password} {databasename} < backupfile.sql
{% endhighlight %} 