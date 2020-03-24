---
title: chrome进行微信浏览器真机调试
date: 2020-03-24 15:24:01
tags:
---

1、在微信打开 http://debugx5.qq.com

如果有错误，先访问 http://debugmm.qq.com/?forcex5=true ，再进入 http://debugtbs.qq.com 选择 “安装线上内核”。

2、在http://debugx5.qq.com页面信息选项卡，勾选“打开TBS内核Inspector调试功能”。

3、然后 USB 连接手机、电脑，打开开发者模式，打开 USB 调试，然后在 Chrome 中进入 chrome://inspect/#devices 页面，就能看到设备打开的网页了。

