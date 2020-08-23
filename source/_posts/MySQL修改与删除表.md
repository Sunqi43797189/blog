---
title: SQL修改与删除表
date: 2020-04-16 22:50:20
tags:
  - MySQL
categories:
  - MySQL
---

1. 查看表结构 `desc table test;`
2. 查看建表语句 `show create table test;`
3. 修改表名 `alter table old_name rename to new_name;`
4. 修改表的某一个字段类型 `alter table test modify age int(11);`
5. 修改表的字段名 `alter table test change age nianling int(11);`
6. 添加字段 `alter table test add name varchar(11);`
7. 添加具有约束的字段 `alter table test add name varchar(11) not null;`
8. 在第一列添加一个字段 `alter table test add phone varchar(11) not null first;`
9. 在某一个列的后边添加一个字段 `alter table test add address varchar(128) after name;`
10. 删除一个字段 `alter table test drop column address;`
11. 修改表的字段位置 `first`和`after` 
    - `alter table test modify id int first;`
    - `alter table test modify name varchar(11) after id;`
12. 更改表的存储引擎 `alter table test engine=InnoDB;`
13. 删除表 `drop table if exists test;`
14. 删除表 `truncate table test;` drop表可以通过日志进行恢复，truncate彻底删除