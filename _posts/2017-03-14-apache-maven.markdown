---
layout: post
title: "Maven 笔记"
date: 2017-03-14 20:00:00 +0800
tags: Apache Maven
---
#### Maven常用命令 ####  

**查看 Maven 版本信息**  
```
mvn -v
``` 

**显示详细错误 信息。**  
```
mvn -e
```  

**创建 Maven 的普通 JAVA 项目**  

{% highlight HTML %}
mvn archetype:create 
 -DgroupId=packageName 
 -DartifactId=projectName
{% endhighlight %}

mvn archetype:create -DgroupId=org.sonatype.mavenbook.ch03 -DartifactId=simple -DpackageName=org.sonatype.mavenbook 

**创建 Maven 的Web项目**

{% highlight HTML %}
mvn archetype:create 
  -DgroupId=packageName 
  -DartifactId=webappName 
  -DarchetypeArtifactId=maven-archetype-webapp  
{% endhighlight %}

**编译源代码**  
```
mvn compile
``` 

**编译源代码并打成 war 包**  
```
mvn compile war:war  
```

**编译源代码并打成 jar 包**  
```
mvn compile jar:jar  
```

**编译测试代码**  
```
mvn test-compile
```

**运行测试**  
```
mvn test
```

**产生site**  
```
mvn site
```

**打包**  
```
mvn package
```   

**在本地 Repository 中安装jar：**  
```
mvn install 
```

**清理产生的项目**  
```
mvn clean   
```

**清理再编译**  
```
mvn clean install 
```

**将项目转化为 Eclipse 项目**  
```
mvn eclipse:eclipse  
```

**清除 Eclipse 的一些系统设置**  
```
mvn eclipse:clean 
```

**生成 IDEA 项目**  
```
mvn idea:idea  
```

**组合使用 goal 命令，如只打包不测试**  
```
mvn package -Dtest   
```

**只打 jar 包**  
```
mvn jar:jar  
```

**只测试而不编译，也不测试编译**  

{% highlight HTML %}
mvn test -skipping compile -skipping test-compile 
      ( -skipping 的灵活运用，当然也可以用于其他组合命令) 
{% endhighlight %}

**插件让我们能够在不往 classpath 载入适当的依赖的情况下，运行这个程序**   
```
mvn exec:java -Dexec.mainClass=org.sonatype.mavenbook.weather.Main Exec 
```

**打印整个依赖树**  
```
mvn dependency:tree 
```

**打印出已解决依赖的列表**  
```
mvn dependency:resolve
```

**想要查看完整的依赖踪迹，包含那些因为冲突或者其它原因而被拒绝引入的构件，打开 Maven 的调试标记运行**  
```
mvn install -X 
```

**给任何目标添加 maven.test.skip 属性就能跳过测试**  
```
mvn install -Dmaven.test.skip=true
```

**构建装配 Maven Assembly 插件是一个用来创建你应用程序特有分发包的插件**  
```
mvn install assembly:assembly 
```

**调用 Jetty 插件的 Run 目标在 Jetty Servlet 容器中启动 web 应用**   
```
mvn jetty:run     
```

**使用 Hibernate3 插件构造数据库**  
```
mvn hibernate3:hbm2ddl 
```

**验证工程是否正确，所有需要的资源是否可用。**  
```
mvn validate
```

**在集成测试可以运行的环境中处理和发布包。**  
```
mvn integration-test 
```

**运行任何检查，验证包是否有效且达到质量标准。**     
```
mvn verify                
```

**产生应用需要的任何额外的源代码，如 xdoclet。**  
```
mvn generate-sources
```     

**把 jar 包部署到 mvn 仓库**  

{% highlight HTML %}
mvn deploy:deploy-file 
-DgroupId=com 
-DartifactId=client 
-Dversion=0.1.0 
-Dpackaging=jar 
-Dfile=d:/client-0.1.0.jar 
-DrepositoryId=maven-repository-inner 
-Durl=ftp://xxxxxxx/opt/maven/repository/
{% endhighlight %}

#### Maven help 命令 ####  

使用 help 插件的  describe 目标来输出 Maven Help 插件的信息。  
```
mvn help:describe -Dplugin=help
```  

使用Help 插件输出完整的带有参数的目标列  
```
mvn help:describe -Dplugin=help -Dfull   
```

获取单个目标的信息, 设置 mojo 参数和 plugin 参数。此命令列出了 Compiler 插件的 compile 目标的所有信息  
```
mvn help:describe -Dplugin=compiler -Dmojo=compile -Dfull 
```

列出所有 Maven Exec 插件可用的目标  
```
mvn help:describe -Dplugin=exec -Dfull  
```

看这个“有效的 (effective)”POM，它暴露了 Maven 的默认设置  
```
mvn help:effective-pom 
```

#### 发布第三方Jar到本地库中 #### 

{% highlight HTML %}
mvn install:install-file 
-DgroupId=com 
-DartifactId=client 
-Dversion=0.1.0 
-Dpackaging=jar 
-Dfile=d:/client-0.1.0.jar
-DdownloadSources=true
-DdownloadJavadocs=true
{% endhighlight %}

#### 在应用程序用使用多个存储库 #### 
{% highlight xml %}
<repositories>    
  <repository>      
    <id>Ibiblio</id>      
    <name>Ibiblio</name>      
    <url>http://www.ibiblio.org/maven/</url>    
  </repository>    
  <repository>      
    <id>PlanetMirror</id>      
    <name>Planet Mirror</name>      
    <url>http://public.planetmirror.com/pub/maven/</url>    
  </repository>  
</repositories>
{% endhighlight %}

**一般使用情况是这样，首先通过 cvs 或 svn 下载代码到本机，然后执行 mvn eclipse:eclipse 生成 Ecllipse 项目文件，然后导入到 Eclipse 就行了；修改代码后执行mvn compile 或 mvn test 检验，也可以下载 eclipse 的 maven 插件。**

mvn -version                                                      | 显示版本信息 
mvn archetype:create -DgroupId=com.x3platform -DartifactId=myapp  | 创建mvn项目
mvn package                                                       | 生成target目录，编译、测试代码，生成测试报告，生成jar/war文件 
mvn jetty:run                                                     | 运行项目于jetty上, 
mvn compile                                                       | 编译 
mvn test                                                          | 编译并测试 
mvn clean                                                         | 清空生成的文件 
mvn site                                                          | 生成项目相关信息的网站 
mvn eclipse:eclipse -Dwtpversion=1.0                              | 生成Wtp插件的Web项目 
mvn eclipse:clean -Dwtpversion=1.0                                | 清除 Eclipse 项目的配置信息(Web项目) 

<br/>   
   
**相关链接**  
[http://maven.apache.org](http://maven.apache.org)  
[http://www.cnblogs.com/grayguo/articles/5431856.html](http://www.cnblogs.com/grayguo/articles/5431856.html)    
[http://blog.csdn.net/lifxue/archive/2009/10/14/4662902.aspx](http://blog.csdn.net/lifxue/archive/2009/10/14/4662902.aspx)  