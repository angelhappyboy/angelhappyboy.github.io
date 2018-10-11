---
layout:     post
title:      "Git应用：git pull 强制"
subtitle:   " \"使用DockerFile建立自己的镜像\""
date:       2018-10-10 12:41:00
author:     "Bin"
header-img: "img/post/bg/docker.svg"
catalog: true
tags:
    - Docker
---

> “Yeah It's on. ”


## git pull部分文件

```bash
mkdir object
```
```bash
cd object
```
初始化
```bash
git init
```
添加pull的地址
```bash
git remote add origin url
```

检出指定文件
```bash
git config core.sparsecheckout true
```
添加文件夹
```bash
echo "dir/" >> .git/info/sparse-checkout
```

拉取
```bash
git pull origin mater
```

ps 设置默认拉取
```bash
git branch --set-upstream-to=orgin/master master
```






