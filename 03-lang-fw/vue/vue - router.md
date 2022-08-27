```
[官网]

	: https://router.vuejs.org/zh/

[github]

  : https://github.com/vuejs/vue-router

[API]

	: https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1

[]

	: Vue官方的路由管理器, 和其的核心深度集成, 让构建单页面应用变得易如反掌
	# 嵌套的路由/视图表
	# 模块化的、基于组件的路由配置
	# 路由参数、查询、通配符
	# 基于 Vue.js 过渡系统的视图过渡效果
	# 细粒度的导航控制
	# 带有自动激活的 CSS class 的链接
	# HTML5 历史模式或 hash 模式，在 IE9 中自动降级
	# 自定义的滚动条行为

```

### 脚本安装

```
[vue-router.js]

	: https://unpkg.com/vue-router/dist/vue-router.js
  
  : <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

[]

<!DOCTYPE html>
<html>
<body>
<div id="app">
    <h1>Hello App!</h1>
    <p>
        <!-- 使用 router-link 组件来导航. -->
        <!-- 通过传入 `to` 属性指定链接. -->
        <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
        <router-link to="/foo">Go to Foo</router-link>
        <router-link to="/bar">Go to Bar</router-link>
    </p>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
</div>
</body>
</html>

<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

<script type="text/javascript">
// 0. 如果使用模块化机制编程，导入 Vue 和 VueRouter，要调用 Vue.use(VueRouter)
// 1. 定义（路由）组件 , 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由 每个路由应该映射一个组件。
// 其中"component" 可以是 通过 Vue.extend() 创建的组件构造器， 或者，只是一个组件配置对象
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置 你还可以传别的配置参数
const router = new VueRouter({
  // （缩写）相当于 routes: routes
  routes
})

// 4. 创建和挂载根实例 -> 通过 router 配置参数注入路由，从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')

</script>

// /login?redirect=%2Fdashboard -> %2F 解析 /
// redirect=/Fdashboard

// 通过注入路由器，我们可以在任何组件内通过 this.$router 访问路由器，也可以通过 this.$route 访问当前路由
// Home.vue
export default {
  computed: {
    username() {
      // 我们很快就会看到 `params` 是什么
      return this.$route.params.username
    }
  },
  methods: {
    goBack() {
      window.history.length > 1 ? this.$router.go(-1) : this.$router.push('/')
    }
  }
}
```

### NODE 安装

```
[vue-router]

	: npm install vue-router

[]

// 0. 如果使用模块化机制编程, 导入Vue和VueRouter, 要调用 Vue.use(VueRouter)

// 1. 定义 (路由) 组件。
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置
const router = new VueRouter({
  routes // (缩写) 相当于 routes: routes
})

// 4. 创建和挂载根实例, 通过 router 配置参数注入路由
const app = new Vue({
  router
}).$mount('#app')

```

```
[<router-link>]

	: 该组件用于设置一个导航链接, 切换不同 HTML 内容
  # to 属性, 目标路由的链接, 即要显示的内容
  # 点击时 值传到 router.push(), 值是字符串或描述目标位置对象

<!-- 字符串 -->
<router-link to="home">Home</router-link>

<!-- 使用 v-bind 的 JS 表达式 -->
<router-link v-bind:to="'home'">Home</router-link>

<!-- 不写 v-bind 也可以, 就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>


	: replace 属性, 点击时,调用router.replace(), 导航后不会留下 history 记录

	: append 属性, 当前 (相对) 路径前添加基路径
  
<router-link :to="{ path: 'relative/path'}" append></router-link>

	: tag 染成某种标签, 使用 tag prop 类指定何种标签, 同样它还是会监听点击, 触发导航
 
 <router-link to="/foo" tag="li">foo</router-link>

	: active-class 链接激活时使用的 CSS 类名

<style>
   ._active{
      background-color : red;
   }
</style>
<p>
   <router-link v-bind:to = "{ path: '/route1'}" active-class = "_active">Router Link 1</router-link>
</p>


	: exact-active-class 配置当链接被精确匹配的时候应该激活的 class

	: event 声明可以用来触发导航的事件。可以是一个字符串或是一个包含字符串的数组

// https://github.com/chrisvfritz/vue-2.0-simple-routing-example

[router-link & exact-active-class]

	: router-link 默认情况下的路由是模糊匹配, exact-active-class 全包含匹配

```

