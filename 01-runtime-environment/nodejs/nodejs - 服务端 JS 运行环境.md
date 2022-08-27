## 一、简介


  Node.js是一个Javascript运行环境[Runtime Environment]，于2009年5月发布，由Ryan Dahl开发，实质是对Chrome V8引擎进行了封装。


  Node.js 不是一个 JavaScript 框架，更不是浏览器端的库。Node.js 是一个能让JavaScript运行在服务端的开发平台，它让 JavaScript 成为与PHP、Python、Perl、Ruby 等服务端语言平起平坐的脚本语言。


```basic
 [官网]

    : https://nodejs.org/

 [中文官网]

    : http://nodejs.cn/

 [官方文档]

    : http://nodejs.cn/api/

 [源码仓库]

    : https://github.com/nodejs/node

 [NPM模块]

    : https://npmjs.org

 [项目仓库]

    : https://git.dev.tencent.com/jiyuan/BootNode.git
```


  Node 是一个基于事件驱动，非阻塞I/O的开源的Javascript运行环境[Runtime Environment]， 是一个能让JavaScript运行在后端的开发运行平台。其，保留了JS前端浏览器中熟悉的接口，没有更改语言本身任何特性，


** Node适合的运行场景，主要有I/O密集型和CPU密集型。**


## 二、基本概念


###   1>. 模块机制


  Node.js使用Module模块去划分不同的功能，以简化应用的开发。Modules模块有点像C++语言中的类库。


  每一个Node.js的类库都包含了十分丰富的各类函数，比如http模块就包含了和http功能相关的很多函数，可以帮助开发者很容易地对比如http,tcp/udp等进行操作，还可以很容易的创建http和tcp/udp的服务器。


  使用模块非常简单，只需要引入了类库，并且对类库的引用存放变量中，然后使用此类库引用的变量。


```javascript

var http = require('http');

var myModule = require('./myModule.js');

// node.js 会在我们应用中搜索是否存在node_modules的目录，并且搜索这个目录中是否存在http的模块

// 如果node.js找不到这个目录，则会到全局模块缓存中去寻找，用户可以通过相对或者绝对路径，指定模块的位置
```


 模块中包含了很多功能代码片断，在模块中的代码大部分都是私有的，意思是在模块中定义的函数方法和变量，都只能在同一个模块中被调用。可以使用exports对象，将某些方法和变量暴露到模块外，以供外部调用。一个模块就是一个JS文件。


###   2>.  CommonJS 模块规范


  CommonJS 对模块的规范，定义的十分简单，主要分为 ：[ 引用、模块定义、模块标识 ]。


  ：1、模块引用


```javascript
  var math = require('math');

  // require 方法，接收模块标识，以此来引入模块的API到当前的上下文环境中
```


  ：2、模块定义 - exports 对象，用于导出当前模块的方法或变量，且是唯一导出出口


    - 模块中还存在 module 对象，用来指代模块本身 ，exports 是 module 对象的一个属性


    - Node 中一个JS文件，就代表一个模块，代表一个独立的上下文环境


```javascript
 // math.js - 求和 : 调用方法 - add(int a, int b);
 exports.add = function (int a, int b) {
    var sum = 0;
    sum = a + b ;
    return sum;   
 }

 // MainApp.js
 var math = require('math');

 var sum = math.add(2,8); // 计算加和

 console.log(sum) ; // 打印
```


  ：3、模块标识 ，就是传递给require方法的参数，必须符合小驼峰命名规则，或者以 . 和 .. 开头的先对路径，或绝对路径


  ：4、小结 ，模块的定义就是为了将类聚的方法和变量限定在私有的作用域中，同时支持导出和导入功能


###   3>. Node对 CommonJS 模块规范的实现


    ：1、Node 引入一个模块执行的过程


      -> 模块路径分析


      -> 文件定位分析


      -> 编译执行


    ：2、Node 模块的分类 - Node 提供的核心模块、用户编写的文件模块


    ：3、路径分析和文件定位


      -> 核心模块路径


      -> . 和 .. 标识的，相对文件路径模块


      -> / 开始的绝对文件路径


      -> 非路径形式的文件模块 【自定义模块的加载】


    ：4、模块的编译 ，每一个文件模块都代表一个对象


