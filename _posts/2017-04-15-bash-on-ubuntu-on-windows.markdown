---
layout: post
title:  "Bash on Ubuntu on Windows"
date: 2017-04-15 20:00:00 +0800
tags: Ubuntu Windows
--- 

#### 开启开发人员模式 ####

无论你是通过全新安装还是 Windows Update 升级到最新 Windows 10 (至少 Build 14316 )后，需要先在「设置」-「安全和更新」-「针对开发人员」选项卡中启用「开发人员模式」。

![启用或关闭 Windows 功能](/images/2017-04-15-bash-on-ubuntu-on-windows/A.png)

#### 开启 Bash for Windows ####

安装可以参考如下两种方式。

**方式 1 图形界面安装**

打开「控制面板」-「程序与功能」- 点击左侧的「启用或关闭 Windows 功能」- 在弹出的窗口中勾选「Windows subsystem for Linux(Beta)」组件进行安装。

![启用或关闭 Windows 功能](/images/2017-04-15-bash-on-ubuntu-on-windows/B.png)

**方式 2 命令行安装**

可以直接在 PowerShell 中执行如下命令启用 Windows subsystem for Linux 功能：

{% highlight HTML %}
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
{% endhighlight %}

__注:不论采用何种方式启用此功能，都需要重启系统之后才能生效。__

#### 使用 Bash on Ubuntu on Windows ####

在命令提示符中输入 bash, 即可进入 Bash on Ubuntu on Windows。

首次启用 Bash on Ubuntu on Windows 之后它会自动提示要下载安装 Ubuntu on Windows，只需敲 y 同意, 系统会自动从 Windows Store 中下载安装。


#### Bash on Ubuntu on Windows 文件存储的位置 ####

导航到以下目录以查找这些文件夹:  
%USERPROFILE%\AppData\Local\lxss 

Ubuntu 系统文件存储在:  
%USERPROFILE%\AppData\Local\lxss\rootfs 

您的 Ubuntu 用户帐户的主文件夹存储在:  
%USERPROFILE%\AppData\Local\lxss\home\USERNAME 

根帐户的主文件夹存储在:  
%USERPROFILE%\AppData\Local\lxss\root 

#### 在 Bash Shell 之外运行 Linux 命令 #### 

由于 Windows 与 Ubuntu「合体」这一先天优势，在 Bash on Ubuntu on Windows 环境之外其实也是可以执行 Linux 命令的，这一些都要归功于  bash -c 命令行，通过它我们可以直接在 CMD 或 PowerShell 中直接执行 Linux 命令：

{% highlight HTML %}
base -c "cat /proc/version"
{% endhighlight %}

**相关链接**  
https://www.sysgeek.cn/enable-bash-on-ubuntu-on-windows/  
https://www.sysgeek.cn/bash-on-ubuntu-on-windows-1/