---
title: CentOS7安装nodejs、nginx及部署nuxt
date: 2019-07-23 18:23:50
tags: linux
---
# 安装nodejs
## 直接安装
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
<!--more-->
# 安装nginx
> 参考 https://qizhanming.com/blog/2018/08/06/how-to-install-nginx-on-centos-7
## 1.添加yum源
Nginx不在默认的yum源中，使用官网的yum源。
```bash
rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

```
安装完成后，查看一下
```bash
[root@vultr ~]# yum repolist
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.mirror.constant.com
 * epel: epel.mirror.constant.com
 * extras: centos.mirror.constant.com
 * updates: centos.mirror.constant.com
repo id                      repo name                                      status
!base/7/x86_64               CentOS-7 - Base                                10,019
!epel/x86_64             Extra Packages for Enterprise Linux 7 - x86_64     13,332
!extras/7/x86_64             CentOS-7 - Extras                              419
!nginx/x86_64                nginx repo                                     152
!updates/7/x86_64           CentOS-7 - Updates                              2,236
repolist: 26,158
```
可以发现 nginx repo 已经安装到本机了。

## 2.安装
```bash
yum install nginx
```

## 3.配置Nginx服务
设置开机启动
```bash
systemctl enable nginx
```
启动服务
```bash
systemctl start nginx
```
停止服务
```bash
systemctl restart nginx
```
启动服务
```bash
systemctl reload nginx
```
## 4.打开防火墙端口
默认 CentOS7 使用的防火墙 firewalld 是关闭 http 服务的（打开 80 端口）。
```bash
firewall-cmd --zone=public --permanent --add-service=http
firewall-cmd --reload
```
查看一下防火墙打开的所有的服务
```bash
firewall-cmd --list-service
```

# 部署nuxt
## 在nginx里新建一个主机绑定文件，可在 /etc/nginx/conf.d/ 目录下新建
通过upstream nodejs 可以配置多台nodejs节点，做负载均衡
keepalive 设置存活时间。如果不设置可能会产生大量的timewait
proxy_pass 反向代理转发 http://nodejs
```bash
upstream nodenuxt {
    server 127.0.0.1:3000; #nuxt项目 监听端口
    keepalive 64;
}

server {
    listen 80;
    server_name me.chensw.top;
    location / {
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Nginx-Proxy true;
        proxy_cache_bypass $http_upgrade;
        proxy_pass http://nodenuxt; #反向代理
    }
}
```
## 打包应用
```
npm run build
```
打包完成后，将下列文件夹和文件上传到服务器
```
.nuxt
static
serve  # 使用的是express来做服务器
nuxt.config.js
package.json
```
## 在服务器上运行
先安装依赖
```bash
npm install
```
运行
```bash
npm run start
```
在浏览器输入me.chensw.top即可访问。

## pm2开启进程守护
pm2是nodejs的一个带有负载均衡功能的应用进程管理器的模块，类似有Supervisor，forever，用来进行进程管理。
### 安装pm2
```bash
npm install pm2 -g
```
### 配置pm2环境变量
/root/node/node-v10.16.0-linux-x64/bin/pm2 是安装后的路径， 链接到/usr/bin/pm2可全局使用
```bash
ln -s /root/node/node-v10.16.0-linux-x64/bin/pm2 /usr/bin/pm2
```
### 开启pm2守护进程
```bash
pm2 start npm --name "hello-nxut" -- run start
```

## pm2介绍
1、安装
    npm install pm2 -g
2、启动
    pm2 start app.js
    pm2 start app.js --name my-api       #my-api为PM2进程名称
    pm2 start app.js -i 0                #根据CPU核数启动进程个数
    pm2 start app.js --watch             #实时监控app.js的方式启动，当app.js文件有变动时，pm2会自动reload
3、查看
    pm2 list
    pm2 show 0 或者 # pm2 info 0         #查看进程详细信息，0为PM2进程id 
4、监控：
    pm2 monit
5、停止：
    pm2 stop all                         #停止PM2列表中所有的进程
    pm2 stop 0                           #停止PM2列表中进程为0的进程
6、重载：
    pm2 reload all                       #重载PM2列表中所有的进程
    pm2 reload 0                         #重载PM2列表中进程为0的进程
7、重启：
    pm2 restart all                      #重启PM2列表中所有的进程
    pm2 restart 0                        #重启PM2列表中进程为0的进程