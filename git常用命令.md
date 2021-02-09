# [Git 创建仓库](https://www.runoob.com/git/git-create-repository.html)

## git init

```
git init
```

该命令执行完后会在当前目录生成一个 .git 目录。

```
git init newrepo
```

在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：

```
$ git add *.c
$ git add README
$ git commit -m '初始化项目版本'
```

以上命令将目录下以 .c 结尾及 README 文件提交到仓库中。

```bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/hjykey/vuecli-demo.git
git push -u origin main
```

以上命令为在本地新建一个仓库后，将readme.md文件加入仓库后提交，然后重命名分支名称为main，添加远程仓库，push。

## git clone

我们使用 **git clone** 从现有 Git 仓库中拷贝项目（类似 **svn checkout**）。

克隆仓库的命令格式为：

```
git clone <repo>
```

如果我们需要克隆到指定的目录，可以使用以下命令格式：

```
git clone <repo> <directory>
```

**参数说明：**

- **repo:**Git 仓库。
- **directory:**本地目录。

比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：

```
$ git clone git://github.com/schacon/grit.git
```

执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。

如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：



```
$ git clone git://github.com/schacon/grit.git mygrit
```

## 配置

git 的设置使用 **git config** 命令。

显示当前的 git 配置信息：

```
$ git config --list
credential.helper=osxkeychain
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
```

编辑 git 配置文件:

```
$ git config -e    # 针对当前仓库 
```

或者：

```
$ git config -e --global   # 针对系统上所有仓库
```

设置提交代码时的用户信息：

```
$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
```

如果去掉 **--global** 参数只对当前仓库有效。

# [git设置忽略文件.gitignore](https://www.cnblogs.com/linsx/p/9335757.html)

在仓库目录下新建一个名为.gitignore的文件（因为是点开头，没有文件名，没办法直接在windows目录下直接创建，必须通过右键Git Bash，按照linux的方式来新建.gitignore文件）。如下图所示。

.gitignore文件对其所在的目录及所在目录的全部子目录均有效。通过将.gitignore文件添加到仓库，其他开发者更新该文件到本地仓库，以共享同一套忽略规则。

以下涉及的ignore文件均为如下格式：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
# 以'#'开始的行，被视为注释.                                                                                                                          

# 忽略掉所有文件名是 foo.txt的文件.

foo.txt

# 忽略所有生成的 html文件,

*.html

# foo.html是手工维护的，所以例外.

!foo.html

# 忽略所有.o和 .a文件.

*.[oa]
配置语法：
以斜杠“/”开头表示目录；
以星号“*”通配多个字符；
以问号“?”通配单个字符
以方括号“[]”包含单个字符的匹配列表；
以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

常用的规则：
1）/mtk/        过滤整个文件夹
2）*.zip         过滤所有.zip文件
3）/mtk/do.c     过滤某个具体文件

被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中：
1）!*.zip
2）!/mtk/one.txt

唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。
为什么要有两种规则呢？想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么我们就需要使用：
1）/mtk/
2）!/mtk/one.txt
假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！

最后需要强调的一点是，如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。
简单来说，出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。因此一定要养成在项目开始就创建.gitignore文件的习惯，否则一旦push，处理起来会非常麻烦。

***



# [**git设置保留空文件夹**.gitkeep](https://www.cnblogs.com/lxwphp/p/9045828.html)

在空文件下新建一个.gitkeep文件即可

```
# win & OSX system files
.DS_Store
Thumbs.db
ehthumbs.db
Desktop.ini
```

 

```
# IDE files
.idea
```

 

```
# project self files
/baidu_verify*
Public/Upload/*
!Public/Upload/.gitkeep
Application/Runtime/*
!Application/Runtime/.gitkeep
Backstage/Runtime/*
!Backstage/Runtime/.gitkeep
```

 

```
.phpstorm.meta.php
Application/Common/Conf/config.php
```

***

# [git 本地与远程仓库同步操作](https://www.jianshu.com/p/b37ff443de15)

### git fetch 做了些什么

git fetch 完成了仅有的但是很重要的两步:

- 从远程仓库**下载**本地仓库中缺失的**提交记录**
- **更新远程分支指针**（假设为 o/master）

`git fetch` 实际上将本地仓库中的远程分支更新成了远程仓库相应分支最新的状态：

