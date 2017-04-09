---
layout: post
title:  "ArcGIS Server 加载百度地图"
date: 2017-03-25 20:00:00 +0800
tags: ArcGIS Baidu
--- 

软件环境 ArcMap 10.1 + 太乐地图下载器 4.9

1.下载地图数据

打开太乐地图下载器

![选择百度地图](/images/2017-03-25-arcgis-baidu-map/A.png)

![选择下载区域](/images/2017-03-25-arcgis-baidu-map/B.png)

![填写任务名称](/images/2017-03-25-arcgis-baidu-map/C.png)

2.导出地图瓦片数据

选择任务右键选择 - 导出  
![选择任务](/images/2017-03-25-arcgis-baidu-map/D.png)

配置好参数之后，点击导出。  
![配置导出参数](/images/2017-03-25-arcgis-baidu-map/E.png)

将导出的目录下 v101\Layers 目录 拷贝到地图数据目录，比如：D:\map\重庆\渝北区，待后面创建地图的时候使用。

3.创建地图  

打开 ArcMap ，文件(F) - 新建 - 空白地图

目录窗口 - 文件夹连接 - 上下文菜单 - 连接到文件夹(C)...  
![连接到文件夹](/images/2017-03-25-arcgis-baidu-map/G.png)

内容列表 - 图层 - 上下文菜单 - 添加数据  
![添加数据](/images/2017-03-25-arcgis-baidu-map/H.png)

4.发布服务

菜单 - 文件(F) - 共享为(H) - 服务(S)...

![发布服务1](/images/2017-03-25-arcgis-baidu-map/I.png)

![发布服务2](/images/2017-03-25-arcgis-baidu-map/J.png)

![发布服务3](/images/2017-03-25-arcgis-baidu-map/K.png)

![发布服务4](/images/2017-03-25-arcgis-baidu-map/L.png)
