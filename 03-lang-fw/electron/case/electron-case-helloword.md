# electron-case-helloword

> [github](https://github.com/xk-yuan/electron-case-helloworld)

## 项目搭建

### 搭建步骤

> 1. 项目初始化

- mkdir electron-case-helloword && cd electron-case-helloword
- yarn init

> 2. 安装 electron 依赖

- yarn add -D electron@^13.1.6
- yarn start

> 3. 配置项目文件

- `README.md`
- `.gitignore`
- `LICENSE`

- `package.json`

- `src/index.html`
- `src/main.js`
- `src/preload.js`

- `src/renderer/index.js`

```json package.json
{
  "main": "src/main.js",
  "scripts": {
    "dev": "electron ."
  },
  "devDependencies": {
    "electron": "^13.1.6"
  }
}
```

> 4. 运行项目

- yarn dev

> 5. 安装, 项目打包分发

```sh
yarn config get registry
yarn add add package --registry https://registry.npm.taobao.org/ # yarn 临时使用国内镜像
yarn config set registry https://registry.npm.taobao.org/        # yarn 配置国内镜像
```

- yarn add -D @electron-forge/cli@^6.0.0-beta.57 # 使用electron-forge项目打包分发
- yarn electron-forge import

```json package.json
{
  "scripts": {
    "dev": "electron .",
    "@electron-forge/cli": "^6.0.0-beta.57",
    "@electron-forge/maker-deb": "^6.0.0-beta.57",
    "@electron-forge/maker-rpm": "^6.0.0-beta.57",
    "@electron-forge/maker-squirrel": "^6.0.0-beta.57",
    "@electron-forge/maker-zip": "^6.0.0-beta.57",
    "start": "electron-forge start",
    "package": "electron-forge package",
    "make": "electron-forge make"
  },
  "devDependencies": {
    "@electron-forge/cli": "^6.0.0-beta.63",
    "@electron-forge/maker-deb": "^6.0.0-beta.63",
    "@electron-forge/maker-rpm": "^6.0.0-beta.63",
    "@electron-forge/maker-squirrel": "^6.0.0-beta.63",
    "@electron-forge/maker-zip": "^6.0.0-beta.63",
    "electron": "^13.1.6"
  },
  "dependencies": {
    "electron-squirrel-startup": "^1.0.0"
  },
  "config": {
    "forge": {
      "packagerConfig": {},
      "makers": [
        {
          "name": "@electron-forge/maker-squirrel",
          "config": {
            "name": "electron_helloword"
          }
        },
        {
          "name": "@electron-forge/maker-zip",
          "platforms": [
            "darwin"
          ]
        },
        {
          "name": "@electron-forge/maker-deb",
          "config": {}
        },
        {
          "name": "@electron-forge/maker-rpm",
          "config": {}
        }
      ]
    }
  }
}
```

> 6. 运行

- yarn start  # 启动项目
- yarn make   # 打包项目

> 7. 提交

git init
git config user.name xknower
git config user.email xknower@126.com
git add .
git commit -m init

### 搭建问题

> 1. 打包项目报错

Q: ✖ Making for target: squirrel - On platform: win32 - For arch: x64
An unhandled error has occurred inside Forge:
An error occured while making for target: squirrel
Failed with exit code: 1

A: package.json的“author”和“description”在打包时是必填内容

[1](https://blog.csdn.net/qq_44238690/article/details/119142913)

