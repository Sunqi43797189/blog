---
title: MySQL基础
date: 2020-04-12 17:23:10
tags:
  - MySQL
categories:
  - MySQL  
---

## 大纲

- SQL语言类型定义
- SQL对数据库简单操作
- MySQL存储引擎

<!-- more -->

### SQL语言：对数据库进行查询和修改操作的语言

1. 数据定义语言 DDL: `drop create alter`
2. 数据操作语言 DML:` insert update delete`
3. 数据库查询语言 DQL: `select`
4. 数据库控制语言 DCL: `grant revoke commit rollback`

### SQL对数据库简单操作

1. 创建数据库     `create database test;`
2. 删除数据库 `drop database test;`
3. 查看数据库定义 `show create database test;` 数据库不存在会报错
4. 展示所有数据库 `show databases;`

### MySQL存储引擎

- 查看支持的引擎类型 `show engines;`
- 查看默认存储引擎`show VARIABLES like 'storage_engine';`
1. InnoDB
2. MyISAM
3. Memory
4. Merge
5. Archive
6. Federated
7. CSV
8. BLACKHOLE


