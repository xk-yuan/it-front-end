
```java
[官网]

	：https://www.npmjs.com/

	：https://www.npmjs.com.cn/

[install]

	：npm install npm -g # 升级

```

### 简介

  NPM 是随NodeJS 一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，Npm ，基于NodeJS ，是对NodeJS 的开源库的功能管理平台。
   Npm 的诞生是由于 Node 的需要而发明的，npm 是 Npm 使用的命令行工具。Nvm ，是另一款命令行工具，用于安装 Node 。

   -> npm 管理包工具，nvm 管理 Node 版本工具。

```java
[项目]

	：npm init ，指令创建项目描述文件 package.json

	：项目描述文件 package.json
    
    ：文件里记录项目的描述信息：项目作者、项目描述、项目依赖哪些包、插件配置信息等等

[参数]

	=> name 项目名称

	=> version 项目的版本号

	=> description 项目的描述信息

	=> entry point 项目的入口文件

	=> test command 项目启动时脚本命令

	=> git repository 如果你有 Git 地址，可以将这个项目放到你的 Git 仓库里

	=> keywords 关键词

	=> author 作者

	=> license 项目要发行的时候需要的证书
```

### 命令

```basic
[安装模块]

	：npm install <Module Name>
    
    # -g 全局安装 , 不加 -g 本地安装
	# --save 同时将安装的模块信息记录在 package.json 文件
	# --save-dev

[本地安装]

	：./node_modules  # 本地安装, 将存放在该目录下

[安装过程输出]

express@4.13.3 node_modules/express  // 版本号及安装位置
├── escape-html@1.0.2
├── range-parser@1.0.2
├── merge-descriptors@1.0.0
├── array-flatten@1.1.1
├── cookie@0.1.3
├── utils-merge@1.0.0
├── parseurl@1.3.0
├── cookie-signature@1.0.6
├── methods@1.1.1
├── fresh@0.3.0
├── vary@1.0.1
├── path-to-regexp@0.1.7
├── content-type@1.0.1
├── etag@1.7.0
├── serve-static@1.10.0
├── content-disposition@0.5.0
├── depd@1.0.1
├── qs@4.0.0
├── finalhandler@0.4.0 (unpipe@1.0.0)
├── on-finished@2.3.0 (ee-first@1.1.1)
├── proxy-addr@1.0.8 (forwarded@0.1.0, ipaddr.js@1.0.1)
├── debug@2.2.0 (ms@0.7.1)
├── type-is@1.6.8 (media-typer@0.3.0, mime-types@2.1.6)
├── accepts@1.2.12 (negotiator@0.5.3, mime-types@2.1.6)
└── send@0.13.0 (destroy@1.0.3, statuses@1.2.1, ms@0.7.1, mime@1.3.4, http-errors@1.3.1)

[查看安装信息]

	：npm list -g # 查看所有全局安装的模块

	# --depth=0 只显示第一层级的模块

├─┬ cnpm@4.3.2
│ ├── auto-correct@1.0.0
│ ├── bagpipe@0.3.5
│ ├── colors@1.1.2
│ ├─┬ commander@2.9.0
│ │ └── graceful-readlink@1.0.1
│ ├─┬ cross-spawn@0.2.9
│ │ └── lru-cache@2.7.3
……

	：npm list grunt # 查看某个模块的版本号

[卸载模块]

	：npm uninstall express
# --save 卸载模块的同时删除在 package.json 文件中的记录
[更新模块]

	：npm update express
	# --save 更新模块的同时将更新信息记录到 package.json 文件中

[搜索模块]

	：npm search express

[淘宝 NPM 镜像]

	$ npm install -g cnpm --registry=https://registry.npm.taobao.org

	$ cnpm install [name] # 安装模块
```

### 创建模块

```basic
[创建模块]
  
  $ npm init # 初始化创建模块

  $ npm adduser # npm 资源库中注册用户（使用邮箱注册
    
  $ npm publish # 发布模块
```

```basic
[npm init]

	=> name    - 包名
	=> version - 包的版本号
	=> description - 包的描述
	=> homepage    - 包的官网 url 
	=> author      - 包的作者姓名
	=> contributors - 包的其他贡献者姓名
	=> dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下
	=> repository   - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上
	=> main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件, 的默认值是模块根目录下面的 index.js。
	=> keywords - 关键字
```

### package.json

```basic
[package.json]

"private": true,
"dependencies": {
	"antd": "^2.11.1",
	"classnames": "^2.2.5"
},
"devDependencies": {
	"axios": "^0.15.3",
	"babel-eslint": "^6.1.2"
},
"bin": {
	"dk-cli": "./bin/dk-cli.js"
},
"scripts": {
	"start": "node index.js"
},
"engines": {
	"node": ">=6.9.0",
	"npm": ">=3.10.10"
}
"publishConfig": {
	"registry": "http://gongsineibu/nexus/repository/npm-hosted/"
}

[属性]

	：private , 可选字段，布尔值。如果 private 为 true，npm 会拒绝发布。
	：dependencies 指定了项目生产环境时所依赖的模块
	：devDependencies 制定了项目开发环境时所依赖的模块
	：bin # bin 属性可以让我们很简单制作命令行工具
	：scripts # 脚本运行方式
	：engines # 当前项目依赖 node 版本
	：publishConfig
```
