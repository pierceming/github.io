---
layout: post
title: VUE工程快速去除eslint检查
categories: vue
description: VUE工程快速去除eslint检查
keywords: vue, vue入门, eslint
---

新手在刚开始接触vue的时候一个头大的问题就是eslint语法检查了。eslint语法检查简直是魔鬼。让我们刚入门的小伙伴很是伤神又费力。在网上找了很多种办法，貌似效果不怎样；下面我介绍一个2步就能解决这种esLint检查的问题。

- 1， 在创建工程的时候，不要添加eslint检查和test模块测试，这样在项目运行的时候，就不会出现这种eslint检查问题了；

- 2， 如果小伙伴不小心在创建工程的时候还是启用的eslint检查和test单元。那在工程启动后如何进行取消呢？

  - 2.1 首先找到.eslintrc.js文件，在文末的rules里面新增一行即可

    ```json
    'indent': 'off'  // 这一行表示取消空格之类的检查
    ```

    总体如下：

    ```json
     rules: {
        // allow async-await
        'generator-star-spacing': 'off',
        // allow debugger during development
        'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
        'indent': 'off'
     }
    ```

  - 2.2 消除文本行末检查，在.eslintignore加入\*.js \*.vue 即可

    ```yaml
    /build/
    /config/
    /dist/
    /*.js
    /test/unit/coverage/
    *.js
    *.vue
    ```

  当然了，vue语法或者其他js语法之类的就不管eslint什么事了。

  祝大家玩得开心！