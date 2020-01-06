---
title: nuxt.js友盟统计
date: 2020-01-06 10:13:14
tags: nuxt
---

> 转载至 [全栈之旅](https://www.kpromise.top/) > [umeng nuxt.js 站长统计 - add umeng analytics for nuxt.js](https://www.kpromise.top/add-umeng-for-nuxt-js/)

nuxt.js 最大的特性是服务端渲染，那么，这种情况下，我们如何添加 umeng 统计呢，并如何隐藏那个站长统计呢，虽然 nuxt.js 是服务端渲染，但同样允许你在客户端渲染，此外，使用 display:none 可能会被搜索引擎惩罚，觉得你是作弊行为。

我们知道 nuxt.config.js 有个 ssr 选项选项，你设置为 false 将在客户端渲染了，那么，我们先看看如何添加 umeng 统计吧。

## nuxt.js 添加 umeng 统计

1、在 static 目录新建 cnzz.js，static 目录在你部署后其实就是根目录，这里你可以存 robots.txt 我们先建 cnzz.js 把，并键入：
```javascript
var siteId = '1273976960';
var cnzz_tag = document.createElement("script");
cnzz_tag.type = "text/javascript";
cnzz_tag.charset = "utf-8";
cnzz_tag.src = "https://s13.cnzz.com/z_stat.php?web_id=" + siteId;
var root = document.getElementsByTagName("script")[0];
root.parentNode.insertBefore(cnzz_tag, root);
```

2、在 nuxt.config.js 里引用这个 js 文件，最终的文件可以参考：
```javascript
module.exports = {
  /*
   ** Headers of the page
   */
  head: {
    title: 'xxx',
    meta: [
    ],
    link: [
    ],
    script: [{
        src: '/cnzz.js',
      }
    ]
  },
```
但是问题来了，每次打开网页，如果网速慢总有一个 站长统计，就不能去掉吗？可以的，比如 display:none 但是这种做法搜索引擎可能会觉得你存在隐瞒，会被惩罚，当然这是我听来的，没有实践过，但想想也有道理。


## 合理去掉站长统计

如上，我已经说了，第一种：display：none如果对seo没有太苛刻要求，是可以的。但我要说的是第二种，具体请看：https://developer.umeng.com/docs/67963/detail/68646

umeng 允许我们使用异步的方式加载，但是异步的方式不提供 显示统计图标。划重点了哦。另外，图片上的代码我已经复制，如下：

```javascript
var siteId = 'xxxxx';
var cnzz_tag = document.createElement("script");
cnzz_tag.type = "text/javascript";
cnzz_tag.async = "true";
cnzz_tag.charset = "utf-8";
cnzz_tag.src = "https://w.cnzz.com/c.php?async=1&id=" + siteId;
var root = document.getElementsByTagName("script")[0];
root.parentNode.insertBefore(cnzz_tag, root);
```
把 siteId 改为你自己的即可，另外，你可能觉得奇怪，为啥用 + 而不是 `` 比如：

```javascript
cnzz_tag.src = `https://w.cnzz.com/c.php?async=1&id=${siteId}`;
```
这种方式是可以，但是请考虑下 IE11 吧，不兼容！