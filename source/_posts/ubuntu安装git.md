---
title: ubuntu安装使用git
date: 2019-08-02 21:49:01
tags: ubuntu
---

## 安装git
```bash
sudo apt-get update
sudo apt-get install git 
```
安装完可使用 git --version命令来验证是否安装成功。

## 设置
安装完之后要进行一些基础设置，如用户名,邮箱。
```bash
git config --global user.name "你的用户名，例如github的账号"
git config --global user.email "你的邮箱，例如github中的邮件地址"
```

## 生成密钥
配置完成后，需要创建验证用的公钥，因为git是通过ssh的方式访问资源库的，所以需要在本地创建验证用的文件。使用命令
```bash
ssh-keygen -C '你的邮箱地址' -t rsa
```
会在用户目录下生成.ssh文件夹，里面有私钥id_rsa和公钥id_rsa

## 出现的问题
- ssh出错 sign_and_send_pubkey: signing failed: agent refused operation
    然后执行了以下命令才好。
    ```bash
    eval "$(ssh-agent -s)"
    ssh-add
    ```
- 执行ssh-add提示信息:
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    Permissions 0775 for '/home/chensw/.ssh/id_rsa' are too open.
    It is required that your private key files are NOT accessible by others.
    This private key will be ignored.
    bad permissions: ignore key: /home/chensw/.ssh/id_rsa
    
    这是因为私钥id_rsa文件权限太高，不允许其他人访问，降低权限即可
    ```bash
    chmod 600 ~/.ssh/id_rsa
    ```
    然后再执行ssh-add即可