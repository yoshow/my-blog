---
layout: post
title:  "SQL Server Management Studio 清除历史登陆记录"
date:   2013-01-14 20:00:00 +0800
categories: SQL Server Management Studio
---
删除 <code>C:\Users\Administrator\AppData\Roaming\Microsoft\Microsoft SQL Server\100\Tools\Shell\</code> 下的SqlStudio.bin文件, 然后重启 SQL Server Management Studio 就可以了。

**说明**  
服务器列表、登陆帐户、密码等信息都记录在如下文件中  
SQL Server 2005 : \%AppData\%\Microsoft\Microsoft SQL Server\90\Tools\Shell\mru.dat  
SQL Server 2008 : \%AppData\%\Microsoft\Microsoft SQL Server\100\Tools\Shell\SqlStudio.bin

删除后, 需要重新启动 SQL Server Management Studio 。

注:\%AppData\% 是环境变量，在命令行中运行 ECHO \%APPDATA\%，就可以看到对应的目录了。  
默认情况下  
Windows 7, \%AppData\% = C:\Users\Administrator\AppData\Roaming\;  
Windows XP, \%AppData\% = C:\Documents and Settings\Administrator\Application Data\;

**相关链接**  
[SQL Server Management Studio 清除历史登陆记录](http://pnig0s1992.blog.51cto.com/393390/346944)  
[清除 Sql Server 登录时的用户记录](http://cool.worm.blog.163.com/blog/static/64339006201063192531755/) 