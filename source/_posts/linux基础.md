---
title: linux基础
date: 2019-06-20 22:02:50
tags: linux
---

# 文件和目录

## 1.Linux 目录

![linux目录结构](/images/linux目录结构.png)

- **/**：根目录，一般根目录下只存放目录，在Linux下有且只有一个根目录。所有的东西都是从这里开始。当你在终端里输入“/home”，你其实是在告诉电脑，先从/（根目录）开始，再进入到home目录。
- **/bin、/usr/bin**: 可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等。
- **/boot**：放置linux系统启动时用到的一些文件，如Linux的内核文件：/boot/vmlinuz，系统引导管理器：/boot/grub。
- **/dev**：存放linux系统下的设备文件，访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱 mount /dev/cdrom /mnt。
- **/etc**：系统配置文件存放的目录，不建议在此目录下存放可执行文件，重要的配置文件有 /etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d。
- **/home**：系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下，\~表示当前用户的家目录，~edu 表示用户 edu 的家目录。
- **/lib、/usr/lib、/usr/local/lib**：系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助。
- **/lost+fount**：系统异常产生错误时，会将一些遗失的片段放置于此目录下。
- **/mnt: /media**：光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。
- **/opt**：给主机额外安装软件所摆放的目录。
- **/proc**：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有 /proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/* 等。
- **/root**：系统管理员root的家目录。
- **/sbin、/usr/sbin、/usr/local/sbin**：放置系统管理员使用的可执行命令，如fdisk、shutdown、mount 等。与 /bin 不同的是，这几个目录是给系统管理员 root使用的命令，一般用户只能"查看"而不能设置和使用。
- **/tmp**：一般用户或正在执行的程序临时存放文件的目录，任何人都可以访问，重要数据不可放置在此目录下。
- **/srv**：服务启动之后需要访问的数据目录，如 www 服务需要访问的网页数据存放在 /srv/www 内。
- **/usr**：应用程序存放目录，/usr/bin 存放应用程序，/usr/share 存放共享数据，/usr/lib 存放不能直接运行的，却是许多程序运行所必需的一些函数库文件。/usr/local: 存放软件升级包。/usr/share/doc: 系统说明文件存放目录。/usr/share/man: 程序说明文件存放目录。
- **/var**：放置系统执行过程中经常变化的文件，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。

## 终端简介
```bash
chensw@chensw:~$
    chensw  当前登录的用户是chensw
    @chensw 当前系统主机名chensw
    ～      当前所在目录的目录名是(~家目录)
    $       当前用户权限为普通用户
    #       当前用户权限为管理员
```

## 基本命令

<!--more-->
#### who
   
   | 命令   | 含义                   |
   | ------ | ---------------------- |
   | who    | 当前用户的登录属性信息 |
   | whoami | 当前登录用户的用户名   |
#### 路径
| 命令     | 含义                   |
| -------- | ---------------------- |
| pwd      | 当前目录所在的绝对路径 |
| 绝对路径 | 以/开头的路径          |
| 相对路径 | 不以/开头的路径        |
| .        | 当前目录               |
| ..       | 上一级目录             |
#### 查看目录文件
| 命令                | 含义                                                |
| ------------------- | --------------------------------------------------- |
| ls                  | 列表显示当前目录下所有文件名                        |
| ls -a               | 列表显示当前目录下所有文件名(隐藏文件(.开头的文件)) |
| ls -l               | 列表显示当前目录下所有文件属性信息                  |
| ls /home/chensw     | 列表显示/home/chensw下所有文件名                    |
| ls -ld /home/chensw | 查看/home/chensw的目录属性信息                      |
         
#### 切换到指定目录
| 命令  | 含义                              |
| ----- | --------------------------------- |
| cd    | 目录切换到家目录                  |
| cd    | /var/log 目录切换到/var/log目录中 |
| cd .. | 目录切换到上一级目录              |
| cd ~  | 目录切换到家目录                  |
| cd -  | 目录切换到上一次操作所在目录      |

## 帮助
####　man
    man ls  查看ls命令的官方手册
####　info
    info ls 查看ls命令的说明文档
####　--help
    ls --help 查看ls命令常用参数

##　目录操作
####　创建(mkdir)
| 命令            | 含义                                          |
| --------------- | --------------------------------------------- |
| mkdir a         | 当前目录下创建空目录a                         |
| mkdir b c       | 当前目录下创建空目录b和空目录c                |
| mkdir "d e"     | 当前目录下创建空目录d e                       |
| mkdir -p f/g/h  | 当前目录下创建级联目录f/g/h(级联目录必须加-p) |
| mkdir /opt/test | 在/opt目录下创建test目录                      |
####　复制(cp)
| 命令      | 含义                                                  |
| --------- | ----------------------------------------------------- |
| cp -r f a | 复制当前目录下f目录到当前目录下的a目录中(a目录存在)   |
| cp -r f g | 复制当前目录下的f目录为当前目录下的g目录(g目录不存在) |
 注意：复制目录必须加-r
