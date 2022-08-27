
```
[安装 Delve调试器]

	：https://github.com/derekparker/delve

[使用VS Code调试Go代码]

	：https://github.com/go-delve/delve

	：https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code
```

### 安装

```
[下载]

	：https://github.com/go-delve/delve

[解压到目录]

	：/src/github.com/go-delve/delve
 
 [安装]
 
 	：cd /src/github.com/go-delve/delve/cmd/dlv
  
  ：go build
  
  ：go install
  
[测试]

	：dlv version
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559692881972-225a8986-426e-4602-b4ea-da4fca1a0871.png#align=left&display=inline&height=100&name=image.png&originHeight=77&originWidth=576&size=12277&status=done&width=746)

### 命令

```
[version]

Delve Debugger
Version: 1.2.0
Build: $Id: 068e2451004e95d0b042e5257e34f0f08ce01466 $

[help]

Delve is a source level debugger for Go programs.

Delve enables you to interact with your program by controlling the execution of the process,
evaluating variables, and providing information of thread / goroutine state, CPU register state and more.

The goal of this tool is to provide a simple yet powerful interface for debugging Go programs.

Pass flags to the program you are debugging using `--`, for example:

`dlv exec ./hello -- server --config conf/config.toml`

Usage:
  dlv [command]

Available Commands:
  attach      Attach to running process and begin debugging.
  connect     Connect to a headless debug server.
  core        Examine a core dump.
  debug       Compile and begin debugging main package in current directory, or the package specified.
  exec        Execute a precompiled binary, and begin a debug session.
  help        Help about any command
  run         Deprecated command. Use 'debug' instead.
  test        Compile test binary and begin debugging program.
  trace       Compile and begin tracing program.
  version     Prints version.

Flags:
      --accept-multiclient   Allows a headless server to accept multiple client connections. Note that the server API is not reentrant and clients will have to coordinate.
      --api-version int      Selects API version when headless. (default 1)
      --backend string       Backend selection:
	default		Uses lldb on macOS, native everywhere else.
	native		Native backend.
	lldb		Uses lldb-server or debugserver.
	rr		Uses mozilla rr (https://github.com/mozilla/rr).
 (default "default")
      --build-flags string   Build flags, to be passed to the compiler.
      --check-go-version     Checks that the version of Go in use is compatible with Delve. (default true)
      --headless             Run debug server only, in headless mode.
      --init string          Init file, executed by the terminal client.
  -l, --listen string        Debugging server listen address. (default "localhost:0")
      --log                  Enable debugging server logging.
      --log-dest string      Writes logs to the specified file or file descriptor. If the argument is a number it will be interpreted as a file descriptor, otherwise as a file path. This option will also redirect the "API listening" message in headless mode.
      --log-output string    Comma separated list of components that should produce debug output, possible values:
	debugger	Log debugger commands
	gdbwire		Log connection to gdbserial backend
	lldbout		Copy output from debugserver/lldb to standard output
	debuglineerr	Log recoverable errors reading .debug_line
	rpc		Log all RPC messages
	fncall		Log function call protocol
	minidump	Log minidump loading
Defaults to "debugger" when logging is enabled with --log.
      --wd string            Working directory for running the program. (default ".")

Use "dlv [command] --help" for more information about a command.
```

```
[常用命令]

	：进入调试模式的几种方法
  
  1、dlv attach pid：类似与gdb attach pid，可以对正在运行的进程直接进行调试(pid为进程号)。
  2、dlv run|debug：run命令已被debug命令取代，运行dlv debug test.go会先编译go源文件，同时执行attach命令进入调试模式，该命令会在当前目录下生成一个名为debug的可执行二进制文件，退出调试模式会自动被删除。
  3、dlv exec executable_file：直接从二进制文件启动调试模式。
  4、dlv core executable_file core_file：以core文件启动调试，通常进行dlv的目的就是为了找出可执行文件core的原因，通过core文件可直接找出具体进程异常的信息。

dlv trace：该命令最直接的用途是可以追踪代码里函数的调用轨迹，可通过help查看其调用方式

bp：查看所有断点

on  ：当运行到某断点时执行相应命令，断点可以是名称（在设置断点时可命名断点）或者编号，例如on 1 p a表示运行到断点1时打印变量a。
```

