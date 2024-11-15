###  安装 man 手册

`sudo apt-get install manpages-posix-dev `

###  VMware tools

安装：`sudo apt-get install open-vm-tools-desktop`

虚拟机设置 -> 选项 -> 共享文件夹 -> 总是启用

卸载：`sudo vmware-uninstall-tools.pl`

### VIM 编辑器

`sudo apt-get install vim`

### 安装 build-essential 软件包

`sudo apt-get install build-essential`

### FTP（File Transfer Protocol）服务

```shell
sudo apt-get install vsftpd
sudo vi /etc/vsftpd.conf
#取消下面两行注释
local_enable=YES
write_enable=YES
#重启
sudo /etc/init.d/vsftpd restart
```

### NFS（Network File System）服务

```shell
sudo apt-get install nfs-kernel-server rpcbind
mkdir linux/nfs/
cd linux/nfs/
sudo vi /etc/exports
#最后一行添加
/home/alientek/linux/nfs *(rw,sync,no_root_squash)
#重启
sudo /etc/init.d/nfs-kernel-server restart
```

### SSH 服务

`sudo apt-get install openssh-server`

`ssh xxx.xxx.xxx.xxx(ip) -l xxx(用户名) -p xx(端口号) `

### VSCode 安装

1. 下载：[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)
2. `sudo dpkg -i xxx.deb  `

### VSCode 插件

1. C/C++
2. C/C++ Snippets
3. C/C++ 
4. Code Runner
5. Include AutoComplete
6. Rainbow Brackets
7. One Dark Pro
8. GBKtoUTF8
9. ARM Assembly
10. Chinese(Simplified)
11. vscode-icons
12. compareit
13. DeviceTree
14. TabNine

### CMake

```shell
sudo apt-get install cmake
```

VSCode 安装插件 CMake Tools。

### 交叉编译工具链

1. 下载：[Downloads | Linaro](https://www.linaro.org/downloads/)（[GNU Toolchain Integration Builds](https://snapshots.linaro.org/gnu-toolchain/?_gl=1*6okto9*_ga*NzMzMTExNTgyLjE3MTIxMzg2MTM.*_ga_E12E6FXFVK*MTcxMjc1MTQ1Mi43LjAuMTcxMjc1MTQ1Mi4wLjAuMA..)）

2. 本地：[交叉编译工具链](Tool/)

```shell
sudo mkdir /usr/local/arm
sudo cp gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf.tar.xz /usr/local/arm/ -f
sudo tar -vxf gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf.tar.xz

##修改环境变量
sudo vi /etc/profile
export PATH=$PATH:/usr/local/arm/gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf/bin

##查询版本
arm-none-linux-gnueabihf-gcc -v
```

### CMakeList 使用交叉编译工具链

```cmake
cmake_minimum_required(VERSION 2.8) 
project(test)

#是否交叉编译到64位arm机器
set(TARGET_aarch64 0)
set(CROSS_CHAIN_PATH /usr/local/arm/gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf)#交叉编译器位置
set(CMAKE_C_COMPILER "${CROSS_CHAIN_PATH}/bin/arm-none-linux-gnueabihf-gcc")
set(CMAKE_CXX_COMPILER "${CROSS_CHAIN_PATH}/bin/arm-none-linux-gnueabihf-g++")

add_executable(test main.cpp)
```

### VSCode SSH

1. 下载拓展 Remote - SSH。

2. 远程资源管理器 -> SSH TARGET 设置 -> 进入 config 文件。

3. 在 config 文件中配置以下内容：

   ```
   Host <服务器名字>
   	HostName <服务器的ip>
   	Port 22
   	User <ssh登录的用户名>
   ```

4. Ctrl+Shift+P，输入 ssh coonect to host ，连接到主机。

5. 选择刚刚配置的主机，输入用户密码即可。



### VSCode 字体更换

```shell
##下载安装Consolas字体
wget https://down.gloriousdays.pw/Fonts/Consolas.zip
unzip Consolas.zip
sudo mkdir -p /usr/share/fonts/consolas
sudo cp consola*.ttf /usr/share/fonts/consolas/
sudo chmod 644 /usr/share/fonts/consolas/consola*.ttf
cd /usr/share/fonts/consolas
sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv
##查看是否安装成功
fc-list | grep Consolas
```

打开 VSCode -> 管理 -> 设置 -> 常用设置 -> Editor:Font Family 最前面加上`'Consolas',`

