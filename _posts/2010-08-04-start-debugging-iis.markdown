---
layout: post
title:  "无法在Web服务器上启动调试"
date:   2010-08-04 20:00:00 +0800
# categories: visualstuido
tags: ["IIS", ".NET", "Visual Studio"]
---

无法在Web服务器上启动调试。与Web服务器通信时出现身份验证错误

使用Visual Studio 2005（Visual Studio 2008亦存在此问题）调试设置了主机头的网站时出现如下错误信息：

—————————  
Microsoft Visual Studio  
—————————  
无法在 Web 服务器上启动调试。与 Web 服务器通信时出现身份验证错误。请参阅“帮助”以协助解决问题。  
—————————  

项目属性的Web中设置“项目URL”为 http://www.x3platform.com

如果将“项目URL”指定为 localhost 则在设置时不会出现以上的错误，所以排除了网上绝大部分文章提供的“集成Windows身份验证”，项目属性中“启用调试”的解决方案。

真正的解决方法如下：

步骤 1： 禁用环回检查  
请遵循以下步骤： 
{% highlight HTML %}
1. 打开注册表编辑器（单击 开始 ， 单击 运行 , 类型 regedit然后单击 确定 ）。
2. 中注册表编辑器, 找到并单击以下注册表项：
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
3. 右击 Lsa ， 指向 新建 , 然后单击 DWORD 值 。
4. 类型 DisableLoopbackCheck然后按 Enter。
5. 右击 DisableLoopbackCheck , 然后单击 修改 。
6. 在 数值数据 框中, 键入 1然后单击 确定 。
7. 退出注册表编辑器, 并重新启动计算机。 （可以不重启计算机）
{% endhighlight %}

步骤 2： 指定主机名  
要指定主机名，映射到环回地址并可连接到 Web 站点上, 请按照下列步骤： 
{% highlight HTML %}
1. 打开注册表编辑器（单击 开始 ， 单击 运行 , 类型 regedit 然后单击 确定 ）。
2. 中注册表编辑器, 找到并单击以下注册表项：
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0
3. 右击 MSV1_0 ，指向 新建 , 然后再单击 多字符串值 。
4. 类型 BackConnectionHostNames 然后按 Enter。
5. 右击 BackConnectionHostNames , 然后单击修改。
6. 在数值数据 框中, 键入主机名或主机名为站点所在的本地计算机名称, 确定 。
7. 退出注册表编辑器, 并重新启动 IISAdmin 服务。
{% endhighlight %}

这个错误的信息只会出现在特定环境的计算机中：IIS6 或 IIS 5.1 + .Net 3.5 SP1 .

**相关链接**  
[Authentication Issues Accessing Companyweb from the Server Itself after 963027 or Windows 2008 SP 2](https://blogs.technet.microsoft.com/sbs/2009/02/24/known-issues-after-installing-ie-8-on-small-business-server-2008-and-the-vista-clients-that-are-joined-to-the-sbs-domain/)  
[MS08-068: Vulnerability in SMB could allow remote code execution](https://support.microsoft.com/en-us/help/957097/ms08-068-vulnerability-in-smb-could-allow-remote-code-execution)  
[Known Issues After Installing IE 8 on Small Business Server 2008 and the Vista Clients That Are Joined to the SBS Domain](https://blogs.technet.microsoft.com/sbs/2009/02/24/known-issues-after-installing-ie-8-on-small-business-server-2008-and-the-vista-clients-that-are-joined-to-the-sbs-domain/)