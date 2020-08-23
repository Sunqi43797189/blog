---
title: scp命令操作
date: 2020-04-04 19:50:00
tags: 
  - Linux
categories:
  - Linux
---

- 从服务器下载文件
  scp username@servername:/path/filename /local/path
- 上传本地文件到服务器
  scp /local/path/local_filename username@servername:/path
- 从服务器下载整个目录
  scp -r username@servername:/path /path
- 上传目录到服务器
  scp  -r  /path  username@servername:/path
