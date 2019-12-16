---
layout: post
title: vue中使用web缓存机制
categories: vue
description: vue中使用web缓存机制
keywords: vue, 缓存, web-storage-cache
---

1，安装web缓存库

npm i --save web-storage-cache

2，在utils文件夹中新建localStorage.js

3，引入web-storage-cache

```js
import Storage from 'web-storage-cache'

const localStorage = new Storage()

export function getLocalStorage(key) {
  return localStorage.get(key)
}

export function setLocalStorage(key, value, expire = 30 * 24 * 3600) {
  return localStorage.set(key, value, { exp: expire })
}

export function removeLocalStorage(key) {
  return localStorage.delete(key)
}

export function clearLocalStorage() {
  return localStorage.clear()
}

export function getTheme(fileName) {
  return getBookObject(fileName, 'theme')
}

export function saveTheme(fileName, theme) {
  setBookObject(fileName, 'theme', theme)
}

export function getFontSize(fileName) {
  return getBookObject(fileName, 'fontSize')
}

export function saveFontSize(fileName, fontSize) {
  setBookObject(fileName, 'fontSize', fontSize)
}

export function getBookObject(fileName, key) {
  if (getLocalStorage(`${fileName}-info`)) {
    return getLocalStorage(`${fileName}-info`)[key]
  } else {
    return null
  }
}

export function setBookObject(fileName, key, value) { // 相当于常见了一个book的缓存对象
  let book = {}
  if (getLocalStorage(`${fileName}-info`)) {
    book = getLocalStorage(`${fileName}-info`)
  }
  book[key] = value
  setLocalStorage(`${fileName}-info`, book)
}

```

2，在vue组件中使用缓存机制

```js
 import { ebookMixin } from '../../utils/mixin'
import {FONT_SIZE_LIST} from '../../utils/book'
import { saveFontSize } from '../../utils/localStorage'
  export default {
    mixins: [ebookMixin],
    data() {
      return {
        fontSizeList:FONT_SIZE_LIST
      }
    },
    methods: {
        setFontSize(fontSize){       
            saveFontSize(this.fileName, fontSize)     // 调用缓存机制，缓存当前字体，页面刷新数据也不会消失 
        },
        showFontFamilyPopup(){
            this.setFontFamilyVisible(true)
        }
    }
  }
</script>
```