```javascript
  // 模块对象定义

  function Module(id , parent) {

    this.id = id ;
    this.exports = {} ;
    this.parent = parent ;

    if(parent && parent.children) {
        parent.children.push(this);
    }

    this.filename = null ;
    this.loaded = false ;
    this.children = [] ;

  }

  // Node , 编译过程中 在文件头尾加入代码以封装成模块,进行作用于隔离

  ( function(exports, require, module, _filename, _dirname){
    // ...
    });
```


  NodeJS ，编译和执行，是文件模块引入的最后阶段。当找到文件后，Node会新建模块对象，根据文件定位加载并编译模块，对不同的扩展名有不同的载入方法 。[ .js文件，通过fs模块同步读取编译执行、.node文件，C/C++编写的扩展文件dlopen方法加载、. json文件 通过fs模块同步读取后，调用JSON.parse() 访问解析返回结果 、其余扩展名都作为 .js 文件加载 ]


###   4>. Node包，以及NPM


    1、 包 ，包的出现，只是在模块的基础上，进一步组织JS代码


    ：定义 ，包结构用于组织包中的各种文件、包描述文件用于描述包的相关信息


    ：包结构，就是一个压缩的文档文件，[zip或tar.gz打包 ，安装时解压还原]


```basic
[包结构相关文件 - 发布包的文档结构]

    : package.json       包描述文件

    : bin                存放二进制可执行文件目录

    : lib                JavaScript代码目录

    : doc                文档目录

    : test               单元测试用例代码目录
```


    2、NPM 【Package Manager - 包管理工具】 ，对包组织管理的一种实践，npm 是其管理工具 ，用于管理第三方包模块


```basic
  [npm 基本命令]

    : npm -v    查看版本

    : npm install express    安装依赖包 , 简写 npm install / npm i

        -> express 安装的第三方包名，只安装一个包 、简写形式是根据包描述文件自动安装所有依赖包

    : npm init            初始化包描述文件 package.json

    : npm ls              分析包
```


    3、小结


  JS 在Node出现后，他的一些模块可以实现前后端公用，即在后端开发的代码，可以直接运行在前端环境下，即，脱离后端Node运行环境，直接运行在浏览器环境中，原因是其API是在各宿主环境下都提供的。


```javascript
[兼容 - 前后端多模块规范]

// 定义hello方法 - 兼容Node、AMD、CMD和常见的浏览器环境

;(function(name, definition){

    // 检测上下文环境是否为AMD或CMD
    var hasDefine = type define ==='function',
        // 检测上下文环境是否符合Node
        hasExports = typeof module !== 'undefined' && module.exports;

    if(hasDefine){
        // AMD环境或CMD环境
        define(definition);
    } else if (hasExports) {
        // 定义为普通Node模块
        module.exports = definition();
    } else {
        // 将模块的执行结果，挂在Window中，浏览器this执行window对象
        this[name] = definition();
    }
})('hello', function(){
    var hello = function(){
        // ...
    }
    return hello;
}
```


###   5>. 异步 I/O 和 异步编程


###   6>. 函数式编程、高阶函数、偏函数


    1、函数的参数只接收基本数据类型或对象的引用，函数返回值只返回基本数据类型或对象引用


    2、函数可以作为参数，函数可以作为返回值


## 三、NodeJS环境安装和基本使用


```basic
 [Download]

    : https://nodejs.org/en/download/

  // 下载合适安装包, 进行安装

  // 安装完成后, 安装目录设置环境变量环境中运行命令

  // 测试命令 : node -v
```

>

###   1>. 自定义设置目录


```basic
 [node-global - npm 全局安装位置 、node-cache - npm 缓存路径] 

   : npm config set prefix "D:\linuxTool\node-v10.14.1-x64\node_modules\node-global" 

   : npm config set cache  "D:\linuxTool\node-v10.14.1-x64\node_modules\node-cache"
```


###   2>. 案例


```javascript
[案例源码, /hello.js]

 // 以严格模式运行JavaScript代码 , 也可以不使用
 // node --use_strict 可以直接传递参数形式设置以严格模式运行
 'use strict;'
 // 控制台打印
 console.log('Hello,world!');
```


