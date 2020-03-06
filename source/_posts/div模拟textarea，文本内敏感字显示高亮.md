---
title: '''vue内div模拟textarea，文本内敏感字显示高亮'''
date: 2020-03-06 14:49:30
tags: HTML、JS
---

```html
<div ref="textarea" class="textarea-test" contenteditable='true' @keydown="keydown"></div>
```
```javascript
export default {
    data() {
        return {
            sensitiveWords: ['敏感词1', '敏感词2'],
            highRiskWords: ['高危词1'，'高危词2']
        }
    },
    methon: {
        // 高危词
        highRiskKeys(keys) {
            if (!this.highRiskKeys.$map) {
                var map = {};
                var maxLength = 0;
                for ( var i = 0; i < keys.length; i++) {
                    map[keys[i]] = 1;
                    maxLength = Math.max(keys[i].length, maxLength);
                }
                this.highRiskKeys.$map = {
                    map : map,
                    length : maxLength
                }
        }
            return this.highRiskKeys.$map;
        },

        // 敏感词
        sensitiveKeys(keys) {
            if (!this.sensitiveKeys.$map) {
                var map = {};
                var maxLength = 0;
                for ( var i = 0; i < keys.length; i++) {
                    map[keys[i]] = 1;
                    maxLength = Math.max(keys[i].length, maxLength);
                }
                this.sensitiveKeys.$map = {
                    map : map,
                    length : maxLength
                }
        }
            return this.sensitiveKeys.$map;
        },
        // 高危词、敏感词高亮
        colorKeyword(str) {            

                var words = this.sensitiveKeys(this.sensitiveWords);
                var highRisk = this.highRiskKeys(this.highRiskWords);
                var output = [];
                var output2 = [];
                while (str) {                  
                    let sub = str.substring(0, words.length);
                    str = str.substring(words.length);
                    while (!words.map[sub] && sub) {
                        str = sub.charAt(sub.length - 1) + str;
                        sub = sub.slice(0, -1);
                    }
                    //console.log('color', sub);
                    if (sub) {
                        output.push( '<span style="background-color:#FEEB6E;">', sub, '</span>');
                    } else {
                        output.push(str.charAt(0));
                        str = str.substring(1);
                    }
                }
                output = output.join('')
                while(output) {
                    let sub = output.substring(0, highRisk.length);
                    output = output.substring(highRisk.length);
                    while (!highRisk.map[sub] && sub) {
                        output = sub.charAt(sub.length - 1) + output;
                        sub = sub.slice(0, -1);
                    }
                    //console.log('color', sub);
                    if (sub) {
                        output2.push( '<span style="background-color:#FE6E6E;">', sub, '</span>');
                    } else {
                        output2.push(output.charAt(0));
                        output = output.substring(1);
                    }
                }
                return output2.join('');
        },

        // 自定义div编辑框光标处插入文本
         insertAtCursor(myField, myValue) { 
            let selection = getSelection()
            let lastEditRange = selection.getRangeAt(0)
            // 判断是否有最后光标对象存在
            if (lastEditRange) {
                // 存在最后光标对象，选定对象清除所有光标并添加最后光标还原之前的状态
                selection.removeAllRanges()
                selection.addRange(lastEditRange)
            }
            // 判断选定对象范围是编辑框还是文本节点
            if (selection.anchorNode.nodeName != '#text') {
                // 如果是编辑框范围。则创建表情文本节点进行插入
                let text = document.createTextNode(myValue)
                
                if (myField.childNodes.length > 0) {
                    // 如果文本框的子元素大于0，则表示有其他元素，则按照位置插入表情节点
                    for (let i = 0; i < myField.childNodes.length; i++) {
                        if (i == selection.anchorOffset) {
                            myField.appendChild(text, myField.childNodes[i])
                        }
                    }
                } else {
                    // 否则直接插入一个元素
                    myField.appendChild(text)
                }
                // 创建新的光标对象
                let range = document.createRange()
                // 光标对象的范围界定为新建的节点
                range.selectNodeContents(text)
                // 光标位置定位在表情节点的最大长度
                range.setStart(text, text.length)
                // 使光标开始和光标结束重叠
                range.collapse(true)
                // 清除选定对象的所有光标对象
                selection.removeAllRanges()
                // 插入新的光标对象
                selection.addRange(range)
            } else {
                // 如果是文本节点则先获取光标对象
                let range = selection.getRangeAt(0)
                // 获取光标对象的范围界定对象，一般就是textNode对象
                let textNode = range.startContainer;
                // 获取光标位置
                let rangeStartOffset = range.startOffset;

                // 文本节点在光标位置处插入新的内容
                textNode.insertData(rangeStartOffset, myValue)
                // 光标移动到到原来的位置加上新内容的长度
                range.setStart(textNode, rangeStartOffset + myValue.length)
                // 光标开始和光标结束重叠
                range.collapse(true)
                // 清除选定对象的所有光标对象
                // selection.removeAllRanges()
                // 插入新的光标对象
                // selection.addRange(range)
            }
            
        },


        test() {
            let textarea = this.$refs.textarea
            let str = textarea.innerText            
            let formatStr =  this.colorKeyword(str)
            textarea.innerHTML = formatStr
        },
    }
}

```