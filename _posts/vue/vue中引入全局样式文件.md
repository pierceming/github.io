---
layout: post
title: vue中引入全局样式文件
categories: vue
description: vue中引入全局样式文件
keywords: vue，全局样式文件
---

1，新建一个global.scss文件

2，在main.js中引入global.scss文件

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
  store,
  render: h => h(App)
}).$mount('#app')
```

3，新建一个reset.scss的全局样式

```scss
/* http://meyerweb.com/eric/tools/css/reset/
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
a {
  text-decoration: none;
  -webkit-backface-visibility: hidden;
}
li {
  list-style: none;
}

html, body {
  width: 100%;
  height: 100%;
  overflow: hidden;
  user-select: none;
}
body {
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
html, body {
  font-family: 'PingFangSC-Light', 'PingFang SC', 'STHeitiSC-Light', 'Helvetica-Light', 'Arial', 'sans-serif';
}

```

在global.scss中引入reset.scss文件样式

```scss
@import './reset.scss';
```

在reset中新增一些样式

```scss
html, body {
  width: 100%;  // 设置宽高全屏
  height: 100%;
  overflow: hidden;  // 超出屏幕宽高部分，隐藏
  user-select: none; // 不允许用户在屏幕中进行长按操作
}
body {
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
html, body {  // 添加默认字体
  font-family: 'PingFangSC-Light', 'PingFang SC', 'STHeitiSC-Light', 'Helvetica-Light', 'Arial', 'sans-serif';
}
```

在global.scss中添加rem算法函数

```scss
$ratio: 375 / 10;
@function px2rem($px) {
  @return $px / $ratio + rem;
}
```

在实例中引入全局样式

```scss
<style lang="scss"  rel="stylesheet/scss" scoped>  // 注意lang='scss'必须要标记，不然会报错
@import "./assets/styles/global";
.text{
    font-family:'Days One';
    font-size: px2rem(20);
    color: orange;
}
</style>
```

