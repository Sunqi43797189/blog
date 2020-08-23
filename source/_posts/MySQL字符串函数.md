---
title: MySQL字符串函数
date: 2020-04-21 20:10:59
tags:
  - MySQL
categories:
  - MySQL
---

- 计算字符个数`char_length("char") `
- 计算字符串字节长度 `length("char")` utf-8 编码
- 连接字符串函数`concat("mysql", "5.7")`
  1. 多个字符串中任意一个或多个为null时，返回null
  2. 多个字符串中任意一个或多个为二进制字符串时返回二进制字符串
- 带分隔符的字符串连接，用逗号连接两个或多个字符串`concat_ws(",", "mysql", "5.7")`
  1. 如果分隔符为 null，则返回的结果是null
  2. 如果需要连接的字符串中有null时，拼接会忽略null值，继续拼接