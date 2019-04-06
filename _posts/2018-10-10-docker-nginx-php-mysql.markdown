---
layout:     post
title:      "实战Docker-nginx+php+mysql"
subtitle:   " \"使用已经存放在dockerhub上的镜像快速部署\""
date:       2018-10-10 12:41:00
author:     "Bin"
header-img: "img/post/bg/docker.svg"
catalog: true
tags:
    - Docker
---

> “docker 配置php+mysql+nginx. 待更新至更完美”


## Mysql容器运行
```bash
docker run -d --name mysql -p 3306:3306 \
           -v /services/mysql/data:/var/lib/mysql \
           -e MYSQL_ROOT_PASSWORD=my-secret-pw \
           angelhappyboy/mysql:5.7
```


## Php容器运行
```bash
docker run -d --name php72 \
           -v /services/nginx/wwwroot:/services/nginx/wwwroot \
           angelhappyboy/php:7.2-fpm
```

## Nginx容器运行
```bash
docker run -d -p 80:80 -p 443:443 --name nginx \
           -v /services/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
           -v /services/nginx/conf/vhosts.conf:/etc/nginx/vhosts.conf \
           -v /services/nginx:/services/nginx \
           --link php72 \
           angelhappyboy/nginx
```
