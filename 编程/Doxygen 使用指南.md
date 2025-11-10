---
tags:
  - Note
  - Doxygen
noteid: 20251024225208
created: 2025-10-24 22:51:36
type: 编程/Doxygen
---
> **简介**
> Doxygen 使用指南：从注释到生成文档。
***
## 安装

### Windows

1. 访问 [Doxygen 官网](https://www.doxygen.nl/download.html)
2. 下载 Windows 安装包并安装
### macOS

```bash
brew install doxygen graphviz
```

### Linux (Ubuntu/Debian)

```bash
sudo apt-get install doxygen graphviz
```

## Doxygen 注释标签说明

| 标签           | 说明    | 示例                              |
| ------------ | ----- | ------------------------------- |
| `@brief`     | 简要说明  | `@brief 这是一个函数`                 |
| `@param`     | 参数说明  | `@param name 用户名`               |
| `@return`    | 返回值说明 | `@return 操作结果`                  |
| `@note`      | 注意事项  | `@note 线程不安全`                   |
| `@see`       | 参考链接  | `@see otherFunction`            |
| `@code`      | 代码示例  | `@code .cpp ... @endcode`       |
| `@exception` | 异常说明  | `@exception std::runtime_error` |
| `@class`     | 类说明   | `@class MyClass`                |
| `@file`      | 文件说明  | `@file main.cpp`                |
| `@author`    | 作者    | `@author John Doe`              |

## 生成文档

### 命令行方式

```bash
# 生成配置文件
doxygen -g
# 生成文档
doxygen Doxyfile
# 或者直接指定配置文件
doxygen path/to/your/Doxyfile
```

### 使用 GUI 工具

```bash
doxywizard
```

## 配置文件内容

```ini
# Doxyfile 配置文件示例

# 项目相关设置
PROJECT_NAME           = "项目名称"
# 版本号
PROJECT_NUMBER         = 1.0
PROJECT_BRIEF          = "项目简介"
PROJECT_LOGO           = 

# 输入文件设置
INPUT                  = ./
RECURSIVE              = YES
EXCLUDE                = 

# 输出格式
GENERATE_HTML          = YES
GENERATE_LATEX         = NO

# 提取设置
EXTRACT_ALL            = YES
EXTRACT_PRIVATE        = YES
EXTRACT_STATIC         = YES

# 图表生成
HAVE_DOT               = YES
CALL_GRAPH             = YES
CALLER_GRAPH           = YES

# 输出目录
OUTPUT_DIRECTORY       = docs/
```
***
## 
最后更新于：**`=dateformat(this.file.mtime, "yyyy-M-d HH:mm")`**
