### 一、起源：

代码需要记录，有些命令长期不用也会忘记，干脆弄一份有亲切感的git笔记；

### 二、Git介绍

- 是目前世界上最先进的分布式版本控制系统
- Git 的工作就是创建和保存你项目的快照及与之后的快照进行对比。

### 三、Git起源

- 1991年Linus创建了开源的Linux，Linux的壮大靠全世界志愿者参与；2002年以前，志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码；

- 2002年，代码库之大让Linus很难继续通过手工方式管理了,社区的弟兄们也对这种方式表达了强烈不满，Linus选择了一个商业的版本控制系统BitMover公司的BitKeeper，授权Linux社区免费使用这个版本控制系统；

- 2005年，开发Samba的Andrew试图破解BitKeeper的协议，被BitMover公司发现，于是要收回Linux社区的免费使用权。Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了；
- Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

### 四、Git使用

##### 4.1 git安装

[Linux和Windows安装Git教程参考](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)

**在Mac OS X上安装Git**

第1种：一是安装homebrew，通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。

第2种：直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

![Xcode](/Users/zyc/Desktop/LearnGit/image/Xcode.png)

Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的,！

##### 4.2 git工作流程

![git工作流程](/Users/zyc/Desktop/LearnGit/image/git工作流程.png)

- 克隆 Git 资源作为工作目录。
- 在克隆的资源上添加或修改文件。
- 如果其他人修改了，你可以更新资源。
- 在提交前查看修改。
- 提交修改。
- 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

#####  4.3 Git 工作区、暂存区和版本库基本概念

- **工作区：**就是你在电脑里能看到的目录。
- **暂存区：**英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **版本库：**工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系：

![工作区版本库暂存区关系](/Users/zyc/Desktop/LearnGit/image/工作区版本库暂存区关系.png)

图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存区（stage, index），标记为 "master" 的是 master 分支所代表的目录树。

图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。

图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。

当对工作区修改（或新增）的文件执行 "git add" 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。

当执行 "git reset HEAD" 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

当执行 "git rm --cached <file>" 命令时，会直接从暂存区删除文件，工作区则不做出改变。

当执行 "git checkout ." 或者 "git checkout -- <file>" 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。

当执行 "git checkout HEAD ." 或者 "git checkout HEAD <file>" 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

##### 4.4 创建版本库

![创建版本库](/Users/zyc/Desktop/LearnGit/image/创建版本库.png)

**内容：**

初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

1. 使用命令`git add `，把文件修改添加到暂存区，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m `，把暂存区的所有内容提交到当前分支，完成。

**演示：**

1.建空目录，变成git可以管理的版本库；

```python
#建目录
$ mkdir LearnGit
#当前目录路径
$ pwd					
#把这个目录变成Git可以管理的仓库：
$ git init
#当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，
$ ls -ah
```

2.把`Git系统整理ZYC总概.md`文件放到Git仓库：

```python
$ git add Git系统整理ZYC总概.md
#没有任何显示说明添加成功。

$ git commit -m "Wrote 4.4 创建版本库"
[master（根提交） 677c17b] Wrote 4.4 创建版本库
 1 file changed, 140 insertions(+)
 create mode 100644 "note/Git\347\263\273\347\273\237\346\225\264\347\220\206ZYC\346\200\273\346\246\202.md"
```

**注意：**

多个文件时，可以分别add，`commit`可以一次提交很多文件最后用commit：

```python
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

##### 4.5 版本切换

![版本切换](/Users/zyc/Desktop/LearnGit/image/版本切换.png)

**内容：**

`git reset --hard commit_id`

`HEAD`指向的版本就是当前版本；

`git log`可以查看提交历史，查看回退到哪个版本。

重返未来，用`git reflog`查看命令历史，确定要回到未来的哪个版本。

**演示：**

```python
#查看提交历史记录,显示从最近到最远的提交日志
$ git log
commit 12cf6587a3ba9ede0249149097b6ce8d6a33c8fe (HEAD -> master)
...
    Wrote 4.5

commit 677c17b707e8bbbcfd6767a4d769d1349c7b973f
...
    Wrote 4.4 创建版本库
    
$ git log --pretty=oneline
12cf6587a3ba9ede0249149097b6ce8d6a33c8fe (HEAD -> master) Wrote 4.5
677c17b707e8bbbcfd6767a4d769d1349c7b973f Wrote 4.4 创建版本库

#切换某一个版本，只要找到commit id即可；id不用写全，写前几个即可；
$ git reset --hard 12cf6587a3
HEAD 现在位于 12cf658 Wrote 4.5

#不确定版本的commit id,`git reflog`记录每一次命令，可找到id；
$ git reflog
4310d64 (HEAD -> master) HEAD@{0}: commit: Wrote 4.5不确定commit id
12cf658 HEAD@{1}: reset: moving to 12cf6587a3
12cf658 HEAD@{2}: reset: moving to 12cf6587a3
677c17b HEAD@{3}: reset: moving to 677c17
12cf658 HEAD@{4}: commit: Wrote 4.5
677c17b HEAD@{5}: commit (initial): Wrote 4.4 创建版本库
```

