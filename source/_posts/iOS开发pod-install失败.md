---
title: iOS开发pod install失败
date: 2021-05-28 12:04:47
tags: ios
---

## 问题
pod install 一直安装不上，原因是源cocoapods下载不下来，经常中断。

## 解决办法
使用CND，在Podfile文件中修改源。
```shell
source 'https://cdn.cocoapods.org/'
```