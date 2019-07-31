---
title: vue-infinite-scroll一直触发loadmore
date: 2019-07-11 18:35:57
tags: vue
---
## 问题
在使用vue-infinite-scroll组件的时候遇到一直触发loadmore的问题，无论infinite-scroll-distance设置多大，都会一直触发

当父容器的display为none时，也会一直触发，因为此时高度为0。

## 解决问题
需要在使用的标签外面的容器上设置height 或 设置 overflow-y:hidden


var viewportBottom = viewportScrollTop + getVisibleHeight(scrollEventTarget);
源码中有这么一段。必须设置包裹ul的外层容器上设置height，不然在判断是否需要拉取更多
shouldTrigger = viewportBottom + distance >= elementBottom;
的时候shouldTrigger一直是true