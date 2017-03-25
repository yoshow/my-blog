---
layout: post
title:  "Eclipse 构建 Spring MVC 项目"
date: 2017-03-21 20:00:00 +0800
categories: eclipse maven spring
tags: Eclipse Maven Spring
--- 
   
1.创建新的 Maven 项目

mvn archetyp:create 
  -DarchetypeArtifactId=maven-archetype-webapp
  -DgroupId=com.x3platform 
  -DartifactId=myapp

2.生成 Eclipse 项目

mvn eclipse:eclipse

3.设置 Project Feats

4.赋予工程的 springmvc 特性

配置 web.xml，使其具有 springmvc 特性，主要配置两处，一个是 ContextLoaderListener，一个是 DispatcherServlet。代码如下：　　

{% highlight XML %}
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <servlet>
        <servlet-name>exam</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>exam</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
</web-app>
{% endhighlight %}

配置ContextLoaderListener表示，该工程要以spring的方式启动。启动时会默认在/WEB-INF 目录下查找 applicationContext.xml 作为 spring 容器的配置文件，这里可以初始化一些 bean，如 DataSource。我们这里什么也不做。代码如下：
exam-servlet.xml

{% highlight XML %}
<?xml version="1.0" encoding="UTF-8"?>
<!-- Bean头部 -->
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:mvc="http://www.springframework.org/schema/mvc" 
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:util="http://www.springframework.org/schema/util"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd  
            http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd  
            http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd              
            http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd">
    
    <!-- 激活@Controller模式 -->
    <mvc:annotation-driven />
    <!-- 对包中的所有类进行扫描，以完成Bean创建和自动依赖注入的功能 需要更改 -->
    <context:component-scan base-package="cc.monggo.web.controller" />

    <bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter" />

    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix">
            <value>/WEB-INF/jsp/</value>
        </property>
        <property name="suffix">
            <value>.jsp</value>
        </property>
    </bean>
</beans>
{% endhighlight %}

5.让 maven 自动配置 jar 包

在用 maven 生成框架时，就生成了 pom.xml，这就是 maven 的配置文件。我们要引入spring-web, servlet 等特性的包。代码如下：

{% highlight XML %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.x3platform</groupId>
  <artifactId>myapp</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>myapp Maven Webapp</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>3.0.5.RELEASE</version>
    </dependency>
    
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>3.0.5.RELEASE</version>
    </dependency>
    
    <dependency>
        <groupId>org.apache.geronimo.specs</groupId>
        <artifactId>geronimo-servlet_2.5_spec</artifactId>
        <version>1.2</version>
    </dependency>
            
  </dependencies>
  <build>
    <finalName>myapp</finalName>
  </build>
</project>
{% endhighlight %}

maven 就是这么简单，一旦保存，maven 就会自动下载 pom.xml 的 jar 包。此时可以看到目录中 Maven Dependencies下生成了 jar 包。

　　更多的 jar 包可以在 maven 中心库下载：http://mvnrepository.com。

6.测试代码

　　说了一大堆，只有运行起来才有意思，下面写个简单的测试。先写Controller。编写两个类，LoginControler.java，LoginForm.java。代码如下：
LoginController.java

{% highlight Java %}
package cc.monggo.web.controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

import cc.monggo.domain.LoginForm;

@Controller
public class LoginController {
    @RequestMapping(value="login")
    public ModelAndView login(HttpServletRequest request,HttpServletResponse response,LoginForm command ){
        String username = command.getUsername();
        ModelAndView mv = new ModelAndView("/index/index","command","LOGIN SUCCESS, " + username);
        return mv;
    }
}
{% endhighlight %}

LoginForm.java

{% highlight Java %}
package cc.monggo.domain;

public class LoginForm {
    private String username;
    private String password;
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
}
{% endhighlight %}

再增加一些jsp,首页的index.jsp,主要是做跳转，代码如下：
<%
    request.getRequestDispatcher("/WEB-INF/jsp/login/login.jsp").forward(request,response);
%>
　  还有两个jsp，做些简单的功能，一个表单login.jsp,一个表单提交的返回index.jsp，代码如下：
login.jsp
{% highlight HTML %}
<%@ page language="java" contentType="text/html; charset=utf-8" pageEncoding="utf-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>Insert title here</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
    <div>
        <form action="login" methed="get">
            <input type="text" name="username">
            <input type="submit" value="SUBMIT">
        </form>
    </div>
</body>
</html>
{% endhighlight %}

index.jsp
{% highlight HTML %}
<%@ page language="java" contentType="text/html; charset=utf-8" pageEncoding="utf-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>首页</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
    ${command}
</body>
</html>
{% endhighlight %}

最后整个项目的目录结构如下:


**相关链接**  
[Eclipse maven构建springmvc项目](http://www.cnblogs.com/fangjins/archive/2012/05/06/2485459.html)  
