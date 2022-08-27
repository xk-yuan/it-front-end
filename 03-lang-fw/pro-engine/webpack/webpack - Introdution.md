```
[官网]

	: https://webpack.js.org
  : https://www.webpackjs.com/
  : https://webpack.docschina.org/
  
  : https://github.com/webpack/webpack
 
 [相关项目]

    : webpack-cli        # https://github.com/webpack/webpack-cli

    : webpack-dev-server # https://github.com/webpack/webpack-dev-server
 
[文档]

	: https://www.webpackjs.com/concepts/

// http://webpack.wuhaolin.cn/ # 深入浅出 Webpack
//
// https://time.geekbang.org/course/intro/190
// https://www.w3cschool.cn/webpackguide/ # w@3.x
// https://segmentfault.com/a/1190000006178770
// https://webpack.wuhaolin.cn/
// https://www.zhihu.com/topic/20032877/hot
// https://blog.csdn.net/jufjzq/article/details/89515112
// https://www.jianshu.com/p/db81016cfa43
// https://github.com/lihongxun945/diving-into-webpack
// https://github.com/ruanyf/webpack-demos
// https://www.ibm.com/developerworks/cn/web/wa-lo-expedite-webpack/index.html
// https://segmentfault.com/a/1190000007264197
// https://www.jianshu.com/p/42e11515c10f
```

> [WebPack 中文指南.pdf]()

    webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler) [ ['bʌndlər] 打包模块] ，其根据应用程序自动归地构建一个依赖关系图 (dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

  在传统的前端只是一个会做交互和静态页，随着WEB架构的变迁，出于项目日益复杂和业务扩展，MV*架构逐渐占领了WEB的光环，其中三大剑客便是 Angular,React和Vue，在使用这些js框架开始时，出于代码可维护性的角度出发，不会再像以往那样使用标签引入的方式，而是采用了一种模块的方式去开发，webpack是其中典型的代表。

    webpack , 前端资源加载/打包工具 , 前端项目构建工具 ，其根据模块的依赖关系进行静态分析，然后将这些模块按照指定的规则生成对应的静态资源。

官网对webpack的定义是MODULE BUNDLER，他的目的就是把有依赖关系的各种文件打包成一系列的静态资源。
_
```
[]

	: 模块加载器兼打包工具, 将各种资源作为模块来使用和处理, 将依赖的模块转化成可以代表这些包的静态文件
  // 将依赖的模块分片化，并且按需加载
  // 解决大型项目初始化加载慢的问题
  // 每一个静态文件都可以看成一个模块
  // 可以整合第三方库, 能够在大型项目中运用, 自定义切割模块的方式
  // 代码转换/文件优化/代码分割/模块合并/自动刷新/代码校验/自动发布

	: webpack vs gulp
  // webpack 主要站在整个项目的角度, 强调处理各种依赖关系, 处理各种文件
  // gulp强调流式管道操作, 强调点对点之间的关系

[]

	: webpack 是以 commonJS 的形式来书写脚本, 对 AMD/CMD 的支持也很全面, 方便旧项目进行代码迁移
  
  : 支持很多模块加载器的调用, 可以使模块加载器灵活定制
  
  : 开发便捷，能替代部分 grunt/gulp 的工作, 比如打包、压缩混淆、图片转base64等
  
  : 以通过配置打包成多个文件，有效的利用浏览器的缓存功能提升性能

```

    其工作方式是 ，把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。

    可以将多种静态资源 js、css、less 转换成一个静态文件，减少了页面的请求。

![](http://localhost/it/front-end/1544626597868-423e2dc9-1166-4081-934f-0c323405e41d.png#align=left&display=inline&height=413&originHeight=1299&originWidth=2598&status=done&style=none&width=826)

```basic
[入口 Entry]

    : 指定起始的入口模块,作为构建其内部依赖图的开始,根据入口模块将自动找出有哪些模块和库是入口起点(直接和间接依赖)

    : 每个依赖项随即被处理，最后输出到称之为 bundles 的文件中

 [输出 output]

    : 输出其所创建的 bundles 的位置, 以及如何命名这些文件

 [loader]

    : 是webpack有能力处理非JavaScript文件,其可以将所有类型的文件转换为webpack能够处理的有效模块

 [插件 plugins]

    : 插件则可以用于执行范围更广的任务,从打包优化和压缩，一直到重新定义环境中的变量

```

