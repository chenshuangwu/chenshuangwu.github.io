---
title: js控制多行内容展开折叠
date: 2020-05-09 14:29:41
tags: javascript
---

##  需求

一段文字说明，多行文字时只显示一行，并显示展开/折叠图标，可以展开/折叠，一行时则不显示图标。

## 方案

展开/折叠的功能就比较简单，设置内容固定宽高，高度设置为一行高，默认1.5em，当点击展开时，高度设置为100%或者auto即可，折叠时高度恢复为一行高，记得要设置overflow为hidden。

比较麻烦的是只有一行时，不需要显示展开/折叠按钮，这时候可以获取元素的scrollHeight和clientHeight作对比。
        
    element.scrollHeight    内容的实际高度
    element.clientHeight    内容的显示高度

如果element.scrollHeight>element.clientHeight,则显示展开/折叠按钮，反之则不显示。
