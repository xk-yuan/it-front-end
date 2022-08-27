# 命令行程序

> 实现 命令行参数解析、管道处理IO、命令行交互

## 帮助信息

``` babel

Usage: babel [options] <files ...>

Options:

  -h, --help                    output usage information
  -f, --filename [filename]     filename to use when reading from stdin
  [...]
  -q, --quiet                   Don't log anything
  -v, --version                 output the version number 

```

> 帮助信息
> 文件数据
> 静默模式
> 版本信息
> -y, -yes  表示使用默认值
> -f,       表示需要从 stdin 中抓取数据

> 连字符 - (参数简称) 和 双连字符 -- (参数全名), 接口命令行参数


## 实现 : parser-json 解析JSON数据

> run: node parser-json.js -f my.json


### 命令行参数解析

> 使用, process.argv 数组, 该数组是执行命令时传给 shell 的字符串
>
> 使用, 第三方模块 yargs 解析参数
> 使用 mississippi 库, 获取命令行数据

```
const readFile = require('fs').readFile;
const yargs    = require('yargs');

// 解析参数
const argv = yargs
    .demand('f')                            // 必须传入识别出 f 参数命令, 才能运行解析
    .nargs('f', 1)                          // -f 必须有参数有值
    .describe('f', 'JSON file to parse')
    .argv;

// 添加使用说明
yargs
  // ...
  .usage('parse-json [options]')
  .help('h')
  .alias('h', 'help')
  // ...
```

>
> npm install mississippi --save-dev -g
> npm install yargs --save-dev -g
```
#!/usr/bin/env node

const readFile = require('fs').readFile;
const concat   = require('mississippi').concat;
const yargs    = require('yargs');

const argv = yargs
    .usage('parse-json [options]')
    .help('h')
    .alias('h', 'help')
    .demand('f')
    .nargs('f', 1)
    .describe('f', 'JSON file to parse')
    .argv;

const file = argv.f;
function parse(str) {
  const value = JSON.parse(str);
  console.log(JSON.stringify(value));
}

if(file === '-' ) {
  // 当文件名是 '-' 时, 加载 mississippi.concat, 对 stdin流进行 cancat
  process.stdin.pipe(concat(parse));
} else {
  readFile(file, (err, dataBuffer) => {
      if(err) {
          throw err;
      } else {
          parse(dataBuffer.toString());
      }
  });
}
```

### npm 共享库

> package.json , 增加 bin 域
```
  "name": "parse-json",
  "bin": {
      "parse-json": "index.js"
  }
```

### 管道技术, 连接脚本

> 管道技术, 将一个程序的 stdout 附着到另一个程序的 stdin 流上, 是进程间通信的中间组件
>
> 管道操作符, |  将前一个程序的运行结果, 作为下一个程序的输入
>
> 管道操作符, && 后一个程序在前一个程序, 执行成功退出码为0时执行
> 管道操作符, || 后一个程序在前一个程序, 执行失败退出码非0时执行

```
/**
 * 输出前面程序( parse-json 执行时长)在被管道中断之前程序运行了多长时间
 * 
 * @run node parse-json -f my.json | node time.js
 */
process.stdin.pipe(process.stdout);

const start = Date.now();

process.on('exit', () => {
  const timeTaken = Date.now() - start;
  console.error(`Time (s): ${timeTaken / 1000}`);
});
```

### 错误处理和退出码

> 控制流, stdin 编号 0, stdout 编号 1, stderr 编号 2
>
>
