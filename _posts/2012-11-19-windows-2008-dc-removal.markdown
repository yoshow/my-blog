---
layout: post
title:  "Windows 2008 R2 辅助域控制器强制降级"
date:   2012-11-19 20:00:00 +0800
tags: ["Windows 2008 R2", "Active Directory"]
---

一、辅助域控上操作,自身降域  
适用于在 Windows Server 2008 、Windows Server 2003 和 Windows 2000 Server 中使用 Active Directory 安装(dcpromo)向导降级时，域控制器无法正常降级时。
在辅助域控上操作：单击“开始”，单击“运行”，然后键入以下命令：

{% highlight HTML %}
dcpromo /forceremoval
{% endhighlight%}

**重要：由于强制降级会导致任何本地保存的更改丢失，如非绝对必要，请勿在生产域或测试域中使用强制降级。当无法解决连接、名称解析、身份验证或复制引擎相关项以致于无法执行正常降级时，您可以将域控制器强制降级。**

二、删除主域服务器上的备份域服务器：  
{% highlight HTML %}
1)打开Active Directory 用户和计算机 -> Domain Controllers,
右键点击所要删除的辅助域控,在菜单上选择删除.
确定 => 删除
这台域控制器永远为脱机并且不再能用Active Directory 安装向导（dcpromo）将其降级
确定 => 删除
2)控制面板 => 管理工具 => AD站点和服务 => Sites=> Default-First-Site-Name 
=> servers下面找到其他的辅助域服务器
在删除备份域服务器前先要把其下面的 NTDS Settings 删除；
会有3种选择：
1.域控制器降级，继续当计算机使用
2.重新开启AD复制
3.这台域控制器永远为脱机并且不再能用Active Directory 安装向导（dcpromo）将其降级。
删除 NTDS　Settings 以后就可以把辅助域服务器删除掉了。
{% endhighlight%}

**相关链接**  
[强制删除 Windows Server 2008 域控制器](https://technet.microsoft.com/en-us/library/ae4dd0e3-2019-4278-8efd-61c36ba9e1c0)  
[域控制器降级失败后如何删除 Active Directory 中的数据](https://support.microsoft.com/en-us/help/216498/how-to-remove-data-in-active-directory-after-an-unsuccessful-domain-controller-demotion)