
```
[文档]

	：https://code.visualstudio.com/docs/editor/debugging#_launch-configurations

```
### 
### 添加调试 => 项目目录下，生成调试文件 launch.json

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559697955440-60e8db03-11d3-43ca-bb7a-415822053972.png#align=left&display=inline&height=325&name=image.png&originHeight=358&originWidth=811&size=29280&status=done&width=737.2727112927716)

### launch.json

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceFolder}/hello.js"
        }
    ]
}

# 预定义变量

${workspaceRoot} 

	=> the path of the folder opened in VS Code (VSCode中打开文件夹的路径)

${workspaceRootFolderName} 

	=> the name of the folder opened in VS Code without any solidus (/) (VSCode中打开文件夹的路径, 但不包含"/")

${file}

	=> the current opened file(当前打开的文件)

${relativeFile}

	=> the current opened file relative to workspaceRoot(当前打开的文件,相对于workspaceRoot)

${fileBasename} 

	=> the current opened file's basename(当前打开文件的文件名, 不含扩展名)

${fileDirname} 

	=> the current opened file's dirname(当前打开文件的目录名)

${fileExtname} 

	=> the current opened file's extension(当前打开文件的扩展名)

${cwd} 

	=> the task runner's current working directory on startup()
```

