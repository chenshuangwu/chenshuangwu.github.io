---
title: CentOS7安装nodejs
date: 2019-07-23 18:23:50
tags: linux
---

## 直接部署
1. 安装wget（已经安装可跳过）
```bash
yum install -y wget
```

2. 下载nodejs最新的包
   在nodejs官网https://nodejs.org/en/download/找到下载地址，执行
```bash
wget https://nodejs.org/dist/v10.16.0/node-v10.16.0-linux-x64.tar.xz
```

3. 解压包
```bash
tar -xvf node-v10.16.0-linux-x64.tar.xz
```

4. 部署bin文件
需要nodejs的路径，刚才解压后的nodejs路径为~/node/node-v10.16.0-linux-x64/bin，执行 
```bash
ln -s ~/node/node-v10.16.0-linux-x64/bin/node /usr/bin/node
ln -s ~/node/node-v10.16.0-linux-x64/bin/npm /usr/bin/npm
```
注意ln指令用于创建关联（类似与Windows的快捷方式）必须给全路径，否则可能关联错误

5. 测试是否安装成功
```bash
[root@vultr node-v10.16.0-linux-x64]# node -v
v10.16.0
[root@vultr node-v10.16.0-linux-x64]# npm -v
6.9.0
```