---
layout: post
title: vue中国际化使用
categories: vue
description: vue中国际化使用
keywords: vue, 国际化, i18n
---

1，安装国际化依赖

2，使用命令安装 npm i --save vue-i18n

3， 我们在语言包中准备好国际化json文件en.js,cn.js文件

```js
// cn.js
const messages = {
  book: {
    pulldownAddMark: '下拉添加书签',
    releaseAddMark: '松手添加书签',
    pulldownDeleteMark: '下拉删除书签',
    releaseDeleteMark: '松手删除书签',
    selectFont: '选择字体'
  }
}
export default messages

// en.js
const messages = {
  book: {
    pulldownAddMark: 'Pull down to add bookmark',
    releaseAddMark: 'Release to add bookmark',
    pulldownDeleteMark: 'Pull down to delete bookmark',
    releaseDeleteMark: 'Release to add bookmark',
    selectFont: 'Select Font'
  }
}
export default messages

```

4，在lang文件中新建一个index.js

5，引入i18n组件

6，加载i18n插件

```js
import Vue from 'vue'
import VueI18n from 'vue-i18n'
import en from './en'
import cn from './cn'
import { getLocale, saveLocale } from '../utils/localStorage'

/**加载插件 */
Vue.use(VueI18n)

const messages = {
  en, cn
}

let locale = getLocale()
if (!locale) {
  locale = 'cn'
  saveLocale(locale)
}

const i18n = new VueI18n({
  locale,
  messages
})

export default i18n
```

7，在main.js中引入国际化资源

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import './assets/styles/icon.css'
import './assets/styles/global.scss'
import i18n from './lang'   // 引入国际化资源文件
Vue.config.productionTip = false

new Vue({
  router,
  store,
  i18n,   //挂载国际化资源
  render: h => h(App)
}).$mount('#app')
```

8，引用国际化$t('xxx.xxx')

```js
<div class="content-page-tab">
                    <div class="content-page-tab-item"
                    :class="{'selected': currentTab === 1}"
                    @click="selectTab(1)">{{$t('book.navigation')}}</div>
                    <div class="content-page-tab-item"
                    :class="{'selected': currentTab === 2}"
                    @click="selectTab(2)">{{$t('book.selectFont')}}</div>   
	// 引用国际化资源 {{$t('book.selectFont')}}
                </div>
```



