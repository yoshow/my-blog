---
layout: post
title:  "Chrome 清除 DNS 缓存"
date:   2013-02-17 20:00:00 +0800
categories: Chrome
tags: Chrome
---
Chrome 会对域名的 DNS 解析进行缓存，一般重启 Chrome 可以清除 DNS 缓存。

如果没有清除也可通过下面的方法清除 DNS 缓存： 地址栏输入 [chrome://net-internals/#dns](chrome://net-internals/#dns)，点击如下按钮  

- 页面中的 <code>Clear host cache</code> 按钮;
- 点击右上角三角形符号，执行弹出菜单中的 <code>Clear cache</code> 和 <code>Flush sockets</code> 菜单项;

执行完后无需重启即刻生效。