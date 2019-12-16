---
layout: post
title: vue中使用scss语法
categories: vue
description: vue中使用scss语法
keywords: vue，scss语法
---

1，scss语法时将css语法进行封装一层的语法，其本质并有发生改变，基本语法页没有发生大的改变，只是在使用的时候会有所区别

2，下载scss的渲染器，加载器

npm i --save-dev node-sass sass-loader

```json
  "dependencies": {
    "core-js": "^3.4.3",
    "vue": "^2.6.10",
    "vue-router": "^3.1.3",
    "vuex": "^3.1.2"
  },
  "devDependencies": {
    "@vue/cli-plugin-babel": "^4.1.0",
    "@vue/cli-plugin-eslint": "^4.1.0",
    "@vue/cli-plugin-router": "^4.1.0",
    "@vue/cli-plugin-vuex": "^4.1.0",
    "@vue/cli-service": "^4.1.0",
    "@vue/eslint-config-standard": "^4.0.0",
    "babel-eslint": "^10.0.3",
    "eslint": "^5.16.0",
    "eslint-plugin-vue": "^5.0.0",
    "vue-template-compiler": "^2.6.10"
  }
```

在package.json文件中会有这一样依赖管理

使用--save-dev 会将下载的组件依赖放入devDependencies中 --save则不会只会在dependencies加入你下载的组件

```json
 "devDependencies": {
    "@vue/cli-plugin-babel": "^4.1.0",
    "@vue/cli-plugin-eslint": "^4.1.0",
    "@vue/cli-plugin-router": "^4.1.0",
    "@vue/cli-plugin-vuex": "^4.1.0",
    "@vue/cli-service": "^4.1.0",
    "@vue/eslint-config-standard": "^4.0.0",
    "babel-eslint": "^10.0.3",
    "eslint": "^5.16.0",
    "eslint-plugin-vue": "^5.0.0",
    "node-sass": "^4.13.0",
    "sass-loader": "^8.0.0",
    "vue-template-compiler": "^2.6.10"
  }
```

