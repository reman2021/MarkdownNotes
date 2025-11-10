## Obsidian 入门

### 优点

数据存储在本地，安全性高。Notion 总是担心哪天服务器出问题了，而且 Notion 导出备份后好像无法导入还原。

思源笔记打开有点慢，Obsidian 目前不存在该问题。

### 下载

[Download - Obsidian](https://obsidian.md/download)

### 官方文档

https://publish.obsidian.md/help-zh/%E7%94%B1%E6%AD%A4%E5%BC%80%E5%A7%8B

### 第三方插件

- DataLoom：数据表
- Dataview
- Iconize：添加图标
- Multi-Column Markdown：分栏实现
- Convert url to preview（iframe）：网站嵌入视图
- Templater：更的高级模板功能
- Annotator：阅读批注插件

## 插件使用

### Templater

文档：[Introduction - Templater](https://silentvoid13.github.io/Templater/introduction.html)
1. 创建 \_Template 文件夹存放各种模板文件。
2. 打开 Templater 设置界面，在 Template folder location 处填入`_Template`。
3. 打开 “Trigger  Templater on new file creation”。
4. 为不同文件夹指定对应的模板文件。

###  Convert url to preview（iframe）


## 主题

设置 -> 外观 -> 主题 -> 管理 -> 下载 *Blue Topaz*
主题色：#648e93 晚波蓝
字体：Times New Roman、华文仿宋（英文字体在前）
字体大小：18

## CSS 样式

### 开始

找到仓库下的 .obsidian 文件夹，新建 snippets 文件夹，将 .css 文件置于 snippets 文件夹下。

### 分栏实现

css 文件下载：[Multi Column | Modular CSS Layout](https://efemkay.github.io/obsidian-modular-css-layout/multi-column/)
```
> [!multi-column]
>
>> [!note]+ Work
>> your notes or lists here. using markdown formatting
>
>> [!warning]+ Personal
>> your notes or lists here. using markdown formatting
>
>> [!summary]+ Charity
>> your notes or lists here. using markdown formatting
```
> [!multi-column]
>
>> [!note]+ Work
>> your notes or lists here. using markdown formatting
>
>> [!warning]+ Personal
>> your notes or lists here. using markdown formatting
>
>> [!summary]+ Charity
>> your notes or lists here. using markdown formatting

## Git 同步
### Windows
步骤如下：
1. 创建云端仓库（Git、Gitee）。
2. 在本地仓库文件夹下打开 Git Bash（需要安装 Git）。
3. 输入`git init`初始化本地仓库。
4. 使用`cat > .gitignore`创建 .gitignore 文件，并配置忽略规则：
```text
# Obsidian 核心忽略规则
.obsidian/workspace.json
.obsidian/workspace
.obsidian/graph.json
.obsidian/icon.json

# 回收站
.trash/

# 临时文件和缓存
*.tmp
*.log
.cache/

# 系统文件（跨平台）
.DS_Store
Thumbs.db
desktop.ini

# 备份文件
*.backup
*.bak
```
5. 输入以下命令提交到本地仓库：
```bash
# 添加所有文件到暂存区（.gitignore 规则会生效）
git add .

# 检查哪些文件将被提交
git status

# 提交到本地仓库
git commit -m "初始提交：Obsidian 仓库初始化"
```
6. 连接远程仓库并推送:
```bash
# 添加远程仓库地址
git remote add origin https://gitee.com/你的用户名/你的仓库名.git

# 推送到 Gitee
git push -u origin main

```
7. 成功后给 Obsidian 安装 Git 插件，设置自动备份时间间隔。

### Android
1. 安装 Termux。
2. 在 Termux 中安装 Git：
```bash
pkg update
pkg upgrade
pkg install git
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```
3. 克隆仓库到手机：
```bash
# 获取文件访问权限
termux-setup-storage

# 克隆仓库到对应目录
cd /storage/emulated/0/Documents
git clone https://gitee.com/你的用户名/仓库名.git obsidian
```
4. 手机版 Obsidian 选择对应仓库，打开即可