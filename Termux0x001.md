写给小白看的Termux使用文档 (一)
---

## 简介：

Termux是迄今为止，运行在Android上最好的终端模拟器（Terminal emulator），Termux不仅仅是终端模拟器，Termux有自己的软件包管理器（apt），
利用`apt`可以安装许多额外的开发工具，如：`vim`代码编辑器，`clang`编译器，`ssh`，Python。（这些工具已经被Termux开发者移植到Android平台下）。
所以Termux也是一个小型的Linux运行环境。我们可以在Termux下学习C，C++，Python，Javascript，甚至在Android手机中搭建一个动态网站。
通过Termux终端，你还可以使用命令控制手机，如清理统计磁盘文件，清理手机垃圾等。如果你是一名黑客，`JJUSEC`提供许多运行在Termux里的Hacking Tools，
此时Termux又是一个小型的渗透测试平台。

Termux是开源软件，任何人都可以通过源代码窥探其内部运行原理，Termux的源码托管在Github上：

[https://github.com/termux/termux-app](https://github.com/termux/termux-app)

## 安装Termux

哪里下载到Termux？

虽软在X软件商店中可以搜索到Termux，但我们推荐同学们去**可信任的站点**下载，**可信任的站点**便是官方网站上标注的可信任下载源，除此之外的一切下载源
都是有风险的。

Termux官方把应用分发到2个app商店，分别是`Google Play Store`，`F-Droid`，阁下可以从[F-Droid](https://f-droid.org/zh_Hans/docs/)上搜索`Termux`下载到安全的安装包。

如果阁下实资源检索能力真的有限，行，这里有我们准备好的[下载链接](https://f-droid.org/repo/com.termux_75.apk)

PS：（2345软件下载，华军纯净下载、ZOL软件下载、天空软件下载都是垃圾毒瘤，应该拖出去乱棍打死）。

## 使用Termux

Termux第一次启动需要下载大概20M左右的文件（包含基础C库，apt软件包管理器，bash等），需要等待几分钟。

进入命令提示符后，需要执行`apt update`命令更性软件库索引。

### 基本操作

**长按屏幕**

显示菜单项（包括复制、粘贴、更多），此时屏幕出现可选择的复制光标。

```
长按屏幕
├── COPY:复制
├── PASTE:更多
├── More:更多
   ├── Select URL: 选择网址
   └── Share transcipt: 分享命令脚本
   └── Reset: 重置
   └── Kill process: 杀掉当前终端会话进程
   └── Style: 风格配色
   └── Help: 帮助文档
从左向右滑动
```

![1](https://image.3001.net/images/20180501/15251424532278.png)


**从左向右滑动**

显示隐藏式导航栏，可以新建、切换、重命名会话session和调用弹出输入法

![2](https://image.3001.net/images/20180501/15251425706184.png)

**配置功能按键**

扩展功能键是什么?就是PC端常用的按键如:ESC键，CTR键，TAB键按键，可以通过termux的配置文件添加。

复制以下命令在termux里执行：

```shell
echo "extra-keys = [['ESC','/','-','HOME','UP','END','PGUP'],['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN']]" > ~/.termux/termux.properties
```

使用`音量+`+`Q键`弹出功能按键。

### 基本命令

apt软件包管理器

```
apt update  更新软件源索引
apt upgrade   更新所有可升级软件
apt install <package> 安装软件包
apt remove <package> 卸载软件包
apt show <package> 现实软件包描述信息
dpkg -L <package> 列出软件安装位置
```

文件操作命令：将原来的https://termux.net官方源替换为http://mirrors.tuna.tsinghua.edu.cn/termux
```
ls 列出当前目录文件
ls  -alv 列出所有文件，包含隐藏文件
rm 删除文件
rm -rf 文件夹与目录一并删除
cp <源文件> <目标位置> 复制文件到目标位置
cp -rf  <源文件> <目标位置> 复制文件和目录到目标位置
mv <源文件> <目标位置>  移动文件到目标位置
mv <老文件名> <新文件名> 重命名文件
```
### 更换国内源

默认的软件源在国外，更换Termux清华大学源,加快软件包下载速度。

首先下载vim代码编辑器： `apt install vim-python`

设置默认编辑器：`export EDITOR=vim`

编辑源文件： `apt edit-sources`

这条命令会调用VIM代码编辑器编辑`${HOME}/../etc/apt/sources.list`文件，使用VIM编辑器将原来的`https://termux.net`官方源替换为
`http://mirrors.tuna.tsinghua.edu.cn/termux`保存退出。

![3](https://image.3001.net/images/20180501/15251457797689.png)

再次更新`apt update`软件源索引。

### 安装zsh shell

默认的bash shell已经够用，如果阁下还想骚一点，可以安装`oh my zsh`，使用了zsh来替代bash作为默认shell.
使用一键安装脚本来安装,一步到位,顺便启动了外置存储,可以直接访问SD卡下的目录。

`sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"  `

Android6.0以上会弹框确认是否授权,允许授权后Termux可以方便的访问SD卡文件。

![4](https://image.3001.net/images/20180501/15251492617193.png)

选择允许后先后命令提示服有如下两个选项:

```
Enter a number, leave blank to not to change: 14
Enter a number, leave blank to not to change: 6
```
分别选择背景色和字体，或者回车不进行更改。终端里执行`exit`命令重启`sessions会话`生效配置。

执行过上面的zsh一键配置脚本后,并且授予文件访问权限的话,会在家目录生成storage目录，并且生成若干目录，软连接都指向外置存储卡的相应目录。
此时就可以修改`SDCARD`上的文件和目录了。

### 修改`oh my zsh`主题配色

```shell
vim ~/.zshrc
```

第一行可以看到,默认的zsh主题是agnoster主题:
![3](https://image.3001.net/images/20180501/15251531807018.png)

在`~.oh-my-zsh/themes`目录下放着oh-my-zsh所有的主题配置文件。可以进行更改，具体请看[oh my zsh 文档](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes)


至此，Termux配置完毕，你可以在终端里愉快的为所欲为了。

[Termux文档](https://wiki.termux.com/wiki/Main_Page)
