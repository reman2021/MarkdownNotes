### 下载主题

文件->偏好设置->外观->获取主题

> 目前使用主题：[Monospace](https://theme.typora.io/theme/Monospace/)

### 安装主题

文件->偏好设置->外观->打开主题文件夹，将下载的主题文件放到该文件夹下，重启 Typora，选择主题即可。

### 主题修改

#### 字体大小

```
html {
  font-size: 18px;
}
```

#### 正文字体修改

[CSS字体中英文名称对照表](http://www.mafengxue.cn/index.php/2016/01/26/css字体中英文名称对照表：如宋体对应simsun/)

```
html,
body {
  font-family: Consolas, STSong, monospace;
}
/* 英文：Consolas，中文：华文宋体 */
```

#### 标题字体修改

```
h1,
[mdlike='h1'] {
  font-size: 2.25rem;
  font-family: Consolas, "Microsoft Yahei";
}
/* 一级标题，英文：Consolas，中文：微软雅黑 */
```

#### 复选框未对齐正文

```
.task-list-item input:before {
  content: '[ ]';
  display: inline-block;
  margin-left: -2ch;
  width: 4ch;
  position: absolute;
  top: -50%;
  vertical-align: middle;
  text-align: center;
  background-color: white;
  color: #438600;
}
/* 通过 top 微调伪元素的垂直位置 */
```

#### 行内公式

```
/* 公式渲染颜色 */
[md-inline='inline_math'] {
    color: #F1BFE9;
}
/* 公式编辑颜色 */
.md-inline-math script {
    color: #f1939c;
}
```

### 参考

[爆改Typora默认样式，世界终于平静了。。。 - 简书](https://www.jianshu.com/p/62b61fd69d33)

[【工具】Typora中主题css修改｜看了这篇，一劳永逸_typora css-CSDN博客](https://blog.csdn.net/qq_46106285/article/details/104732197)