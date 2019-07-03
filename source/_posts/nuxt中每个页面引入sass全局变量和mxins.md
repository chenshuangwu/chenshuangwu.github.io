---
title: '''nuxt中每个页面引入sass全局变量和mxins'''
date: 2019-07-03 14:13:34
tags: nuxt
---

在页面中经常用到一些常用的变量和mixins，避免每个页面都要导入，可以使用@nuxtjs/style-resources

> 可参考nuxt官方文档 https://zh.nuxtjs.org/api/configuration-build/#styleresources
## 配置
- 安装@nuxtjs/style-resources模块
```bash
npm install @nuxtjs/style-resources --save-dev
```

- 修改nuxt.config.js
```javascript
  export default {
    modules: [
      '@nuxtjs/style-resources'
    ],
    styleResources: {
      scss: ['./assets/_mixins.scss', './assets/_variables.scss'] // 定义的全局mixins、变量文件路径
      less: './assets/****.less'
      ...
      // 根据需要添加相应文件
    }
  }
```