####　剪切(mv)
| 命令   | 含义                                              |
| ------ | ------------------------------------------------- |
| mv g c | 剪切当前目录下g目录到当前目录下c目录中(c目录存在) |
| mv a k | 重命名当前目录下a目录为k(k目录不存在)             |
####　删除
| 命令       | 含义                     |
| ---------- | ------------------------ |
| rmdir test | 删除当前目录下空目录test |
| rm -r k    | 删除当前目录下的k目录    |
##　文件操作
####　创建(touch)
| 命令                | 含义                       |
| ------------------- | -------------------------- |
| touch passwd        | 当前目录下创建空文件passwd |
| touch /opt/user/opt | 目录下创建空文件user       |
        
重定向

    >    覆盖(删除文件中所有内容，加入新内容)
    >>   追加(文件末尾增加新内容) 
| 命令      | 含义                                       |
| --------- | ------------------------------------------ |
| echo a>b  | 把a打印到文件b中(如果没有该文件，自动创建) |
| echo c>>d | 追加c到文件d中(如果没有该文件，自动创建)   |
####　复制
         cp user passwd b 复制当前目录下user和passwd文件到b目录中
         cp user user1    复制当前目录下user文件为user1文件
####　剪切
         mv user* f      剪切user开头的文件到f目录下(f目录存在)
####　删除
         rm zhenshuai   删除当前目录下zhenshuai文件
        rm -rf haleshao     强制删除haleshao文件
        rm -rf *            删除当前目录下所有文件
####　查看
    cat   不分页显示文件内容
      cat example.txt
    less  分页显示文件内容，可以向上向下翻页
      less example.txt
    more  分页显示文件内容，只能向下翻页
      more eexample.txt
    head  查看文件前几行
      head -3 example.txt
    tail  查看文件后几行
      tail -2 example.txt
    vi    打开文件后不进行修改
####　编辑
 安装vim：  apt-get install vim

 **vi/vim编辑器**
#### vi的模式
    命令模式
    编辑模式
    末行模式
#### 命令模式
##### 跳转
      G     光标跳转到文件末行行首
      gg    光标跳转到文件首行行首
      100gg 光标跳转到文件100行的行首
      ^     光标跳转到本行行首
      $     光标跳转到本行行尾
##### 复制
      yy   复制当前行内容
      10yy 复制10行内容
##### 粘贴
      p
##### 剪切/删除
      dd   剪切/删除当前行内容
      10dd 剪切/删除10行内容
##### 搜索
      /a    全文搜索a关键字
      ?a    全文搜索a关键字
#### 命令模式进入到编辑模式的方法
    i     光标所在位置进行插入，进入到编辑模式
    O  o
    S  s
    A  a
#### 编辑模式
    编辑模式无法直接进入到末行模式，需要返回命令模式(esc)
#### 末行模式
    命令模式：
    :set nu    显示行号
    :set nonu  取消显示行号
    :w         保存、另存
    :q         退出
    :wq!       强制保存退出
    :1,$s/a/b/ 全文搜索a替换为b，只替换每行第一个
    :20s/a/b/g 20行搜索a替换为b，全部替换(末尾的g代表全部)

## 包、压缩文件、压缩包
#### 包（tar）
##### 打包
    创建的包文件通常以.tar结尾
    tar -cvf test.tar example download
    创建包文件test.tar,包含内容example和download
##### 查看包
    tar -tvf test.tar
    查看包文件test.tar中所有文件属性信息
##### 解包
    tar -xvf test.tar
    解压包到当前目录下
    tar -xvf test.tar -C /opt
    解压包到指定目录下（需要加-C）
#### 压缩文件(gzip)
##### 查看文件大小
    查看example文件的大小
    du -sh example
##### 创建压缩文件(压缩文件不能压缩目录)
    压缩文件example
    gzip example
##### 查看压缩文件
    查看example.gz压缩文件的属性
    gzip -l example.gz
##### 解压压缩文件
    gzip -d example.gz
#### 压缩包(tar)
先打包后压缩,产生的文件一般为.tar.gz或者.tgz
##### 创建压缩包
    tar -czvf test.tar.gz example
    创建压缩包文件test.tar.gz包括example
##### 查看压缩包
    tar -tzvf test.tar.gz
    查看压缩包文件test.tar.gz内容
##### 解压压缩包
    tar -xzvf test.tar.gz
    解压压缩包文件test.tar.gz到当前目录下
    tar -xzvf test.tar.gz -C /optqiqq
    解压压缩包文件到/opt目录下
