---
title: hexo部署到服务器
date: 2020-04-09 23:40:28
tags:
  - hexo
categories:
  - hexo  
---

1. 安装nginx
2. 配置git文件
3. 修改hexo的 _config.yml配置

<!--more-->

- 安装nginx

- mkdir /var/www/blog

- Vim /etc/nginx/conf.d/blog.conf， 然后重启nginx

  > server {
  >     listen 80;
  >     server_name 你的域名;
  >     root /var/www/blog;
  > }

- mkdir ~/blog.git && cd ~/blog.git

- git init --bare

- vim blog.git/hooks/post-receive

  > #!/bin/bash
  >
  > rm -rf /var/www/blog
  > git clone /root/blog.git /var/www/blog

- chmod +x blog.git/hooks/post-receive

- 修改hexo_config.yml

  > deploy:
  >   type: 'git'
  >   repository: root@服务器ip地址:blog.git
  >   branch: master

