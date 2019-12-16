---
layout: post
title: vue中使用mixin.scss控制公共样式
categories: vue
description: vue中使用mixin.scss控制公共样式
keywords: vue，mixin.scss
---

1，在assestswe文件夹中新建mixin.scss文件

```js
$ratio: 375 / 10;

@function px2rem($px) {
  @return $px / $ratio + rem;
}
// mixin语法
  @mixin center{
    dispaly:flex;
    justify-content:center;
    align-items:center;
  }
```

2，将mixin.scss放在global.js中进行管理

```js
@import './reset.scss';
@import './mixin.scss';
```

3，在vue文件样式中引入全局样式

```js
<style lang="scss"  rel="stylesheet/scss" scoped>
@import "./assets/styles/global";
.right{
  flex:1;
  display:flex;
  justify-content:flex-end;
  .icon-wrapper{
    flex:0 0 px2rem(40);
    @include center;  // 引入mixin语法中样式
    .icon-cart{
      font-size:px2rem(22);
    }
  }
}
</style>
```

4，注意点：

```scss
1, 在mixin.scss中css中的函数需要加上@
@function px2rem($px){
  @return $px / 20 + rem;
}
// mixin语法
  @mixin center{
    dispaly:flex;
    justify-content:center;
    align-items:center;
  }
```

