---
tags:
  - Note
noteid: 20250916225644
created: 2025-09-16 22:55:50
type: VSCode
---
> **简介**
> 在 Windows 中配置 VSCode 的编译环境，包括 C/C++、Python，并给出对应的工程示例。
***
## C/C++

### VSCode 插件

1. C/C++
2. C/C++ Extension Pack
3. CMake
4. CMake Tools
5. Chinese

### 安装 MinGW-W64 及配置环境变量

[mingw-w64 官网](https://www.mingw-w64.org/)

1. 下载链接：[Source Code - mingw-w64](https://www.mingw-w64.org/source/) 或 [WinLibs - GCC+MinGW-w64 compiler for Windows](https://winlibs.com/)
2. 解压后放到指定路径，如`D:\mingw64` 
3. 将`D:\mingw64\bin`添加到系统环境变量的 path 里
4. 测试，CMD 中分别输入`gcc -v`、`g++ -v`、`gdb -v`

**或者**

1. 下载 [MSYS2](https://www.msys2.org/)

2. 打开 "MSYS2 UCRT64"，输入`pacman -S mingw-w64-ucrt-x86_64-gcc`下载编译器

3. 检查

   ```shell
   $ pacman -Qi mingw-w64-ucrt-x86_64-gcc | grep Version
   Version : 14.2.0-2  # GCC Version
   $ pacman -Qi mingw-w64-ucrt-x86_64-headers | grep Version
   Version : 12.0.0.r473.gce0d0bfb7-1  # mingw-w64 Version
   ```

> 以上命令只会下载编译器，没有调试器，路径为 msys64\ucrt64\bin
>
> 下载工具链：
>
> - 32 位：`pacman -S  mingw-w64-i686-toolchain`
> - 64 位：`pacman -S  mingw-w64-x86_64-toolchain`
>
> 下载后路径为 msys64\mingw64（或 mingw32）\bin

### 安装 CMake

下载[CMake](https://cmake.org/download/)并安装

### 项目配置

#### 项目目录结构

```
HelloWorld/
├── src/
│   └── HelloWorld.c
└── .vscode/
	├── c_cpp_properties.json
    ├── launch.json
    └── tasks.json
    
```

用 VSCode 打开 HelloWorld 项目文件夹，VSCode 会默认该文件夹是一个 workspace。

#### main.c

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

#### 认识 JSON

> JSON 语法是 JavaScript 语法的子集。
>
> JSON（JavaScript Object Notation，JavaScript对象表示法）是存储和交换文本信息的语法，类似 XML。


#### 配置 tasks.json

tasks.json 用于配置编译任务，该文件配置后程序才能被 C/C++ 编译器正常编译。

Terminal->Configure Tasks...->选择 gcc 编译器，则会生成 .vscode 下的 tasks.json 文件，生成的文件内容如下。

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",//任务类型
			"label": "C/C++: gcc.exe build active file",//任务标签(标记)，也即任务名称，任务名称要和 launch.json 里的 "preLaunchTask" 值对应一致。
			"command": "D:\\Program Files\\msys64\\ucrt64\\bin\\gcc.exe",//编译器及其路径，.c用 gcc.exe 编译器，.cpp 用 g++.exe 编译器
			"args": [
				"-fdiagnostics-color=always",
				"-g",//生成和调试有关的信息，launch.json 会用到这些信息。
				"${file}",//编译当前打开的.c(或.cpp)文件。
				"-o",//指定编译的输出，windows 系统下输出 .exe 文件。
				"${fileDirname}\\${fileBasenameNoExtension}.exe"//指定windows 系统下输出 .exe 文件及其路径,应该与 launch.json 的 "program" 的值代表的路径一致。修改为"${fileDirname}\\..\\bin\\${fileBasenameNoExtension}.exe"将 .exe 放在工作空间的 bin 文件夹下。
			],
			"options": {
				"cwd": "${fileDirname}"
			},
			"problemMatcher": [
				"$gcc"//使用gcc的问题匹配器。
			],
			"group": "build",
			"detail": "compiler: D:\\Program Files\\msys64\\ucrt64\\bin\\gcc.exe"
		}
	]
}
```

配置完成后，点击 Terminal->Run Built Tasks... （Ctrl+Shift+B）便会生成可执行文件。

在当前工作空间打开终端，输入 bin\hello.exe 即可运行。

#### 配置 launch.json

launch.json 文件主要用于配置调试器。

Run and Debug->creat a launch.json file->C++(GDB/LLDB)，便会生成 launch.json 文件，点击 Add Configuration->{}C/C++:（gdb）Launch 添加配置项后，文件如下。

> 使用 "launch" 模式进行调试时，VSCode 将直接启动并控制你想要调试的应用程序。
>
> "attach" 模式通常用于调试那些不能由 VSCode 直接启动的程序，或者用于在程序运行到某个特定状态时才开始调试的情况。在 "attach" 模式下，你需要先手动启动你的应用程序，然后配置调试器去连接到该应用程序的进程 ID 或监听的端口。

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",//自定义命名运行与调试的名称，将在左侧运行和调试菜单中显示名称
            "type": "cppdbg",//调试器类型
            "request": "launch",//配置请求类型，可以为 launch 或 attach
            "program": "enter program name, for example ${workspaceFolder}/a.exe",//需要进行调试的可执行文件及其路径，应该与 tasks.json 编译后输出的可执行文件及其路径一致
            "args": [],
            "stopAtEntry": false,//设为 true 时程序将暂停在程序入口处，一般为false
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,//true 开启外部控制台窗口，false 则使用 vscode 内部控制台窗口
            "MIMode": "gdb",//指示 MIDebugEngine 要连接到的控制台调试程序，允许的值为 “gdb”、“lldb”，这里使用gdb进行调试。
            "miDebuggerPath": "/path/to/gdb",//调试器 debugger 文件及其路径，这里是调用gdb调试器的路径。
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "Set Disassembly Flavor to Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc.exe build active file",//运行和调试前要启动的 tasks 任务，即要启动的编译任务，任务名要和 tasks.json 里面的 "label" 值一致
        }
        
    ]
}
```

修改 "program" 和 "miDebuggerPath" 为对应的路径即可进行调试。

#### 生成 tasks.json、launch.json 的另一种方式

源文件右上角小齿轮（Add Launch Configuration）。

#### 配置 c_cpp_properties.json

主要用于指定头文件、库的位置。

Ctrl+Shift+P 打开命令面板，输入 `C/C++:Edit Configuration`，选择后生成的 c_cpp_properties.json 文件如下。

```json
{
    "configurations": [
        {
            "name": "Win32",//windows系统：Win32；Linux系统：Linux；macOS系统：Mac
            "includePath": [
                "${workspaceFolder}/**",//当前项目所在根目录
                "${workspaceFolder}/include"//包含 include 目录
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "D:\\Program Files\\msys64\\ucrt64\\bin\\gcc.exe",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

### 多个源文件

> tasks.json 文件中使用了 "${file}" 参数，表示编译当前打开的 .c (或 .cpp )文件，因此 vscode 只能编译一个 .c (或 .cpp )文件。
>
> 若要编译多个文件，需要把 "${file}" 参数更换成各个文件路径的参数。
>
> 若项目文件和层级较多，手动添加目录会非常麻烦，这时可以使用 CMake 工具，管理程序的编译，提高项目管理效率。

#### 项目目录结构

```
HelloWorld/
├── CMakeLists.txt
├── bin/
├── include/
│   └── HelloWorld.h
├── src/
│   ├── HelloWorld.c
	└── main.c	
└── .vscode/
    ├── launch.json
    └── tasks.json
    
```

#### 配置 CMakeLists.txt

```cmake
# CMakeLists.txt
# CMake 最低版本需求，不加入此行会有警告信息
cmake_minimum_required(VERSION 3.10)
# 项目名称,即生成的 .exe 文件名称,这里的文件名称必需与 launch.json 的参数 "program" 的一致。
project(HelloWorld)
# 设置可执行文件输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
# 添加头文件目录
include_directories(include)
# 添加源文件
# 把当前目录下所有源文件加入变量SRC_LIST，. 代表 workspace 目录，这里给 src 目录
aux_source_directory(src SRC_LIST)
# 添加可执行文件
add_executable(HelloWorld ${SRC_LIST})
```

#### 配置 tasks.json、launch.json

```json
// tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {   //Cmake active file 操作，要和 launch.json 里的 "preLaunchTask" 值对应一致。
            "label": "Cmake active file", 
            "dependsOn":[
                //Cmake active file 操作依赖于下面的cmake和 make操作
                "cmake", 
                "make"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }//为 build 任务添加 "group": "build"，支持通过 Ctrl+Shift+B 触发。
        },
        {
            "label": "cmake",//cmake 操作。
            "type":"shell",           
            "command":"cmake",//执行 cmake 操作所使用的命令。
            "args": [                 //cmake 命令执行时的命令行参数。
                "-G", "MinGW Makefiles", //生成 mingw32-make 能够编译的 Makefile。
                "-S", "${workspaceFolder}",
                "-B", "${workspaceFolder}/build",
                "-DCMAKE_BUILD_TYPE=Debug"
                //使用 "-S" 指定源码目录，"-B" 指定构建目录，无需手动创建目录。添加 "-DCMAKE_BUILD_TYPE=Debug" 明确构建类型。
            ],
            "options": {
        		"cwd": "${workspaceFolder}"
              },  //项目根目录执行 CMake
        },
        {
            "label": "make",             //make 操作
            "type":"shell", 
            "command":"mingw32-make.exe", //执行 make 操作所使用的命令（mingw32-make.exe 已经添加了环境变量）。
            "args": [
            ],
            "options": {
                "cwd": "${workspaceFolder}\\build" //表示执行当前操作的工作目录。
            }
        },
    ]
}
```

```json
// launch.json
{
    "version": "2.0.0",
    "configurations": [
      {
        "name": "build and debug active file",
        "type": "cppdbg",
        "request": "launch",
        //下面是windows系统下需要调试的.exe文件及其路径,应该与 CmakeLists.txt 文件中project的文件名一致。
        "program":  "${workspaceFolder}\\bin\\HelloWorld.exe",  
        "args": [],
        "stopAtEntry": false,
        //使用${fileDirname}，需要先打开项目的一个c/c++文件再运行,
        //因为这个值表示打开的文件所在的绝对路径,因而需要打开一个文件来确定路径，
        //否则会提示 variable ${fileDirname} can not be resolved。
        //下面也可以用${workspaceFolder},表示工作台下的路径,这个值不需要打开文件来确定路径。
        "cwd": "${workspaceFolder}",
        "environment": [],
        "externalConsole": false,
        "MIMode": "gdb",
        "miDebuggerPath": "D:/Program Files/msys64/mingw64/bin/gdb.exe",
        "setupCommands": [
          {
            "description": "Enable pretty-printing for gdb",
            "text": "-enable-pretty-printing",
            "ignoreFailures": true
          },
          {
            "description": "Set Disassembly Flavor to Intel",
            "text": "-gdb-set disassembly-flavor intel",
            "ignoreFailures": true
          }
        ],
        "preLaunchTask": "Cmake active file"//要和 tasks.json 里的 "label" 值对应一致。
      }
    ]
  }
 
