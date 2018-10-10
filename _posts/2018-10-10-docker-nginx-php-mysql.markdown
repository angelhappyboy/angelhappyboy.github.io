---
layout:     post
title:      "实战Docker-nginx+php+mysql"
subtitle:   " \"使用DockerFile建立自己的镜像\""
date:       2018-10-10 12:41:00
author:     "Bin"
header-img: "img/post/bg/docker.svg"
catalog: true
tags:
    - Docker
---

> “Yeah It's on. ”


## Php容器运行
```bash
docker run -d -p 9000:9000 --name php72 \
           -v /services/nginx/wwwroot:/services/nginx/wwwroot \
           php72
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






