    webpack是一个基于Node的项目 ，所有开发环境需要安装并配置Node项目环境 ，其自身的配置文件 webpack.config.js


    Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。

    所以如果我们需要在应用中添加 css 文件，就需要使用到 css-loader 和 style-loader，他们做两件不同的事情，css-loader 会遍历 CSS 文件，然后找到 url() 表达式然后处理他们，style-loader 会把原来的 CSS 代码插入页面中的一个 style 标签中。

### Install


```
[项目架构]

// webpack 打包后的项目
├── dist
│   └── app.js             // 打包后的app.js
├── src
│   └── index.js           // 源目录入口文件
│
├── package.json
└── webpack.config.js

[install]

	# 初始化NodeJS项目环境
	: mkdir react-demo && cd react-demo && npm init -y

	# 4.x版本, 一般 -D 安装，不全局安装
	: npm install webpack webpack-cli -D --save-dev

// 3.x 中打包和命令在一起，4.x 中命令行由 webpack-cli 提供
// 4.x 在 webpack.config.js 中新增 mode 选项，可选值为 development 和 production

	# 配置文件
	: webpack.config.js

  # 配置
  : package.json


// webpack.config.js
const path = require('path');

module.exports = {
    entry: './src/index.js',                        // 入口文件
    output: {                                       // webpack打包后出口文件
        filename: 'app.js',                         // 打包后js文件名称
        path: path.resolve(__dirname, 'dist')       // 打包后自动输出目录
    }
}

// package.json
"scripts": {
    "build": "webpack"
}

// src/index.js

[]

	: npm run build

```

### webpack module - loader

```javascript
[webpack module - loader]

	: 所有文件都为模块，图片，css文件，字体等静态资源都会打包进js文件, 所以会需要用到loader文件

	: 引入loader后，就可以在你的src/index.js文件import你想引入的css文件或者其他静态资源

	# loader
	: npm install style-loader css-loader url-loader --save-dev

// webpack.config.js
module.exports = {
	...
  // 加入module配置
	module: {
		rules: [
			{
				test: /\.css$/,
				use: ['style-loader', 'css-loader']
			},
			{
				test: /\.(png|svg|jpg|gif)$/,
				use: ['url-loader']
			},
			{
				test: /\.(woff|woff2|eot|ttf|otf)$/,
				use: ['url-loader']
			}
		]
	}
}
```

### webpack plugin - html-webpack-plugin

```javascript
[webpack plugin - html-webpack-plugin]

	# html-webpack-plugin # 将打包好的JS和静态文件，放入HTML文件中
	: npm install html-webpack-plugin --save-dev

// webpack.config.js
const path = require('path');
// 引入插件
const HtmlWebpackPlugin = require('html-webpack-plugin'); 

module.exports = {
	...
  // plugins 配置
	plugins: [
		new HtmlWebpackPlugin({title: 'production'})
	] 
};

[run]

	: npm run build

// 构建生成index.html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>name</title>
  </head>
  <body>
 // 打包后的app.js已经被自动插入了html文件
  <script type="text/javascript" src="app.js"></script></body>
</html>

// webpack 打包后的项目
├── dist  // 生产目录
│   ├── app.js              // 打包后的app.js
│   └── index.html
│ 
├── src  // 源目录        
│   ├── index.js           // 源目录入口文件
│   └── main.css
│ 
├── package.json
└── webpack.config.js
```

### webpack plugin - webpack-dev-server

```javascript
[webpack plugin - webpack-dev-server]

	: npm install webpack-dev-server --save-dev

	# "dev": "webpack-dev-server --open --mode development"
	: package.json

// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
// webpack 引入
const webpack = require('webpack');

module.exports = {
	...
	plugins: [
		new HtmlWebpackPlugin({
			title: 'production',
      // 自定义模板
			template: './src/index.html'    
		}),
		// hot 检测文件改动替换 plugin
		new webpack.NamedModulesPlugin(),      
		new webpack.HotModuleReplacementPlugin()		
	],
  // webpack-dev-server 配置
	devServer: {
		contentBase: './build',
		hot: true
	},
};

// src/index.html (html-webpack-plugin 模板配置)
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div id="root"></div>
</body>
</html>

[]

	: npm run dev # http://localhost:8080

```

### webpack & react

```
[Install]

	#
	: npm install react react-dom --save-dev

	# 安装 react，wepback 转换依赖 ，React组件由JSX组成，浏览器无法识别JSX，需要babel进行转换
	: npm install babel-core babel-preset-env babel-preset-react babel-loader@7.1.5 --save-dev

// .babelrc 配置文件
{
  "presets": ["env", "react"]
}

// webpack.config.js - 添加moduel配置
{
	test: /\.(js|jsx)$/,
	exclude: /node_modules/,
	use: ['babel-loader']
}

// ./src/index.js
import React from 'react';
import ReactDom from 'react-dom';

import './main.css'

ReactDom.render(
	<h1>hello world</h1>,
	document.getElementById('root')
);

[run]
	
  # 渲染出 : "hello world"
	: npm run build # 进入编译输出目录, 运行index.html文件, 验证运行效果

```

#### 错误问题 -> [参考链接](https://www.yuque.com/thinxz_front_end/kdgwuu/gbb5i3)

