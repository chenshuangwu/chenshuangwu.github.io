---
title: watch与computed
---


## watch

### watch

``` javascript
watch:{
  test(newVal, oldVal){
    console.log(newVal)
  }
}
```

### watch深度监听与立即执行

``` javascript
watch: {
  immediate: true,
  deep: true,
  test: handler(newVal, oldVal){
    console.log(newVal)
  }
}
```
