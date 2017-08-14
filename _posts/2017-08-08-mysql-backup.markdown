---
layout: post
title:  "XtraBackup 备份 MySQL 增量备份和全量备份脚本"
date: 2017-08-08 08:00:00 +0800
tags: ["MySQL"]
--- 

#### 测试环境 ####   

操作系统 CentOS 7.2  
MySQL 5.7


#### 安装 Xtrabackup ####   

{% highlight bash %}
cd /usr/local/src

wget https://www.percona.com/downloads/XtraBackup/Percona-XtraBackup-2.4.4/\
binary/redhat/7/x86_64/percona-xtrabackup-24-2.4.4-1.el7.x86_64.rpm

yum localinstall percona-xtrabackup-24-2.4.4-1.el7.x86_64.rpm
{% endhighlight %}

### 创建备份帐号 

{% highlight SQL %}
CREATE USER 'xtrabackup'@'localhost' IDENTIFIED BY 'xtra$password';
GRANT SELECT, SHOW VIEW, RELOAD, LOCK TABLES, PROCESS, REPLICATION 
CLIENT ON *.* TO 'xtrabackup'@'localhost';
FLUSH PRIVILEGES;
{% endhighlight %}

#### 设置备份环境 ####  
设置需要的目录
{% highlight bash %}
mkdir /usr/local/xtrabackup \
/usr/local/xtrabackup/bash \
/usr/local/xtrabackup/base \
/usr/local/xtrabackup/full \
/usr/local/xtrabackup/incremental 
{% endhighlight %}

#### 全量备份脚本 ####  
vi /usr/local/xtrabackup/bash/mysql-base-backup

{% highlight bash %}
#!/bin/bash
# Program
#  use xtasback to fully backup mysql data per week!

# 帐号
user=xtraback
# 密码
password=xtra@password
# 需要备份的数据库
# database=test_db
# MySQL Socket File
defaults_file=/etc/my.cnf
# MySQL Socket File
socket=/usr/local/mysql/mysql.sock
# 备份的文件位置
basedir=/usr/local/xtrabackup/base/

/usr/bin/innobackupex --defaults-file=${defaults_file} \
--user=$user --password=${password} --socket=${socket} --no-lock ${basedir}

{% endhighlight %}

#### 全量还原脚本 ####  
vi /usr/local/xtrabackup/bash/mysql-base-restore

{% highlight bash %}
#!/bin/bash
# Program
#  use xtasback to fully backup mysql data per week!

# 备份的文件位置 需要根据实际情况修改
basedir=/usr/local/xtrabackup/base/2017-08-10_03-00-00

mysql_daemon=/usr/local/mysql/mysqld

mysql_data_dir=/usr/local/mysql/data

$mysql_daemon stop

rm -rf $mysql_data_dir/*

innobackupex --copy-back $basedir

chown -R mysql:mysql $mysql_data_dir/*

$mysql_daemon start

{% endhighlight %}

#### 增量备份脚本 ####  
vi /usr/local/xtrabackup/bash/mysql-incremental-backup

{% highlight bash %}
#!/bin/bash
# Program
#  use xtasback to incremental backup mysql data per week!

# 帐号
user=xtraback
# 密码
password=xtra@password
# 需要备份的数据库
# MySQL Socket File
defaults_file=/etc/my.cnf
# MySQL Socket File
socket=/usr/local/mysql/mysql.sock
# 备份的文件位置
basedir=/usr/local/xtrabackup/base/
# 增量备份文件位置
incremental=/usr/local/xtrabackup/incremental/

# 最新的备份文件位置
cd ${basedir}

latest_basedir=''
for dir in `ls -t`;
do
 [ -d $dir ] && latest_basedir=$dir && break;
done;

# 完整备份的位置
incremental_basedir=${basedir}/$latest_basedir

# 调试命令
innobackupex --defaults-file=${defaults_file} --user=$user --password=${password} \
--socket=$socket --incremental-basedir=${incremental_basedir} --incremental ${incremental}
{% endhighlight %}


#### 增量备份脚本 ####  
增量还原和全量还原使用的命令是一样的

{% highlight bash %}
innobackupex --copy-back /path/to/BACKUP-DIR
{% endhighlight %}

vi /usr/local/xtrabackup/bash/mysql-incremental-merge

{% highlight bash %}
#!/bin/bash
# Program
#  use xtasback to incremental backup mysql data per week!

# 帐号
user=xtraback
# 密码
password=xtra@password
# 需要备份的数据库
# MySQL Socket File
defaults_file=/etc/my.cnf
# MySQL Socket File
socket=/usr/local/mysql/mysql.sock
# 备份的文件位置
basedir=/usr/local/xtrabackup/base/
# 增量备份文件位置
incremental=/usr/local/xtrabackup/incremental/

# 最新的备份文件位置
cd ${basedir}

latest_basedir=''
for dir in `ls -t`;
do
 [ -d $dir ] && latest_basedir=$dir && break;
done;

# 完整备份的位置
incremental_basedir=${basedir}/$latest_basedir

# 调试命令
innobackupex --defaults-file=${defaults_file} --user=$user --password=${password} \
--socket=$socket --incremental-basedir=${incremental_basedir} --incremental ${incremental}
{% endhighlight %}

#### 定时任务设置 #### 

{% highlight Bash %}
crontab -e
{% endhighlight %}
 
添加如下内容
{% highlight Bash %}
#每个星期日凌晨3:00执行完全备份脚本
0 3 * * 0 /usr/local/xtrabackup/bash/mysql-base-backup. >/dev/null 2>&1
#周一到周六凌晨3:00做增量备份
0 3 * * 1-6 /usr/local/xtrabackup/bash/mysql-incremental-backup >/dev/null 2>&1
#每个星期日凌晨4:00执行清理备份脚本
0 4 * * 0 /usr/local/xtrabackup/bash/mysql-clear-backup. >/dev/null 2>&1
{% endhighlight %}

相关的源码  
https://github.com/yoshow/percona-xtrabackup-scripts

**相关链接**  
[CentOS 安装 xTrabackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation/yum_repo.html)  
[innobackupex 使用手册](https://www.percona.com/doc/percona-xtrabackup/2.4/innobackupex/innobackupex_script.html)
