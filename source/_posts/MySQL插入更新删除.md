---
title: MySQL插入删除
date: 2020-05-02 22:35:04
tags:
  - MySQL
categories:
  - MySQL
---

- 插入语句果指定的列和值的数量不一致会报错

  ```sql
  insert into rc_risk_check_prices (supplier, category,  price, created_at, updated_at) values (0, 1, 10);
  # Column count doesn't match value count at row 1
  ```

- 批量插入时如果列和值数量不一致会报错

  ```sql
   insert into rc_risk_check_prices (supplier, category,  price, created_at, updated_at) values (0, 1, 10, now(), now()), (1, 1, 20,now());
   #  Column count doesn't match value count at row 2
  ```

- 删除表的所有数据

  ```sql
  truncate table rc_risk_check_price; # 删除表后自动创建一个新的表
  ```