## 远程拷贝(scp)
前提：目标电脑中一定安装了ssh服务，可以copy文件，目录

    安装： apt-get install openssh-server
    scp 用户@ip:文件路径 本机路径
    scp chensw@192.168.7.139:/opt /

    chensw:用户名
    @192.168.7.139:目标ip
    /opt：复制目标主机的目录
    /：   复制到我电脑的哪里
#### 远程连接linux
    ssh 用户@ip

## 用户和权限
### 用户
    /etc/passwd  存放用户配置信息
    /etc/shadow  存放用户密码配置信息
    /etc/group   存放组配置信息
    组：属性，不同的用户拥有相同的属性
    a.创建用户
         useradd simon  创建用户simon
         passwd  simon  给simon用户添加密码
    b.修改用户
         usermod -L simon 锁定用户simon
         usermod -U simon 解锁用户simon
    c.删除用户
         userdel -r simon 删除simon用户
### 权限
    查看权限
        ls -l examples.desktop 
        -rw-r--r-- 1 chensw chensw 9194 7月  17 10:02 examples.desktop
        1.文件类型  d：目录 -：普通文件
        2-10.文件权限
        11.文件节点
        12.文件拥有者
        13.拥有组
        14.文件大小
        15.最后修改时间
        16.文件名

    常用权限
        r(读)
            文件：可以查看文件内容
            目录：可以列表显示
        w(写)
            文件：可以修改文件内容
            目录：可以在目录中创建、重命名、删除文件
        x(执行)
            文件：可以执行，一般来说是二进制文件
            目录：可以进入

    权限分组
        rw-            r--         r-- 
        拥有者权限    拥有组权限     其他人权限
        系统判断权限的方法：
        1.判断用户是否为文件拥有者，如果是，赋予拥有者权限 
        2.如果不是，判断用户是否为拥有组成员(id 用户)，如果是，赋予拥有组权限
        3.如果都不是，赋予其他人权限
        补充：查看组信息(id simon)

    权限的修改
        chown  修改文件属主来修改权限
        chmod  直接修改权限
        d1.chmod修改权限
            1>字符类型修改
            u  拥有者
            g  拥有组
            o  其他人
            a  所有人
             chmod u+x examples.desktop
                修改文件权限，拥有者增加执行权限
             chmod g+x,o+x examples.desktop
                修改文件权限，拥有组和其他人增加执行权限
             chmod a-x examples.desktop 
                修改文件权限，所有人取消执行权限
            2>数字类型修改
            r：4
            w: 2
            x: 1
            -: 0
             chmod 777 examples.desktop 
                修改文件权限，所有人都拥有读写执行权限
            udo chmod 000 examples.desktop 
                修改文件权限，所有人没有任何权限
        d2.chown
             chown zelin examples.desktop 
                修改文件拥有者位zelin
             chown :bin examples.desktop
                修改文件拥有组为bin
             chown chensw:chensw examples.desktop 
                修改文件拥有者是chensw，拥有组是chensw
## 搜索和管道
#### find(搜索到系统中所有文件，相对慢)
        find /etc -name passwd 在/etc/目录下搜索名字位passwd的文件
        find /etc -name *.conf 在/etc/目录下搜索以.conf结尾的文件
####  locate(搜索到系统中所有文件，相对比较快，缺点是需要刷新系统数据库)
        updatedb  刷新系统数据库
####  grep(搜内容)
        grep root /etc/passwd 搜索/etc/passwd中含有root的行
        grep ^r /etc/passwd  搜索/etc/passwd中以r开头的行
        grep bash$ /etc/passwd 搜索/etc/passwd中以bash结尾的行
####  管道 |
    前面的输出作为后面的输入
    cat /etc/passwd | grep root
    查看一个文件第7行数据
head -7 examples.desktop | tail
## 管理命令
| 命令                   | 含义                                   |
| ---------------------- | -------------------------------------- |
| ifconfig               | 查看网卡信息                           |
| ping                   | 测试网络连接(跟ip地址或者域名)         |
| nslookup               | www.baidu.com(解析baidu的ip  域名--IP) |
| top                    | 监控系统资源                           |
| ps -ef                 | 查看系统进程                           |
| ps -ef \| grep sshd    | 查看ssh进程是否运行正常                |
| ps -ef \| grep tomcat  | 查看tomcat进程是否正常                 |
| ps -ef \| grep mysqld  | 查看mysqld进程是否正常                 |
| ps -ef \| grep java    | 查看java相关进程是否正常               |
| netstat -an            | 查看系统中所有端口信息                 |
|                        | mysql   3306                           |
|                        | apache  80                             |
|                        | tomcat  8080                           |
|                        | oracle  1521                           |
|                        | ssh     22                             |
| netstat -an \| grep 22 | 查看sshd的端口是否运行正常             |
| free -m                | 查看系统内存情况                       |
| df -h                  | 查看磁盘使用率                         |
| mount                  | 查看系统挂载情况                       |
| vmstat                 | 监控系统资源                           |