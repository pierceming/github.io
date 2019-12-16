---
layout: post
title: vue中使用mixin.js实现组件使用
categories: vue
description: vue中使用mixin.js实现组件服用
keywords: vue，mixin.js
---

1，在工程根目录中新建utils目录，在utils中新建mixin.js

```js
import {mapGetters,mapActions} from 'vuex'
export const ebookMixin = {
    computed:{
        ...mapGetters([
            'fileName',
            'menuVisible'
        ])
    },
    methods: {
        ...mapActions([
            'setFileName',
            'setMenuVisible'
        ]),
        initGlobalStyle(){
            removeAllCss()
        }
    }
}
```

2，在vue组件中引用mixin组件

```js
<script type="text/ecmascript-6">
  import { ebookMixin } from '../../utils/mixin'
  export default {
    mixins: [ebookMixin],
    data() {
      return {
        
      }
    },
    methods: {
        setFontSize(fontSize){
            this.setDefaultFontSize(fontSize)
          // this.$store.dispatch('setDefaultFontSize',fontSize).then(() => {   })
        },
        showFontFamilyPopup(){
            this.setFontFamilyVisible(true)
        }
    
    }
  }
</script>
```

3，我们在actions.js的文件中写入的代码

```js
const actions = {
      setMenuVisible: ({ commit }, visible) => {
        return commit('SET_MENU_VISIBLE', visible)
      },
      setFileName: ({ commit }, fileName) => {
        return commit('SET_FILENAME', fileName)
      }
}

export default actions
```

4， 我们早getter.js中的文件

```js
const book = {
    fileName: state => state.book.fileName,
    menuVisible: state => state.book.menuVisible
}
export default book

```

5，我们在模块book.js的文件

```js
const book = {
    state: {
        fileName: '',
        menuVisible: true
    },
    mutations: {
        'SET_FILENAME':(state,fileName)=>{
          state.fileName = fileName
        },
        'SET_MENU_VISIBLE':(state,menuVisible)=>{
            state.menuVisible = menuVisible
          }
    }
}
export default book

```

