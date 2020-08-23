---
title: MySQl时间与条件判断函数
date: 2020-04-22 23:09:32
tags:
  - MySQL
categories:
  - MySQL

---

### 时间函数

- 获取当前日期函数`curdate() current_date()`

  > curdate(): 2020-04-22
  >
  > curent_date(): 2020-04-22 
  >
  > curdate() + 0: 20200422

- 获取当前时间函数 `curtime() current_time()`

  > curtime(): 23:16:53
  >
  > current_time(): 23:16:53
  >
  > curtime() + 0: 231653

- 获取当前日期和时间函数`current_timestamp()`, `now()`, `localtime()`, `sysdate()`

  > `current_timestamp()`: 2020-04-22 23:19:36
  >
  > `now()`: 2020-04-22 23:19:13
  >
  > `localtime()`: 2020-04-22 23:20:16
  >
  > `sysdate()`: 2020-04-22 23:21:03

- unix时间戳函数 `unix_timestamp(date)`

  > unix_timestamp(): 返回当前时间时间戳, 1587569265
  >
  > unix_timestamp("20200422"): 1587484800

- 时间戳转时间函数 `from_unixtime(timestamp)`

- 时间和秒钟转换函数`time_to_sex("23:23:23")`, `sec_to_time(1111)`

- utc时间与utc日期函数 `UTC_DATE()` `UTC_TIME`

### 条件判断函数

- `if(expr, v1, v2)` 如果expr为true（e x p r <> 0 and expr <> null），返回v1，否则返回v2

- `ifnull(v1, v2)`如果v1 不为null，返回v1，否则返回v2

- `case`函数

  ```sql
  select case 2 when 1 then 'one' when 2 then 'two' else 'more' end;
  select case when 1 < 2 then '小于' else '大于' end;
  ```

  

