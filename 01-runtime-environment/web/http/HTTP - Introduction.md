
```
[官网]

	: https://httpwg.org/

  : https://http2.github.io/

	: https://www.w3.org/Protocols/

	: https://developer.mozilla.org/zh-CN/docs/Web/HTTP

// https://www.jianshu.com/p/f344c9a96be3
// http://tools.jb51.net/table/http_header
// http://www.ruanyifeng.com/blog/2016/08/http.html
```

    超文本传输协议 HyperText Transfer Protocol ， HTTP ，基于TCP/IP通信协议来传递数据。是因特网上应用最为广泛的一种网络传输协议，所有的WWW文件都必须遵守这个标准。

    HTTP协议工作于客户端-服务端架构上。浏览器作为HTTP客户端通过URL向HTTP服务端即WEB服务器发送所有请求。

    HTTP是基于客户端/服务端（C/S）的架构模型，通过一个可靠的链接来交换信息，是一个无状态的请求/响应协议。其使用统一资源标识符（Uniform Resource Identifiers, URI）来传输数据和建立连接。

    一旦建立连接后，数据消息就通过类似Internet邮件所使用的格式[RFC5322]和多用途Internet邮件扩展（MIME）[RFC2045]来传送。

```
HTTP是无连接

	无连接的含义是限制每次连接只处理一个请求。
  服务器处理完客户的请求，并收到客户的应答后, 即断开连接。采用这种方式可以节省传输时间。

HTTP是媒体独立的

	这意味着, 只要客户端和服务器知道如何处理的数据内容, 任何类型的数据都可以通过HTTP发送。
  客户端以及服务器指定使用适合的 MIME-type内容类型。

HTTP是无状态

	HTTP协议是无状态协议。
  无状态是指协议对于事务处理没有记忆能力。
  缺少状态意味着如果后续处理需要前面的信息, 则它必须重传. 这样可能导致每次连接传送的数据量增大。
  另一方面, 在服务器不需要先前信息时它的应答就较快。

MIME Type

  资源的媒体类型, 互联网（IETF）组织协商, 以 RFC 的形式作为建议的标准发布在网上的

```

![](http://localhost/it/front-end/1573084188429-89028157-093d-4ef6-b540-32670f58f1b4.png#align=left&display=inline&height=249&originHeight=401&originWidth=1200&size=0&status=done&width=746)

### 客户端请求 [请求行（request line）、请求头部（header）、空行、请求数据]



| 请求行 | 方法 | URL | 版本 | CRLF |
| **请求头** | -- | -- | -- | -- |
| :---: | :---: | :---: | :---: | :---: |
| **请求体** | -- | -- | -- |  |


![](http://localhost/it/front-end/1573046024109-9b3c2cc6-1e66-40bb-aa7e-a5a1050c427d.png#align=left&display=inline&height=264&originHeight=165&originWidth=466&size=0&status=done&width=746)

![image.png](http://localhost/it/front-end/1573049288205-489fc3fa-f36c-4b83-b56d-7fdbd643629d.png#align=left&display=inline&height=399&name=image.png&originHeight=373&originWidth=697&size=69671&status=done&width=746)

```
GET /hello.txt HTTP/1.1
User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
Host: www.example.com
Accept-Language: en, mi
```

```
Accept     指定客户端能够接收的内容格式类型
Accept-Language 指定客户端能够接受的语言类型
Accept-Ecoding  指定客户端能够接受的编码类型
User-Agent      用户代理，向服务器说明自己的操作系统、浏览器等信息
Connection      是否开启持久连接（keepalive）
Host            服务器域名

Date 信息来源的日期时间
Content-Type 指定服务器文档的MIME类型，帮助用户代理去处理接收到的数据。
Content-Length 表示 body 的字节长度。
Host 服务器的域名。
User-Agent 可以用来识别发送请求的浏览器，是产品标记符和注释的清单。
Accept 用户代理期望的MIME类型列表
Accept-Encoding 列出用户代理支持的压缩方法
Accept-Ranges 期望范围。参数：byte、none。
Assess-Control-Allow-Origin 允许组织连接控制 。
Age 对象在代理缓存中的时间
Cache-Control 指定缓存机制
Connection 是否保持网络连接打开状态。参数：keep-alive、close。
ETag 特定版本资源标识符
Expires 过期时间日期
Server 服务器信息，如JSP、Apache等。
Referer 可用于识别用户访问位置

```

### 服务端响应 [状态行、消息报头、空行、响应正文]

| 状态行 | 版本 | 状态码 | 解释状态码短语 | CRLF |
| :---: | :---: | :---: | :---: | :---: |
| **响应头** | -- | -- | -- | -- |
| **响应体** | -- | -- | -- | -- |


![](http://localhost/it/front-end/1573046057501-e7c5e513-c669-4b84-8263-a5675deb64d6.jpeg#align=left&display=inline&height=333&originHeight=305&originWidth=683&size=0&status=done&width=746)

```
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
ETag: "34aa387-d-1568eb00"
Accept-Ranges: bytes
Content-Length: 51
Vary: Accept-Encoding
Content-Type: text/plain

```

![](http://localhost/it/front-end/1573084165894-f11f70dd-783a-44be-a641-7acb9ced9514.jpeg#align=left&display=inline&height=739&originHeight=1588&originWidth=1602&size=0&status=done&width=746)

### 历史版本

###### HTTP 0.9版本      1991年

    这个版本最初用来向客户端传输HTML页面的，所以只有一个GET命令，服务器返回客户端一个HTML页面，不能是其它格式。利用这个版本完全可以构建一个简单的静态网站了。

###### HTTP 1.0版本      1996年


    1.0 版本改变是比较大的，奠定了现在HTTP协议的基础，这个版本的协议不仅可以传输HTML的文本页面，还可以传输其它二进制文件，例如图片、视频。而且还增加了现在常用的POST和HEAD命令，请求消息和响应消息也不是单一的，规定了一些元数据字段，例如：字符集、编码、状态码等
###### 
###### HTTP 1.1版本      1997年

    实际上是在1.0版本之后半年时间又发布了一个版本，这个版本在1.0版本的基础上更加完善了。

   增加了持久连接，就是说之前版本的协议一次请求就是一次TCP连接，请求完成后这个连接就关闭掉了。

    众所周知TCP协议是可靠的，建立连接需要3次握手，断开连接需要4次挥手，并且TCP有流量控制和拥塞控制，有慢开始机制，刚建立连接时传输比较慢，这是比较耗费资源的。

    一个丰富的页面会有许多图片、表单和超链接。这样的话就会有多次的HTTP请求，所以在这个版本上默认不关闭TCP连接也不用声明Connection: keep-alive字段。

   确实要关闭可以指定Connection: close字段。

    引入了管道机制，就是说在一个TCP连接里可以同时发送多个HTTP请求，而不必等待上一个请求响应成功再发送。还增加了PUT、PATCH、HEAD、 OPTIONS、DELETE等命令，丰富了客户端和服务端交互动作。还增加了Host字段。
###### 
###### HTTP 2版本      2015年

    这个版本也是随着互联网的发展，有了新的需求制定了新的功能还有对上一个版本的完善。1.1版本有了管道机制，但是正在服务端还是要对请求进行排队处理。这个版本可以多工的处理。还有了头信息压缩和服务器的主动推送。





