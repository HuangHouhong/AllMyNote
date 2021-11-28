# Ubuntu Flutter开发环境配置

## android studio配置

直接打开，然后下载flutter插件即可

下载Flutter插件android studio 会提示同时下载dart插件，一起下载了。



## Flutter SDK安装

首先下载 https://flutter.dev/docs/development/tools/sdk/releases?tab=linux

下载完成后，解压缩到任意目录，这里解压到了 ~/sofeware/flutter 目录下面。

然后在配置文件（.bashrc）中填写如下内容:

```shell
# 配置flutter
# flutter 国内镜像
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
# flutter安装路径
export PATH=~/software/flutter/bin:$PATH
```

执行 source  .bashrc 让配置文件生效

执行 flutter --version ，查看flutter版本，这个过程可能有点长，3分钟左右，等着

执行 flutter doctor，查看环境配置是否完成。这里提示如下：

```shell
Running "flutter pub get" in flutter_tools...                       5.3s
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 2.2.2, on Linux, locale zh_CN.UTF-8)
[!] Android toolchain - develop for Android devices (Android SDK version 30.0.3)
    ✗ Android licenses not accepted.  To resolve this, run: flutter doctor
      --android-licenses
[✓] Chrome - develop for the web
[✓] Android Studio (version 4.1)
[✓] IntelliJ IDEA Community Edition (version 2020.3)
[✓] Connected device (1 available)
```

按照上面的执行 flutter doctor --android-licenses ，然后一路选择y，执行完成后在运行 flutter doctor 诊断一下，完美。

## 第一个项目运行

直接 new flutter project 就可以创建一个demo项目。但是进入后，点开android 项目发现很多关于 Flutter 的都会报红，但是能够点击安装，不影响使用。

比如 MainActivity 继承自 FlutterActivity， FlutterActivity就会报红色。可以右击andorid 文件夹 -> Flutter -> open android  module in Android Studio ,然后等待完成就可以，打开这个单独的 android 项目，就不会再有红色了。

小提示，在打开前可以把 android 项目下的 gradle-wrapper.properties 文件修改一下，尤其是gralde 版本号，尽量选择本地有缓存的，这样加载可以快点，不用每次都从网络上拉。

