### VSCode 拓展

1. C/C++
2. C/C++ Extension Pack
3. CMake
4. CMake Tools

### 安装 MinGW-W64 及配置环境变量

1. 下载链接：[WinLibs - GCC+MinGW-w64 compiler for Windows](https://winlibs.com/)
2. 解压后放到指定路径，如`D:\mingw64`
3. 在 MSYS 终端输入命令 `pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain` 
4. 将`D:\mingw64\bin`添加到系统环境变量的 path 里
5. 测试，CMD 中分别输入`gcc -v`、`g++ -v`、`gdb -v`

### 安装 CMake

下载[CMake](https://cmake.org/download/)并安装

### 测试

#### 项目目录结构

```
HelloWorld/
├── CMakeLists.txt
├── src/
│   └── HelloWorld.c
└── .vscode/
    ├── launch.json
    └── tasks.json
```

#### main.c

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

#### CMakeLists.txt

```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.10)
project(HelloWorld)
# 添加可执行文件
add_executable(HelloWorld src/main.c)
```

#### lauch.json

用于配置调试器。

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/HelloWorld",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc build active file",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ]
}
```

#### tasks.json

用于定义构建任务。

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "C/C++: gcc build active file",
            "type": "shell",
            "command": "gcc",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "${workspaceFolder}"
            },
            "problemMatcher": ["$gcc"],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```



https://blog.csdn.net/qq_45807140/article/details/112862592
