---
layout: post
title: vue中构建常量管理组件管理数据
categories: vue
description: vue中构建常量管理组件管理数据
keywords: vue, 常量管理组件
---

1，在utils中新建book.js文件

```js
export const FONT_SIZE_LIST = [
    {fontSize: 12},
    {fontSize: 14},
    {fontSize: 16},
    {fontSize: 18},
    {fontSize: 20},
    {fontSize: 22},
    {fontSize: 24}
]

export const FONT_FAMILY = [
    { font: 'Default' },
    { font: 'Cabin' },
    { font: 'Days One' },
    { font: 'Montserrat' },
    { font: 'Tangerine' }
  ]

  export function themeList(vue) {
    return [
      {
        alias: vue.$t('book.themeDefault'),
        name: 'Default',
        style: {
          body: {
            'color': '#4c5059',
            'background': '#cecece'
          },
          img: {
            'width': '100%'
          },
          '.epubjs-hl': {
            'fill': 'red', 'fill-opacity': '0.3', 'mix-blend-mode': 'multiply'
          }
        }
      },
      {
        alias: vue.$t('book.themeGold'),
        name: 'Gold',
        style: {
          body: {
            'color': '#5c5b56',
            'background': '#c6c2b6'
          },
          img: {
            'width': '100%'
          },
          '.epubjs-hl': {
            'fill': 'red', 'fill-opacity': '0.3', 'mix-blend-mode': 'multiply'
          }
        }
      }
      }
    ]
}


export function addCss(href){
    const link = document.createElement('link')
    link.setAttribute('rel','stylesheet')
    link.setAttribute('type','text/css')
    link.setAttribute('href',href)
    document.getElementsByTagName('head')[0].appendChild(link)
}

export function removeCss(href){
    const links = document.getElementsByTagName('link')
    for(let i = links.length; i >= 0; i--){
        const link = links[i]
        if(link && link.getAttribute('href') && link.getAttribute('href') === 'href'){
            link.parentNode.removeChild(link)
        }
    }
}

```

2，常量组件的使用

```js
// 一般，我们会把这种常量混入带mixin.js中，减少引用次数
import {mapGetters,mapActions} from 'vuex'
import {themeList, addCss, removeAllCss} from './book'
export const ebookMixin = {
    computed:{
        ...mapGetters([
            'fileName',
            'menuVisible'
        ]),
        themeList(){
            return themeList(this)
        }
    }
```

3, 在vue组件中使用

```js
<script type="text/ecmascript-6">
import {FONT_SIZE_LIST} from '../../utils/book'    // 引入常量模块
  export default {
    mixins: [ebookMixin],
    data() {
      return {
        fontSizeList:FONT_SIZE_LIST   // 使用常量
      }
    },
    methods: {
        setFontSize(fontSize){

        },
        showFontFamilyPopup(){
        
        }
  }
</script>
```

