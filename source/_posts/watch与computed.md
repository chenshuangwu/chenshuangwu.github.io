---
title: watch与computed
date: 2019/6/19 20:46:25
tags:
- vue
---


## watch

### watch
当需要在数据变化时执行异步或开销较大的操作时，使用watch是最有用的。
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

## computed

```javascript
data(){
  return {
    name: 'nickname'
  }
},
computed:{
  // 计算属性的 getter
  // temp的值随着name的改变而改变
  temp(){
    return 'temp' + this.name
  }
}

```
