### 01 回调函数

  异步编程的直接体现就是回调，异步编程依托于回调来实现，回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

```java
[回调函数一般作为最后一个参数传递]

function foo1(name, age, callback) { }

function foo2(value, callback1, callback2) { }
```

#### 阻塞 & 非阻塞

### 02 事件循环

  Node  是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。

事件驱动模型，(events 事件模块)

![image.png](http://localhost/it/front-end/1558538412733-9b2f12f5-4c7a-4762-8688-283273dcf1e6.png#align=left&display=inline&height=252&name=image.png&originHeight=252&originWidth=626&size=67081&status=done&width=626)

  所有异步操作都会发往 事件队列，EventEmitter 类。EventEmitter 的核心就是事件触发与事件监听器功能的封装。

```java
[引入 events 模块，并通过实例化 EventEmitter 类来绑定和监听事件]

// 引入 events 模块
var events = require('events');

// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

// 绑定事件处理程序
eventEmitter.on('eventName', eventHandler);

// 触发事件
eventEmitter.emit('eventName');

// 创建事件处理程序
var eventHandler = function connected() {
   console.log('连接成功。');

   // 触发 data_received 事件 
   eventEmitter.emit('data_received');
}

console.log("程序执行完毕!");
```

```java
[事件]

	：error 事件 # EventEmitter 实例化失败
    
    ：newListener 事件 # 添加新的监听器
    
    ：removeListener 事件 # 监听器被移除
```


### 03 缓冲区 BUFFER

  JavaScript 只有字符串数据类型，没有二进制数据类型，Node.js 专门定义了一个 Buffer 类，用来创建一个专门存放二进制数据的缓存区。

  Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据。

#### 字符编码

```java
[字符编码]

	：ascii - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。

	：utf8 - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。

	：utf16le - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。

	：ucs2 - utf16le 的别名。

	：base64 - Base64 编码。

	：latin1 - 一种把 Buffer 编码成一字节编码的字符串的方式。

	：binary - latin1 的别名。

	：hex - 将每个字节编码为两个十六进制字符
```

```java
// 字符编码转换

const buf = Buffer.from('runoob', 'ascii');

// 输出 72756e6f6f62
console.log(buf.toString('hex'));

// 输出 cnVub29i
console.log(buf.toString('base64'));
```

```javascript
[Buffer]

	：Buffer.alloc(size[, fill[, encoding]]) # 返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0

    ：Buffer.allocUnsafe(size) # 返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据

	：Buffer.allocUnsafeSlow(size)

    ：Buffer.from(array) # 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖）

	：Buffer.from(arrayBuffer[, byteOffset[, length]]) # 返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。

	：Buffer.from(buffer) # 复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例

	：Buffer.from(string[, encoding]) # 返回一个被 string 的值初始化的新的 Buffer 实例

// 创建一个长度为 10、且用 0 填充的 Buffer。
const buf1 = Buffer.alloc(10);

// 创建一个长度为 10、且用 0x1 填充的 Buffer。 
const buf2 = Buffer.alloc(10, 1);

// 创建一个长度为 10、且未初始化的 Buffer。
// 这个方法比调用 Buffer.alloc() 更快，
// 但返回的 Buffer 实例可能包含旧数据，
// 因此需要使用 fill() 或 write() 重写。
const buf3 = Buffer.allocUnsafe(10);

// 创建一个包含 [0x1, 0x2, 0x3] 的 Buffer。
const buf4 = Buffer.from([1, 2, 3]);

// 创建一个包含 UTF-8 字节 [0x74, 0xc3, 0xa9, 0x73, 0x74] 的 Buffer。
const buf5 = Buffer.from('tést');

// 创建一个包含 Latin-1 字节 [0x74, 0xe9, 0x73, 0x74] 的 Buffer。
const buf6 = Buffer.from('tést', 'latin1');
```

```javascript
[写入缓冲区]

  ：buf.write(string[, offset[, length]][, encoding])


[参数]

  => string - 写入缓冲区的字符串
  => offset - 缓冲区开始写入的索引值，默认为 0 
  => length - 写入的字节数，默认为 buffer.length
  => encoding - 使用的编码。默认为 'utf8' 

buf = Buffer.alloc(256);
len = buf.write("xxxx");

console.log("写入字节数 : "+  len);

[缓冲区读取数据]

	：buf.toString([encoding[, start[, end]]])

[参数]

  => start - 指定开始读取的索引位置，默认为 0
  => end - 结束位置，默认为缓冲区的末尾。

buf = Buffer.alloc(26);
for (var i = 0 ; i < 26 ; i++) {
  buf[i] = i + 97;
}

console.log( buf.toString('ascii'));       // 输出: abcdefghijklmnopqrstuvwxyz
```

```javascript
[Buffer 转换为 JSON 对象]

	：buf.toJSON()

const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
const json = JSON.stringify(buf);

// 输出: {"type":"Buffer","data":[1,2,3,4,5]}
console.log(json);

const copy = JSON.parse(json, (key, value) => {
  return value && value.type === 'Buffer' ?
    Buffer.from(value.data) :
    value;
});

// 输出: <Buffer 01 02 03 04 05>
console.log(copy);
```

```javascript
[缓冲区合并]

	：Buffer.concat(list[, totalLength])

[参数]

  => list - 用于合并的 Buffer 对象数组列表
  => totalLength - 指定合并后Buffer对象的总长度

var buffer1 = Buffer.from(('Hello, '));
var buffer2 = Buffer.from(('World!'));
var buffer3 = Buffer.concat([buffer1,buffer2]);

console.log(buffer3.toString()); // Hello, World!
```

```javascript
[缓冲区比较]

	：buf.compare(otherBuffer); // buf 在 otherBuffer, 之前 , 之后, 相同

var buffer1 = Buffer.from('ABC');
var buffer2 = Buffer.from('ABCD');
var result = buffer1.compare(buffer2);

if(result < 0) {
   console.log(buffer1 + " 在 " + buffer2 + "之前");
}else if(result == 0){
   console.log(buffer1 + " 与 " + buffer2 + "相同");
}else {
   console.log(buffer1 + " 在 " + buffer2 + "之后");
}
```

```javascript
[拷贝缓冲区]

	：buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])

[参数]

	=> targetBuffer - 要拷贝的 Buffer 对象。
	=> targetStart - 数字, 可选, 默认: 0
	=> sourceStart - 数字, 可选, 默认: 0
	=> sourceEnd - 数字, 可选, 默认: buffer.length

[缓冲区裁剪]

	：buf.slice([start[, end]])

[缓冲区长度]

	：buf.length;
```

### 04 流 Stream

  Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。所有的 Stream 对象都是 EventEmitter 的实例。

```basic
[流类型]

  => Readable - 可读操作
  => Writable - 可写操作
  => Duplex - 可读可写操作
  => Transform - 操作被写入数据，然后读出结果

[常用事件]

  => data   - 当有数据可读时触发
  => end    - 没有更多的数据可读时触发
  => error  - 在接收和写入过程中发生错误时触发
  => finish - 所有数据已被写入到底层系统时触发
```

#### 读数据

```javascript
[读数据]

var fs = require("fs");
var data = '';

// 创建可读流
var readerStream = fs.createReadStream('input.txt');

// 设置编码为 utf8。
readerStream.setEncoding('UTF8');

// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});

readerStream.on('end',function(){
   console.log(data);
});

readerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

#### 写数据

```javascript
[写数据]

var fs = require("fs");
var data = '写数据';

// 创建写入流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');

// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');

// 标记文件末尾
writerStream.end();

// 处理流事件 --> data, end, and error
writerStream.on('finish', function() {
    console.log("写入完成。");
});

writerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

#### 管道流

提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中

![image.png](http://localhost/it/front-end/1558568658139-8f666e22-8b86-4565-914e-943eccce90fe.png#align=left&display=inline&height=398&name=image.png&originHeight=398&originWidth=397&size=20873&status=done&width=397)

```javascript
// 读取一个文件内容并将内容写入到另外一个文件中

var fs = require("fs");

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);

console.log("程序执行完毕");
```

#### 链式流

通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。

```javascript
// 管道和链式来压缩文件

var fs = require("fs");
var zlib = require('zlib');

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
  
console.log("文件压缩完成。");


// 管道和链式来解压文件

var fs = require("fs");
var zlib = require('zlib');

// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input.txt'));
  
console.log("文件解压完成。");
```

### 05 模块系统 module 

  模块是Node.js 应用程序的基本组成部分，文件和模块是一一对应的，一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。

  提供 ，exports 和 require 两个对象，exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。

#### 模块创建

```javascript
[mian.js - 创建mian.js文件]

// 引入了当前目录下的 hello.js 文件，hello 模块
var hello = require('./hello');

//
hello.world();

[hello.js - 创建 hello.js , hello 模块]

// 导出接口方法, world()
exports.world = function() {
  console.log('Hello World');
}
```

```javascript
// 把一个对象封装到模块

// hello.js
module.exports = function() {
  // ...
}

// hello.js 
function Hello() { 
    var name; 
    this.setName = function(thyName) { 
        name = thyName; 
    }; 
    this.sayHello = function() { 
        console.log('Hello ' + name); 
    }; 
}; 
module.exports = Hello;

// main.js 
var Hello = require('./hello'); 
hello = new Hello(); 
hello.setName('BYVoid'); 
hello.sayHello(); 
```

#### 模块 - 存在 4 类模块（原生模块和3种文件模块）

![image.png](http://localhost/it/front-end/1558569286029-2c80185c-319e-4968-b307-d317d4a76d03.png#align=left&display=inline&height=601&name=image.png&originHeight=601&originWidth=479&size=91217&status=done&width=479)

```javascript
[模块类别]

	=> 文件模块缓存
	=> 原生模块 , 原生模块缓存
	=> 文件加载

[require方法参数]

	=> http、fs、path等，原生模块。
	=> ./mod或../mod，相对路径的文件模块。
	=> /pathtomodule/mod，绝对路径的文件模块。
	=> mod，非原生模块的文件模块

// 路径 Y 下执行 require(X) 语句执行顺序

1. 如果 X 是内置模块
   a. 返回内置模块
   b. 停止执行
2. 如果 X 以 '/' 开头
   a. 设置 Y 为文件根路径
3. 如果 X 以 './' 或 '/' or '../' 开头
   a. LOAD_AS_FILE(Y + X)
   b. LOAD_AS_DIRECTORY(Y + X)
4. LOAD_NODE_MODULES(X, dirname(Y))
5. 抛出异常 "not found"

LOAD_AS_FILE(X)
1. 如果 X 是一个文件, 将 X 作为 JavaScript 文本载入并停止执行。
2. 如果 X.js 是一个文件, 将 X.js 作为 JavaScript 文本载入并停止执行。
3. 如果 X.json 是一个文件, 解析 X.json 为 JavaScript 对象并停止执行。
4. 如果 X.node 是一个文件, 将 X.node 作为二进制插件载入并停止执行。

LOAD_INDEX(X)
1. 如果 X/index.js 是一个文件,  将 X/index.js 作为 JavaScript 文本载入并停止执行。
2. 如果 X/index.json 是一个文件, 解析 X/index.json 为 JavaScript 对象并停止执行。
3. 如果 X/index.node 是一个文件,  将 X/index.node 作为二进制插件载入并停止执行。

LOAD_AS_DIRECTORY(X)
1. 如果 X/package.json 是一个文件,
   a. 解析 X/package.json, 并查找 "main" 字段。
   b. let M = X + (json main 字段)
   c. LOAD_AS_FILE(M)
   d. LOAD_INDEX(M)
2. LOAD_INDEX(X)

LOAD_NODE_MODULES(X, START)
1. let DIRS=NODE_MODULES_PATHS(START)
2. for each DIR in DIRS:
   a. LOAD_AS_FILE(DIR/X)
   b. LOAD_AS_DIRECTORY(DIR/X)

NODE_MODULES_PATHS(START)
1. let PARTS = path split(START)
2. let I = count of PARTS - 1
3. let DIRS = []
4. while I >= 0,
   a. if PARTS[I] = "node_modules" CONTINUE
   b. DIR = path join(PARTS[0 .. I] + "node_modules")
   c. DIRS = DIRS + DIR
   d. let I = I - 1
5. return DIRS
```

### 06 全局对象 Global Object

  global 最根本的作用是作为全局变量的宿主，在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性。

```
[__filename]

	：当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。

[__dirname]

	：当前执行脚本所在的目录

[setTimeout(cb, ms)]

	：全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
  ：setTimeout() 只执行一次指定函数。返回一个代表定时器的句柄值。

[clearTimeout(t)]

	：停止一个之前通过 setTimeout() 创建的定时器

[setInterval(cb, ms)]

	：指定的毫秒(ms)数后执行指定函数(cb), 返回一个代表定时器的句柄值
  ：setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭

[clearInterval(t)]

	：清除定时器

[console]

	：控制台标准输出

[process]

	：描述当前Node.js 进程状态的对象，提供了一个与操作系统的简单接口

```

