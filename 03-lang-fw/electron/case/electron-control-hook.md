# iohook

## iohook

> [iohook](https://wilix-team.github.io/iohook/usage.html)
>
>  [ELECTRON中引入IOHOOK来监听系统级鼠标键盘事件](https://www.freesion.com/article/92401381309/)

npm install iohook@0.6.5 --save-dev

```json package.json
"iohook": {
    "targets": [
        "node-72",
        "electron-70"
    ],
    "platforms": [
        "win32",
        "darwin",
        "linux"
    ],
    "arches": [
        "x64",
        "ia32"
    ]
}

// 重新编译
"rebuildnew": "npm rebuild --runtime=electron --target=5.0.0 --disturl=https://atom.io/download/atom-shell --abi=70"
console.log(nodeAbi.getAbi('12.16.1','node'))  // 68
console.log(nodeAbi.getAbi('5.0.0','electron'))// 70
console.log(nodeAbi.getTarget('68','node'))    // 12.0.0
console.log(nodeAbi.getTarget('70','electron'))//5.0.0

// npm install node-abi --save-dev # 使用node-abi来获取electron和node对应的abi版本
// 
```

```js ioHook-app.js
const ioHook = require('iohook');
 
ioHook.start(false);
const eventHandler =function(type){
    switch (type) {
        case 'mouseclick':
            console.log('mouse is click!')
            break;
        case 'mousedown':
            console.log('mouse is press!')
            break;
        case 'mouseup':
            console.log('mouse is release!')
            break;
        case 'mousedrag':
            console.log('mouse is moving!')
            break;
        case 'mousedrag':
            console.log('mouse is moving!')
            break;
        case 'mousewheel':
            console.log('keybord is rolling!')
            break;
        case 'keydown':
            console.log('keybord is press!')
            break;
        default:
            console.log('move mouse or keyboard try it!')
            break;
    }
}

ioHook.start(false);
ioHook.on('mouseclick', ()=>{eventHandler('mouseclick')});
ioHook.on('mousedown', ()=>{eventHandler('mousedown')});
ioHook.on('mouseup', ()=>{eventHandler('mouseup')});
ioHook.on('mousedrag', ()=>{eventHandler('mousedrag')});
ioHook.on('mousewheel', ()=>{eventHandler('mousewheel')});
ioHook.on('mouse', ()=>{eventHandler('mousedrag')});
ioHook.on('keyup', ()=>{eventHandler('keyup')});
ioHook.on('keydown', ()=>{eventHandler('keydown')});


app.on('before-quit', () => {
    // 卸载iohook监听
    ioHook.unload();
    ioHook.stop();
});
```

gyp info using node-gyp@3.6.3
gyp info using node@16.4.1 | win32 | x64
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "C:\Python39\python.EXE", you can set the PYTHON env variable.

npm --add-python-to-path='true' --debug install --global windows-build-tools
npm install --global node-gyp


error F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\electron: Command failed.
Exit code: 1
Command: node install.js
Arguments:
Directory: F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\electron
Output:
Downloading electron-v2.0.18-win32-x64.zip
Error: read ECONNRESET
F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\electron\install.js:54

ELECTRON_MIRROR="https://cdn.npm.taobao.org/dist/electron/"
cnpm install


gyp verb check python checking for Python executable "python2" in the PATH
gyp verb `which` failed Error: not found: python2
gyp verb `which` failed     at getNotFoundError (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:13:12)
gyp verb `which` failed     at F (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:68:19)
gyp verb `which` failed     at E (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:80:29)
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:89:16
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_isexe@2.0.0@isexe\index.js:42:5
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_isexe@2.0.0@isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (node:fs:195:21)
gyp verb `which` failed  python2 Error: not found: python2
gyp verb `which` failed     at getNotFoundError (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:13:12)
gyp verb `which` failed     at F (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:68:19)
gyp verb `which` failed     at E (F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:80:29)
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_which@1.3.1@which\which.js:89:16
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_isexe@2.0.0@isexe\index.js:42:5
gyp verb `which` failed     at F:\w-svn\front-end\fw\electron\code\electron-control-hook\remote-monitor-client\node_modules\_isexe@2.0.0@isexe\windows.js:36:5
gyp verb `which` failed     at FSReqCallback.oncomplete (node:fs:195:21) {
gyp verb `which` failed   code: 'ENOENT'
gyp verb `which` failed }
gyp verb check python checking for Python executable "python" in the PATH
gyp verb `which` succeeded python C:\Python39\python.EXE
gyp ERR! configure error 
gyp ERR! stack Error: Command failed: C:\Python39\python.EXE -c import sys; print "%s.%s.%s" % sys.version_info[:3];
gyp ERR! stack   File "<string>", line 1
gyp ERR! stack     import sys; print "%s.%s.%s" % sys.version_info[:3];
gyp ERR! stack                       ^
gyp ERR! stack SyntaxError: invalid syntax
gyp ERR! stack
gyp ERR! stack     at ChildProcess.exithandler (node:child_process:397:12)
gyp ERR! System Windows_NT 10.0.19042

下载安装 python2 : 设置环境变量 PYTHON=python2
