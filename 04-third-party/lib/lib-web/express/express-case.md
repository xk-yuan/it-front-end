# express-case

> express 项目案例

## [案例 express-example](https://www.expressjs.com.cn/starter/hello-world.html)

> 1. 安装nodejs 并 创建nodesjs项目

mkdir -p express-example && cd express-example

npm init

> 2. 安装 express 库

npm install express --save-dev

```js helloworld.js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

> 3. 执行

node helloworld.js

> 4. package.json 添加, script -> "dev": "node helloworld.js"

执行: npm run dev

> 5. 访问: http://localhost:3000

## [案例 express-generator-example](https://www.expressjs.com.cn/starter/generator.html)

> 1. 安装 express-generator

npm install express-generator -g

```
express -h

  Usage: express [options] [dir]

  Options:

    -h, --help          输出使用方法

    -v, --view <engine> 
    -c, --css <engine>  
        --git           
    -f, --force         
> express -h

  Usage: express [options] [dir]

  Options:

        --version        output the version number                                                            (输出版本号)
    -e, --ejs            add ejs engine support                                                               (添加对 ejs 模板引擎的支持)
        --pug            add pug engine support                                                               (添加对 handlebars 模板引擎的支持)
        --hbs            add handlebars engine support                                                        (添加对 pug 模板引擎的支持)
    -H, --hogan          add hogan.js engine support                                                          (添加对 hogan.js 模板引擎的支持)
    -v, --view <engine>  add view <engine> support (dust|ejs|hbs|hjs|jade|pug|twig|vash) (defaults to jade)
                         添加对视图引擎（view） <engine> 的支持 (ejs|hbs|hjs|jade|pug|twig|vash) （默认是 jade 模板引擎)
        --no-view        use static html instead of view engine                                               (创建不带视图引擎的项目)
    -c, --css <engine>   add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain css)
                         添加样式表引擎 <engine> 的支持 (less|stylus|compass|sass)  (默认是普通的 css 文件)
        --git            add .gitignore                                                                       (添加 .gitignore)
    -f, --force          force on non-empty directory                                                         (强制在非空目录下创建)
    -h, --help           output usage information                                                             (输出使用方法)
```

> 2. 执行命令 express --view=ejs express-generator-example-ejs

创建了一个名称为 express-generator-example-ejs 的 Express 应用。此应用将在当前目录下的 express-generator-example-ejs 目录中创建，并且设置为使用 ejs 模板引擎（view engine）

- express --no-view express-generator-example
- express --view=ejs express-generator-example-ejs

```
> express --view=ejs express-generator-example-ejs

   create : express-generator-example-ejs\
   create : express-generator-example-ejs\public\
   create : express-generator-example-ejs\public\javascripts\
   create : express-generator-example-ejs\public\images\
   create : express-generator-example-ejs\public\stylesheets\
   create : express-generator-example-ejs\public\stylesheets\style.css
   create : express-generator-example-ejs\routes\
   create : express-generator-example-ejs\routes\index.js
   create : express-generator-example-ejs\routes\users.js
   create : express-generator-example-ejs\views\
   create : express-generator-example-ejs\views\error.ejs
   create : express-generator-example-ejs\views\index.ejs
   create : express-generator-example-ejs\app.js
   create : express-generator-example-ejs\package.json
   create : express-generator-example-ejs\bin\
   create : express-generator-example-ejs\bin\www

   change directory:
     > cd express-generator-example-ejs

   install dependencies:
     > npm install

   run the app:
     > SET DEBUG=express-generator-example-ejs:* & npm start
```

```
> express --no-view express-generator-example

   create : express-generator-example\
   create : express-generator-example\public\
   create : express-generator-example\public\javascripts\
   create : express-generator-example\public\images\
   create : express-generator-example\public\stylesheets\
   create : express-generator-example\public\stylesheets\style.css
   create : express-generator-example\routes\
   create : express-generator-example\routes\index.js
   create : express-generator-example\routes\users.js
   create : express-generator-example\public\index.html
   create : express-generator-example\app.js
   create : express-generator-example\package.json
   create : express-generator-example\bin\
   create : express-generator-example\bin\www

   change directory:
     > cd express-generator-example

   install dependencies:
     > npm install

   run the app:
     > SET DEBUG=express-generator-example:* & npm start
```

```项目架构
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.ejs
    └── index.ejs
```

> 3. 安装依赖

cd express-generator-example-ejs && npm install

> 4. 启动

npm run start

> 5. 访问：http://localhost:3000/

