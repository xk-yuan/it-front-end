# Nodejs

> nodejs 相关学习

> [官网](https://nodejs.org/)
>
> [中文官网](http://nodejs.cn/)
> [文档](http://nodejs.cn/api/)
>
> [nodejs-github](https://github.com/nodejs)
>

## 项目

> - [nodejs](https://github.com/nodejs/node.git)


## API

### 基础部分

> - console        控制台  (全局对象, 提供了一个简单的调试控制台, 类似于 Web 浏览器提供的 JavaScript 控制台)

> - events         事件
>   - EventEmitter

> - global         全局对象

> - process        进程     (全局对象, 提供了有关当前 Node.js 进程的信息并对其进行控制)

> - Error          错误
>   - Error
>   - AssertionError
>   - RangeError
>   - ReferenceError
>   - SyntaxError
>   - SystemError
>   - TypeError

> - timer          定时器 (全局模块, 实现了与 Web 浏览器提供的定时器 API 类似的 API, 但是使用了不同的内部实现)

> - module         模块

### 操作系统

> - path           路径 (提供了一些实用工具, 用于处理文件和目录的路径)

> - stream         流   (处理流式数据的抽象接口, 用于构建实现了流接口的对象, 流可以是可读的、可写的、或者可读可写的, 所有流都是 EventEmitter 的实例)
>   - 四种基本的流类型
>   - Writable  - 可写流
>   - Readable  - 可读流
>   - Duplex    - 读写流
>   - Transform - 在读写过程中可以修改或转换数据的 Duplex 流

> - Buffer         缓冲器 (全局模块, 用于表示固定长度的字节序列, 用于直接处理二进制数据)

> - fs             文件系统 (用于与文件系统进行交互, 所有的文件系统操作都具有同步的、回调的、以及基于 promise 的形式)
>   - 文件路径
>   - 文件描述符
>   - Dir         目录
>   - Dirent
>   - FSWatcher
>   - StatWatcher
>   - ReadStream
>   - Stats
>   - WriteStream
>
>   - FileHandle

> - os             操作系统 (提供了与操作系统相关的实用方法和属性)

### 网络部分

> - url            URL

> - http           HTTP

> - http2          HTTP2/2

> - https          HTTPS

> - net            网络

> - dgram          数据报   (提供了 UDP 数据包 socket 的实现)

> - tls            安全传输层 (对安全传输层（TLS）及安全套接层（SSL）协议的实现，建立在OpenSSL的基础上)

> - dns            域名服务器 (用于启用名称解析)

### 进阶部分

> - debugger       调试器 (进程外的调试实用程序)

> - assert         断言   (断言函数，用于验证不变量)

> - work_threads   工作线程 (允许使用并行地执行 JavaScript 的线程)

### 工具部分

> - readline       逐行读取 (用于一次一行地读取可读流中的数据)

> - querystring    查询字符串   (解析和格式化 URL 查询字符串的实用工具)

> - string_decoder 字符串解码器 (用一种能保护已编码的多字节 UTF-8 和 UTF-16 字符的方式将 Buffer 对象解码为字符串)

> - util           工具

> - zlib

> - crypto         加密

### 其他部分

> - child_process  子进程

> - async_hooks    异步钩子

> - perf_hooks     性能钩子

> - inspector      检查器

> - v8

> - vm

> - tty            终端

> - repl           交互式解释器

> - cluster        集群

> - trace_events   跟踪事件

> - wasi

> - punycode       域名代码 (弃用)

> - domain         域 (弃用)
