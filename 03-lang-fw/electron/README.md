# Electron

> 使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序。Electron 是一个使用 JavaScript, HTML 和 CSS 等 Web 技术创建原生程序的框架，它负责比较难搞的部分，你只需把精力放在你的应用的核心上即可。

> Atom Shell, 使用 Web 技术搭建桌面端程序

- Electron 基于 Chromium 和 Node.js, 让你可以使用 HTML, CSS 和 JavaScript 构建应用。
- Electron是一个由OpenJS基金会和一个活跃的贡献者社区管理的开源项目。
- Electron 兼容 Mac、Windows 和 Linux，可以构建出三个平台的应用程序。

> 语言框架学习整理步骤
>
> 1. 收集整理资料: 官网、官方文档、官方安装软件和项目地址
> 2. 简介, 简洁说明, 用途(是什么？功能, 解决什么问题？)
> 3. 简单项目案例
>   - a. 安装初始化项目步骤
>   - b. 说明核心文件功能及其简单配置

## 资源

> [官网](https://www.electronjs.org/)
>
>   - [文档](https://www.electronjs.org/docs)
>
>   - [npm electron package](https://www.npmjs.com/package/electron)
>
>   - [ELECTRON 沙盒 - Electron Fiddle是由Electron开发并由其维护者支持的沙盒程序](https://www.electronjs.org/fiddle)
>
> [Electron Forge - 打包分发工具](https://www.electronforge.io/)
>
>   - [electron-fiddle-0.25](https://github.com/electron/fiddle/releases/download/v0.25.2/electron-fiddle-0.25.2-win32-ia32-setup.exe)

### 项目资源

> 官方项目
>
>   - [electron](https://github.com/electron/electron)
>   - [electronjs.org](https://github.com/electron/electronjs.org)
>   - [electron-apps](https://github.com/electron/apps)
>   - [electron-api-demos](https://github.com/electron/electron-api-demos)
>   - [electron-quick-start](https://github.com/electron/electron-quick-start)
>   - [electron-sample-apps](https://github.com/hokein/electron-sample-apps)

## 简介

Electron 是一个使用 JavaScript、HTML 和 CSS 构建桌面应用程序的框架。通过将Chromium和Node.js嵌入到其二进制文件中，Electron 允许您维护一个 JavaScript 代码库并创建可在 Windows、macOS 和 Linux 上运行的跨平台应用程序——无需原生开发经验。

任何 Electron 应用程序的入口都是 main 文件。 这个文件控制了主进程，它运行在一个完整的Node.js环境中，负责控制您应用的生命周期，显示原生界面，执行特殊操作并管理渲染器进程。执行期间，Electron 将依据应用中 package.json配置下main字段中配置的值查找此文件。

在 Electron 中，每个窗口中无论是本地的HTML文件还是远程URL都可以被加载显示。应用程序窗口在每个OS下有不同的行为，Electron将在app中实现这些约定的责任交给开发者们。

一般而言，你可以使用 进程 全局的 platform 属性来专门为某些操作系统运行代码。

每个 Electron 应用都有一个单一的主进程，作为应用程序的入口点。 主进程在 Node.js 环境中运行，这意味着它具有 require 模块和使用所有 Node.js API 的能力。主进程的主要目的是使用 BrowserWindow 模块创建和管理应用程序窗口。

BrowserWindow 类的每个实例创建一个应用程序窗口，且在单独的渲染器进程中加载一个网页。 您可从主进程用 window 的 webContent 对象与网页内容进行交互。

### HelloWorld

```js
const { BrowserWindow } = require('electron')

const win = new BrowserWindow({ width: 800, height: 1500 })
win.loadURL('https://github.com')

const contents = win.webContents
console.log(contents)
```

每个 Electron 应用都会为每个打开的 BrowserWindow ( 与每个网页嵌入 ) 生成一个单独的渲染器进程。 洽如其名，渲染器负责 渲染 网页内容。 所以实际上，运行于渲染器进程中的代码是须遵照网页标准的 (至少就目前使用的 Chromium 而言是如此) 。渲染器无权直接访问 require 或其他 Node.js API。

预加载（preload）脚本包含了那些执行于渲染器进程中，且先于网页内容开始加载的代码 。预加载脚本可以在 BrowserWindow 构造方法中的 webPreferences 选项里被附加到主进程。由于预加载脚本与渲染器共享同一个全局 Window 接口，并且可以访问 Node.js API，因此它通过在 window 全局中暴露任意您的网络内容可以随后使用的 API 来增强渲染器。

语境隔离（Context Isolation）意味着预加载脚本与渲染器的主要运行环境是隔离开来的，以避免泄漏任何具特权的 API 到您的网页内容代码中。

取而代之，我们將使用 contextBridge 模块来安全地实现交互：

~~~js
const { contextBridge } = require('electron')

contextBridge.exposeInMainWorld('myAPI', {
  desktop: true
})

//
console.log(window.myAPI)
// => { desktop: true }
~~~

$ npx electron . # -> main.js -> 

- electron 模块

> 主进程   , 启动 Node 脚本, 及提供原生的 Node 模块访问
>
> 渲染进程 , chromium 管理的 Web 页面
>
> remote 模块, 实现在主进程和渲染进程之间做进程间通信(IPC)

