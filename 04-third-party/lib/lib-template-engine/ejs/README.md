# ejs

> 嵌入式 JavaScript 模板

## 资源

> [官网](https://ejs.co/)
>
>   - [GITHUB](https://github.com/mde/ejs)

> [](https://ejs.bootcss.com/)


## 简介


## 安装

> 1. 安装

$ npm install ejs

> 2. 

```js
let ejs = require('ejs');
let people = ['geddy', 'neil', 'alex'];
let html = ejs.render('<%= people.join(", "); %>', {people: people});
```

> 3. 指令渲染输出

ejs ./template_file.ejs -f data_file.json -o ./output.html

> 4. 网页中使用

```js
<script src="ejs.js"></script>
<script>
  let people = ['geddy', 'neil', 'alex'];
  let html = ejs.render('<%= people.join(", "); %>', {people: people});
</script>
```
