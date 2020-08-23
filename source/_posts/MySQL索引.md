---
title: MySQL索引
date: 2020-05-02 22:50:41
tags:
  - MySQL
categories:
  - MySQL
---

### MySQL索引分类

- `普通索引`：允许在定义索引的列中插入重复值和空值
- `唯一索引`：索引列的值必须唯一，允许有空值
- `单列索引`：一个索引只包含单个列，一个表可以有多个单列索引
- `组合索引`：在表的多个字段组合上创建的索引，只有在查询条件中使用了这些字段的左边字段时，索引才会被使用。使用组合索引时遵循最左前缀集合
- `全文索引`：索引类型为FULLTEXT，在定义索引的列上支持值的全文查找，允许在这些索引列中插入重复值和空值。全文索引可以CHAR, VARCHAR, TEXT类型上创建，只有MyISAM存储引擎支持。
- `空间索引`：空间索引时对空间数据类型的字段建立的索引，MySQL中的空间数据类型有4种，分别是GEOMETRY, POINT, LINESTRING, POLYGON。创建空间索引的列，必须将其声明为not null，使用 SPATIAL进行声明，只有MyISAM存储引擎支持。

<!-- more -->

### 建表时创建索引

- 创建表时创建索引
  
  ```sql
  create table table_name [ col_name data_type]
  [ UNIQUE|FULLTEXT|SPATIAL ] [ INDEX|KEY ] [ INDEX_NAME ] (col_name [length]) [ ASC|DESC ]
  ```
  
  只有字符串类型的字段才能指定索引的长度，ASC或DESC指定升序或者降序存储索引值

- 创建普通索引，两种方式
  
  ```sql
  create table books(
    book_id int not null,
    author_id int not null,
    year_publication year not null,
    INDEX(year_publication),
    Key author_id (author_id)
  );
  ```

- 创建唯一索引
  
  ```sql
  create table books(
    book_id int not null,
    author_id int not null,
    year_publication year not null,
    unique INDEX(year_publication),
    unique Key author_id (author_id)
  );
  ```

- 创建组合索引
  
  ```sql
  create table books(
    book_id int not null,
    author_id int not null,
    year_publication year not null,
    unique index book_id_and_author_id(book_id, author_id),
    unique key book_id_and_year_publication (book_id, year_publication)
  );
  ```

### 已经存在的表上创建索引

- 使用 `alter table` 语句创建索引
  
  ```sql
  alter table books add unique index authod_id_and_year_publication ( author_id, year_publication );
  ```

- 使用 `create index` 语句创建索引
  
  ```sql
  create unique index authod_id_and_year_publication on books ( author_id, year_publication )
  ```

### 删除索引

- 使用 `alter table` 删除索引
  
  ```sql
  alter table books drop index book_id_and_author_id;
  ```

- 使用`drop index` 删除索引
  
  ```dql
  drop index book_id_and_year_publication on books;
  ```


