---
layout: post
title:  "利用 NTP POOL PROJECT 设置服务器正确的时间"
date:   2013-01-20 20:00:00 +0800
categories: NTP Windows 
tags: ntp
---

租用的美国的 VPS, 虽然可以手动设置时间, 但是每次重启后操作系统默认为美国的时间。

将 Windows 的 NTP 服务器设置为 cn.pool.ntp.org。

具体设置方法参考: [Windows NTP 客户端时间同步设置](/ntp/windows/2012/12/22/windows-ntp-client-setting.html)  

然后需要重启 w32time 服务  
执行命令行 <code>net stop w32time</code>  
然后再执行 <code>net start w32time</code>  

好了，如果你运气足够好的话，此时在客户端就能进行时钟同步了。

如果你需要其他地区的NTP服务器，可以参考 http://www.pool.ntp.org/en/