```

### 注意

Windows 路径分隔符 `\\` 不兼容 Linux/macOS，最好改成 `/`  确保跨平台兼容性。

### 编译时插件输出乱码

编译时输出乱码 `[build] 閫傜敤浜� .NET Framework MSBuild 鐗堟湰 17.11.9+a69bbaaf5`。

解决：cmd->运行 control intl.cpl->管理->更改系统区域设置->勾选"使用 Unicode UTF-8 提供全球语言支持"

### 参考

[最新VS code配置C/C++环境(tasks.json, launch.json,c_cpp_properties.json)及运行多个文件、配置Cmake-CSDN博客](https://blog.csdn.net/thefg/article/details/137474276)

[VScode环境下使用CMake构建工程_vscode cmake-CSDN博客](https://blog.csdn.net/qq_32348883/article/details/128890057)

[在VScode下配置C/C++环境(tasks.json、launch.json、c_cpp_properties.json)_vscode c++ launch.json-CSDN博客](https://blog.csdn.net/m0_46610658/article/details/140450473)

## Python

### Python 环境安装

官网下载地址：[Python Releases for Windows | Python.org](https://www.python.org/downloads/windows/)。
下载想要的版本并安装，安装时勾选添加环境变量选项。
验证：`Win+R`->`cmd`打开命令行->输入`python`并运行->出现版本号并进入 python 运行环境即代表安装成功。

### VSCode 插件

- Python
- flake8
- yapf

### 配置 Python 解释器

`Ctrl+Shift+P`->输入`Python: Select Interpreter`并选择该命令->选择想要使用的Python解释器版本。

### Python 项目

#### 创建虚拟环境

> 在 VSCode 中使用虚拟环境是管理项目依赖的最佳实践。通过虚拟环境，你可以为每个项目隔离不同的包和依赖，避免不同项目之间的依赖冲突。

1. 打开终端（`` Ctrl+` ``）进入项目目录。
2. 使用`python -m venv venv`命令创建虚拟环境。

