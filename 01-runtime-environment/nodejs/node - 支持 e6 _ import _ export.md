### 说明


通过nodejs进行服务端开发时,


nodejs 目前版本，不支持 es6 import/export ，但是可以使用 babel 进行编译

### 步骤




> - npm install babel-cli  -D
> - npm install babel-preset-env -D
> - babel-node --presets env main.js
> 


> - npm install -g nodemon # 监听代码文件的变动，自动重启服务
> - 

> - nodemon --exec babel-node --presets env main.js



