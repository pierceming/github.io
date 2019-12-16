---
layout: post
title: vue中使用vuex进行组件间的数据传递
categories: vue
description: vue中使用vuex进行组件间的数据传递
keywords: vue, 组件间的数据传递, vuex
---

1，创建项目的时候已经选择了vuex的组件，如果没有选择则需要安装组件

npm i --save vuex

2, 在工程的根目录中新建一个store文件夹在其中新建store.js的文件

3，引入vue, vuex, 在vue中挂载vuex

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: { // 用来存数据
    test: 1
  },
  mutations: {  // 用来设置数据
    'SET_TEST':(state, newTest) => {
        state.test = newTest
    }
  },
  actions: {   // commit调用mutations改变test的值
      setTest:({commit,state},newTest) => {
          return commit('SET_TEST',newTest)
      }
  },
  modules: {
  }
})
```

4, 在main.js中引入store.js 然后挂载store即可

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import './assets/styles/icon.css'
import './assets/styles/global.scss'

Vue.config.productionTip = false

new Vue({
  router,
  store,   // 挂载store
  render: h => h(App)
}).$mount('#app')
```

5, 在具体引用中使用

```js
 mounted(){
        this.$store.dispatch('setTest',10).then(()=>{
            console.log(this.$store.state.test)
        })
    }
// $store.dispatch('setTest',10) 调用的是store.js中action方法
```

6，vuex的改进

我们观察发现，如果我们的系统中有大量的这种属性值需要进行后期计算，这样的维护是不可持续的。这样vuex为我们引入了一个模块化的概念，就是一个模块管理自己的一个store，通过module的方式进行集中式管理

7, 在store的文件夹中建立一个module的文件夹，在module文件夹中建立一个book.js的模块。

```js
const book = {
    state: { // 用来存数据
        test: 1
      },
      mutations: {  // 用来设置数据
        'SET_TEST':(state, newTest) => {
            state.test = newTest
        }
      },
      actions: {   // commit调用mutations改变test的值
          setTest:({commit,state},newTest) => {
              return commit('SET_TEST',newTest)
          }
      }
}
export default book
```

8, 在store的目录下面添加一个getters.js的文件，来获取module中book的数据

```js
const book = {
    test: state => state.book.test
}

export default book
```



9，在index.js中引入getters

```js
import Vue from 'vue'
import Vuex from 'vuex'
import book from './modules/book'
import getters from './getters'
Vue.use(Vuex)

export default new Vuex.Store({
  modules: {
    book
  },
  getters
})
```

10，在具体使用中使用mapGetters方法

```js
import {mapGetters} from 'vuex'
export default {
    computed:{
        ...mapGetters(['test'])
    },
    mounted(){
        this.$store.dispatch('setTest',10).then(()=>{
            console.log(this.test)  //直接使用this.test就可改变属性值
        })
    }
}
```

11， 扩展...mapgetters

```typescript
1, ...表示es6的扩展运算符
仿写...mapgettes（['test']）
const getters = {
  a：()=> 1,
  b:()=> 2
}
function fn(keys){
  const data = {}
  keys.forEach(key => {
    if(getters.hasOwnProperty(key)){
      data[key] = getters[key]
    }
  })
  return data
}
export default{
  computed:{
    ...fn(['a','b','c'])
  },
  mounted(){
    console.log(this.a,this.b)
  }
}
```



