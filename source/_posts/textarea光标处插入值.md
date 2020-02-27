---
title: textarea光标处插入值
date: 2020-02-27 16:24:53
tags: javascript
---

有时候需要在文本域主动插入一些文本。

```javascript
// @params
// myField: textarea的DOM
// myValue: 需要插入的文本

// 光标处插入文本
function insertAtCursor(myField, myValue) { 
    //IE 浏览器
    if (document.selection) {
        myField.focus();
        sel = document.selection.createRange();
        sel.text = myValue;
        sel.select();
    }

    //FireFox、Chrome等
    else if (myField.selectionStart || myField.selectionStart == '0') {
        var startPos = myField.selectionStart;
        var endPos = myField.selectionEnd;

        // 保存滚动条
        var restoreTop = myField.scrollTop;
        myField.value = myField.value.substring(0, startPos) + myValue + myField.value.substring(endPos, myField.value.length);
        
        if (restoreTop > 0) {
            myField.scrollTop = restoreTop;
        }
        
        myField.focus();
        myField.selectionStart = startPos + myValue.length;
        myField.selectionEnd = startPos + myValue.length;
    } else {
        myField.value += myValue;
        myField.focus();
    }
}
```
