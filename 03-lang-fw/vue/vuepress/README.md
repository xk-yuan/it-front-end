# VuePress

> Vue 驱动的静态网站生成器。

> WordPress、Jekyll、Hexo

> SPA = Vue 、Vue Router 和 webpack、Node.js 版本 >= 8.6

> Features

- Markdown (内置拓展、在Markdown中使用Vue)
- 主题系统 (Vue驱动的可自定义、默认主题、博客主题)
- Plugin
- 约定优于配置原则

> 优点

- 界面简洁优雅
- 上手简单
- 兼容、扩展 Makedown 语法
- 响应式布局，PC端、手机端
- Google Analytics 集成
- 支持 PWA

## 资源

> [官网](https://vuepress.vuejs.org/zh/)
>
>   - [github](https://github.com/vuejs/vuepress) @Star 20.2k @Fork 4.4k @latcommittime 2022 年 2 月 17 日
>
>   - [用户指南](https://vuepress.vuejs.org/zh/guide/)
>
>   - [配置](https://vuepress.vuejs.org/zh/config/)
>
>   - [主题](https://v1.vuepress.vuejs.org/zh/theme/)
>
>
>   - [vuepress-next](https://github.com/vuepress/vuepress-next) @V2.0.0-beta.37

> [VitePress](https://vitepress.vuejs.org/)
>
>   - [github](https://github.com/vuejs/vitepress) @ 0.x 状态

> [](https://www.moyundong.com/frontend/vuepress/2%E5%BF%AB%E9%80%9F%E6%90%AD%E5%BB%BA.html#%E5%AE%89%E8%A3%85nodejs)

### 博客搭建

> [手把手教你使用 VuePress 搭建个人博客](https://www.cnblogs.com/softidea/p/10084946.html)
>
> [vuepress使用简介及个人博客搭建](https://blog.csdn.net/xiaoxianer321/article/details/119548202)
>
> [VuePress 完整使用教程](https://www.jianshu.com/p/f2d2848542f1)
>
> [使用vuepress搭建一个完全免费的个人网站](https://blog.csdn.net/qq_36538012/article/details/106990967)
>
> [VuePress 快速踩坑](https://zhuanlan.zhihu.com/p/36116211)
>
> [Vuepress 快速搭建博客--一款你值得拥有的博客主题](https://blog.csdn.net/weixin_44002432/article/details/105897210)
>
> [vue论坛网站的文章自动排版_基于 VuePress 定制个人博客网站](https://blog.csdn.net/weixin_39719042/article/details/111099680)
>
> [VuePress 手摸手教你搭建一个类Vue文档风格的技术文档/博客](https://segmentfault.com/a/1190000016333850)
>
> [](https://segmentfault.com/t/vuepress)
>
> [读 VuePress（四）插件系统的设计](https://www.jianshu.com/p/b8000f6b24da)

> [vuepress-devkit](https://github.com/zhangyunchencc/vuepress-devkit)

[manual guide tutorial](https://www.cnblogs.com/jiangleads/p/11238232.html)

> [VuePress侧导航及自定义主题样式的配置](https://www.jianshu.com/p/424e0451e030)

### 功能

- 统计: 访问统计: 访问页面次数统计、页面访问停留时长统计 (多维度过滤, 时间和IP)

> [VuePress 博客优化之添加数据统计功能](https://zhuanlan.zhihu.com/p/455574827)
>
> [搭建 VuePress 站点必做的 10 个优化](https://zhuanlan.zhihu.com/p/485902693)
>
> [vuepress-plugin-toolbar 侧边工具栏](https://zq99299.github.io/vuepress-plugin/vuepress-plugin-toolbar/#vuepress-plugin-toolbar-%E4%BE%A7%E8%BE%B9%E5%B7%A5%E5%85%B7%E6%A0%8F)
>
> [](https://zhuanlan.zhihu.com/p/467830386)
>
> [](https://wenku.baidu.com/view/bf57fb325c0e7cd184254b35eefdc8d376ee143a.html)
>
> [](https://www.csdn.net/tags/MtTaEg0sMDQ1OTY5LWJsb2cO0O0O.html)

- 统计: 点赞 (按照访问次数和IP过滤, 一次访问和IP 只能点赞一次)

- 评论

- 多媒体: 音视频播放

> [](https://segmentfault.com/a/1190000041217167)
>
> [](https://daodaolee.cn/fe/vuepress_plugin_awesome_musicplayer.html#%E5%89%8D%E8%A8%80)

## 简介

VuePress, 以Markdown为写框架, Vue + webpack 驱动, 可以自定义主题, 并为每个页面预渲染生成静态的 HTML, 同时，每个页面被加载的时候，将作为 SPA 运行。

### 使用

```bash
# 安装
yarn global add vuepress # 或者：npm install -g vuepress

# 新建一个 markdown 文件
echo '# Hello VuePress!' > README.md

# 开始写作
vuepress dev .

# 构建静态文件
vuepress build .
```

> 入门案例搭建

$ mkdir vuepress-starter & cd vuepress-starter
$ yarn init
$ yarn add -D vuepress
$ echo '# vuepress-starter' > doc/README.md

$ vuepress dev .    # 启动
$ vuepress build .  # 编译

$ vi .gitignore

$ vi package.json
```json add
{
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  }
}
```

$ yarn docs:dev  # 启动, 访问 http://localhost:8080 热重载的开发服务器

### 目录结构

```tree
.
├── docs
│   ├── .vuepress      (可选的)
│   │   ├── components (可选的)
│   │   ├── theme      (可选的)
│   │   │   └── Layout.vue
│   │   ├── public     (可选的)
│   │   ├── styles     (可选的)
│   │   │   ├── index.styl
│   │   │   └── palette.styl
│   │   ├── templates  (可选的, 谨慎配置)
│   │   │   ├── dev.html
│   │   │   └── ssr.html
│   │   ├── config.js  (可选的)
│   │   └── enhanceApp.js (可选的)
│   │ 
│   ├── README.md
│   ├── guide
│   │   └── README.md
│   └── config.md
│ 
└── package.json
```

- docs/.vuepress: 用于存放全局的配置、组件、静态资源等。
- docs/.vuepress/components: 该目录中的 Vue 组件将会被自动注册为全局组件。
- docs/.vuepress/theme: 用于存放本地主题。
- docs/.vuepress/styles: 用于存放样式相关的文件。
- docs/.vuepress/styles/index.styl: 将会被自动应用的全局样式文件，会生成在最终的 CSS 文件结尾，具有比默认样式更高的优先级。
- docs/.vuepress/styles/palette.styl: 用于重写默认颜色常量，或者设置新的 stylus 颜色常量。
- docs/.vuepress/public: 静态资源目录。
- docs/.vuepress/templates: 存储 HTML 模板文件。
- docs/.vuepress/templates/dev.html: 用于开发环境的 HTML 模板文件。
- docs/.vuepress/templates/ssr.html: 构建时基于 Vue SSR 的 HTML 模板文件。
- docs/.vuepress/config.js: 配置文件的入口文件，也可以是 YML 或 toml。
- docs/.vuepress/enhanceApp.js: 客户端应用的增强。

当你想要去自定义 templates/ssr.html 或 templates/dev.html 时，最好基于 默认的模板文件 (opens new window)来修改，否则可能会导致构建出错。

```json package.json
{
  "scripts": {
    "dev": "vuepress dev docs",
    "build": "vuepress build docs"
  }
}
```

> 基于目录结构的默认路由

- /README.md	/
- /guide/README.md	/guide/
- /config.md	/config.html

### 基本配置

```tree
.
├─ docs
│  ├─ README.md
│  └─ .vuepress
│     └─ config.js
└─ package.json
```

一个 VuePress 网站必要的配置文件是 .vuepress/config.js，它应该导出一个 JavaScript 对象。或者使用 .vuepress/config.yml 和 .vuepress/config.toml 格式进行配置。

```js .vuepress/config.js
module.exports = {
  title: 'Hello VuePress',
  description: 'Just playing around'
}
```

### 主题

一个 VuePress 主题应该负责整个网站的布局和交互细节。目前自带了一个默认的主题，它是为技术文档而设计的。

VuePress 是一个标准的 Vue 应用，你可以通过创建一个 .vuepress/enhanceApp.js 文件来做一些应用级别的配置，当该文件存在的时候，会被导入到应用内部。enhanceApp.js 应该 export default 一个钩子函数，并接受一个包含了一些应用级别属性的对象作为参数。你可以使用这个钩子来安装一些附加的 Vue 插件、注册全局组件，或者增加额外的路由钩子等：

```js .vuepress/enhanceApp.js
// 使用异步函数也是可以的
export default ({
  Vue,     // VuePress 正在使用的 Vue 构造函数
  options,  // 附加到根实例的一些选项
  router,   // 当前应用的路由实例
  siteData, // 站点元数据
  isServer  // 当前应用配置是处于 服务端渲染 或 客户端
}) => {
  // ...做一些其他的应用级别的优化
}
```

### 静态资源

所有的 Markdown 文件都会被 webpack 编译成 Vue 组件，因此你可以，并且应该更倾向于使用相对路径（Relative URLs）来引用所有的静态资源。

```md
![An image](./image.png)
```

同样地，这在 *.vue 文件的模板中一样可以工作，图片将会被 url-loader 和 file-loader 处理，在运行生成静态文件的构建任务时，文件会被复制到正确的位置。除此之外，你也使用 ~ 前缀来明确地指出这是一个 webpack 的模块请求，这将允许你通过 webpack 别名来引用文件或者 npm 的依赖：

```md
![Image from alias](~@alias/image.png)
![Image from dependency](~some-dependency/image.png)
```

Webpack 的别名可以通过 .vuepress/config.js 中 configureWebpack 来配置

```js
module.exports = {
  configureWebpack: {
    resolve: {
      alias: {
        '@alias': 'path/to/some/dir'
      }
    }
  }
}
```

需要提供一个静态资源，但是它们并不直接被你的任何一个 markdown 文件或者主题组件引用 —— 举例来说，favicons 和 PWA 的图标，在这种情形下，你可以将它们放在 .vuepress/public 中， 它们最终会被复制到生成的静态文件夹中。

当网站会被部署到一个非根路径，你将需要在 .vuepress/config.js 中设置 base。有了基础路径（Base URL），如果你希望引用一张放在 .vuepress/public 中的图片，VuePress 提供了内置的一个 helper $withBase（它被注入到了 Vue 的原型上），可以帮助你生成正确的路径。

```md
<img :src="$withBase('/foo.png')" alt="foo">
```

最后补充一句，一个 base 路径一旦被设置，它将会自动地作为前缀插入到 .vuepress/config.js 中所有以 / 开始的资源路径中。

### Markdown 拓展

所有的标题将会自动地应用 anchor 链接，anchor 的渲染可以通过 markdown.anchor 来配置。

网站内部的链接，将会被转换成 router-link 用于 SPA 导航。同时，站内的每一个文件夹下的 README.md 或者 index.md 文件都会被自动编译为 index.html，对应的链接将被视为 / 。可以通过官方插件 vuepress-plugin-clean-urls (opens new window)定制你的网站路径。


