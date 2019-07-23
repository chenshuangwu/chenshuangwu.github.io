---
title: JS验证input输入框（字母，数字，符号，中文）
date: 2019-07-06 23:08:41
tags: js
---
 
 
只能输入英文
```html
<input type="text" onkeyup="value=value.replace(/[^a-zA-Z]/g,'')">
```

 
 

只能输入英文
```html
<input type="text" onkeyup="value=value.replace(/[^\a-\z\A-\Z]/g,'')"
    onkeydown="fncKeyStop(event)" onpaste="return false"
    oncontextmenu="return false" />
无法粘贴，右键不会弹出粘贴菜单
 ```
 
只能输入数字：
```html
<input onkeyup="this.value=this.value.replace(/\D/g,'')"
    onafterpaste="this.value=this.value.replace(/\D/g,'')">
 ```

 

只能输入数字，小数点：
```html
<input name="price" type="text"
    onkeyup="value=value.replace(/[^\d\.]/g,'')">
 ```
 
只能输入数字，小数点，下划线：
```html
<input name="price" type="text"
    onkeyup="value=value.replace(/[^\d\._]/g,'')">
 ```

 

只能输入英文和数字：
```html
<input onkeyup="value=value.replace(/[\W]/g,'') "
    onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\d]/g,''))">
```
 
 
只能输入汉字：
```html
<input onkeyup="value=value.replace(/[^\u4E00-\u9FA5]/g,'')" onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\u4E00-\u9FA5]/g,''))">
```
 
 
禁止输入法输入：
```html
<input type="text" style="ime-mode: disabled">
无法切换输入法
 ```

 

只能输入中文、英文、数字、@符号和.符号：
```html
<input type="text" onkeyup="value=value.replace(/[^\a-\z\A-\Z0-9\u4E00-\u9FA5\@\.]/g,'')">
 ```
 
不能为空：
```html
<input onblur="if(this.value.replace(/^ +| +$/g,'')=='')alert('不能为空!')">
```