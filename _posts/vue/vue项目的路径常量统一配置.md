---
layout: post
title: vue项目的路径常量统一配置
categories: vue
description: vue项目的路径常量统一配置
keywords: vue，路径常量统一配置
---

1，在我们的项目中经常会将测试环境和生产环境分开，我们在项目中请求nginx中的静态资源文件时，不能讲路径写死，这时候我们需要统一配置下不同环境下请求的路径地址

方法：在工程的根目录下创建.env.production文件

```properties
VUE_APP_EPUB_URL=http://47.99.166.157/epub
VUE_APP_EPUB_OPF_URL=http://47.99.166.157/epub2
VUE_APP_RES_URL=http://47.99.166.157/book/res
VUE_APP_BASE_URL=http://47.99.166.157:3000
VUE_APP_VOICE_URL=http://47.99.166.157:3000
VUE_APP_BOOK_URL=http://47.99.166.157:3000
```

具体使用中使用process API进行数据调用

![https://pierceming.github.io/images/vue/18.png](D:\software\piercespage\pierce.github.io\images\vue\18.png)

同样在根目录下见一个开发环境配置文件.env.development

```properties
VUE_APP_EPUB_URL=http://47.99.166.158/epub
VUE_APP_EPUB_OPF_URL=http://47.99.166.158/epub2
VUE_APP_RES_URL=http://47.99.166.158/book/res
VUE_APP_BASE_URL=http://47.99.166.158:3000
VUE_APP_VOICE_URL=http://47.99.166.158:3000
VUE_APP_BOOK_URL=http://47.99.166.158:3000
```

在打包的时候，可以选择是哪个环境的配置即可。如何打包，见打包页详情