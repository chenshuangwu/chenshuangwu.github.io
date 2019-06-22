---
title: vee-validate国际化
date: 2019-06-20 21:38:03
tags: vue
---

使用的是Nuxt.js框架

## 安装vee-validate
```sh
npm install vee-validate --save
```

## 新建vee-validate.js插件

在plugins目录下新建vee-validate.js插件

```javascript
import Vue from 'vue'
import zh_CN from 'vee-validate/dist/locale/zh_CN'
import zh_TW from 'vee-validate/dist/locale/zh_TW'

import VeeValidate, { Validator } from 'vee-validate'

Vue.use(VeeValidate)

export default ({ app, store }) => {
  app.validator = Validator
  // Localize takes the locale object as the second argument (optional) and merges it.

  // 修改默认错误提示
  const dict = {
    zh_CN: { messages: { required: name => `${name}不能为空!` } }, // name接受alias的值.
    zh_TW: { messages: { password: name => `${name}必須有數字、英文` } }
  }
  app.validator.localize('zh_CN', zh_CN)
  app.validator.localize('zh_CN', dict.zh_CN)


  // 自定义规则password
  app.validator.extend('password', {
    getMessage: field => field + '必须有数字、英文',
    validate: (value) => {
      return /^(?=.*[a-zA-Z]+)(?=.*[0-9]+)\S+$/.test(value)
    }
  })

  // 根据store.state.locale来做相对应的vee-validate本地化
  app.validator.changeLocale = () => {
    switch (store.state.locale) {
      case 'zh-cn':
        app.validator.localize('zh_CN', zh_CN)
        app.validator.localize('zh_CN', dict.zh_CN)
        break
      case 'zh-tw':
        app.validator.localize('zh-TW', zh_TW)
        app.validator.localize('zh-TW', dict.zh_TW)
        break
    }
  }
}
```

## 配置插件
根目录下的nuxt.config.js配置文件
```javascript
plugins: ['@/plugins/i18n.js', // 此插件是项目用来做国际化的,基于vue-i18n
          '@/plugins/vee-validate.js' //  
  ],
```

## middleware中进行本地化
在middleware目录下新建veelocale.js文件
```javascript
export default function ({ app}) {
  app.validator.changeLocale()
}

```

## 页面中使用middleware
```javascript
<script>
export default {
  middleware: "veelocale",
</script>
```