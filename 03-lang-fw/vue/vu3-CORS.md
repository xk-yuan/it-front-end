# VUE3 结局CORS跨域问题

> vue3项目搭建, 访问 baidu 跨域问题

## 方案

> [1](https://www.jianshu.com/p/2ba47c66d6dc)
> [2](https://blog.csdn.net/weixin_45629294/article/details/125243642)

1. npm install --save-dev http-proxy-middleware

2. 配置

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    open: true,
    host: 'localhost',
    port: 80,
    proxy: {
      '/api/baidu': {
        target: 'https://www.baidu.com/',
        ws: true,
        changeOrigin:true, // 虚拟的站点需要更管origin
        secure: true,      // 是否https接口
        pathRewrite: {
          '^/api/baidu':'' // 重写路径
        },
        headers: {
          "Content-Type": "application/json; charset=utf-8",
          "Host": 'www.baidu.com',
          "Referer": 'https://www.baidu.com/', // 这里后端做了拒绝策略限制，请求头必须携带referer，否则无法访问后台
        }
      }
    }
  }
})
```