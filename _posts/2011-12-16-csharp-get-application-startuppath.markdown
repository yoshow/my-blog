---
layout: post
title:  ".NET 获得应用程序路径的方法(C# 版)"
date:   2011-12-16 20:00:00 +0800
tags: [".NET"]
---

#### 获取文件的路径 ####

System.Windows.Forms.Application.StartupPath

//获取包含清单的已加载文件的路径或 UNC 位置。
System.AppDomain.CurrentDomain.SetupInformation.ApplicationBase

public static string sApplicationPath = Assembly.GetExecutingAssembly ( ).Location;

//result: X:xxxxxxxxx.dll (.dll文件所在的目录+.dll文件名)

//获取当前进程的完整路径，包含文件名(进程名)。

this.GetType ( ).Assembly.Location;

//result: X:xxxxxxxxx.exe (.exe文件所在的目录+.exe文件名)

//获取新的 Process 组件并将其与当前活动的进程关联的主模块的完整路径，包含文件名(进程名)。

System.Diagnostics.Process.GetCurrentProcess ( ).MainModule.FileName;

//result: X:xxxxxxxxx.exe (.exe文件所在的目录+.exe文件名)

//获取和设置当前目录（即该进程从中启动的目录）的完全限定路径。

System.Environment.CurrentDirectory;

//result: X:xxxxxx (.exe文件所在的目录)

//获取当前 Thread 的当前应用程序域的基目录，它由程序集冲突解决程序用来探测程序集。

System.AppDomain.CurrentDomain.BaseDirectory;

//result: X:xxxxxx (.exe文件所在的目录+””)

//获取和设置包含该应用程序的目录的名称。

System.AppDomain.CurrentDomain.SetupInformation.ApplicationBase;

//result: X:xxxxxx (.exe文件所在的目录+””)

//获取启动了应用程序的可执行文件的路径，不包括可执行文件的名称。

System.Windows.Forms.Application.StartupPath;

//result: X:xxxxxx (.exe文件所在的目录)

//获取启动了应用程序的可执行文件的路径，包括可执行文件的名称。

System.Windows.Forms.Application.ExecutablePath;

//result: X:xxxxxxxxx.exe (.exe文件所在的目录+.exe文件名)

//获取应用程序的当前工作目录(不可靠)。

System.IO.Directory.GetCurrentDirectory ( );

//result: X:xxxxxx (.exe文件所在的目录)

在系统服务中最好用这个方式去取路径

string stmp = Assembly.GetExecutingAssembly ( ).Location;

stmp = stmp.Substring ( 0 , stmp.LastIndexOf ( \ ) );//删除文件名

if ( pathType == 1 )

return stmp + @”inputLog.xml”;

else if ( pathType == 2 )

return stmp + @”MiddleDB.xml”;

else

return stmp + @”AppNo.xml”;

using System.IO;

string path = “d:asdfasdf.bmp”;

string fileName = Path.GetFileName(path); //文件名

string ext = Path.GetExtension(path); //扩展名

#### 获取当前路径 ####

1.System.Diagnostics.Process.GetCurrentProcess().MainModule.FileName － 获取模块的完整路径。

2.System.Environment.CurrentDirectory － 获取和设置当前目录(该进程从中启动的目录)的完全限定目录。

3.System.IO.Directory.GetCurrentDirectory() － 获取应用程序的当前工作目录。这个不一定是程序从中启动的目录，有可能程序放在C:xxx里,这个函数有可能返回C:Documents and SettingsYB,或者C:Program FilesAdobe,有时不一定返回什么。

4.System.AppDomain.CurrentDomain.BaseDirectory － 获取程序的基目录。

5.System.AppDomain.CurrentDomain.SetupInformation.ApplicationBase － 获取和设置包括该应用程序的目录的名称。

6.System.Windows.Forms.Application.StartupPath － 获取启动了应用程序的可执行文件的路径。效果和2、5一样。只是5返回的字符串后面多了一个””而已

7.System.Windows.Forms.Application.ExecutablePath － 获取启动了应用程序的可执行文件的路径及文件名，效果

#### 路径相关操作 ####

1、判定一个给定的路径是否有效,合法  
通过 Path.GetInvalidPathChars或Path.GetInvalidFileNameChars方法获得非法的路径/文件名字符，可以根据它来判断路径中是否包含非法字符；

2、如何确定一个路径字符串是表示目录还是文件  
使用Directory.Exists或File.Exist方法，如果前者为真，则路径表示目录；如果后者为真，则路径表示文件
上面的方法有个缺点就是不能处理那些不存在的文件或目录。这时可以考虑使用Path.GetFileName方法获得其包含的文件名，如果一个路径不为空，而文件名为空那么它表示目录，否则表示文件；

3、获得路径的某个特定部分  
Path.GetDirectoryName ：返回指定路径字符串的目录信息。
Path.GetExtension ：返回指定的路径字符串的扩展名。
Path.GetFileName ：返回指定路径字符串的文件名和扩展名。
Path.GetFileNameWithoutExtension ：返回不具有扩展名的路径字符串的文件名。
Path.GetPathRoot ：获取指定路径的根目录信息。

4、准确地合并两个路径而不用去担心那个烦人的“\”字符  
使用Path.Combine方法，它会帮你处理烦人的“\”。

5、获得系统目录的路径  
Environment.SystemDirectory属性：获取系统目录的完全限定路径
Environment.GetFolderPath方法：该方法接受的参数类型为Environment.SpecialFolder枚举，通过这个方法可以获得大量系统    文件夹的路径，如我的电脑，桌面，系统目录等
Path.GetTempPath方法：返回当前系统的临时文件夹的路径

6、判断一个路径是绝对路径还是相对路径  
使用 Path.IsPathRooted 方法

7、读取或设置当前目录  
使用 Directory 类的 GetCurrentDirectory 和 SetCurrentDirectory 方法

8、使用相对路径  
设置当前目录后（见上个问题），就可以使用相对路径了。对于一个相对路径，我们可以使用 Path.GetFullPath 方法获得它的完全限定路径（绝对路径）。
注意：如果打算使用相对路径，建议你将工作目录设置为各个交互文件的共同起点，否则可能会引入一些不易发现的安全隐患，被恶意用户利用来访问系统文件。

9、文件夹浏览对话框（FolderBrowserDialog类）
主要属性： Description：树视图控件上显示的说明文本，如上图中的“选择目录–练习”；RootFolder：获取或设置从其开始浏览的根文件夹，如上图中设置的我的电脑（默认为桌面）；SelectedPath：获取或设置用户选定的路径，如果设置了该属性，打开对话框时会定位到指定路径，默认为根文件夹，关闭对话框时根据该属性获取用户用户选定的路径；         ShowNewFolderButton：获取或设置是否显示新建对话框按钮；
主要方法： ShowDialog：打开该对话框，返回值为DialogResult类型值，如果为DialogResult.OK，则可以由SelectedPath属性获取用户选定的路径；