> `python`：调用 Python 解释器。
> `-m` ：表示要运行一个模块（module）。
> `venv`：Python 内置的虚拟环境模块。
> `.venv`：要创建的虚拟环境的目录名称（前面的点表示在 Unix-like 系统中这是一个隐藏目录），指定虚拟环境将被创建在当前目录下的 .venv 文件夹中。

#### 激活虚拟环境

使用`.\venv\Scripts\activate`命令激活运行虚拟环境。
若遇到无法禁止运行脚本的问题，需要更改安全策略：
1. 以管理员身份打开 powershell
2. 执行`set-executionpolicy remotesigned`（默认值为`Restricted`）
3. 提示是否更改执行策略时，输入“y”并回车后即可执行脚本。

### 项目配置

#### 项目结构

```
PythonTest/
├── .vscode
├── venv/
├── utils/
│   ├── __init__.py
│   ├── module1.py
│   └── module2.py
└── main.py
```

各文件内容如下，输入代码后在 main.py 界面按 *F5* 即可运行。

```python
# utils/__init__.py
from .module1 import test1
from .module2 import test2

# utils/module1.py
def test1():
    print("Hello World!")
    
# utils/module2.py
def test2():
    print("Hello World2!")

# main.py
from utils import test1
from utils import test2

if __name__ == "__main__":
    test1()
    test2()
```

#### 调试

1. 点击“运行和调试”，点击“创建 launch.json 文件”
2. 选择“Python Debugger”作为调试器
3. 选择“Python 文件”进行调试配置
4. 生成 launch.json 文件后，即可进行调试

***
## 
最后更新于：**`=dateformat(this.file.mtime, "yyyy-M-d HH:mm")`**