### 概念

```
[动态路由匹配]

	: 某种模式匹配到的所有路由, 全都映射到同个组件
  
  : 路由路径中使用“动态路径参数” (dynamic segment) 
  // { path: '/user/:id', component: User } // 动态路径参数 以冒号开头
  // $route.params.id // 获取动态参数 (对应的值都会设置到 $route.params)
  // 响应路由参数的变化 -> 原来的组件实例会被复用, 两个路由都渲染同个组件, 比起销毁再创建, 复用则显得更加高效
  // 件的生命周期钩子不会再被调用

[嵌套路由]

	: 应用界面, 通常由多层嵌套的组件组合而成, URL 中各段动态路径也按某种结构对应嵌套的各层组件
  // children 配置

[编程式的导航]

	: 除了使用 <router-link> 创建 a 标签来定义导航链接, 也可以使用 router 实例方法, 通过编写代码来实现

	: router.push(location, onComplete?, onAbort?) 向 history 栈添加一个新的记录
  // 在 Vue 实例内部, 你可以通过 $router 访问路由实例 , this.$router.push
  // 当你点击 <router-link> 时, 这个方法会在内部调用, 等同于调用 router.push(...)
  // 声明式 <router-link :to="...">	
  // 编程式 router.push(...)
  
  : router.replace(location, onComplete?, onAbort?)
  // 它不会向 history 添加新记录, 直接替换 当前的 history 记录
  // 声明式 <router-link :to="..." replace>
  // 编程式 router.replace(...)
  
  : router.go(n) history 记录中向前或者后退多少步
  

// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})

[命名路由]

	: 名称来标识一个路由

[命名视图]

	: 同时 (同级) 展示多个视图，而不是嵌套展示
  // 界面中拥有多个单独命名的视图，而不是只有一个单独的出口
  // router-view 没有设置名字，那么默认为 default

<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>

  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]

  : 嵌套命名视图, 使用命名视图创建嵌套视图的复杂布局

<div>
  <h1>User Settings</h1>
  <NavBar/>
  <router-view/>
  <router-view name="helper"/>
</div>

{
  path: '/settings',
  // 你也可以在顶级路由就配置命名视图
  component: UserSettings,
  children: [{
    path: 'emails',
    component: UserEmailsSubscriptions
  }, {
    path: 'profile',
    components: {
      default: UserProfile,
      helper: UserProfilePreview
    }
  }]
}

[重定向和别名]

	: 重定向也是通过 routes 配置来完成
  // { path: '/a', redirect: '/b' }
  //  { path: '/a', component: A, alias: '/b' }

[路由组件传参]

	: 组件中使用 $route 会使之与其对应路由形成高度耦合

[HTML5 History 模式]

[导航守卫]

	: 用来通过跳转或取消的方式守卫导航
  
  : 全局前置守卫 router.beforeEach
  
  : 全局解析守卫 router.beforeResolve
  
  : 全局后置钩子 router.afterEach
  
  : 路由独享的守卫 路由配置上直接定义 beforeEnter
  
  : 组件内的守卫 beforeRouteEnter beforeRouteUpdate beforeRouteLeave

[路由元信息]

	: 定义路由的时候可以配置 meta 字段, 称呼 routes 配置中的每个路由对象为 路由记录

[过渡动效]

	: <transition> 组件给它添加一些过渡效果

[数据获取]

	: 进入某个路由后，需要从服务器获取数据
  // 导航完成之前获取  beforeRouteEnter
	// 导航完成之后获取  created

[滚动行为]

[路由懒加载]

	: 不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件

```

