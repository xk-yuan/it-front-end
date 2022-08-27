# c/c++

> vscode 配置 c/c++ 环境

## 资源

> [官网](https://code.visualstudio.com/docs/cpp/)

> 插件
>
> [1. ms-vscode.cpptools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)


## 简介


## 三种配置方式

> 1. [Using GCC with MinGW](https://code.visualstudio.com/docs/cpp/config-mingw)

> 2. [Using C++ and WSL in VS Code](https://code.visualstudio.com/docs/cpp/config-wsl)

WSL（Windows Subsystem Linux，windows内置的Linux子系统）下运行，还需要安装 Remote-WSL extension插件。安装方式与其他插件安装方式相同。

> 3. [Microsoft C]()

### 安装步骤

> 1. 安装语言插件

扩展 -> 搜索 c++ -> 安装 ：C/C++ ms-vscode.cpptools, C/C++ IntelliSense, debugging, and code browsing.

> 2. 方式一：在Windows下安装GCC并进行C++语言开发

a. 安装Mingw-w64

下载安装

配置环境PATH: mingw-w64\MinGW-w64\mingw32\bin

b. 测试

c:\xkower> g++ --version
g++ (i686-posix-dwarf-rev0, Built by MinGW-W64 project) 8.1.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

C:\xkower>gdb --version
GNU gdb (GDB) 8.1
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "i686-w64-mingw32".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word".

> 3. 配置测试项目

mkdir c-c++-projects && cd c-c++-projects
mkdir helloworld && cd helloworld
code .

touch helloworld.cpp

```c++
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};

    for (const string& word : msg)
    {
        cout << word << " ";
    }
    cout << endl;
}
```

选择 Terminal -> Configure Default Build Task（终端，配置默认build任务），选择c/c++: g++.exe build active file，会创建一个新的tasks.json文件

配置task.json文件: helloworld/task.json

```json helloworld/task.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "g++.exe build active file",
            "command": "D:\\tool\\env-lang\\mingw-w64\\MinGW-w64\\mingw32\\bin\\g++.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "D:\\tool\\env-lang\\mingw-w64\\MinGW-w64\\mingw32\\bin\\"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

Termina -> Tasks:Tun Build Task (终端-->任务:执行编译任务)，快捷键为Ctrl+Shift+B 。一切正常的话编译会迅速完成，并在相同目录下生成helloworld.exe文件。在终端运行 .\helloworld.exe可以看到文件的输出结果。

> 4. 程序调试配置

Run -> Add Configuration (运行-->添加配置) 添加配置，选择C++(GDB/LLDB) (如果默认没有出现，则需选择最下面的more进行安装相应插件)。

在下拉菜单中选择需要的编译器，使用windows下的gcc时选择 g++.exe。

修改：miDebuggerPath 路径，program 路径

```json helloworld/.vscode/launch.json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "F:\\w-svn\\front-end\\project-engineering\\ide\\vscode\\code\\c-c++-projects\\helloworld\\helloworld.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\tool\\env-lang\\mingw-w64\\MinGW-w64\\mingw32\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

调试测试：

按F5 或者 选择 Run -> Start Debugging 开始进行程序调试

