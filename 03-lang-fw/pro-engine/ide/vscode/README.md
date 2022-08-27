# VSCODE

> 

## 资源

> [官网](https://code.visualstudio.com/)
>
>   - [文档](https://code.visualstudio.com/docs)
>
>   - [GITHUB](https://github.com/microsoft/vscode.git)
>
>   - [](https://code.visualstudio.com/Download) | [](https://aka.ms/win32-x64-user-stable)
>
>   - [插件](https://marketplace.visualstudio.com/) | [](https://www.bilibili.com/video/av27545681/)


> 插件
>
> [中文简体包插件]() | [Chinese (Simplified) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans)
>
> [代码拼写检查器]() | [Code Spell Checker]()

launch.json # 当前开发目录自动生成的一个配置文件，序启动的路径和运行环境配置

配置类插件, Settings Sync 通过GitHub Gist同步环境配置

## 简介

vscode, 一款免费开源的轻量级的源码编辑器

微软于2015年4月30日 在Build 开发者大会上正式宣布了 Visual Studio Code 项目，一个运行于 Mac OS X、Windows和 Linux 之上的，针对于编写现代 Web 和云应用的跨平台源代码编辑器。微软公司第一次向开发者们提供了一款真正的跨平台编辑器。


> 01. 配置编辑器语言 configure language

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559124589614-113c9526-86e6-4c15-93da-4cb7e6d1e3b2.png#align=left&display=inline&height=356&name=image.png&originHeight=356&originWidth=892&size=85191&status=done&width=892)


```
[方式一]

	：F1 / Ctrl + Shift + P -> extensions

[方式二]

	：ext install

[方式三]

	：点击扩展命令图标
```

![](https://cdn.nlark.com/yuque/0/2019/png/210477/1559124966965-a4c671c2-41d2-4724-9f39-02458c6e7f0c.png#align=left&display=inline&height=303&originHeight=341&originWidth=839&status=done&width=746)

#### 扩展命令图标, 打开扩展

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559125135907-178577f9-a052-4817-aece-c2a93acef59c.png#align=left&display=inline&height=429&name=image.png&originHeight=429&originWidth=750&size=86276&status=done&width=750)

#### vscode-icons 显示Visual Studio代码的图标

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559125653117-c699f94b-d7f4-4cd1-ac94-a42a63f0739e.png#align=left&display=inline&height=742&name=image.png&originHeight=742&originWidth=764&size=161076&status=done&width=764)

### 工作区配置

```
[配置文件]

	：.vscode/settings.json
```

golang 配置

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559129649938-d6912dfd-fd14-454e-9057-6b62ac629322.png#align=left&display=inline&height=302&name=image.png&originHeight=302&originWidth=614&size=34899&status=done&width=614)

```
{

    "files.autoSave": "onFocusChange",
    
    "go.buildOnSave": true,
    
    "go.lintOnSave": true,
    
    "go.vetOnSave": true,
    
    "go.buildFlags": [],
    
    "go.lintFlags": [],
    
    "go.vetFlags": [],
    
    "go.useCodeSnippetsOnFunctionSuggest": false,
    
    "go.formatOnSave": false,
    
    "go.formatTool": "goreturns",
   
    "go.goroot": "C:\\go",
    
    "go.gopath": "D:\\GoWorks"

}
```

调试工具配置

```
[文件]

	：launch.json
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559129705868-2d736456-2434-4398-82f6-fe8b04ec1052.png#align=left&display=inline&height=316&name=image.png&originHeight=316&originWidth=413&size=19761&status=done&width=413)

### 添加启动配置 => launch.json

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559695372214-f53ff765-7e0d-4696-90a5-2ae5335951e9.png#align=left&display=inline&height=338&name=image.png&originHeight=372&originWidth=1124&size=78898&status=done&width=1021.8181596708697)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559695405105-b690d49a-bdf2-47c6-89a7-dad3740b7db5.png#align=left&display=inline&height=328&name=image.png&originHeight=361&originWidth=1174&size=53082&status=done&width=1067.2727041402145)
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "debug",
            "program": "${workspaceRoot}",
            "env": {},
            "args": []
        }
    ]
}

program参数可以指一个包的文件夹进行调试，或该文件夹中的一个文件。

mode参数可以被设置为：

debug 编译调试器下的程序文件夹和发射的内容。 [默认]
test 在程序文件夹中调试测试。
exec 来运行构建当前代码的程序文件夹的预建的二进制文件来代替。

```

