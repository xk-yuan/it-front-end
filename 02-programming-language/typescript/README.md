# typescript

> 

## 资源

> - [typescript](https://github.com/microsoft/typescript)
>
> - [socket-io-typescript-chat](https://github.com/luixaviles/socket-io-typescript-chat)
> - [blog-vue-typescript](https://github.com/biaochenxuying/blog-vue-typescript)


[](https://www.typescriptlang.org/)
[](https://www.tslang.cn/)
[](https://www.tslang.cn/docs/home.html)

[](https://github.com/microsoft/TypeScript)
[<TypeScript 中文手册>](https://typescript.bootcss.com/ )

[](https://www.runoob.com/typescript/ts-tutorial.html)
[](https://www.jianshu.com/p/70a03e21936c)

> [TIOBE 排行榜](https://www.tiobe.com/tiobe-index/)

![image.png](http://localhost/it/front-end/1572749137532-c803d140-9908-44a3-86eb-b15cc821918b.png#align=left&display=inline&height=225&margin=%5Bobject%20Object%5D&name=image.png&originHeight=252&originWidth=836&size=29492&status=done&style=none&width=746)

![image.png](http://localhost/it/front-end/1572749587314-f991b8d5-1550-4e8e-b840-c1a80cd14516.png#align=left&display=inline&height=765&margin=%5Bobject%20Object%5D&name=image.png&originHeight=765&originWidth=946&size=65820&status=done&style=none&width=946)

![image.png](http://localhost/it/front-end/1572749608626-926ed4fd-ebc4-4fdd-ae07-af94ea46a87b.png#align=left&display=inline&height=396&margin=%5Bobject%20Object%5D&name=image.png&originHeight=396&originWidth=929&size=111791&status=done&style=none&width=929)


- vscode 插件 : open in brower
- debugger for chrome

## 简介

TypeScript 是一种由微软开发的自由和开源的编程语言。它是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。

其本质是 TS编译器，将TS源码编译成 JS ，然后执行JS 程序。

2012年十月份，微软发布了首个公开版本的TypeScript，2013年6月19日，在经历了一个预览版之后微软正式发布了正式版TypeScript 0.9。


其扩展了JavaScript的语法，所以任何现有的JS程序可以不加改变的在TS下工作。qi其是为大型应用的开发而设计，而编译它时产生 JavaScript 以确保兼容性。其支持为已存在的 JavaScript 库添加类型信息的头文件，扩展了它对于流行的库如 jQuery，MongoDB，Node.js 和 D3.js 的好处。


## 安装

> npm install -g typescript@3.9.6


> tsc helloworld.ts  # 编译

## gulp-ts

> - init project

> npm init -y

> - install dependencies

> npm install gulp-cli@2.3.0 --save-dev

> npm install --save-dev typescript@4.0.2 gulp@4.0.2 gulp-typescript@6.0.0-alpha.1

> .\node_modules\.bin\gulp # 编译

> node dist/main.js  # 运行

> - Browserify (支持CommonJS, 支持浏览器环境)

> npm install --save-dev browserify@16.5.2 tsify@5.0.2 vinyl-source-stream@2.0.0

> - 自动监听编译 Watchify

> npm install --save-dev watchify@3.11.1 gulp-util@3.0.8

> - 压缩混淆 Uglify

> npm install --save-dev gulp-uglify@3.0.2 vinyl-buffer@1.0.1 gulp-sourcemaps@2.6.5

> - ES2015支持 Babel

> npm install --save-dev babel-core@6.26.3 babelify@8.0.0 babel-preset-es2015@6.24.1 vinyl-buffer@1.0.1 gulp-sourcemaps@2.6.5


## react-webpack-ts

> npm install -save-dev webpack@4.44.1 webpack-cli@3.3.12

> npm install --save react@16.13.1 react-dom@16.13.1 @types/react@16.9.49 @types/react-dom@16.9.8

> npm install --save-dev typescript@4.0.2 awesome-typescript-loader@5.2.1 source-map-loader@1.1.0