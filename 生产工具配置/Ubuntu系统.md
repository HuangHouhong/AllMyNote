# 1 重要目录

在Ubuntu中，一般有三个安装目录:

-  /usr

  系统级别目录，可以理解为windows中 C:/Windows 目录。其中 /usr/lib 可以理解为 C:/Windows/System32，存放所有可执行文件的库文件。这个目录下通常都是系统发行时自带的程序。

- /usr/local

  用户的程序目录，可以理解为 C:/Program Files 。 用户自己编译的软件默认会安装到这个目录下

- /opt

  用户的程序目录，opt 就是optional 缩写，可选项。一般情况下，安装一些大型的第三方软件都放在这个地方。可以理解为windows中的 D盘中自定义的安装目录。如果不需要里面的东西，可以直接 rm -rf 删除掉

以上仅仅是程序的目录，源码存放目录有两个：

- /usr/src 

  系统级的源码目录

- /usr/local/src

   用户级的源码目录

其他重要目录：

- /usr/share 

  各种程序间的共享文件，如字体，图标，文档等

- /usr/local/share

   同上，只是这个针对的程序是 /usr/local目录下的
  /usr/share/applications ， ubuntu有的时候不会自动创建图标，所以得自己制作启动图标，启动图标都是放在这个目录下的

# 2 配置文件

“/bin”、“/sbin”、“/usr/bin”、“/usr/sbin”、“/usr/local/bin”等路径已经在系统环境变量中了，如果可执行文件在这几个标准位置，在终端命令行输入该软件可执行文件的文件名和参数(如果需要参数)，回车即可。

使用 export 或者 echo $PATH 查看定义的环境变量，配置环境变量的文件 /etc/profile 和 .bashrc 文件

ubuntu一般有五个配置文件：

- /etc/environment
  设置整个系统的环境变量。查看一下该文件，就可以看到那些路径已经在系统的环境变量中了。
- /etc/profile
  为所有的用户都添加环境信息。当用户第一次登录时，该文件被执行，并从/etc/profile.d目录下搜集 shell 的所有设置。如果该文件修改了，必须重新启动才会生效。
- /etc/bash或者/etc/bash.bashrc
  为每个运行 bash shell的用户执行次文件，配置bash 信息，不需要重启，直接重新打开一个bash就生效。
- ~/.profile
  只为当前用户添加环境信息。相当于/etc/profile的私人版本。
- ~/.bashrc
  只作用于当前用户。相当于/etc/bash或者/etc/bash.bashrc的私人版本。

登录时，配置文件读取的顺序依次是： /etc/environment /etc/profile ~/.profile
一般情况下，我们只会使用到两个配置文件，即　/etc/profile 和　~/.profile

对配置文件修改，最好直接重启一下。也可以通过source命令立即让修改生效。
示例：　 source /etc/profile　就可以让文件立即生效