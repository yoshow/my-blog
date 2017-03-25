---
layout: post
title:  "Windows NTP 客户端时间同步设置"
date:   2012-12-22 20:00:00 +0800
categories: NTP Windows 
tags: Windows NTP
---

1. 开始=>运行输入 gpedit.msc

2. 计算机配置=>管理模板=>系统=>Windows 时间服务=>时间提供程序=>右单击”配置 Window NTP 客户端”，选择属性。
<pre><code>a.选择 “已启用”
b.在 NTP Server 对应栏位输入时间同步服务器的地址。
c.Tpye 栏位选择 NTP。
d.SpecialPollInterval栏位输入需要同步的时间周期，单位：秒，如：每10分钟同步一次，输入600。
e.确定。</code></pre>

3. 计算机配置=>管理模板=>系统=>Windows 时间服务=>时间提供程序=>右单击”启用Window NTP客户端”，选择属性。
a.选择 “已启用”

4. 计算机配置=>管理模板=>系统=>Windows 时间服务=>时间提供程序=>右单击”启用Window NTP服务端”，选择属性。
a.选择 “已禁用”