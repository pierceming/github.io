---
layout: post
title: vue中使用路由
categories: vue
description: vue中使用路由
keywords: vue, 路由, Router
---

1，在根目录中新建一个router.js文件

2，引入vue, Router

3,挂载路由

4，设置路由

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    redirect: '/ebook'
  },
  {
      path:'/ebook',
      component:() => import('../views/ebook/index.vue'),
      children:[
          {
              path:':fileName',
              component: () => import('../components/ebook/EbookReader.vue')
          }
      ]
  }
]

const router = new VueRouter({
  routes
})

export default router
```

5，在main.js中引入路由组件

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import './assets/styles/icon.css'
import './assets/styles/global.scss'
import i18n from './lang'
Vue.config.productionTip = false

new Vue({
  router,
  store,
  i18n,
  render: h => h(App)
}).$mount('#app')
```

6，在component中创建一个组件ebook-reader用于接收动态路由

```js
<template>
  <div class="ebook-reader">
      <div id = 'reader'{{$route.params.fileName}}</div>
  </div>
</template>

<script>
export default {
  
}
```

7,在view文件下的index.vue中引入ebook-reader组件

```js
<template>
  <div class="ebook">
      <ebook-reader></ebook-reader>
  </div>
</template>

<script>
import EbookReader from '../../components/ebook/EbookReader'
export default {
    components:{
        EbookReader
    }
}
</script>
```

