[TOC]



领到的是mac mini ，作为首次使用mac的萌新，一切都要先熟悉熟悉。之前一直使用ubuntu系统，都是linux，习惯习惯就好了。

# 电脑配置



## 快捷键更改

 首先是快捷键，command键在ctrl 与 alt 中间，着实不习惯。设置-》键盘 -》右下角的修饰键 ，然后两个键互相更换一下，ok。

## 终端修改

系统自带的bash也足够好，但是不太喜欢，因为无法分成多个窗口，所以推荐使用 iTerm

### 修改终端启动快捷键

习惯了linux的ctrl + alt + T 启动终端，这里也需要搞一下。详情参考https://blog.csdn.net/suwenlai/article/details/80065501

### 修改大小以及背景

ctrl + 空格，输入terminal ，快速打开终端，太小了，所以需要扩大一点点。

点击 屏幕右上角终端-》偏好设置 -》描述文件 -》窗口大小。

然后直接修改就可以了

### 修改内部字体颜色路径显示等

默认的终端文字颜色都是白色的，并且cd到目录深处，不会显示，这里是改变一下用户名的颜色以及进入的目录路径

在.bash_profile里面添加如下语句，改变用户名的颜色，用户名格式，用户名后路径颜色：

```
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;35;40m\]\u\[\033[00;00;40m\]@\[\033[01;35;40m\]\h\[\033[00;31;40m\] : \[\033[00;33;40m\]\w \[\033[01;32;40m\]\$ \[\033[01;37;40m\]'
```

在 .bash_profile 里面输入一下颜色，改变文件以及文件夹颜色，这里将文件夹改为绿色，是因为经常cd 操作，需要知道哪个是文件夹：

```
export CLICOLOR=1
export LSCOLORS=cxgxgxgxgxgxgxgxgxcxcx
```

###  自定义命令

linux中有些命令mac没有，所以需要自定义一下，在 .bash_profile文件中添加一下即可：
```
alias ll='ls -la'
alias la='ls -a'
```



# 常用软件与配置



## Markdown文本工具之Typora

直接下载就可以，不过下载过程巨慢，慢慢等待着。



## 文本神器Sublime

虽然mac的备忘录很好用，但是我还是喜欢使用sublime，没办法，win系统与ubuntu系统的后遗症。

同上，下载巨慢无比。建议直接拷贝dmg文件过来安装。无需配置，直接使用



## 吃饭的家伙Android studio

需要先下载jdk然后配置环境。在配置环境的时候，一般是配置到 .bash_profile 文件中的，如果没有这个文件，可以直接创建该文件即可。

android studio 安装也简单，直接一路next 即可，完成后，随便创建一个项目，开始接下来的个性化配置。

### 字体配置

代码字体大小：android studio -> preferences ->  Editor -> Font

菜单以及侧边栏目字体大小：android studio -> preferences ->  Appearance & Behaviro -> Appearance ，把Use custom font 打上勾，然后 size 调整一下即可，我调整为16

### 拼写设置

忽略大小写：android studio -> preferences -> Editor -> General -> Code completion  ，把 Match case 的钩去掉即可

快捷键设置：

android studio -> preferences ->  Appearance & Behaviro -> Keymap

### logcat 颜色配置

android studio -> preferences -> Editor -> Color Scheme -> Android Logcat

推荐颜色配置：

Assert级别 ：FF0000 大红色

Error级别：FF6B68 保持不变，粉红色

Warning 级别： BB8C0B黄色偏暗

Info 级别：0DBB54 暗绿色

Debug级别：8EB1BB 白色偏蓝

Verbose级别不配拥有，原来的白色就行

### 插件安装与推荐

android studio -> preferences -> plugins ，然后在搜索栏上搜索，安装即可。下面推荐几个好用的插件。

侧边栏预览：Code Glance

彩虹括号：Rainbow Brackets

彩色进度条：Nyan Progress Bar

马里奥进度条：Mario progress Bar 。这个进度条更好玩，不推荐上面的彩色进度条，推荐使用这个。

颜色资源命名：Name that color 。这个没用过，看上去挺不错的，可以试试

快捷键提示： key promoter X 。比较鸡肋。你使用鼠标的操作之后，会在右下角提示你可以是哪些快捷键组合完成这个操作。

### gradle 下载

同样巨慢无比，直接在网上下载好，我这里是6.5，下载好后直接放入到 ~/.gradle/wrapper/dists/gradle-6.5-all 目录，找到那一堆乱码的文件夹，然后放入进去即可

### Adb 工具设置

如果不设置，发现在terminal上使用adb命令是无效的，所以需要设置。在 .bash_profile 文件中添加：
```
#android adb 配置
export ANDROID_HOME=~/Library/Android/sdk
export PATH=${PATH}:${ANDROID_HOME}/tools
export PATH=${PATH}:${ANDROID_HOME}/platform-tools
```











