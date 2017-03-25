---
layout: post
title:  "MySQL 设置注释信息"
date:   2014-09-17 08:00:00 +0800
categories: MySQL
tags: MySQL
---

#### 1 创建表的时候写注释

<pre><code>create table {TableName}
(
  field_name int comment '字段的注释'
) comment='表的注释';
</code></pre>

#### 2 修改表的注释

<code>
alter table {TableName} comment '修改后的表的注释';
</code>

#### 3 修改字段的注释

<pre><code>-- 注意：字段名和字段类型照写就行  
alter table {TableName} modify column field_name int comment '修改后的字段注释';
</code></pre>

#### 4 查看表注释的方法
<pre><code>-- 在生成的SQL语句中看  
show create table {TableName};
</code></pre>

<pre><code>-- 在元数据的表里面看  
use information_schema;

select * from TABLES where TABLE_SCHEMA='{DatabaseName}' and TABLE_NAME='{TableName}'
</code></pre>

#### 5 查看字段注释的方法
<pre><code>-- show columns  
show full columns from {TableName};

-- 在元数据的表里面看  
select * from COLUMNS where TABLE_SCHEMA='{DatabaseName}' and TABLE_NAME='{TableName}'
</code></pre>
