---
title: Docker常用命令
date: 2020-05-30 22:16:48
tags: 
  - Docker
categories: 
  - Docker
---

- 删除镜像:  `docker rmi image_id`
- 删除容器:  `docker rm 容器ID`
- 进入运行中的容器 `docker attach centos`,再次使用命令进入容器使，两个窗口内容同步显示
- 进入一个容器的bash:  `docker exec -it mysql /bin/bash`
- 查看容器状态:  `docker stats`
- 列出运行中的容器:  `docker ps`
- 列出所有容器:  `docker ps -a`
- 列出所有镜像: `docker images`
- 后台运行centos :  `docker run -d --name centos -it centos:7 /bin/bash`
- 进入后台运行的容器后输入exit会退出容器，` ctrl + p + q `退出
- 容器间单向通信（不使用IP地址通信)用link把想要通信的容器连接 `docker run -d --name ubuntu -it --link centos7 centos:7 /bin/bash`
- docker 底层网络服务明细 `docker network ls`
- docker 添加一个新的网桥，用于容器间双向通信` docker network create -d bridge my_bridge`
- `docker network connect my_bridge centos` 将容器绑定到网桥上
- 查看一个容器的信息 `docker inspect docker-redis`
- 清除临时镜像文件`docker image prune -a`,会清楚所有临时和处于停止状态的容器
- 进入运行中的容器 `docker attach centos`,再次使用命令进入容器使，两个窗口内容同步显示