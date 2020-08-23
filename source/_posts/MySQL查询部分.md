---
title: MySQL查询部分
date: 2020-04-23 20:30:33
tags:
  - MySQL
categories:
  - MySQL
---

- 基本查询
- 分组查询
- 子查询
- 合并多个结果

<!-- more -->

### 基本查询

- select ` in ` 操作速度要快于 ` or ` 操作
- `and`的优先级高于`or`

### 分组查询

- 分组查询合并字段 `group_concat(name)`

- 在group by 之后添加`with rollup`可以统计查询返回的记录数的总和

- 多字段分组，分组层次从左到右，先按照第一个字段进行分组，然后对结果第二个字段进行分组，依次类推

  ```sql
  select like_count , member_id, GROUP_CONCAT(content) as content, count(*) as total from moments where like_count is not null group by member_id, like_count HAVING like_count > 5 ORDER BY total;
  ```

- `count(*)`计算时，不管某列有数值或者为空值

- `count(cloumn_name)`计算时会忽略空值null

  ```sql
  select member_id, sum(like_count) as num from moments where like_count is not null group by member_id having sum(like_count) > 10 order by num ;
  ```

### 子查询

- 子查询`any`关键字，表示若与子查询返回的任何值比较为true，则返回true,

  ```sql
  create table tbl1 (num1 int not null);
  create table tbl2 (num2 int not null);
  select num1 from tbl1 where num1 > any ( select num2 from tbl2 ); 只要num1大于自查询返回的结果中的任意一个之都会返回true
  ```

- 子查询`all`关键字，表示若值与子查询的所有结果比较都为true则返回true

  ```sql
  select num1 from tbl1 where num1 > all ( select num2 from tbl2 ); num1 需要大于num2的所有值 
  ```

- 子查询`exists` 关键字，系统对自查询进行运算以判断它是否返回记录，至少返回1行，那么exists结果为true，外层查询将继续进行

  ```sql
  select num1 from tbl1 where exists ( select num2 from tbl2 where num2 > 100 );
  ```

- 子查询`in`关键字，内层子查询仅返回一个数据列，这个数据列里的值将提供给外层查询语句进行比较操作，反之`not in`

  ```sql
  select * from members where id in ( select member_id from pictures where status = 0 );
  ```

### 合并查询结果

- `union` 可以对多条select语句的结果进行合并，要求多个select的结果对应的列数和数据类型必须相同，执行的时候会删除重复的记录
- `union all` 使用时不会删除重复结果，也不会对结果进行自动排序