![](https://cdn.nlark.com/yuque/0/2018/png/210477/1544107502644-de599185-966e-4c95-8d94-807dcb8b3e9a.png#align=left&display=inline&height=102&margin=%5Bobject%20Object%5D&originHeight=102&originWidth=543&status=done&style=none&width=543)


###   3>. NodeJS 项目开发环境 Visual Studio Code ，[简单案例视频](https://www.bilibili.com/video/av5827351/)


  ：VS Code以文件夹作为工程目录（Workspace Dir），所有的JavaScript文件都存放在该目录下。此外，VS Code在工程目录下还需要一个`.vscode`的配置目录，里面存放里VS Code需要的配置文件。


###   4>. NodeJS 核心模块与基本概念，结合实例学习


  [ ：扫盲参考文档](http://www.runoob.com/nodejs/nodejs-tutorial.html) ，[参考](https://blog.csdn.net/u010365819/article/details/81567948) ，[参考](https://www.yiibai.com/nodejs)


[    ：视频资源](https://www.imooc.com/learn/348)


   [：进阶参考文档](http://blog.fens.me/series-nodejs/)


## 四、基本概念案例学习


###   1>. 回调函数


  Node.js 异步编程的直接体现就是回调 ，异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。


  回调函数就是一个通过函数指针调用的**函数**。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。


  简言之，回调函数就是一个函数，其将函数指针(标识)作为参数，传递给相应事件的产生方，当相应事件发生时，就会通过函数指针来调用[回调]此函数。


```basic
[实现步骤]

  1、定义一个回调函数;

  2、提供函数实现的一方在初始化的时候，将回调函数的函数指针注册给调用者;

  3、当特定的事件或条件发生的时候，调用者使用函数指针调用回调函数对事件进行处理;
```


###   2>. 回调函数传参


将回调函数的参数作为与回调函数同等级的参数进行传递


![](https://cdn.nlark.com/yuque/0/2018/png/210477/1544147059948-fa1e1cff-6fde-446e-962a-0f938a88cbf7.png#align=left&display=inline&height=479&margin=%5Bobject%20Object%5D&originHeight=479&originWidth=1487&status=done&style=none&width=826)


回调函数的参数在调用回调函数内部创建
![](https://cdn.nlark.com/yuque/0/2018/png/210477/1544147225408-d964ff40-6238-461b-8b8f-552c3c0cea52.png#align=left&display=inline&height=594&margin=%5Bobject%20Object%5D&originHeight=594&originWidth=1415&status=done&style=none&width=826)![](https://cdn.nlark.com/yuque/0/2018/png/210477/1544149115187-35c94f24-e60d-4ea9-986b-38b8a688bd5b.png#align=left&display=inline&height=743&margin=%5Bobject%20Object%5D&originHeight=743&originWidth=1920&status=done&style=none&width=826)
###   3>. 事件


  Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。其，基本上所有的事件机制都是用设计模式中观察者模式实现。


  Node.js 有多个内置的事件，我们可以通过引入 events 模块，并通过实例化 EventEmitter 类来绑定和监听事件
![](https://cdn.nlark.com/yuque/0/2018/png/210477/1544149197154-39f725a2-066c-4ad0-9cd4-d66db4b94c3e.png#align=left&display=inline&height=252&margin=%5Bobject%20Object%5D&originHeight=252&originWidth=626&status=done&style=none&width=626)
```javascript
[事件]

// 1、引入 events 模块
var events = require('events');

// 2、创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

// 3、实现事件处理程序
var eventHandler = function() {}

// 3、绑定事件及事件的处理程序
eventEmitter.on('eventName', eventHandler);

// 4、触发事件
eventEmitter.emit('eventName');
```
 
 Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。所有这些产生事件的对象都是 events.EventEmitter 的实例。events 模块只有一个对象- events.EventEmitter ，EventEmitter 的核心就是事件触发与事件监听器功能的封装。


 EventEmitter 对象如果在实例化时发生错误，会触发 error 事件。当添加新的监听器时，newListener 事件会触发，当监听器被移除时，removeListener 事件被触发。


  EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，其支持若干个事件监听器。当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。


###   4>. Buffer 缓冲区


  JavaScript语言自身只有字符串数据类型，没有二进制数据类型，在处理像TCP流或文件流时，必须使用到二进制数据。因此在 Node中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区，其是Node核心模块。


  Buffer库为Node带来了一种存储原始数据的方法，可以让Node处理二进制数据，在处理I/O操作中移动的数据时，就有可能使用Buffer库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。


###   5>. Stream 流


  Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）


  Stream 有四种流类型 ：Readable - 可读操作、Writable - 可写操作、Duplex - 可读可写操作.、Transform - 操作被写入数据，然后读出结果。所有的 Stream 对象都是 EventEmitter 的实例 ，常用的事件有 ：data - 当有数据可读时触发、end - 没有更多的数据可读时触发、 error - 在接收和写入过程中发生错误时触发、finish - 所有数据已被写入到底层系统时触发。


  管道流 Pipe ，管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。


  链式流 ，链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。


###   6>. 模块系统


  模块是Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。


  Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。


###   7>. 路由


  路由就是，将访问请求与具体的执行代码之间建立联系，其，根据请求的 URL 和其他需要的 GET 及 POST 参数，来判断并执行相应的代码。


  简言之，路由的功能就是，根据不同的请求来，来判断需要执行的业务代码，使得业务和请求之间建立路由关系。


## 五、总结
 


 


