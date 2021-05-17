---
title: nuxt+vant从零开始配置
date: 2021-04-10 18:57:00
tags:
---

## 1、安装
> 官网 [中文官网](https://zh.nuxtjs.orgs)

```bash
npx create-nuxt-app '项目名'
```
一路选择配置下来，UI框架选择Vant。

## 2、配置
### 2.1 配置axios并统一管理api
用的是官方的@nuxtjs/axios，在plugins目录下新建api.js文件来自定义axios，把封装的axois当作参数传入api目录下的各个接口方法中。
使用@nuxtjs/axios需要在nuxt.config.js配置文件中设置，顺便设置一下代理。

nuxt.config.js
```javascript
export default {
    modules: [
        '@nuxtjs/axios',
    ]，
}
```
在根目录下新建api文件夹，里面是各模块的接口
```
api
    index.js
    user.js
    auth.js
```
index.js文件
```JavaScript
import user from './user'
import auth from './auth'

export default {
    user,
    auth,
}
```
auth.js文件
```javascript
export default axios => ({
    login(params) {
        return axios.$post('/login', params)
    }
})
```

在plugins目录下新建api.js文件
> [@nuxtjs/axios官网](https://go.nuxtjs/dev/axios)，更多配置可去官网查看文档。
```javascript
import apis from '../api/index'

export default function({ app, $axios, store, req }, inject) {
    $axios.onRequest(config => {
        // 请求前的一些配置
    })

    $axios.onResponse(response => {
        // 响应后的统一处理
    })

    $axios.onError(err => {
        // 请求错误处理
    })
    
    var apiObject = {};
    for (var i in apis) {
        apiObject[i] = apis[i]($axios)
    }

    inject('api', apiObject)
}
```

### 2.2 代理配置
使用@nuxtjs/proxy模块，@nuxtjs/proxy 代理需要引入module中

nuxt.config.js
```javascript
export default {
    modules: [
        '@nuxtjs/proxy', // 使用代理
    ]，

    axios： {
        proxy: true,    // 开启代理
        prefix: '/api', // 请求前缀
    },

    proxy: {
        '/api': {
            target: 'https://api.xxxxxx.com',
            changeOrigin: true,
            secure: false,
            logLevel: 'debug',
            // pathRewrite: { '/api': '' }
        }
    }
}
```
vant lazyload 需要单独 vue.use(lazyload)

## 问题

### 1.微信浏览器内跳转不生效
使用keep-alive组件，key设置为$router.fullPath，在微信浏览器内会有问题，直接访问某一页面时，页面跳转不生效，路径变了，但是内容没变，在其他浏览器无此问题，后来把key去掉后正常。初步怀疑是keep-alive问题， key被设置为了/，因为刚进入时fullPath是/，但在其他浏览器没问题，可能是浏览器的一些机制我没有了解导致的这个问题，目前的项目不设置特定的key也可以，所以直接去掉了。（分析：给路由fullPath赋值是微任务，直接获取只能拿到跟路由‘/’。）