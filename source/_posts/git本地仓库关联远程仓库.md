---
title: git本地仓库关联远程仓库
date: 2020-12-08 10:48:49
tags: git
---

## 情景
有时候现在本地开发，远程仓库还未创建，需要把现有本地仓库与远程仓库关联起来。

## 本地仓库创建

本地先创建一个项目

```
git init
git add .
git commit -m '备注'
```
## 远程仓库创建

直接在远程仓库创建一个仓库

## 关联仓库

关联：

```
git remote add origin 远程仓库地址
```

推送到远程仓库：

```
git push -u origin master
```