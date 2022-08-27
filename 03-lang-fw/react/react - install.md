### 脚本安装

```
[脚本安装]

  <!-- 核心React库 -->
  <script src="https://fb.me/react-0.13.3.js"></script>
  <!--浏览器中的JSX变换器，在预编译JSX时删除。 -->
  <script src="https://fb.me/JSXTransformer-0.13.3.js"></script>
  
  <!-- React 的核心库 -->
  <script src="//www.w3cschool.cn/statics/assets/react/react.min.js"></script>
  <!-- DOM 相关的功能 -->
  <script src="//www.w3cschool.cn/statics/assets/react/react-dom.min.js"></script>
  <!-- ES6支持, Babel 内嵌了对 JSX 的支持 -->
  <script src="//www.w3cschool.cn/statics/assets/react/babel.min.js"></script>

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <script src="//www.w3cschool.cn/statics/assets/react/react.min.js"></script>
    <script src="//www.w3cschool.cn/statics/assets/react/react-dom.min.js"></script>
    <script src="//www.w3cschool.cn/statics/assets/react/babel.min.js"></script>
  </head>

  <body>
    <div id="example"></div>
    <script type="text/babel">
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
  </body>
</html>
```

### cli install [[react-cli-demo]](https://github.com/xknower/react-cli-demo)

```
[cli install]

	: npm install create-react-app -g
  
  : create-react-app react-app-demo
  
  : cd react-app-demo && npm start

```

### node install [[react-demo]](https://github.com/xknower/react-demo)

```
[react + webpack]

	: mkdir react-demo && cd react-demo && npm init -y

	: npm install react react-dom --save-dev

	# webpack & webpack-dev-server & html-webpack-plugin
	: npm install webpack webpack-cli -D --save-dev
  : npm install webpack-dev-server --save-dev
  : npm install html-webpack-plugin --save-dev

[loader]

	: npm install style-loader css-loader url-loader --save-dev

  # babel
  : npm install babel -g
  : npm install babel-core babel-preset-env babel-loader@7.1.5 babel-preset-react --save-dev

  : babel-preset-react

[项目架构]

// webpack 打包后的项目
├── dist  // 生产目录
│   ├── app.js              // 打包后的app.js
│   └── index.html
│ 
├── src  // 源目录
│   ├── index.html
│   │── index.js           // 源目录入口文件
│   └── main.css
│
├── package.json
└── webpack.config.js
```

```
[配置文件]

// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin'); 
const webpack = require('webpack');

module.exports = {
    entry: './src/index.js',                        // 入口文件
    output: {                                       // webpack打包后出口文件
        filename: 'app.js',                         // 打包后js文件名称
        path: path.resolve(__dirname, 'dist')       // 打包后自动输出目录
    },
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
        },
        {
          test: /\.(js|jsx)$/,
          exclude: /node_modules/,
          use: ['babel-loader']
        }
      ]
    },
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
}

// .babelrc 配置文件
{
  "presets": ["env", "react"]
}

// package.json
"build": "webpack --mode production",
"dev": "webpack-dev-server --open --mode development"

[资源文件]

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

// ./src/index.js
import React from 'react';
import ReactDom from 'react-dom';

import './main.css'

ReactDom.render(
  <h1>hello world</h1>,
  document.getElementById('root')
);
```

