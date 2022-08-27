```
[官网]

	: https://vuex.vuejs.org/zh/

[]

// Flux、Redux、 The Elm Architecture

// http://www.ayqy.net/blog/vuex/
// https://cloud.tencent.com/developer/article/1454687
// https://www.jianshu.com/p/f91cbb1ade41
// https://segmentfault.com/a/1190000012881956
```

    Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式库。 以利用 Vue.js 的细粒度数据响应机制来进行高效的状态更新。

    采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。对 vue 应用中多个组件的共享状态进行集中式的管理(读/写)。

    Vuex实现了一个单向数据流，在全局拥有一个State存放数据，当组件要更改State中的数据时，必须通过Mutation进行，Mutation同时提供了订阅者模式供外部插件调用获取State数据的更新。

```
[状态管理模式]

	: state
  // 单一状态树, 一个对象就包含全部的应用层级状态
  // 作为一个 “唯一数据源 (SSOT)” 而存在, 每个应用将仅仅包含一个 store 实例
  //  Vuex 的状态存储是响应式, 驱动应用的数据源
  // 从 store 实例中读取状态最简单的方法就是在计算属性中返回某个状态
  

// 创建一个 Counter 组件
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}

// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

// mapState 辅助函数帮助我们生成计算属性
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })

  : view    以声明方式将 state 映射到视图

  : getters
  // 接受 state 作为其第一个参数
  // 返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算
  //  对数据获取之前的再次编译，可以理解为state的计算属性
  
  : mutations 修改状态
  // 状态的唯一方法是提交 mutation , 同步的 ($store.commit('',params))

  : actions 响应在 view 上的用户输入导致的状态变化
  // 提交的是 mutation，而不是直接变更状态, 可以包含任意异步操作
  // 异步操作 $store.dispath('')

  : modules 子模块, 为了开发大型项目，方便状态管理而使用
  // store 分割成模块（module）
  // 每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块

```

### 单向数据流图示

![](http://localhost/it/front-end/1573628501312-848cf008-6181-44df-a621-ec1a8042803a.png#align=left&display=inline&height=505&originHeight=866&originWidth=1280&size=0&status=done&style=none&width=746)

### 流程示意图

![](http://localhost/it/front-end/1573628714860-49283ad0-b497-434c-b9e2-66398466208b.png#align=left&display=inline&height=551&originHeight=551&originWidth=701&size=0&status=done&style=none&width=701)

![image.png](http://localhost/it/front-end/1578016895766-e5780832-ba8e-4bf6-8c0a-98b4510b973b.png#align=left&display=inline&height=650&name=image.png&originHeight=602&originWidth=691&size=231677&status=done&style=none&width=746)

### 安装

![image.png](http://localhost/it/front-end/1578016944686-608d66c4-8d5f-4680-bb11-3c5f0740ee59.png#align=left&display=inline&height=126&name=image.png&originHeight=135&originWidth=800&size=11587&status=done&style=none&width=746)

```
[安装配置]

	: npm install vuex --save

// store/index.js
import Vue from 'vue'
import Vuex from 'vuex';

Vue.use(Vuex);

// 全局访问的state对象 (this.$store.state.x)
const state= {}

// 实时监听state值的变化 (this.$store.getters.x)
const getters= {}

// 自定义改变state初始值的方法, 参数除了state之外还可以再传额外的参数, this.$store.commit('x')
const mutations = {}

// 自定义异步触发mutations里函数的方法, this.$store.dispatch('x')
const actions = {}

const store = new Vuex.Store({
       state,
       getters,
       mutations,
       actions
});

export default store;

// main.js
import {store} from '../store/index'

new Vue({
  ...
  store,
  ...
})
```

![image.png](http://localhost/it/front-end/1578015641513-701e8051-8231-4235-8546-1d60ddebc8d8.png#align=left&display=inline&height=242&name=image.png&originHeight=312&originWidth=960&size=108247&status=done&style=none&width=746)
