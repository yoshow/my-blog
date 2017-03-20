---
layout: post
title:  "Windows 环境下安装 Protobuf"
date:   2016-07-01 20:00:00 +0800
categories: google protobuf
tags: google protobuf
---
#### 环境安装 ####  
1：下载CMake 
2:打开VS Command Prompt
3:修改工作目录到目标目录
cd C:\Path\to
4:创建编译完后 protobuf headers/libraries/binaries 将要安装的文件夹
 C:\Path\to>mkdir install
5：确保 'cmake' 命令可用，(如果不可用确保 把它加入到 path 环境变量中)
set PATH=%PATH%;D:\Program Files\cmake-3.5.2-win32-x86\bin
6：确保Git命令可用(如果不可用,添加到到 path 环境变量)
set PATH=%PATH%;D:\Program Files\Git\cmd
源设置
下载 packages https://github.com/google/protobuf/releases
把protobuf 放入  C:\Path\to 目标
cd  C:\Path\to\protobuf\cmake
CMake 配置
参考: Visual Studio Generators
注意:64位请用对应的 64位VS命令行
1:创建一个 build 目录，并且改变当前工作目录到build
mkdir build & cd build
------创建Release配置
C:\Path\to\protobuf\cmake\build>mkdir release & cd release
C:\Path\to\protobuf\cmake\build\release>cmake -G "NMake Makefiles" ^
-DCMAKE_BUILD_TYPE=Release ^
-DCMAKE_INSTALL_PREFIX=../../../../install ^
../..
------创建Debug 配置
C:\Path\to\protobuf\cmake\build>mkdir debug & cd debug
C:\Path\to\protobuf\cmake\build\debug>cmake -G "NMake Makefiles" ^
-DCMAKE_BUILD_TYPE=Debug ^
-DCMAKE_INSTALL_PREFIX=../../../../install ^
../..
-----创建Visual Studio 解决方案文件
C:\Path\to\protobuf\cmake\build>mkdir solution & cd solution
C:\Path\to\protobuf\cmake\build\solution>cmake -G "Visual Studio 11 2012 Win64" ^
-DCMAKE_INSTALL_PREFIX=../../../../install ^
-Dprotobuf_BUILD_TESTS=OFF ^
../..
备注
Generates Visual Studio 11 (VS 2012) project files.
Visual Studio 11 2012 Win64　　--Specify target platform x64.
Visual Studio 11 2012 ARM　　　--Specify target platform ARM.
Visual Studio 11 2012 <WinCE-SDK>  --Specify target platform matching a Windows CE SDK name.
Generates Visual Studio 12 (VS 2013) project files:
Visual Studio 12 2013 Win64  --Specify target platform x64.
Visual Studio 12 2013 ARM     --Specify target platform ARM.
 
Generates Visual Studio 14 (VS 2015) project files:
Visual Studio 11 2012 Win64  --Specify target platform x64.
Visual Studio 11 2012 ARM   --Specify target platform ARM.
Visual Studio 11 2012 <WinCE-SDK>  --Specify target platform matching a Windows CE SDK name.
编译
To compile protobuf:
C:\Path\to\protobuf\cmake\build\release>nmake
或者
C:\Path\to\protobuf\cmake\build\debug>nmake
或者
VS:打开生成的.sln 文件 即可。
如果出现如下错误:
 
 
修改Platform Toolset 即可

 
安装
To install protobuf to the specified *install* folder:
C:\Path\to\protobuf\cmake\build\release>nmake install
or
C:\Path\to\protobuf\cmake\build\debug>nmake install
 
或者编译VS解决方案中的“INSTALL”。
如果出现编译错误，尝试用管理员权限打开VS重新试试

定义消息体

package tutorial;

message Person {
  required string name = 1;
  required int32 id = 2;
  optional string email = 3;

  enum PhoneType {
    MOBILE = 0;
    HOME = 1;
    WORK = 2;
  }

  message PhoneNumber {
    required string number = 1;
    optional PhoneType type = 2 [default = HOME];
  }

  repeated PhoneNumber phone = 4;
}

message AddressBook {
  repeated Person person = 1;
}

编译生成对应library
c++：(protoc -I=$SRC_DIR --cpp_out=$DST_DIR $SRC_DIR/addressbook.proto)
 
protoc -I=. --cpp_out=. HookMessage.proto
 
 生成对应的 .h 和.cpp 文件
 
c#:(protoc -I=$SRC_DIR --csharp_out=$DST_DIR $SRC_DIR/addressbook.proto)
生成.cs 文件
 
c++项目使用
1:添加protobuf头文件：   protobuf下的Src (protobuf-3.0.0-beta-2\src)
 Property-->Configuration Properties-->c/c++-->General：Additional Include Directories

2:添加类库文件 (上面build出来的类库,如上例:C:\Path\to\protobuf\cmake\build\debug)
 Property-->Configuration Properties-->Linker-->General-->Additional Library Directories

在使用cpp文件顶部加上 
#pragma comment(lib, "libprotobufd.lib") 
#pragma comment(lib, "libprotocd.lib") 
build项目：
 
可能提示错误

该错误又由于 生成的类库和当前的项目使用的是不一样的 Runtime Library
修改如下配置即可: Property-->Configuration Properties-->c/c++-->Cide Generation-->Runtime Library( 　　Multi-threaded DLL (/MD)　　|　　Multi-threaded Debug (/MTd)  等)
 
C#项目使用
引用Google.Protobuf.dll        protobuf 源包中C#项目生成的DLL（需要打开项目自己编译生成）

**相关链接**  
[Windows 安装 Protobuf](http://www.cnblogs.com/grayguo/articles/5431856.html)