# http-server

> 一个简单的静态 HTTP 服务器

## 资源

> [官网](https://github.com/http-party/http-server) [gitee](https://gitee.com/mirrors/http-server)

> [简单的零配置命令行 http 服务器--http-server入门](https://www.cnblogs.com/linyb-geek/p/13267686.html)
>
> [http-server基本使用](https://blog.csdn.net/chen__cheng/article/details/114981025)


## 简介

是一个简单的、零配置的命令行静态 HTTP 服务器。它对于生产使用来说足够强大，但它足够简单和可破解，可以用于测试、本地开发和学习。

### 安装使用

> 1. 安装 node 环境

> 2. 安装 http-server

```sh
npm install -g http-server
```

> 3. 运行

```sh
http-server . -p 80
```

### 命令参数

> Available Options:

| Command                | Description   | Defaults    |
| -------------          |-------------  |-------------|
| `-p` or `--port`       | Port to use. Use `-p 0` to look for an open port, starting at 8080. It will also read from `process.env.PORT`. | 8080 |
| `-a`                   | Address to use | 0.0.0.0|
| `-d`                   | Show directory listings | `true` |
| `-i`                   | Display autoIndex | `true` |
| `-g` or `--gzip`       | When enabled it will serve `./public/some-file.js.gz` in place of `./public/some-file.js` when a gzipped version of the file exists and the request accepts gzip encoding. If brotli is also enabled, it will try to serve brotli first.| `false` |
| `-b` or `--brotli`     | When enabled it will serve `./public/some-file.js.br` in place of `./public/some-file.js` when a brotli compressed version of the file exists and the request accepts `br` encoding. If gzip is also enabled, it will try to serve brotli first. | `false`|
| `-e` or `--ext`        | Default file extension if none supplied | `html` | 
| `-s` or `--silent`     | Suppress log messages from output  | |
| `--cors`               | Enable CORS via the `Access-Control-Allow-Origin` header  | |
| `-o [path]`            | Open browser window after starting the server. Optionally provide a URL path to open. e.g.: -o /other/dir/ | |
| `-c`                   | Set cache time (in seconds) for cache-control max-age header, e.g. `-c10` for 10 seconds. To disable caching, use `-c-1`.| `3600` |
| `-U` or `--utc`        | Use UTC time format in log messages.| |
| `--log-ip`             | Enable logging of the client's IP address |`false` |
| `-P` or `--proxy`      | Proxies all requests which can't be resolved locally to the given url. e.g.: -P http://someurl.com | |
| `--proxy-options`      | Pass proxy [options](https://github.com/http-party/node-http-proxy#options) using nested dotted objects. e.g.: --proxy-options.secure false |
| `--username`           | Username for basic authentication | |
| `--password`           | Password for basic authentication | |
| `-S`, `--tls` or `--ssl` |Enable secure request serving with TLS/SSL (HTTPS)|`false`|
| `-C` or `--cert`       | Path to ssl cert file |`cert.pem` | 
| `-K` or `--key`        | Path to ssl key file |`key.pem` |
| `-r` or `--robots`     | Automatically provide a /robots.txt (The content of which defaults to `User-agent: *\nDisallow: /`)  | `false` |
| `--no-dotfiles`        | Do not show dotfiles| |
| `--mimetypes`          | Path to a .types file for custom mimetype definition| |
| `-h` or `--help`       | Print this list and exit. | |
| `-v` or `--version`    | Print the version and exit. | |


```sh
-p 端口号 (默认 8080)

-a IP 地址 (默认 0.0.0.0) 指定的地址必须是空闲的

-d 显示目录列表 (默认 'True')

-i 显示 autoIndex (默认 'True')

-e or --ext 如果没有提供默认的文件扩展名(默认 'html')

-s or --silent 禁止日志信息输出

--cors 启用 CORS via the Access-Control-Allow-Origin header

-o 在开始服务后打开浏览器
-c 为 cache-control max-age header 设置Cache time(秒) , e.g. -c10 for 10 seconds (defaults to '3600'). 禁用 caching, 则使用 -c-1.
-U 或 --utc 使用UTC time 格式化log消息

-P or --proxy Proxies all requests which can't be resolved locally to the given url. e.g.: -P http://someurl.com

-S or --ssl 启用 https

-C or --cert ssl cert 文件路径 (default: cert.pem)

-K or --key Path to ssl key file (default: key.pem).

-r or --robots Provide a /robots.txt (whose content defaults to 'User-agent: *\nDisallow: /')

-h or --help 打印以上列表并退出
```