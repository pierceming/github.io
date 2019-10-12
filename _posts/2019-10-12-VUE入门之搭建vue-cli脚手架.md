---
layout: post
title: VUE入门之搭建vue-cli脚手架
categories: vue
description: VUE入门之搭建vue-cli脚手架
keywords: vue, vue入门, nodeJs
---

近来公司开始新的项目组建，在选取前端框架的时候，选取了VUE作为前端的开发框架，后台用的是SpringBoot，这个后面再讨论。今天我们讨论下VUE开发环境搭建问题，超级简单的几步；

## 1，下载nodeJs

- nodeJs网址：http://nodejs.cn
- 根据自己电脑的属性进行下载对应的版本号；

![](https://pierceming.github.io/images/vue/1570881679.png)

- 安装好nodeJs之后，在命令行窗户口输入node -v 检查nodeJs的版本，确认安装成功

- 安装完nodeJs之后，设置npm的镜像位淘宝镜像，

  ```shell
  npm config set registry https://registry.npm.taobao.org
  ```

- 检查镜像：

  ```shell
  npm config get registry
  ```

  出现https://registry.npm.taobao.org，说明镜像配置成功

- 搭建vue-cli全局脚手架

  ```sh
  npm install --global vue-cli

  ```

- 输入vue命令验证脚手架是否搭建成功

  ![](https://pierceming.github.io/images/vue/1570882479.png)

- 搭建第一个vue工程

  输入：vue init webpack my-vue (建议不要在c盘下操作，换一个盘，my-vue是工程的名字，会创建出一个这样的目录)

  ![](https://pierceming.github.io/images/vue/15708827471.png)

- 注意，工程名字与my-vue一致。下面会出现是否需要js语法检测，这个我们暂时用不到，就可以直接输入no，后面的都可以直接输入no，都是我们暂时用不到的

  ![](https://pierceming.github.io/images/vue/15708828501.png)

- 进入到工程文件夹内： cd my-vue

- 执行安装命令：npm install 

- 安装结束后，执行运行命令 npm run dev 

  ![](https://pierceming.github.io/images/vue/15708829901.png)

- 进入浏览器，输入localhost:8080就可以打开默认的模板了

  ![](https://pierceming.github.io/images/vue/15708830791.png)

  至此，我们的第一个vue工程就启动，并且搭建好了

  ​

  ​

  ​