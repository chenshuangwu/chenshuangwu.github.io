---
title: jellyfin安装
date: 2020-05-29 14:24:11
tags: jellyfin
---

## CentOs7下安装

### 使用Docker安装

1. 获取jellyfin镜像

```bash
docker pull jellyfin/jellyfin
```

2. 创建jellyfin需要的配置文件目录和缓存目录

```bash
mkdir -p /opt/jellyfin/config
mkdir -p /opt/jellyfin/cache
```

3. 运行jellyfin服务

```bash
docker run -d -p 8096:8096 -v /jellyfin/config:/config -v /home/gdscu/:/media jellyfin/jellyfin
```

参数说明：
> 1. -p 后面是jellyfin服务的端口号，安装时可以指定，这里使用默认的8096;
> 2. -v 后面是指定的配置路径，比如/home/gdscu/就是我原来的影音物理路径，/media就是jellyfin的映射路径


安装完成后可通过 http://ip地址:8096来访问，本地可用http://127.0.0.1:8086访问。


