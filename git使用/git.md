# 安装git

```
sudo add-apt-repository ppa:git-core/ppa

sudo apt-get update

sudo apt-get install git 
```

 安装完成后，通过 git --verison ，查看是否出现版本号，出现说明就ok了。

# 配置 Git

## 本地配置

git配置文件分为三种，系统级别，用户级别以及目录级别。

这里同意配置用户级别的。

在本地目录下创建一个 .gitconfig 文件，然后输入一下内容

```
[user]
        name = XXX
        email = XXX@qq.com
```

或者，直接在命令行里面输入一下命令，就不需要创建文件了：

```
git config --global user.name "xxx"

git config --global user.email "xxx@qq.com"
```

在配置的时候一定更要注意空格空格空格，不然就等着提示错误吧。

另外，个人喜欢使用 vim 编辑器，所以设置 git 使用vim 编辑器

```
git config --global core.editor vim
```

以上配置完成后后，使用 git config --global --list 查看一下自己的配置是否正确

## SSH 配置

输入以下命令

```
ssh-keygen -C "xxx@qq.com" -t rsa
```

然后到 .ssh 目录下查看，发现多了两个文件，即 id_rsa，id_rsa.pub

## Github配置

到github下，点击个人头像 -》setting -》SSH and GPG keys，把上面生成的 id_rsa.pub 用文本编辑器打开，复制内容到 github中即可。

# 本地仓库与远程仓库首次连接

在本地创建一个文件夹，在文件夹中初始化仓库：

```
git init
```

执行完成命令后，终端提示你已经初始化git仓库了。

然后需要本地创建一个分支。这里创建一个test文件，随便写点啥。然后执行下面两个命令：

```
git add .
git commit -s
```

使用 git branch -vv 命令可以看到当前本地分支的名称为master，为了学习，使用命令讲本地分支明明为 local_branch

```
git branch -m master local_branch
```

本地仓库创建完毕，并且分支创建好了，下面需要把本地仓库与远程仓库相关联。

在github 上创建一个仓库 ，这里名称为 GitTest，进入到仓库里面，然后点击右上角绿色的 Code 按钮，弹窗中选择 ssh，复制下面方框的的内容。我这里的内容 git@github.com:xxx/GitTest.git，然后终端执行：

```
git remote add origin git@github.com:xxx/GitTest.git
```

执行完成后，可以使用 git remote  -v 查看远程分支。

关联完成后，有两种操作。各自有各自的优缺点：

## 第一种方法：放弃本地分支内容

先拉一下远程仓库内容。

```
git pull origin main:local_branch --allow-unrelated-histories
```

注意，以前是远程分支都是master，但是github后来改成了默认分支是main，所以这里故意讲本地分支名称改一下，方便能够看清。

以上命名很有可能会提示没有共同提交，然后 pull 失败。所以，可以直接强制拉取一下：

```
git pull -f  origin main:local_branch 
```

完成后，就可以了。但是先pull 有个缺点，就是你本地仓库里面的东西都没了。

## 第二种方法：放弃远程仓库内容

如果你还想要的本地仓库内容，就先push再pull，但是push的时候会告诉你 fetch first 错误，直接强制推送：

```
git push -u origin local_branch:main -f
```

推送完成后，就发现远程仓库被强制更新了。

# git 的一些命令

- 推送当前分支到远程分支

  当前分支名称为work1，远程分支为main，远程仓库为origin，推送命令如下:

  git push origin work1:main

  或者

  git push origin HEAD:main

- 设置本地已存在的分支追踪远程分支

  当前分支名称为 work2 ，远程分支main，远程仓库为origin。先切换到本地分支下，然后：

  git branch --set-upstream-to=origin/main

- other





