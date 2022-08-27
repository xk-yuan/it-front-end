# nodejs项目

> 创建nodejs项目：nodejs + javascript; nodejs + typescript;  nodejs + typescript + webpack

- 命令行项目
- 后端WEB项目
- 前端项目

## 资源

> [如何创建一个NodeJs命令行交互项目](https://blog.51cto.com/u_15067238/4000251)

> [使用 Typescript 开发 Nodejs 命令行工具](https://blog.51cto.com/u_15127603/2754372)

> [node_modules本地安装与全局安装](https://www.kancloud.cn/a173512/node/2160974)

> [前端 npm5中本地间模块引用的最好方式（附带引用方法总结）](https://blog.csdn.net/zhangxin09/article/details/119344515)

> [在nodejs中使用Typescript](https://www.jianshu.com/p/2afde8626429)

> [前端业务研发问题总结](https://zhuanlan.zhihu.com/p/378375839)

> [workspaces - monorepo实战](https://juejin.cn/post/7051832110121746440)

> 单代码仓库 VS 多代码仓库 => 合适的才是最好的, 根据团队项目产品以及时间段进行单体或组合使用 (考虑权限可见性问题,引入git submodule以及多组合项目拉取)
> - 测试git submodule,子库有自己时间项; 多父库,也记录总体的时间线;
>
> [Monorepo 是什么，为什么大家都在用](https://zhuanlan.zhihu.com/p/77577415)
>
> [多项目版本管理：monorepo 策略](https://blog.csdn.net/qq_42415326/article/details/125148474)
>
> [5分钟搞懂Monorepo](https://www.jianshu.com/p/c10d0b8c5581)
>
> [实践 Monorepo 模式两年多的一些总结](https://zhuanlan.zhihu.com/p/516546403)
>
> [什么是 monorepo](https://www.kancloud.cn/chandler/web_technology/2625186)

## 项目架构

> 基于node workspaces组织项目架构, 进行项目组模块划分

> - platform-packages 基础架构平台
>
> - platform
>   - packages => platform-packages
>     - platform-common         基础公共模块, 提供基础工具类
>       - utils
>         - http                支持HTTP请求工具类
>         - storage             支持存储工具类
>     - platform-api            支撑平台APISDK
>     - platform-component
>       - comp-web              基于VUE封装WEB
>       - comp-router           基于VUE ROUTER封装
>       - comp-layout           基于布局模块
>       - comp-auth             封装权限校验模块
>     - platform-components     VIEW公共组件模块, 基于VUE封装公共组件
>     - platform-views          封装公共页面模块
>   - src
>     - api
>     - assets
>     - components
>     - layout
>     - plugins
>     - router
>     - store
>     - styles
>     - utils

```js
platform-parent
|
├── package.json
├── index.js
├── .git
├── module-common     公共基础能力模块
    ├── package.json
    ├── index.js
    ├── .git
    ├── utils
        ├── request.js
        ├── axios.js
        ├── fetch.js
        ├── permissions.js
        ├── datetime.js
        ├── storage.js
├── module-component  公共能力模块
    ├── package.json
    ├── index.js
    ├── .git
├── module-core       WEB能力模块
    ├── package.json
    ├── index.js
    ├── .git
├── module-api        服务能力接口模块 (对后端服务接口能力封装)
    ├── package.json
    ├── index.js
    ├── .git
        ├── api-auth      APISDK鉴权能力
            ├── api
            ├── vo
                ├── req
                ├── res
        ├── api-file      APISDK文件服务
            ├── api
            ├── vo
                ├── req
                ├── res
        ├── api-message   APISDK消息服务
        ├── api-system    APISDK系统服务
        ├── api-tenant    APISDK租户服务
├── module-web        
    ├── package.json
    ├── index.js
    ├── .git
    ├── web-express      案例 WEB Express
        ├── package.json
        ├── index.js
        ├── .git
    ├── web-vue          案例 WEB Vue
        ├── package.json
        ├── index.js
        ├── .git

- package.json nodejs模块定义
- index.js 模块导出, 及模块间相互引用
- .git GIT SUBMODULE模块定义
```

