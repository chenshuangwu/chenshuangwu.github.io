---
title: gclone安装使用及常用命令
date: 2020-05-29 10:31:51
tags: gclone、rclone
---

## gclone 安装
gclone 其实就是 rclone 的加强版，为Google Drive 操作增加自动切换账户和命令行根目录id操作支持
其他功能与原版 rclone 相同，安装了之后也是可以使用rclone的。
```bash
bash <(wget -qO- https://git.io/gclone.sh)
```

## gclone 配置
使用命令：
```bash
gclone config
```


## gclone使用
- 复制文件
```bash
gclone copy gd:{目录id} gd:{目录id} --drive-server-side-across-configs -v
```
--drive-server-side-across-configs 用于谷歌盘之间传输时使用，不走服务器流量，传输速度也更快

-v 显示详细日志

-P 显示进度


- 去除重复文件
```bash
gclone dedupe gd:/xxx/xxx/ (路径) -P
```

## rclone 挂载 Google Drive

基本挂载命令：
```bash
rclone mount remote:path /path/to/mountpoint [flags]
```
示例：
```bash
rclone mount gdrive1: /home/gdrive1 \
 --umask 0000 \   #  --umask int 覆盖文件系统设置的权限位
 --default-permissions \  ##  使内核执行基于文件模式的访问控制
 --allow-non-empty \  # 允许在非空目录(不是Windows)上挂载
 --allow-other \ # 允许其他用户访问
 --buffer-size 32M \  #  在读取每个文件时的内存缓冲区大小——传输。(默认16M)
 --dir-cache-time 12h \  #  缓存目录项的时间。(默认5m0s)
 --vfs-read-chunk-size 64M \ #  以块的形式读取源对象。(默认128M)
 --vfs-read-chunk-size-limit 1G & # 如果大于 ——vfs-read-chunk-size，则在每个块读取后将块大小加倍，直到达到限制。“off”是无限的。(默认 off)
```

## rclone 自动挂载
```bash
cat > /etc/systemd/system/rclone.service <<EOF
[Unit]
Description=Rclone
AssertPathIsDirectory=LocalFolder
After=network-online.target

[Service]
Type=simple
ExecStart=/usr/bin/rclone mount gdrive1: /home/gdrive1 \
 --umask 0000 \
 --default-permissions \
 --allow-non-empty \
 --allow-other \
 --buffer-size 32M \
 --dir-cache-time 12h \
 --vfs-read-chunk-size 64M \
 --vfs-read-chunk-size-limit 1G
ExecStop=/bin/fusermount -u LocalFolder
Restart=on-abort
User=root

[Install]
WantedBy=default.target
EOF
```

设置启动
```bash
systemctl start rclone
```

开机启动
```bash
systemctl enable rclone
```


## rclone mount 报错

报错内容：
```bash 
Fatal error: failed to mount FUSE fs: fusermount: exec: "fusermount": executable file not found in $PATH
```
解决办法：
- CentOS
```bash
yum insstall fuse
```
- Debian/Ubuntu
```bash
apt-get install fuse
```

