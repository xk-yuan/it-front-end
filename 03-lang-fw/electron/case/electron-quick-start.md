# electron-case-electron-quick-start

> 案例项目 electron-quick-start

## electron-quick-start

> 1. 初始化项目

$ mkdir electron-quick-start && cd electron-quick-start
$ yarn init # > entry point 应为 main.js, > package.json -> "start": "electron ."
$ yarn install --save-dev electron@^13.1.6
$ yarn start

> 2. 克隆项目

$ git clone https://github.com/atom/electron-quick-start
$ cd electron-quick-start
$ yarn install && yarn start

```md 项目架构
> electron-quick-start
>
> - .gitignore
> - LICENSE
> - README.md
>
> - src
>   - index.html         // 主窗口
>   - main.js            // 项目入口
>   - preload.js
>
>   - rederer            //
>     - index.js
```

```html index.html 主窗口内容
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <!-- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP -->
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <meta http-equiv="X-Content-Security-Policy" content="default-src 'self'; script-src 'self'">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using Node.js <span id="node-version"></span>,
    Chromium <span id="chrome-version"></span>,
    and Electron <span id="electron-version"></span>.
  </body>
</html>
```

> - Electron模块
>  -  app           模块，其控制应用程序的事件生命周期
>  -  BrowserWindow 模块，其创建和管理应用程序 窗口
>
>  -> 导入: const { app, BrowserWindow } = require('electron')

```js main.js
// createWindow() 方法来将index.html加载进一个新的BrowserWindow实例
function createWindow () {
  const win = new BrowserWindow({
    width: 800,
    height: 600
  })

  win.loadFile('index.html')
}

// 在 Electron 中，只有在 app 模块的 ready 事件被激发后才能创建浏览器窗口
// 使用 app.whenReady() API来监听此事件。 在whenReady()成功后调用createWindow()。
app.whenReady().then(() => {
  createWindow()
})

// 在Windows和Linux上，关闭所有窗口通常会完全退出一个应用程序。
// 为了实现这一点，监听 app 模块的 'window-all-closed' 事件，并在用户不是在 macOS (darwin) 上运行时调用 [app.quit()][app-quit]
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})

// 当 Linux 和 Windows 应用在没有窗口打开时退出了，macOS 应用通常即使在没有打开任何窗口的情况下也继续运行，并且在没有窗口可用的情况下激活应用时会打开新的窗口。
// 为了实现这一特性，监听 app 模块的 activate 事件，并在没有浏览器窗口打开的情况下调用你仅存的 createWindow() 方法。
// 因为窗口无法在 ready 事件前创建，你应当在你的应用初始化后仅监听 activate 事件。 通过在您现有的 whenReady() 回调中附上您的事件监听器来完成这个操作。
app.whenReady().then(() => {
  createWindow()

  app.on('activate', function () {
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

// 要将此脚本附加到渲染器流程，请在你现有的 BrowserWindow 构造器中将路径中的预加载脚本传入 webPreferences.preload 选项。
// 在文件头部引入 Node.js 中的 path 模块
const path = require('path')

// 修改现有的 createWindow() 函数
function createWindow () {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  win.loadFile('index.html')
}
// __dirname 字符串指向当前正在执行脚本的路径 (本例中，你的项目的根文件夹)。
// path.join API 将多个路径段联结在一起，创建一个跨平台的组合路径字符串。
```

```js preload.js
// 通过预加载脚本从渲染器访问Node.js
// 预加载脚本在渲染器进程加载之前加载，并有权访问两个 渲染器全局 (例如 window 和 document) 和 Node.js 环境。
// 上面的代码访问 Node.js process.versions 对象，并运行一个基本的 replaceText 辅助函数将版本号插入到 HTML 文档中
window.addEventListener('DOMContentLoaded', () => {
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector)
    if (element) element.innerText = text
  }

  for (const dependency of ['chrome', 'node', 'electron']) {
    replaceText(`${dependency}-version`, process.versions[dependency])
  }
})
```

```html renderer.js
<!--
  与您的网页内容的任何交互，您想要将脚本添加到您的渲染器进程中。 由于渲染器运行在正常的 Web 环境中，因此您可以在 index.html 文件关闭 </body> 标签之前添加一个 <script> 标签，来包括您想要的任意脚本：
-->
<script src="./renderer.js"></script>
```

## renderer 实现 功能

> 通知, 桌面弹出通知

```js renderer.js
// 通知, 桌面弹出通知
const NOTIFICATION_TITLE = 'Title'
const NOTIFICATION_BODY = 'Notification from the Renderer process. Click to log to console.'
const CLICK_MESSAGE = 'Notification clicked'

new Notification(NOTIFICATION_TITLE, { body: NOTIFICATION_BODY }).onclick = () => console.log(CLICK_MESSAGE)
```

> 通知, 主窗口中显示通知

```js main.js
// 主窗口中显示通知
const { Notification } = require('electron')

const NOTIFICATION_TITLE = 'Basic Notification'
const NOTIFICATION_BODY = 'Notification from the Main process'

function showNotification () {
  new Notification({ title: NOTIFICATION_TITLE, body: NOTIFICATION_BODY }).show()
}

app.whenReady().then(createWindow).then(showNotification)
```
