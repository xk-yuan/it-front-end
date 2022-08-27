### 脚本安装

```
[VueJs JS 库安装]

	: <script src="https://unpkg.com/vue/dist/vue.js"></script>

	: https://unpkg.com/vue/dist/vue.js

[简单案例]

<!DOCTYPE html>
<html>
<body>
<div id="app">
    <h1>site : {{site}}</h1>
    <h1>{{details()}}</h1>
    <h1 v-html="rawHtml"></h1>
</div>
</body>
</html>

[实例化 Vue]

<script type="text/javascript">
    var vm = new Vue({
        el: '#app',
        data: {
            site: "Web Blog",
            rawHtml: "<p>Html</p>"
        },
        methods: {
            details: function() {
                return this.site + " Vue ";
            }
        }
    })
</script>

[解析]

	: el -> 指定实例化的元素, 此后所有修改限定在该元素内部
    
    : data 定义属性 -> 上面定义了 site 属性, 值为 "Web Blog"

	: methods 定义方法
    
    # 当Vue实例化时, 将data对象的所有属性加入到Vue的 响应式系统中
    # 当这些属性的值发生改变时, html 视图将也会产生相应的变化

[数据绑定 - {{ }} Mustache 语法 - 文本插值]

	: {{ 属性/方法名 }} -> 用于输出对象属性和函数返回值
    
    # Mustache 标签将会被替代为对应数据对象上 (属性/方法名) 属性的值
    # 无论何时, 绑定的数据对象上属性发生了改变, 插值处的内容都会更新
    
    : v-html 指定以 html 元素进行渲染
    # 双大括号会将数据解释为普通文本, 而非 HTML 代码
    # <span v-html="rawHtml"></span>

[Vue实例属性方法的访问]

	: $符号开头访问, 实例的属性和方法
    # vm.$el
    # vm.$data

```

### vue-cli install [[vue-cli-demo]](https://github.com/xknower/vue-cli-demo)

```
[环境配置]

	: nodejs & npm

[vue-cli]

	: npm install vue-cli -g

	: vue init webpack pro-name

	: npm install

  : npm run dev

[项目架构]

vue-cli-demo
	│
  ├─build                    // 项目构建 (webpack) 相关代码
  ├─config                   // 配置目录，包括端口号等
  │
  ├─src  // 源码目录
  │  │  App.vue  // 项目入口
  │  │  main.js  // 项目入口-项目核心文件
  │  │
  │  ├─assets      // 资源目录
  │  │
  │  ├─components  // 组件目录
  │  │
  │  └─router      // 路由配置目录
  │
  ├─static         // 静态资源目录，如图片、字体等。
  │      
  └─test

// 项目根文件

│  .babelrc
│  .editorconfig
│  .eslintignore
│  .eslintrc.js
│  .gitignore
│  .postcssrc.js
│  index.html              // 首页入口文件，你可以添加一些 meta 信息或统计代码啥的。
│  package-lock.json
│  package.json
└─ README.md

```

![image.png](http://localhost/it/front-end//1579445408025-e30d7f8f-7302-45d8-99a8-9aa210521ca0.png#align=left&display=inline&height=305&name=image.png&originHeight=302&originWidth=738&size=16826&status=done&style=none&width=746)

![image.png](http://localhost/it/front-end//1579446177247-64e1df6e-de9b-46d4-945b-a23777ceae4c.png#align=left&display=inline&height=207&name=image.png&originHeight=207&originWidth=1606&size=30966&status=done&style=none&width=1606)

![image.png](http://localhost/it/front-end//1579446216201-3e09b4df-2c16-4223-8404-3ea6b67593e1.png#align=left&display=inline&height=256&name=image.png&originHeight=256&originWidth=1024&size=21794&status=done&style=none&width=1024)

![image.png](http://localhost/it/front-end//1579446245659-01e10336-7b64-4691-97dc-ca740442d2d8.png#align=left&display=inline&height=355&name=image.png&originHeight=355&originWidth=1315&size=36081&status=done&style=none&width=1315)

![image.png](http://localhost/it/front-end//1579446273080-1ca53c7f-ae43-4579-b60c-6ea725421faa.png#align=left&display=inline&height=354&name=image.png&originHeight=282&originWidth=595&size=11465&status=done&style=none&width=746)

node install  [[vue-demo]](https://github.com/xknower/vue-demo)


```
[vue + webpack]

  : mkdir vue-demo && cd vue-demo && npm init -y

  # webpack & webpack-dev-server & html-webpack-plugin
  : npm install webpack webpack-cli -D --save-dev
  : npm install webpack-dev-server --save-dev
  : npm install html-webpack-plugin --save-dev

  : npm install vue --save-dev
  : npm install vue-loader vue-template-compiler --save-dev

{
  test: /\.(vue)$/,
  exclude: /node_modules/,
  use: ['vue-loader']
}

// https://vue-loader.vuejs.org/migrating.html#a-plugin-is-now-required
// Vue-loader在15.*之后的版本都是 vue-loader的使用都是需要伴生 VueLoaderPlugin的

[loader]

  # babel
  : npm install babel -g
  : npm install babel-core babel-preset-env babel-loader@7.1.5  --save-dev

  : npm install style-loader css-loader url-loader --save-dev

[项目架构]

// webpack 打包后的项目
├── dist  // 生产目录
│   ├── app.js              // 打包后的app.js
│   └── index.html
│
├── src  // 源目录
│   ├── index.html
│   └── index.js           // 源目录入口文件
│
├── package.json
└── webpack.config.js
```

```
// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin'); 
const webpack = require('webpack');
//
const VueLoaderPlugin = require('vue-loader/lib/plugin');

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
          test: /\.(vue)$/,
          exclude: /node_modules/,
          use: ['vue-loader']
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
      new webpack.HotModuleReplacementPlugin(),
      // VUE
      new VueLoaderPlugin()
    ],
    // webpack-dev-server 配置
    devServer: {
      contentBase: './build',
      hot: true
    },
}

// .babelrc 配置文件
{
  "presets": ["env", "vue"]
}

// package.json
"build": "webpack --mode production",
"dev": "webpack-dev-server --open --mode development"
```

```
[资源文件]

// ./src/index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue demo</title>
</head>
<body>
    <div id="app">
    </div>
    <script src="./app.js"></script>
</body>
</html>

// ./src/index.js
import Vue from 'vue'
import App from './app.vue'

new Vue({
  render: h => h(App)
}).$mount("#app")

// app.vue
<template>
  <div id="app">
    <span>{{msg}}</span>
  </div>
</template>

<script>
export default {
  name:'app',
  data(){
    return {
      msg:"Hello World !"
    }
  },
}
</script>

<style ></style>

// https://blog.csdn.net/wxl1555/article/details/83187647
```

### [Element UI](https://www.yuque.com/thinxz_front_end/front_end_fw/npnrq2)

```
[]

	: npm install element-ui -S

// 引入全局UI组件
import ElementUI from 'element-ui';
// 样式文件需要单独引入 [全部引入]
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);

```

