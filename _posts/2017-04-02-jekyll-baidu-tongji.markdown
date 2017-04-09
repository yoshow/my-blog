---
layout: post
title:  "Jekyll 添加百度统计功能"
date: 2017-04-02 20:00:00 +0800
tags: Jekyll Baidu
--- 

1.在 _include文件夹中新建文件 baidu-tongji.html，文件内容如下： 
{% highlight HTML %}
<script>
  var _hmt = _hmt || [];
  (function() {
    var hm = document.createElement("script");
    hm.src = "//hm.baidu.com/hm.js?{{ site.baidu_tongji }}";
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(hm, s);
  })();
</script>
{% endhighlight %}

2.在博客的入口网页合适位置添加如下代码
{% assign  specialSymbol = '{%' %}

{% highlight HTML %}
{{specialSymbol}} include baidu-tongji.html %}
{% endhighlight %}

Jekyll 的入口一般在 _layouts/default.html 中。

3.在 _config.yml 配置文件中添加如下配置:  
{% highlight HTML %}
# Baidu TongJi
baidu_tongji： xxxxxxxxxxxxxxxxxxxxxxxxxxx
{% endhighlight %}

*注:在 _config.yml 中不能有 tab，否则会提示‘found character that cannot start any token while scanning for the next token at line’的错误。*

然后执行   
{% highlight HTML %}
jekyll serve
{% endhighlight %}

本地 server 启动后访问 http://localhost:4000/

在百度统计的网站中心查看是否有访问记录。

**相关链接**  
[https://tongji.baidu.com](https://tongji.baidu.com)