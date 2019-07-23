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


<!--more-->

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

## 组合使用，只监听某个对象的某个属性

现在有个banner_info对象，有时候只想监听某个属性（如object_type），可以使用computed和watch来达到目的
```javascript
data(){
  return {
    banner_info: {
        location: "",
        previewImg: "",
        cover: "",
        object_type: "",
        object_id: "",
        url: "",
        start_at: "",
        end_at: "",
        status: "",
        note: "",
        order_number: "",
        os: "",
        title: "",
      }
  }
},

computed:{
    type(){
      return this.banner_info.object_type
    }
  },

watch:{
  type(newVal, oldVal){
      // do something
}

```