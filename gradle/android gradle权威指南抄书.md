# 注意点

<< 该符号已经被4.0以后已经被弃用了，所以不需要使用了。

可以使用idea创建一个groovy项目，然后在该项目中的 groovy文件夹下创建一个gradle文件，在该文件中编辑有代码提示。编辑好负责到另一个文件中保存，然后在使用命令行执行命令比较舒服。

# Gradle 基础知识

## 安装

安装前需要确保安装java 环境

直接下载 gralew 文件，然后解压缩。我这里放在了 ～/gradle/gradle-6.5 目录下。然后配置环境，可以在系统配置文件下，也可以在用户配置文件下，反正任意。

这里放在了 /etc/profile 文件下配置：

```
#配置gradle环境
export GRADLE_HOME=~/gradle/gradle-6.5
export PATH=$GRADLE_HOME/bin:$PATH
```

配置完成后，需要执行一下 source /etc/profile 命令，让刚刚的配置生效，或者直接重启也行。

然后终端输入 gradle -v 查看版本号，如果出现版本号，就说明安装成功了

## 写个hello world

创建一个文件 build.gradle ,这个名称不可更改，因为gradle默认的执行文件名称就是这个。在该文件中写入下面内容：

```groovy
task hello{
	doLast{
		println "hello world"
	}
}
```

该文件可以放到任意位置。我当前放到了 ～/gradle/workspace/chapter1 文件夹下。然后终端切到该文件夹下，执行 gradle -q hello 。 然后就可以看到终端中输出内容了。

## Gradle wrapper

打开终端，切入到项目地址下面，通过 gradle wrapper 即可初始化 wrapper，实际上就是因为内置了一个名称为 wrapper 的 task 。

执行完成后就可以看到项目地下有个 gradle 文件夹和 gradlew 、gradlew.bat 文件。

gradlew 文件就是linux 下的脚本，gradlew.bat 就是 window 下的脚本。

打开gradle 文件夹，里面有个 wrapper 文件夹，打开后，gradle-wrapper.properties 文件就是对应的配置文件。主要修改一下 distributionUrl 对应的地址，这里修改为本地的 gradle 文件，这样就不需要去慢慢下载文件了：

```groovy
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
# 修改这里为本地的目录下面
distributionUrl=file\:///home/hhh/gradle/gradle-6.5-all.zip
# 下面是mac os 下目录
# distributionUrl=file\:///Users/hhh/gradle/gradle-6.5-all.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

distributionUrl对动态url的支持是不友好的，比如无法识别上层目录符号../  ，如果想使用相对目录，必须把zip文件放到 gradle-wrapper.properties 这个文件所在目录或者子目录下，可以直接这么写 distributionUrl=gradle-6.5-all.zip

当然，关于 wrapper 这个 task ，可以去修改他更新里面的值，如下所示：

```groovy
wrapper{
    distributionUrl='file:///Users/hhh/gradle/gradle-6.5-all.zip'
}
```

上面是把distributionUrl值给修改为mac下本地的包路径了。其他的参数也可以同样使用这种方式修改。但是要特别注意特殊字符 \ ，有的时候需要加，有的时候不需要加。比如上面路径file后面就不需要加，生成的 gradle-wrapper.properties 里面回自动给你加上，你要是为了有单斜杠而在file字段后面加了双斜杠，生成的文件就会变成三斜杠，显然是错误的。

另外，如果是在idea中， 建议将gradle-wrapper.properties文件的distributionUrl改为 xxx-all.zip ，默认情况下是 xxx-bin.zip，不带源码的，在查看源码的时候很不方便。

完成后，linux 上就可以通过 ./gradlew 命令代替 grade了。比如上面的 hello 这个task ，可以使用 ./gradlew hello  执行任务。

## Gradle 日志

日志分为三种：普通日志，堆栈日志，自己输出日志。

### 普通日志

gradle 日志分为6个等级，从左到右一次降低：error，quiet，warning，lifecycle，info，debug。默认输出 lifecycle 及其以上级别的日志。

可以在 ./gradlew 命令后面加参数输出日志，例如执行 hello 这个task时输出 debug 级别以上的日志：./gradlew -d hello

### 堆栈日志

一般构建失败的时候，需要输出堆栈信息。默认情况下并不会输出堆栈信息。

在命令后面加上 -s 或者 --stacktrack 参数，输出关键性堆栈信息，比较精简，推荐使用。

在命令后面加上 -S 或者 --full-stacktrack 参数，输出全部堆栈信息。

### 自己加日志

直接使用 printn 打印日志或者使用内置的 logger 打印日志。logger 日志六个级别，同普通日志信息级别。

## Gradle 常用命令

帮助任务：./gradlew help

查看可执行的任务：./gradlew tasks 。通常我们可以在后面加上 -all ，就可以在下面的Other tasks 看到我们自定义的task了

help任务：./gradlew help --task  任务名称

多用用 --help 命令，可以看到后面更哪些参数。其他还有一些比较常用的如：

- --refresh-dependencies 强制刷新依赖
- -x 排除指定的任务。即执行一系列任务时，排除这个

# Gradle 基本使用







