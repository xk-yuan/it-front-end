# electron video audio

> 基于 electron 实现的多媒体应用

## 视频播放器案例

### 1. 

> [Electron实现跨平台视频播放器](https://www.jianshu.com/p/66c80009102c)
>
>  - [](https://github.com/relaxrock/rockplayer)

```html
<video id="video" width="800" height="480" preload>
    <source src="http://127.0.0.1:8888?startTime=0" type='video/mp4'>
</video>
```

### 2.

> [基于electron的音视频播放器](https://blog.csdn.net/vgub158/article/details/91490185)

### 1. 实现视频播放器

> 1. 项目初始化

$ mkdir electron-video-ffmepg && cd electron-video-ffmepg
$ npm init # > entry point  src/main.js > package.json -> "start": "electron ."
$ npm install --save-dev electron@^13.1.6
$ npm start

src/main.js
src/preload.js
src/index.html
src/renderer.js

> 2. 依赖并实现播放功能

> 安装依赖
$ npm install --save-dev electron@^13.1.6

$ electron-packager@^14.2.1

$ npm install --save @ffmpeg-installer/ffmpeg@1.0.20
$ npm install --save fluent-ffmpeg@2.1.2
$ npm install --save video.js@^7.7.5

$ npm install --save-dev @babel/core@^7.9.6
$ npm install --save-dev @babel/preset-env@^7.2.3
$ npm install --save-dev babel@^6.23.0
$ npm install --save-dev css-loader@^3.5.3
$ npm install --save-dev style-loader@^1.2.1

$ npm install --save-dev gulp@^4.0.2
$ npm install --save-dev gulp-babel@^8.0.0
$ npm install --save-dev webpack@^2.5.1
$ npm install --save-dev webpack-dev-server@^3.1.11
$ npm install --save-dev webpack-target-electron-renderer@^0.4.0

>
src/main/app-menu.js
src/main/ffmpeg-helper.js
src/main/video-server.js

>
src/renderer/stream-play-tech.js
src/index.js
src/video-player.html

>
.babelrc
gulpfile.js
webpack.conifg.js