![img](https://upload-images.jianshu.io/upload_images/5418798-859b2e45a7b4215c.png?imageMogr2/auto-orient/strip|imageView2/2/w/522/format/webp)

`git fetch` 通常通过互联网（使用 http:// 或 git:// 协议) 与远程仓库通信。

### git fetch 不会做的事

`git fetch` 并不会改变你本地仓库的状态。它**不会更新你的 master 分支**，也**不会修改你磁盘上的文件**。

理解这一点很重要，因为许多开发人员误以为执行了 git fetch 以后，他们本地仓库就与远程仓库同步了。它可能已经将进行这一操作所需的所有数据都下载了下来，但是并没有修改你本地的文件。

所以，你可以将 `git fetch` 的理解为单纯的下载操作。

### 合并远程分支

当远程分支中有新的提交时，你可以像合并本地分支那样来合并远程分支。也就是说就是你可以执行以下命令:

- `git cherry-pick o/master`
- `git rebase o/master`
- `git merge o/master`
- 等等

实际上，由于先抓取更新再合并到本地分支这个流程很常用，因此 Git 提供了一个专门的命令来完成这两个操作，它就是 `git pull`。

### git pull

`git pull` 就是 `git fetch` + `git merge o/master`。

当你想要 push 你的新提交时，发现远程仓库在你上次拉取以后已经又有了改变，也就是说你的新 commit 是基于旧提交的修改，这种情况下 Git 是不允许你进行 push 操作的，你需要使自己的工作基于远程的提交，这个过程可以用以下命令：

- `git fetch; git merge o/master`
- `git fetch; git rebase o/master`
- 最简单的当然还是 `git pull -r`（`git pull --rebase` 的缩写）

然后再 `git push` 就没问题了。

在开发社区里，有许多关于 merge 与 rebase 的讨论。以下是关于 rebase 的优缺点：

- 优点：rebase 使你的提交树变得很干净, 所有的提交都在一条线上
- 缺点：rebase 修改了提交树的历史。比如，提交 C1 可以被 rebase 到 C3 之后。这看起来 C1 中的工作是在 C3 之后进行的，但实际上是在 C3 之前。

一些开发人员喜欢保留提交历史，因此更偏爱 merge。而其他人可能更喜欢干净的提交树，于是偏爱 rebase。仁者见仁，智者见智。

### git push

`git push` 负责将你的变更上传到指定的远程仓库。远程仓库中的 master 分支被更新，我们的远程分支（o/master）也同样会被更新。

未指定参数时，Git 是通过当前检出分支的属性来确定远程仓库以及要 push 的目的地的。我们可以为 push 指定参数，语法是 `git push <remote> <place>`。这句话的含义是：切到本地仓库中的 <place> 分支，获取所有的提交，再到远程仓库 <remote> 中找到 <place> 分支，将远程仓库中没有的提交记录都添加上去，搞定之后告诉我。

如果不指定参数，且 HEAD 没有跟踪任何分支，`git push` 不会有任何响应：

![img](https://upload-images.jianshu.io/upload_images/5418798-571565b87c0730f0.png?imageMogr2/auto-orient/strip|imageView2/2/w/622/format/webp)

要同时为源和目的地指定 <place> 的话，只需要用冒号将二者连起来就可以了 `git push origin <src>:<dst>`。

> 注意如果 <src> 传了个空值过去，会**删除该远程分支**。

## 从远程库删除某些文件但保留本地的文件

有时我们会误把一些不必要的文件（如目标文件、log 日志等）提交并推送到了远程库，现在希望从远程库删除这些文件但保留本地的文件，可以像这样 执行：



```bash
git rm -r --cached dir1
git rm --cached dir2/*.pyc
git commit -m "remove irrelated files"
git push origin branch1
```

+++

# [git新建分支并将分支提交到远程仓库](https://blog.csdn.net/huzhenv5/article/details/104475178)

### 步骤

1. 新建并切换到新分支

```
git checkout -b dev
```

说明：该命令的作用是，基于当前分支新建一个名为“dev”的分支（分支名可以自定义），并切换到该分支

> 补充：该命令相当于同时执行了`git branch dev`和`git checkout dev`，前者是创建新分支，但并不切换过去；后者是切换到指定分支，并将本地代码也切换成指定分支的代码

1. 代码提交

```
git add *

git commit -m "first commit dev"
123
```

说明：这些命令会将你所做的更改提交到当前分支上，也就是“dev”分支上

1. push到远程仓库

```
git push --set-upstream origin dev
```

说明：`orgin`是远程仓库名，可以通过`git remote -v`查看，如果是git2.5以上版本，会看到两个同名的远程仓库，一个是fetch一个是push
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200224170541598.png)
这是因为git 2.5版本后，把远程仓库的fetch和push配置区分开来，主要是为了简化三角工作流，这样就可以方便的从一个仓库拉取代码，修改后，再推送到另一个仓库中。不过一般使用中，fetch和push配置都是一致的。
如果你使用不到配置不同的fetch和push，则在使用git remote的时候不加`-v`参数

`dev`就是刚刚创建的分支名称

> 补充：`--set-upstream`这个参数的作用是将当前默认提交的远程仓库名和分支名绑定到后面的`orgin`和`dev`上，这样我们以后继续push代码时，只需要执行`git push`就可以了，不用再指定远程仓库名和分支名

做完这些，我们就能再git上的仓库管理页面，看到我们刚刚push的分支啦

### 删除本地分支

```
git branch -d 分支名
```

### 删除远程分支

```
git push origin --delete 分支名
```

### 重命名分支

```bash
git branch -M main
```

-m/M的区别在于：-M: 是 --move --force的缩写，而-m只是--move

--move(-m): Move/rename a branch.

--force(-f): 即使新命名的branch名存在也执行。

### git升级

git update-git-for-windows

将github仓库的访问方式从https切换成ssh：(https://jerry.blog.csdn.net/mailto:git@github.com)

``` 
1.git remote -v 查看当前的方式

2. git remote set-url origin git@github.com:i042416/KnowlegeRepository.git
```

测试ssh的是否成功 ssh -T git@github.com

