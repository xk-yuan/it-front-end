
###   CSS ，不是一种编程语言，而是一种 网页样式的描述方法。

  **为了解决，CSS 像编程语言来书写，其经历了 ：Less 、SASS(SCSS) 、Stylus [css预处理器] -> PostCSS [插件系统] -> CSS in JS 、 CSS Modules**

![image.png](../../imgs/1572945671994-68e7c616-dcac-461e-ad74-e243689990bc.png#align=left&display=inline&height=489&name=image.png&originHeight=452&originWidth=689&size=124487&status=done&width=746)

```
[CSS Modules]

	：https://github.com/css-modules/css-modules
  
  # 其不是将CSS改造成编程语言，而是功能很单纯，只加入了局部作用域和模块依赖

[案例]

	：https://github.com/ruanyf/css-modules-demos
  
  # git clone https://github.com/ruanyf/css-modules-demos.git
  
  #  npm install
  
  # npm run xxx
  
  # 访问 -> http://localhost:8080
  
[相关文档]

	：https://segmentfault.com/a/1190000011595620?utm_source=tag-newest
  
  ：http://www.ruanyifeng.com/blog/2017/04/css_in_js.html

```

## 一、局部作用域

  CSS的规则都是全局的，任何一个组件的样式规则，都对整个页面有效。

  产生局部作用域的唯一方法，就是使用一个独一无二的class的名字，不会与其他选择器重名。这就是 CSS Modules 的做法。

CSS Modules 提供各种插件，可以支持不同的构建工具。-> Webpack 的css-loader插件
  
```javascript
[React组件, App.js 样式文件]

import React from 'react';
import style from './App.css';

export default () => {
  return (
    <h1 className={style.title}>
      Hello World
    </h1>
  );
};

# 样式文件App.css输入到style对象，然后引用style.title代表一个class

[App.css]

.title {
  color: red;
}

# 构建工具会将类名style.title编译成一个哈希字符串
<h1 class="_3zyde4l1yATCOkgn-DBWEL">
  Hello World
</h1>

# App.css也会同时被编译, 类名就变成独一无二了，只对App组件有效
._3zyde4l1yATCOkgn-DBWEL {
  color: red;
}

# 
```

###   Webpack 的css-loader插件, 对CSS Modules 支持

```javascript
[案例]

	：https://github.com/ruanyf/webpack-demos
  
[webpack.config.js]

module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'stage-0', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: "style-loader!css-loader?modules"
        // -> 在css-loader后面加了一个查询参数modules，表示打开 CSS Modules 功能
      },
    ]
  }
};
```

## 二、全局作用域

### CSS Modules 允许使用:global(.className)的语法，声明一个全局规则。

 **-> 凡是这样声明的class，都不会被编译成哈希字符串。**

```css
[App.css加入一个全局class]

.title {
  color: red;
}

:global(.title) {
  color: green;
}

[App.js使用普通的class的写法，就会引用全局class]

import React from 'react';
import styles from './App.css';

export default () => {
  return (
    <h1 className="title">
      Hello World
    </h1>
  );
};
```

### 显式的局部作用域语法:local(.className)，等同于.className

```
[显式的局部作用域]

:local(.title) {
  color: red;
}

:global(.title) {
  color: green;
}
```

## 三、定制哈希类名

**css-loader默认的哈希算法是[hash:base64]，这会将.title编译成._3zyde4l1yATCOkgn-DBWEL这样的字符串。**

```javascript
[定制哈希字符串的格式]

[webpack.config.js]

module: {
  loaders: [
    // ...
    {
      test: /\.css$/,
      loader: "style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]"
    },
  ]
}

# .title被编译成了demo03-components-App---title---GpMto
```

## 四、Class 的组合

**CSS Modules 中，一个选择器可以继承另一个选择器的规则，这称为"组合"。**

```css
[.title继承 .className]

.className {
  background-color: blue;
}

.title {
  composes: className;
  color: red;
}

# 编译后

._2DHwuiHWMnKTOYG45T0x34 {
  color: red;
}

._10B-buq6_BEOTOl9urIjf8 {
  background-color: blue;
}

# h1的class也会编译成<h1 class="_2DHwuiHWMnKTOYG45T0x34 _10B-buq6_BEOTOl9urIjf8">
```

## 五、输入其他模块

**选择器也可以继承其他CSS文件里面的规则。**

```css
[another.css]

.className {
  background-color: blue;
}

[App.css 继承 another.css里面的规则]

.title {
  composes: className from './another.css';
  color: red;
}
```

## 六、输入变量

**CSS Modules 支持使用变量，不过需要安装 PostCSS 和 postcss-modules-values。**

```javascript
[postcss-modules-values]

	：https://github.com/css-modules/postcss-modules-values
  
  # npm install --save postcss-loader postcss-modules-values
  
[webpack.config.js 配置 postcss-modules-values]

var values = require('postcss-modules-values');

module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'stage-0', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: "style-loader!css-loader?modules!postcss-loader"
      },
    ]
  },
  postcss: [
    values
  ]
};

[colors.css 定义变量]

@value blue: #0c77f8;
@value red: #ff0000;
@value green: #aaf200;

[App.css 引用变量]

@value colors: "./colors.css";
@value blue, red, green from colors;

.title {
  color: red;
  background-color: blue;
}
```

## 七、相关学习资源

```basic
[官网]

	：https://css-tricks.com/css-modules-part-1-need/
  
  # 译文简介 -> https://www.jianshu.com/p/15caa7af321c
  
  # 相关文档 -> https://segmentfault.com/a/1190000010301977
```

