---
layout: post
title:  "Windows 环境下安装 RabbitMQ"
date:   2017-02-03 14:00:00 +0800
categories: rabbitmq
---
RabbitMQ是一个在AMQP基础上完整的，可复用的企业消息系统。他遵循Mozilla Public License开源协议。

1：安装RabbitMQ需要先安装Erlang语言开发包。  

下载地址 http://www.erlang.org/download.html  
在win7下安装Erlang最好默认安装。  
配置环境变量 ERLANG_HOME=C:\Program Files (x86)\erl5.9  
添加到PATH=%ERLANG_HOME%\bin;  

2：安装RabbitMQ  

下载地址 http://www.rabbitmq.com/download.html  
安装教程：http://www.rabbitmq.com/install-windows.html  
配置环境变量 C:\Program Files (x86)\RabbitMQ Server\rabbitmq_server-2.8.0
添加到PATH=%RABBITMQ_SERVER%\sbin;

3：进入%RABBITMQ_SERVER%\sbin 目录  

执行rabbitmq-plugins enable rabbitmq_management
安装完成后再执行：
rabbitmq-service.bat stop  
rabbitmq-service.bat install  
rabbitmq-service.bat start  

4.设置一个帐号  
rabbitmqctl add_user rabbit rabbit  
rabbitmqctl set_permissions -p / rabbit ".*" ".*" ".*"  

4：浏览器访问http://localhost:15672  
默认账号：guest 密码：guest
