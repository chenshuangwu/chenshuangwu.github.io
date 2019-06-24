---
layout: '''vue'
title: vue自定义指令实现v-loading'
date: 2019-06-24 18:48:18
tags: vue 
---

新建js文件

```javascript
import Vue from 'vue'
import '~/assets/style/_loading.scss'

Vue.directive('loading', {
  bind: (el, binding) => {
    const tempDiv = document.createElement('div')
    tempDiv.className = 'custom-loading'
    const round = document.createElement('div')
    round.className = 'custom-loading-round'
    tempDiv.appendChild(round)
    el.loadingElement = tempDiv
    /* if (binding.value) {
      const curStyle = window.getComputedStyle(el)
      const position = curStyle.position
      if (position === 'absolute' || position === 'relative') {
        el.style.position = position
      } else {
        el.style.position = 'relative'
      }
      el.appendChild(tempDiv)
    } else {
      if (tempDiv.parentNode !== null) {
        tempDiv.parentNode.removeChild(tempDiv)
      }
    } */
    const curStyle = window.getComputedStyle(el)
    const position = curStyle.position
    if (position === 'absolute' || position === 'relative') {
      el.style.position = position
    } else {
      el.style.position = 'relative'
    }
    if (binding.value) {
      el.appendChild(tempDiv)
    }
  },
  update: (el, binding) => {
    if (binding.value) {
      if (el.loadingElement.parentNode === null) {
        el.appendChild(el.loadingElement)
      }
    } else if (el === el.loadingElement.parentNode) {
      el.removeChild(el.loadingElement)
    }
  },
  unbind: (el) => {
    if (el.loadingElement.parentNode === el) {
      el.removeChild(el.loadingElement)
    }
    el.loadingElement = null
  }
})
```

新建样式文件_loading.scss
```scss
@keyframes custom-loading-rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.custom-loading {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 100;
  background-color: rgba(255, 255, 255, 0.6);
  overflow: hidden;
}

.custom-loading .custom-loading-round {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: 4px solid #FE6E6E;
  border-left-color: transparent;
  animation: custom-loading-rotate 1s linear infinite;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}
```

在组件中使用

```html
<div v-loading="loading">
</div>
```
当loading为真时，出现loading效果