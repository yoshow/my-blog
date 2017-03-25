---
layout: post
title:  "清理 SQL Server 数据库日志"
date:   2012-12-15 20:00:00 +0800
tags: ["SQL","SQL Server"]
---
#### 清理数据库日志 ####

{% highlight SQL %}
DECLARE @Database nvarchar(50)

Set @Database='X3_Development'

-- 1.清空日志  
DUMP TRANSACTION @Database WITH NO_LOG

-- 2.截断事务日志  
BACKUP LOG @Database WITH NO_LOG

-- 3.收缩数据库  
DBCC SHRINKDATABASE(@Database)

-- 4.设置数据库自动收缩  
EXEC sp_dboption @Database,'autoshrink','TRUE'
{% endhighlight %}

#### 压缩日志及数据库文件大小 ####

1.清空日志  
DUMP TRANSACTION 数据库名 WITH NO_LOG

2.截断事务日志  
BACKUP LOG 数据库名 WITH NO_LOG

3.收缩数据库文件(如果不压缩,数据库的文件不会减小  
企业管理器–右键你要压缩的数据库–所有任务–收缩数据库–收缩文件  
–选择日志文件–在收缩方式里选择收缩至XXM,这里会给出一个允许收缩到的最小M数,直接输入这个数,确定就可以了

也可以用SQL语句来完成  
–收缩数据库  
DBCC SHRINKDATABASE(数据库名)  

–收缩指定数据文件,1是文件号,可以通过这个语句查询到:select * from sysfiles  
DBCC SHRINKFILE(1)

4.为了最大化的缩小日志文件  
a.分离数据库:  
企业管理器–服务器–数据库–右键–分离数据库

b.在我的电脑中删除LOG文件  

c.附加数据库:  
企业管理器–服务器–数据库–右键–附加数据库

此法将生成新的LOG，大小只有500多K

或用代码：  
下面的示例分离 pubs，然后将 pubs 中的一个文件附加到当前服务器。

a.分离  
EXEC sp_detach_db @dbname = ‘pubs’

b.删除日志文件  

c.再附加数据库  
EXEC sp_attach_single_file_db @dbname = ‘pubs’,
@physname = ‘C:\Program Files\Microsoft SQL Server\MSSQL\Data\pubs.mdf’

5.为了以后能自动收缩,做如下设置:  
企业管理器–服务器–右键数据库–属性–选项–选择”自动收缩”

-SQL语句设置方式:  
EXEC sp_dboption ‘数据库名’, ‘autoshrink’, ‘TRUE’

6.如果想以后不让它日志增长得太大  
企业管理器–服务器–右键数据库–属性–事务日志–将文件增长限制为xM(x是你允许的最大数据文件大小)

–SQL语句的设置方式:  
alter database 数据库名 modify file(name=逻辑文件名,maxsize=20)