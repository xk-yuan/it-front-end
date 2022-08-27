# vue-case-helloworld

> Vue 3 + Vite

> 页面 + 组件 + 路由 + 存储 + 权限 + API模块 + 工具模块

> Vue 3 + Vite + vue-router + vuex + axios + mockjs + vite-plugin-mock + js-cookie + element-plus

## 资源

> [Vite + Vue3 遇到的一些问题汇总](https://juejin.cn/post/7028137821269393438)
>
> [Vue3学习与实战 · 配置使用vue-router路由](https://www.cnblogs.com/tive/p/15609082.html)
> [vite 项目配置](https://blog.csdn.net/CirtusSoda/article/details/122600036)
> [Vue3的Vue—Router配置](http://events.jianshu.io/p/00366c996087)

> [vue3 +vite 动态菜单和路由懒加载](https://blog.csdn.net/qq_44747508/article/details/122494308)
> [vue路由权限管理（vue2和vue3）](https://www.csdn.net/tags/NtTaYg4sMzE5MzQtYmxvZwO0O0OO0O0O.html)
>
> [vue3使用mockjs](https://blog.csdn.net/wenhui6/article/details/121909804)


## 项目搭建

### 搭建步骤 (vite 脚手架)

> 1. 通过 vite 创建项目

- yarn create vite vue-vite-helloworld --template vue
- cd vue-vite-helloworld

> 2. 安装依赖

- yarn

> 3. 启动

- yarn dev

> 4. 配置

```js 项目架构
vue-vite-helloworld
  │
  ├─.vscode
  │
  ├─ README.md
  ├─ .gitignore
  ├─ LICENSE
  ├─ package.json
  ├─ yarn.lock
  │
  ├─ vite.config.js
  ├─ index.html
  │
  ├─ mock
  ├─ public
  │   └─ favicon.ico
  └─src
      ├─ main.js
      ├─ App.Vue
      │
      ├─ api
      ├─ assets
      │   └─ logo.png
      ├─ components
      │   └─ HelloWorld.vue
      ├─ layout
      ├─ router
      ├─ store
      ├─ styles
      ├─ utils
      └─ views
```

- vite.config.js      Vite配置

- index.html          页面入口
- src/main.js         Vue3入口
- App.Vue             APP入口

- src    项目源码模块
- 
- api    API模块
- utils  工具模块
- 
- router     路由模块
- store      存储模块
- 
- components 组件模块
- views      页面模块
- layout     布局模块
- assets     静态资源模块
- styles     样式模块

### 页面 + 组件 + 路由 + 存储 + 权限

> 5. API模块 + 工具模块 + MOCK

- yarn add -D axios
- yarn add -D mockjs
- yarn add -D vite-plugin-mock

```json package.json
{
  "devDependencies": {
    "axios": "^0.27.2",
    "mockjs": "^1.1.0",
    "vite-plugin-mock": "^2.9.6",
  }
}
```

```js utils/request.js
import axios from 'axios'
//
import store from '../store'
import { getToken } from '../utils/auth'

// Axios
const service = axios.create({
  baseURL: '/mockapi',   // /mockapi, 或 import.meta.env.VITE_APP_BASE_API 引入 .env.development 里的配置 VITE_APP_BASE_API
  withCredentials: true,
  // timeout: 5000
})

// Axios Interceptors Request
service.interceptors.request.use(
  (config) => {
    console.info("axios request : %s => %s ", config.baseURL + config.url, JSON.stringify(config.data))

    // 请求前处理, 设置请求头 : Token 和 用户相关信息 
    if (store.getters.token) {
      config.headers['Authorization'] = getToken()
    }
    return config
  }, (error) => {
    // 请求错误
    return Promise.reject(error)
  }
)

// Axios Interceptors Response
service.interceptors.response.use((response) => {
  // 处理请求相应结果
  const data = response.data
  console.info("axios response : %s ", JSON.stringify(data))

  if (data && data.code && data.code == '9527') {
    // 登录失效 (Token失效)
    store.dispatch('user/nologin')
  } else if (data && data.code && data.code !== '200') {
    // 返回失败
  }
  return data
}, (error) => {
  // 错误处理
  if (error.response) {
    console.error("message: " + error.message)
  }
  return Promise.reject(error)
})

export default service
```

```js vite.config.js
import { viteMockServe } from 'vite-plugin-mock'
export default defineConfig({
  plugins: [
    viteMockServe({
      supportTs: false,
      logger: false,
      mockPath: "./src/api/mock/"  // mock文件夹路径
    })
  ]
}
```

```js mock/index.js
export default [
  {
    type: 'get',
    url: '/mockapi/service/101/api/v1/login',
    response: () => {
      return { code: 200, data: token }
    }
  }
]
```

> 6. 配置路由 (vue-router@4.x)

- yarn add -D vue-router@4

```json package.json
{
  "devDependencies": {
    "vue-router": "4",
  }
}
```

```js vite.config.js
import path from 'path'

// https://vitejs.dev/config/ | https://cn.vitejs.dev/config/
export default defineConfig({
  resolve: {
    alias: {
      '@': path.join(__dirname, 'src')
    }
  }
})
```

```js main.js
import router from './router'

createApp(App)
  .use(router)
  .mount('#app')
```

```js router/index.js
import {createRouter, createWebHistory, createWebHashHistory} from 'vue-router'
import { defineAsyncComponent } from 'vue'

// 公共静态路由
const staticRoutes = [
  {
    path: '/',
    name: 'Index',
    component: defineAsyncComponent(() => import('@/views/home.vue')),
    meta: {
      title: '首页',
    },
  },
  {
    path: '/home',
    name: 'home',
    component: defineAsyncComponent(() => import('@/views/home.vue')),
    meta: {
      title: '主页',
    },
  },
  {
    path: '/404',
    component: () => import('@/views/404.vue'),
    hidden: true,
  },
  {
    path: '/*',
    component: () => import('@/views/404.vue'),
    hidden: true,
  },
]

// 路由配置
const router = createRouter({ 
  history: createWebHistory(),  // createWebHistory: history 模式; createWebHashHistory:hash 模式 
  routes: [
    ...staticRoutes,
  ]
})

export default router
```

```js App.vue
<template>
  <router-view/>
</template>
```

> 7. 配置存储 (vuex)

- yarn add -D vuex@next

```json package.json
{
  "devDependencies": {
    "vuex": "^4.0.2",
  }
}
```

```js main.js
import store from './store'

createApp(App)
  .use(store)
  .mount('#app')
```

```js store/index.js
import { createStore } from 'vuex'
 
const store = createStore({
  state () {
    return {
    }
  },
  mutations: {
  }
})
 
export default store;
```

> 8. 权限 (权限 = 用户 + 角色 + 菜单路由)

- vue-router (路由) + vuex (存储) + js-cookie (Cookie) + Auth (Token, User 用户信息, Role 角色信息, App 应用信息)
- yarn add -D js-cookie

```js permission.js
// 4. 权限校验, 校验Token权限, 校验菜单路由权限
// 注册路由守卫, 路由变更时进行路由权限判断控制
import store from '../../store'
// progress bar
import NProgress from 'nprogress'
// progress bar style
import 'nprogress/nprogress.css'
// cookie token
import { getToken, removeToken } from '../../utils/auth'
import { getPageTitle } from '../../utils/settings'
import { flat, deepCopy } from '../../utils'

console.debug('router permission.js')

NProgress.configure({
  showSpinner: false,
})

// 白名单
const whiteList = ['/login', '/404']

/**
 * 获取当前用户菜单资源列表
 * @returns 
 */
const getMenu = () => {
  return deepCopy(store.getters.relevanceResource)
}

/**
 * 判断菜单资源访问权限
 *
 * @param {*} to 
 * @param {*} from 
 * @returns 
 */
const hasMenu = (to, from) => {
  // 获取菜单资源列表
  const relevanceResource = getMenu();
  // 菜单资源列表为空, 则绕过判断; 如果是从首页点击跳转，或者跳转到首页、404、登录页，则绕过判断;
  if (!relevanceResource || !relevanceResource.length) return true

  console.debug("router beforeEach hasMenu : " + relevanceResource)
  // 菜单资源树, 扁平化处理
  const flatMenu = flat(relevanceResource)
  const menus = flatMenu.filter((item) => item.type == 2)
  const menuPath = menus.map((item) => item.url)
  // 将要跳转的菜单路由
  const fullPath = to.fullPath.split('/table')[0]
  const matchPath = to.matched[0].path

  console.info("router beforeEach fullPath : " + fullPath + ", matchPath : " + matchPath)
  if (menuPath.includes(fullPath) || menuPath.includes(matchPath)) {
    return true
  }

  return false
}

/**
 * 全局路由守卫: 路由菜单资源, 访问权限校验
 * 1. 校验Token是否存在, 不存在在跳转登录页
 * 2. 校验应用信息
 * 3. 校验路由菜单是否有访问权限, 没有跳转404
 *
 * @param {*} to 
 * @param {*} from
 * @param {*} next 
 * @returns 
 */
function beforeEach(to, from, next) {
  console.debug("router beforeEach ...");

  // 1. 获取信息 : Token, User 用户信息, Role 角色信息, App 应用信息
  const hasToken = getToken()
  // 应用信息: 是否只有一个产品
  const isOneProduct = null; // store.state.app.productList && store.state.app.productList.length == 1
  // 初始路由
  const initialUrl = '/'; // store.state.app.initialUrl

  //
  NProgress.start()
  document.title = getPageTitle(to.meta.title)

  console.debug("router beforeEach token : " + hasToken);

  // 是否有 token
  if (hasToken) {
    if (to.path === '/login') {
      removeToken()
      next({ path: '/home', })
      NProgress.done()
    } else {
      console.debug("router beforeEach path : " + to.path);

      if (to.path === '/home') {
        // 如果进入首页，产品只有一个的话，直接进入初始url
        isOneProduct &&
          next({
            path: initialUrl,
          })
      }
      // 在白名单则直接跳转
      if (whiteList.indexOf(to.path) !== -1) {
        // if (to.redirectedFrom && to.redirectedFrom !== '/') {
        //   next(to.redirectedFrom)
        // }
        next()
      } else {
        // 判断菜单路由是否有访问权限
        if (hasMenu(to, from)) {
          next()
        } else {
          next('/404')
          NProgress.done()
        }
      }
    }
  } else {
    // 在白名单则直接跳转, 否则跳转到登录页
    if (whiteList.indexOf(to.path) !== -1) {
      next()
    } else {
      next(`/login?redirect=${to.path}`)
      NProgress.done()
    }
  }
};

// 全局路由守卫
function afterEach(to, from) {
  console.debug("router afterEach ...");
  NProgress.done()
};
 
export default {beforeEach, afterEach}
```

```js router/index.js
// 注册权限控制
import permission from './auth/permission'

// 全局路由守卫
router.beforeEach((to, from, next)=>{
  permission.beforeEach(to, from, next)
})

router.afterEach((to, from)=>{
  permission.afterEach(to, from)
})
```


```js utils/auth.js
// Cookies
import Cookies from 'js-cookie'

const TokenKey = 'token'

/**
 * 获取鉴权Token
 * @returns {String}
 */
export function getToken() {
  return Cookies.get(TokenKey)
}

/**
 * 设置鉴权Token
 * @param {String} token 
 * @returns 
 */
export function setToken(token) {
  return Cookies.set(TokenKey, token)
}

/**
 * 移除鉴权Token
 * @returns void
 */
export function removeToken() {
  return Cookies.remove(TokenKey)
}
```

```js utils/index.js
/**
 * 把要被比较的数据扁平化，并且去掉所有的childList，便于比较
 * @param {*} arr - delkey 被比较的数组
 * @param {*} delKey 
 * @returns 
 */
export function flat(arr, delKey = 'childList') {
    return arr.reduce((prev, current) => {
        prev.push(current)
        if (current[delKey] && current[delKey].length) {
            prev = [...prev, ...flat(current[delKey])]
        }
        delete current[delKey]
        return prev
    }, [])
}

/**
 * 深拷贝
 * @param {*} obj 
 * @returns 
 */
export function deepCopy(obj) {
  let result = obj
  if (typeof obj === 'object' && obj !== null) {
    result = Object.prototype.toString.call(obj) === '[object Array]' ? [] : {}
    for (let prop in obj) {
      result[prop] = deepCopy(obj[prop])
    }
  }
  return result
}
```


### 布局、导航 Layout & UI

- yarn add -D element-plus

> 9. Layout & UI

```json package.json
{
  "devDependencies": {
    "element-plus": "^2.2.0",
  }
}
```

```js main.js
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

//
createApp(App)
  .use(ElementPlus)
  .mount('#app')
```
