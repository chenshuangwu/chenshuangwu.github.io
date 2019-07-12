---
title: vue中数组和对象改变时视图不更新
date: 2019-07-12 14:31:04
tags: vue
---

## 问题描述
 在vue中，有时会出现数组或者对象改变了，但是视图没有更新的问题。其实这是因为数组或者对象改变的方式没有触发数据的set方法。

## 不会触发set的情况

当数据是一个对象的时候，修改、添加、删除数据的属性值都不会触发set方法。
当数据是一个数组时，push、pop、shift、unshift 等原生方法也无法触发set方法。

## 解决方法

- 数组更新检测

  Vue为我们定义了一系列的变异方法，可以直接使用：
  - push() 
  - pop() 
  - shift() 
  - unshift() 
  - splice() 
  - sort() 
  - reverse()

- 对象更新检测

  使用 Vue.set(object, key, value) 方法将响应属性添加到嵌套的对象上
  ```javascript
  Vue.set(this.obj, 'test', 1)
  ```
  还可以使用 vm.$set 实例方法，这也是全局 Vue.set 方法的别名：
   ```javascript
  this.$set(this.obj,'test',2)
  ```