**注意：**

```python
677c17b707...的是commit id（版本号）
```

##### 4.6 当前状态

```python
$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
	修改：     "Git\347\263\273\347\273\237\346\225\264\347\220\206ZYC\346\200\273\346\246\202.md"

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
	../.DS_Store

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```



##### 4.7 修改管理

**增加修改：**

Git管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

`git diff HEAD -- readme.txt`：查看工作区和版本库里面最新版本的区别；

**撤销修改**

场景1.

![丢弃工作区修改](/Users/zyc/Desktop/LearnGit/image/丢弃工作区修改.png)

当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

```
$ git checkout -- readme.txt
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

场景2.当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD `，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。

##### 4.8 文件删除

1.文件确实不要了，删掉；

在自己工作区`rm 文件名`把文件删掉，用`git status`查看哪些删了，此时版本库里还存在这个文件，`git rm 文件名`,`git commit -m "remove 文件名"`,闲杂文件就从版本库中删除了；

2.文件误删：

在自己工作区`rm 文件名`把文件删掉，此时版本库里还存在这个文件，`git checkout --文件名`把误删的文件恢复到最新版本：

**注意**

命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

### 五、Git远程仓库-高效利用GitHub

Github.com网站就是提供Git仓库托管服务的，注册一个GitHub账号(注册网址)，就可以免费获得Git远程仓库。

##### 5.1 SSH加密设置 

本地Git仓库和GitHub仓库之间的传输是通过SSH加密的；

创建SSH Key：

- ```python
  #主目录下没有.ssh目录，打开Shell（Windows下打开Git Bash），创建SSH Key：
  $ ssh-keygen -t rsa -C "youremail@example.com"
  #你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可；成功后可在主目录找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，
  ```

- ```python
  #主目录下进入.ssh目录，有id_rsa和id_rsa.pub两个文件；这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
  $ cat id_rsa.pub
  ```

在github网站个人中心，找到`SSH and GPG keys`,在`SSH keys`中点击`New SSH key`；在终端用把公钥内容拷贝，放这里;需要SSH Key,因为github需要识别是不是你推送的，而不是别人冒充的，Git支持SSH协议，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

**注意**

github上免费托管的Git仓库，任何人都可以看到，但只有你自己可改，敏感信息不要放进去；

##### 5.2 github创建远程库

- 进入[github官网](https://github.com/),如果么有账号，就注册一个；
- 进入首页，点击New，填写数据库名称、描述；

![进入页面new](/Users/zyc/Desktop/LearnGit/image/进入页面new.png)

- 我创建的是：LearnGit仓库；

  ![建库](/Users/zyc/Desktop/LearnGit/image/建库.png)



先有本地库，再有远程库，如果库是空的；

`LearnGit`仓库，可以找它的链接，克隆到本地，也可以把本地`LearnGit`文件的与`LearnGit`仓库关联；在本地的`LearnGit`仓库下运行命令：

```python
$ git remote add originl git@github.com:zhixinI/LearnGit.git
```

请千万注意，把上面的`zhixinI`替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是`originl`，Git默认的叫法`origin`,让人一下子能明白这是远程库；

把本地库的所有内容推送到远程库上：

```
$ git push -u originl master
```

本地库内容推送到远程，`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：从现在起，只要本地作了提交，就可以通过命令：

```
$ git push originl master
```

把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

##### 5.3github创建远程库

现有远程库，再有本地库：

在github网站创建远程库，LearnGit；

```python
#克隆一个本地库zhixinI用户名；LearnGit库名；
$ git clone (远程库链接)

#做修改；

#从本地工作去添加到暂存区、提交到当前分支
$ git add .#把当前都添加；
$ git commit -m 'Right'
#关联远程仓库origin；zhixinI是用户名
$ git remote add origin git@github.com:zhixinI/LearnGit.git
#获取远程库与本地同步（远程仓库不为空需要这一步）
git pull --rebase origin master
#推上去；
$ git push -u origin master
```

![image-20200317190631837](/Users/zyc/Desktop/LearnGit/image/image-20200317190631837.png)



### 知识参考连接：

- [git官方](https://git-scm.com/)

- https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000

- https://cn.udacity.com/course/github-collaboration--ud456

- https://www.runoob.com/git/git-basic-operations.html

- https://www.yangzhiping.com/tech/github.html



