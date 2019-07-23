---
title: 淘宝npm镜像
date: 2019-07-06 21:18:57
tags: npm
---

## 使用淘宝npm镜像
npm作为国外的node仓库安装工具，会受到我大长城防火墙的干扰，国内用户在安装相关的资源的时候，会出现安装失败，以及速度很慢的情况。为了解决npm安装的问题，国内出现了很多npm的镜像网址，taobao的npm镜像算是使用频率比较高的了。
使用的方法有三种，首先是淘宝npm自己提供的两种：
1）你可以使用我们定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
 
2）或者你直接通过添加 npm 参数 alias 一个新命令:
```
alias cnpm="npm --registry=https://registry.npm.taobao.org \ --cache=$HOME/.npm/.cache/cnpm \ --disturl=https://npm.taobao.org/dist \ --userconfig=$HOME/.cnpmrc" # Or alias it in .bashrc or .zshrc $ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org \ --cache=$HOME/.npm/.cache/cnpm \ --disturl=https://npm.taobao.org/dist \ --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```

 
3）直接将本地的npm仓库指向淘宝的镜像地址
```bash
npm config set registry https://registry.npm.taobao.org
```

 
// 配置后可通过下面方式来验证是否成功

    npm config get registry
// 或
    npm info express
 
其实还有第四种，那就是临时使用的时候

    npm --registry https://registry.npm.taobao.org install express