---
title: UTC时间转换为本地时间
date: 2019-06-21 19:42:19
tags: js
---

### javascript转UTC时间为本地时间
因为后端传的不是标准的UTC时间格式的字符串，标准的是“2019-06-21T19:45:23Z”，后端传的是“2019-06-21 19:45:23”字符串，所以要先处理一下，转成标准的

```javascript
 function UTCDateStrToLocale(str) {
    str = str.replace(' ', 'T') + 'Z'  // UTC时间字符串
    let data = new Date(str) // data本地时间
    data = formatDate(data) // 格式化显示为“yyyy-mm-dd hh:mm:ss”
    return data
  })
}

function formatDate(dataObj) {
  const year = dataObj.getFullYear()
  const month = formatFunc(dataObj.getMonth() + 1)
  const date = formatFunc(dataObj.getDate())
  const hour = formatFunc(dataObj.getHours())
  const min = formatFunc(dataObj.getMinutes())
  const sec = formatFunc(dataObj.getSeconds())
  const dataStr = year + '-' + month + '-' + date + ' ' + hour + ':' + min + ':' + sec
  return dataStr
}
// 格式化显示
function formatFunc(str) {
  return str > 9 ? str : '0' + str
}
```