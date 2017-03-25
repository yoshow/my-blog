---
layout: post
title:  "Kafka 笔记"
date:   2017-03-12 20:00:00 +0800
categories: apache kafka
tags: Apache Kafka
---

#### 安装 Kafka #### 

1.下载 Kafka  
{% highlight bash %}
# cd /usr/local/src/
# wget http://mirror.bit.edu.cn/apache/kafka/0.10.2.0/kafka_2.11-0.10.2.0.tgz  
# tar -xzf kafka_2.11-0.10.2.0.tgz
{% endhighlight %}

剪切目录到 /opt/kafka  
{% highlight bash %}
# mv kafka_2.11-0.10.2.0 /opt/kafka
{% endhighlight %}


2.启动 zookeeper
{% highlight bash %}
# cd /opt/kafka
# bin/zookeeper-server-start.sh config/zookeeper.properties
{% endhighlight %}

3.启动 kafka
{% highlight bash %}
# in/kafka-server-start.sh config/server.properties
{% endhighlight %}

创建一个主题
{% highlight bash %}
# bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
# bin/kafka-topics.sh --list --zookeeper localhost:2181
{% endhighlight %}

发送消息
{% highlight bash %}
# bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
{% endhighlight %}

接收消息
{% highlight bash %}
# bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
{% endhighlight %}

#### 安装 Kafka Monitor ####
{% highlight bash %}
git clone https://github.com/linkedin/kafka-monitor.git
cd kafka-monitor 
./gradlew jar
{% endhighlight %}

./bin/kafka-monitor-start.sh config/kafka-monitor.properties

http://localhost:8000/index.html 

**相关链接**  
https://kafka.apache.org  
https://kafka.apache.org/quickstart  
https://github.com/linkedin/kafka-monitor