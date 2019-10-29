---
title: nuxt引用谷歌广告js代码
date: 2019-10-29 17:35:42
tags: nuxt
---

## nuxt引用谷歌广告js代码
> [Nuxt.js引用谷歌广告的JS代码,只配置nuxt.config.js文件就可以!](https://chuihu.com/p-8800000294)
```javascript
  // 这段是谷歌广告要引入的JS代码，这里装在一个字符串变量里xxxxx就是你的ID
const absbygoogle = '(adsbygoogle=window.adsbygoogle||[]).push({google_ad_client:"ca-pub-xxxxx",enable_page_level_ads:true});';

export default {
  mode: 'universal',

  /*
  ** Headers of the page
  */
  head: {
    meta: [
      {charset: 'UTF-8'},
      {name: 'viewport', content: 'width=device-width, initial-scale=1, shrink-to-fit=no'},
      {httpEquiv: 'Content-Type', content: 'text/html; charset=UTF-8'},
      {httpEquiv: 'content-language', content: 'zh-CN'}
    ],
    script: [
      // 这里引入谷歌广告的JS文件，async要为true
      {src: 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js', async: 'true'},
      // 把上面的JS代码变量引用到这里
      {innerHTML: absbygoogle, type: 'text/javascript', charset: 'utf-8'}
    ],
    // 禁止对JS转义，这一句一定要加上
    __dangerouslyDisableSanitizers: ['script']
  },

  /*
  ** Customize the progress-bar color
  */
  loading: '@/components/loading.vue',

  /*
  ** Global CSS
  */
  css: [
    '@/assets/common.css',
    '@/assets/icon/iconfont.css'
  ],

  /*
  ** Plugins to load before mounting the App
  */
  plugins: [
    '@/plugins/axios'
  ],

  /*
  ** Nuxt.js modules
  */
  modules: [
    // Doc: https://bootstrap-vue.js.org/docs/
    'bootstrap-vue/nuxt',
    '@nuxtjs/axios'
  ],

  /*
  ** Build configuration
  */
  build: {
    extractCSS: {allChunks: true},
    /*
    ** You can extend webpack config here
    */
    extend(config, ctx) {
    }
  }
}
```

