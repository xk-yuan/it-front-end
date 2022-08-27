# VUE Install

> 安装

### 安装方式

> 1. script 引入

```js
<script src="https://unpkg.com/vue@next"></script>
```

[helloworld 案例](case/vue-case-helloworld.md)

> 2. npm安装

npm install vue@next

npm install -D @vue/compiler-sfc # 单文件组件的配套工具。使用单文件组件，需要安装。需要为已选择的打包工具选择一个配套的单文件组件 loader 或 plugin。Vue 2 过渡而来的，请注意 @vue/compiler-sfc 替换掉了 vue-template-compiler。


> 2. 通过脚手架 Vite

npm init vite hello-vue3 -- --template vue # 或 yarn create vite hello-vue3 --template vue

> 3. 通过脚手架 vue-cli

npm install -g @vue/cli # 或 yarn global add @vue/cli
vue create hello-vue3   # 选择 vue 3 preset

