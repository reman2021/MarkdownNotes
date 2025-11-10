### 附加功能包获取

1. 下载：[获取和共享代码](https://ww2.mathworks.cn/matlabcentral/fileexchange)
2. 在 Matlab 里双击运行并安装

### mlapp 生成 .exe
```
% 生成原型文件
loadlibrary('libnuaa_111_x8664_Windows_DLL.dll', 'head.h', 'mfilename', 'libnuaa_protofile');
% 编译为可执行文件
appFile = 'znysapp.mlapp';
outputDir = 'D:\myFiles\Project\GUI_ZNYS\znysxt\software';
compiler.build.standaloneApplication(appFile, ...
    'AdditionalFiles', {...
    'libnuaa_111_x8664_Windows_DLL.dll', ...
    'libnuaa_protofile.m', ...
    'libnuaa_111_x8664_Windows_DLL_thunk_pcwin64.dll'}, 'OutputDir', outputDir);
