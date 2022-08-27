![image.png](http://localhost/it/front-end/1572961591046-8d7596e9-6850-479a-b23e-3f38c8397d29.png#align=left&display=inline&height=213&name=image.png&originHeight=200&originWidth=699&size=25994&status=done&width=746)

```
[官网]

	: https://eslint.org/

	: https://eslint.bootcss.com

[github]

	: https://github.com/eslint/eslint

  # eslint-plugin-react
  : https://github.com/yannickcr/eslint-plugin-react

[]

	: http://eslint.cn/docs/rules/

// https://segmentfault.com/a/1190000019896962
// https://cloud.tencent.com/developer/section/1135569
```

    ESLint最初是由Nicholas C. Zakas 于2013年6月创建的开源项目。它的目标是提供一个插件化的javascript代码检测工具。其是一个语法规则和代码风格的检查工具，可以用来保证写出语法正确、风格统一的代码

```
[安装初始化]

	: npm install eslint
  
  : eslint --init

[配置文件]

// 配置文件优先级
.eslintrc.js
.eslintrc.yaml
.eslintrc.yml
.eslintrc.json
.eslintrc
package.json

# .eslintrc
{
  "extends": "standard"
}

# vue 配置
# npm i eslint-plugin-html
{
  "extends": "standard",
  "plugins": [
    "html"
  ]
}

# "lint": "eslint --ext .js --ext .jsx --ext .vue src/"

# "lint-fix": "eslint --fix --ext .js --ext .jsx --ext .vue src/"

# eslint-loader # npm i eslint-loader babel-eslint -D
{
  "extends": "standard",
  "plugins": [
    "html"
  ],
  "parser": "babel-eslint"
}
rules: [
  {
    test: /\.(vue|js|jsx)$/,
    loader: 'eslint-loader',
    exclude: /node_modules/,
    enforce: 'pre'
  },
  ......
]

[配置]

  # npm i \
  eslint \
  eslint-config-standard eslint-plugin-standard eslint-plugin-promise \
  eslint-plugin-import eslint-plugin-node -D

	: eslint-config-standard

module.exports = {
    "env": {//如brower、node环境变量、es6环境变量、mocha环境变量等
        "browser": true,
        "es6": true,
        "node": true
    },
    "extends": [//继承一套基础配置，如："@tencent/eslint-config-idata",'standard'
        "eslint:recommended",
        "plugin:vue/essential"
    ],
    "globals": {//额外的全局变量
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parserOptions": {//指定传给 parser 的信息，eslint使用的默认是Espree
        "ecmaVersion": 2018,
        "sourceType": "module"
    },
    "plugins": [//插件可以用于rules、env和extends等配置中
        "vue"
    ],
    "rules": {//开启规则和发生错误时报告的等级
　　　　// 强制使用单引号 
　　　　'quotes': ['error', 'single'],
　　　　// 在块级作用域外访问块内定义的变量是否报错提示 
　　　　'block-scoped-var': 0,
    }
};

// .eslintrc.js文件 https://eslint.org/docs/user-guide/configuring
```


