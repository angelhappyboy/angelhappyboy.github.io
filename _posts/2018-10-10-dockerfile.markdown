---
layout:     post
title:      "使用Docker,第二部分:容器(Containers)"
subtitle:   " \"使用DockerFile建立自己的镜像\""
date:       2018-10-10 12:41:00
author:     "Bin"
header-img: "img/post/bg/docker.svg"
catalog: true
tags:
    - Docker
---

> “Yeah It's on. ”


## 使用Dockfile文件定义一个容器(Define a container with Dockerfile)

```bash

# 使用父镜像
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]

```

## 构建应用(Build the app)

使用``docker build``命令构建镜像  
``-t``是镜像名称  
``-f``Dockerfile的名称(默认是'PATH/Dockerfile')  
``.``是生成镜像路径

```bash
docker build -t friendlyhello -f Dockerfile .
```

## 启动应用(Run the app)
使用``docker run``命令使用已有构建的镜像启动一个容器[(更多run命令)](/2018/10/10/docker/cmd)  
``-p 4000:80`` 端口映射(寄主端口:容器端口)   
``friendlyhellow`` 使用的镜像名称 
```bash
docker run -p 4000:80 friendlyhello
```


## 分享你的镜像(Share your image)






