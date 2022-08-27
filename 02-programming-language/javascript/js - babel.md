![image.png](../../imgs/1572444743489-38847ebc-fada-401f-b8c6-20f039b90d7c.png#align=left&display=inline&height=179&name=image.png&originHeight=278&originWidth=1158&size=61547&status=done&width=746)

```
[官网]

	: https://www.babeljs.cn/

  : https://github.com/babel/babel

[文档]

	: https://www.babeljs.cn/docs/index.html

```

    Babel 是一个 JavaScript 编译器，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。

```
[功能]

	语法转换

	通过 Polyfill 方式在目标环境中添加缺失的特性 (通过 @babel/polyfill 模块)

	源码转换 (codemods)

```

```
[]

	# 核心包
	: @babel/core 

  # 命令行工具
  : @babel/cli

  # 插件 - 用来转换ES6/ES7或更高级的语法
  : @babel/preset-env

  # API补丁包
  : @babel/polyfill

[]

	# webpack loader
	: babel-loader
  
  # react 语法转译
  : @babel/preset-react

```

```
[]

	npm install --save-dev @babel/core @babel/cli @babel/preset-env
	npm install --save @babel/polyfill

[配置 babel.config.js]

module.exports = {
    presets: [
        [
            '@babel/env',
            {
                useBuiltIns: 'usage',
                corejs: 2,
                targets: {
                    edge: "17",
                    firefox: "60",
                    chrome: "67",
                    safari: "11.1",
                }
            }
        ]
    ]  
}

// targets表示支持的浏览器，useBuiltIns为babel7.x新增的一个属性

[执行 - 执行babel, npx为npm的包执行器]

	: ./node_modules/.bin/babel src --out-dir lib

	: npx babel src --out-dir lib
```

