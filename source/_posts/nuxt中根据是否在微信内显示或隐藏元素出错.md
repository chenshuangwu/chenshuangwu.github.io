---
title: nuxt中根据是否在微信内显示或隐藏元素出错
date: 2019-08-12 19:10:07
tags:
---


combined-inject.js
```js
export default ({ $axios, app, store, route, req }, inject) => {
  inject('isWeChat', () => {
    const UA = process.server ? req.headers['user-agent'] : navigator.userAgent
    return (/MicroMessenger/i).test(UA)
  })
}
```

```js
<nuxt-link v-if="$isWeChat()" :to="$i18n.path('personal/recharge')" class="btn-pill">
    <i class="iconfont icon-recharge"></i> 充值
</nuxt-link>
```

进入页面会报错 n.setAttribute is not a function


## 解决方法
把v-if改为v-show，具体原因还不懂。

