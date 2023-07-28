# Git

## 基本概念

1. 啥是Git？

   >Git是一个免费开源的**分布式版本控制工具**，几乎所有的操作都是在本地进行，需要网络的操作仅仅是同步。
   >
   >基本的设计思想和原理就是在本地复制一个代码库，每次操作都是提交到自己的代码库中。
   >
   >- 分布式：
   >
   >  Git主要是在本地进行版本控制管理，每个人在本地都可以建立一个自己的仓库，进行文件更改等等操作，需要多人云端协作时再推到云端。为什么要这么做呢？我们可以先来看看集中式的版本控制是怎么样的。
   >
   >  ![集中式版本控制.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E9%9B%86%E4%B8%AD%E5%BC%8F%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6.jpg)
   >
   >  版本控制交由中心服务器，本地文件更改后提交到服务器。但是如果中心服务器寄了以后，就容易受到损失，并且带来其他很多不利后果。
   >
   >  那如果是分布式呢？
   >
   >  ![分布式版本控制.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E5%88%86%E5%B8%83%E5%BC%8F%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6.jpg)
   >
   >  每个本地的仓库都是独立的，可以拥有自己的版本变动体系，同时也可以使用一个中心服务器来实现云端多人协同开发。这样就可以避免了许多集中式版本控制的方案带来的问题。
   >
   >- 版本控制：当我们需要长期开发或者对一个文件进行多次变动的时候，就会涉及到版本控制，我们每次的更改都会让文件产生出不同的版本，我们需要利用Git对这些不同的版本进行管理和控制。

2. Git有什么作用？

   > 1. 对文件进行版本控制，方便进行版本的迭代、回滚，以及分支的合并等操作。
   >
   >    想象一下，假如我们没有对版本进行控制的工具，会是一个怎样的情景？
   >
   >    ![1689823422327.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689823422327.png)
   >
   >    看起来很乱很繁杂对不对？
   >
   >    这样不仅看起来很乱，而且在进行版本管理操作的时候很不方便，也很容易出现问题。
   >
   >    使用Git后，我们可以在不同的版本之间切换，修改等等，就不会因为版本变动导致同一目录有多个文件，让我们眼花缭乱分不清楚。
   >
   > 2. 方便进行多人的协同工作。
   >
   >    当我们需要多人协同开发时，Git可以让我们更加方便的把自己开发的版本与别人开发的版本进行合并，或是基于其他人的版本继续开发新的内容。（在出事故的时候还可以精准地找人背锅）
   >    
   >    ![1690373705592.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690373705592.png)

3. GitHub、GitLab、Gitee和Git的关系？

   > 前者其实就是后者的一个托管平台，当我们本地做好Git仓库以后，就可以上传到平台进行托管，同时也可以让其他用户对平台上的代码进行进一步开发，利用平台进行多人协作开发。



## 基本操作

### 创建仓库

- 本地新建仓库

  在终端执行 `git init` ，在当前文件夹下创建一个git仓库

- 从远程仓库拉到本地

  在终端执行 `git clone <仓库地址>` ，将远程仓库拉到当前文件夹下

  clone 命令会自动将远程仓库命名为 origin，拉取它的所有数据，创建一个指向它的 master 分支的指针，并且在本地将其命名为 origin/master。同时Git 也会给你一个与 origin 的master 分支在指向同一个地方的本地 master 分支。

  例如从GitHub上拉取掌上重邮的仓库到本地：
  
  ```shell
  git clone git@github.com:RedrockMobile/CyxbsMobile_Android.git
  ```

在执行上述操作后，我们可以在项目文件夹中看到一个名称为 `.git` 的隐藏文件夹，Windows需要在显示中勾选 `隐藏的项目` 才能看到

![1689841720944.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689841720944.png)

然后我们就可以看到以下文件夹，这个文件夹中的内容就是用于帮助我们进行版本管理的。

![1689841830043.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689841830043.png)

这样我们就得到了一个Git仓库，接下来看看一些基础的命令使用。

### 基础命令

#### .gitignore文件

`.gitignore` 文件：里面声明了让Git忽略的某些文件和目录，例如：

![1689843342812.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689843342812.png)

就是把当前目录下的 `build` 目录让Git忽略，当提交版本的时候也不会将 `build` 目录下的文件提交上去。

#### add

```shell
git add [文件名]  # 将文件添加到暂存区
git add .  # 将所有“没被忽略”的文件的修改添加到暂存区(有些文件被.gitignore过滤,一般来说会过滤掉build文件来减小GitHub上仓库的体积)
git add *  #添加所有的文件，包括(被.gitignore忽略的)
```

1、当一个文件被add了，他的修改自始至终都会被Git追踪（tracked），包括被删除

2、当一个文件没有被add，git中的各种操作将对他毫无影响（untracked）

3、当我们准备提交一部分文件作为新的commit时，一般会在commit前进行add操作，这里的add只是标注“哪些文件的**修改**需要添加到这次commit中”。而不是“将哪些**文件**添加到这次commit”。

#### rm

相比大家都听过 `rm -rf /*` 吧

![1690453445877.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690453445877.png)

Git 中也有 `rm` 操作，具体作用如下：

```shell
# 会删除暂存区或者分支上的文件，工作区的文件也会被删除（相当于rm后再git add）
git rm [文件名] 
# 是从git取消对本文件的追踪（不会删除工作区文件）。当你不想对本文件进行版本控制了，但想保留文件在目录中，就用本命令。
git rm --cached [文件名]
```

#### commit

```shell
# 直接提交信息
git commit -m "[提交描述]"
# 会弹出一个vim编辑器，按i进入insert插入模式，输入一些commit信息后退出。
# 这个git commit命令实际上和gitcommit -m 命令是等效的。
git commit
# 相当于执行git commit -m前先执行git add .
git commit -a -m "[提交描述]"
```

commit信息输入完成后按Esc，按“:”键输入命令“wq”按回车会自动保存,后退出，如果输入“q”表示不保存

如果已经commit了，发现commit描述里面缺少了部分信息，想要补加上，怎么办？可以使用以下命令：

```shell
git commit --amend
```

来对commit的描述进行补充和修改

#### stash

假如有这么一种情况，我们正在写一个功能，写到一半突然被老板告知需要修复另外一个bug，这时我们就需要另外切一个分支去修复这个bug

![1690373606291.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690373606291.png)

但是对于当前分支写了一半的新功能，我们有以下三种选择：

1. 直接丢弃已有的更改，checkout到目标分支进行后续操作。

   这样会让我们之前写的东西功亏一篑，在上一次commit之后的更改都将会丢失，损失惨重。

2. 对于已有的更改进行一次commit用于保存变动。

   但是并不推荐对未完成的内容进行一次commit，尽量在完整地完成一个板块后再进行commit。

3. 使用stash操作进行更改内容的暂存，完成其他分支的工作后再恢复暂存的内容继续开发。

   这样就可以让我们保存写了一半的内容，并且安心地去完成其他分支的工作了。

```shell
# 等同于git stash save/git stash push，能够将所有未提交的修改（工作区和暂存区）快照至堆栈中，用于后续恢复当前工作目录。
git stash
# 查看当前stash中的内容
git stash list
# 将当前stash中的内容种最近一次stash弹出，并应用到当前分支对应的工作目录上。相当于回退，但是该次stash的内容会消失
git stash pop

# 以下内容涉及到stash名字的地方需要注意：
# 如果你使用Windows系统并且是在PowerShell中使用以下命令，大括号会被识别为代码块，如果想正常使用，请在大括号前加反引号 `
# 使用反引号对大括号进行转义，例如： git stash apply stash@`{1`}

# 将堆栈中的内容应用到当前目录 如：git stash apply stash@{1}
git stash apply [stash名字]
# 从stash的堆栈中删去指定的一次stash
git stash drop [stash名字]
# 清空stash列表 
git stash clear
# 查看堆栈中最新保存的stash和当前目录的差异
git stash show
```

#### 状态变更

上述的几个命令会改变文件在Git仓库中的状态，状态变更以及对应的操作如下图所示：

![状态变更.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E7%8A%B6%E6%80%81%E5%8F%98%E6%9B%B4.jpg)

#### status

当文件状态改变后，应该如何查看文件目前处于一个什么状态呢？未跟踪，或是暂存？这时候就可以使用 `status` 命令查看各文件当前的状态

```shell
# 查看当前文件夹下文件的状态（例如:未追踪或未加入暂存区等状态）
git status
```

#### log

在提交之后会生成对应的提交记录，每次提交都会有一个哈希值，通过这些提交记录我们可以通过一些操作查看每次提交相关的信息。要查看提交记录可以使用 `git log` 相关的指令

```shell
# 查看log
git log
# 使用图形化的方式查看log
git log --graph
# 会显示每次提交的差异细节
git log -p
# 显示每次提交的统计信息（行数变化，修改过哪些文件）
git log --stat
# 查看引用的历史,默认为HEAD
git reflog
```

#### diff

如何显示不同提交之间的差异呢？可以使用 `diff` 操作查看两次commit之间文件的变动等信息。

```shell
# 显示工作区和暂存区文件的差异，如果没有add过（暂存区没有它），则对比的是最近一次版本和工作区的差异。
git diff [文件名]
# 对比工作区的文件和分支的文件的差别
git diff [分支名] [文件名]
# 对比暂存区和git仓库的区别（就是暂存区和最近一次commit的差异）
git diff --cached [文件名]
# 对比工作区和git仓库中某次提交的区别
git diff [哈希码] [文件名]
# 对比暂存区和git仓库中某次提交的区别
git diff --cached [哈希码] [文件名]
# 对比任意两次提交（可以来自不同分支，因为每次提交都有唯一的哈希码）
git diff [哈希码] [哈希码]
```

#### branch

分支相关的操作

```shell
# 新建一个分支
git branch [名称]
# 新建一个本地分支，并让其追踪一个远程分支
git branch [本地分支名称] [远程分支名称]
# 列出远程分支
git branch -r
# 列出本地分支，并且在当前分支前面加*号
git branch
# 删除在本地分支
git branch -d [名称]
# 删除远程分支
git branch -d -r [名称]
# 分支重命名
git branch -m [旧名称] [新名称]
# 查看本地仓库和远程仓库的对应关系
git branch -vv
```

#### checkout

checkout会将HEAD指针指向分支或者指向某一个commit

```shell
# 切换到某一分支
git checkout [分支名称]     # 切换分支
git checkout -b [分支名称]  # 新建一个分支并切换到该分支上
git checkout -b [本地分支名称] [远程分支名称] 	# 同branch操作，新建一个本地分支，让其追踪一个远程分支，并切换过去
git checkout -q [分支名称]  # 无提示切换分支
git checkout -f [分支名称]  # 强制切换（如果工作区有修改，则丢弃本次修改，强制切换到分支）

# 切换到某一次commit
git checkout [哈希值]		 # 切换到哈希值对应的commit上，commit对应的哈希值可通过log相关操作查看
```

#### reset

![img](https://ts1.cn.mm.bing.net/th/id/R-C.56f8b5e148fa570afaa8ffab058d6a0a?rik=OT2d8GQ%2bL1aOlg&riu=http%3a%2f%2fwww.linuxeden.com%2fwp-content%2fuploads%2f2021%2f11%2frefactor.jpg&ehk=Rjg1wzF0N%2fyddpNoP9yiBX8c3gD4mRx9TgFGt7x8Kaw%3d&risl=&pid=ImgRaw&r=0) 

当我们尝试对代码进行改动时，总会出现明明没改什么东西但是代码却无法运行的情况。如果在这之前有commit记录，那么可以使用 **reset** 操作回到上一次commit的样子，让程序恢复正常。

**reset** 是一个比较常用的操作，可以带着分支一起往某个commit移动，或者将当前分支移动到某个分支所指向的commit

```shell
git reset [目标commit的哈希值] [reset的模式，默认为 --soft ]
```

reset的模式有两个

| 模式   | 含义                                                         |
| ------ | ------------------------------------------------------------ |
| --soft | 只移动到对应的commit，文件的变动仍然存在，但是在Git中的状态会对应改变 |
| --hard | 移动到对应的commit，文件的变动也会丢失，文件会完全还原至目标commit的样子 |

#### rebase

使用rebase可以简化美化分支，也是合并操作，但是他会将分支复制一份，然后只显示从1-5‘这一条线路（如下图所示）

![image-20220307182521763](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20220307182521763.png)

使用 `rebase -i`可以使用交互式的提交修改，可以使用其他指令来修改这个rebase过程

进入交互式的界面后可以看到如下的命令提示：

```shell
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
```

#### merge

将目标分支合并进当前分支

```shell
git merge [可选参数] [分支名]
# 参数 --commit（默认）自动生成一个提交，包含两个节点合并的结果。
# 参数 --no-commit 为了防止合并失败，先不提交，让用户手动提交
```

如果有冲突则要先处理冲突，Git会列出冲突的文件，我们需要打开这些文件一个一个地合并（Git自动合并了全部，我们只用删掉不需要的部分即可），然后重新commit就行了（这时不用再merge了）

merge的分类

| 类别         | 含义                                                 |
| ------------ | ---------------------------------------------------- |
| fast forward | 分支合并无冲突，直接砍掉分支信息，认为是主分支的推进 |
| no-ff        | 单独创建一个commit来完成合并                         |
| squash       | 可以对分支上的多次提交压缩为一条提交信息             |

#### cherry-pick

如果某个分支不需要了，但是其中的3个commit的变动需要迁移到当前分支，可以使用 `cherry-pick` 操作，获取另一个分支中的commit信息

```shell
git cherry-pick hashcode1 hashcode2 hashcode3
```

#### Git分支概念

前面介绍完了一些有关Git分支的操作，相信大家对分支有了一些自己的理解，那么Git分支到底是一个什么样的存在呢？在我们对其进行切换，新建，合并等等操作的时候，分支到底具体发生了哪些变化？

在Git中，分支指的是从主线上分离出来进行另外的操作，既不影响主线，主线又可以继续干它的事，它可用来解决临时需求；当分支做完事后可合并到主线上，而分支的任务完成可以删掉了。

每一个分支相当于一个隔离的环境进行开发，可以用于：

- 开发新功能
- 修复bug

在Git中有一个特殊的引用HEAD，它只会指向当前最新的commit。

Git的分支功能特别的强大，它不需要将所有数据进行复制，只要重新创建一个分支的指针指向你需要从哪里开始创建分支的提交对象(commit)，然后进行修改再提交，那么新分支的指针就会指向你最新提交的这个commit对象，而原来分支的指针则指向你原来开发的位置，当你在哪个分支开发，HEAD就指向那个分支的最新提交对象(commit)。

当我们使用  `git branch` 指令查看分支时，前面有个*号的就为我们目前所处的分支，而这个分支的指针就指向最新的commit对象，也就和HEAD指向同一对象。也可以通过 `checkout`  操作来切换到目的分支，我们默认的主分支为 `master` 。分支的创建和切换操作，其实只是简单的创建指针找指针而已，而根据找到的指针找到所指向的commit对象，然后将工作空间恢复成该commit对象所指的文件快照让我们来进行后续的工作。当提交一次，指针就重新指向这个最新提交的对象。

例如我们在新建分支前：

![image-20230311092252353](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311092252353.png)

此时只有一个master分支，同时**HEAD**指向**最新的commit**也就是c3

此时我们如果通过 `git branch dev` 新建一个dev分支的话，dev也指向c3

![image-20230311092651390](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311092651390.png)

由于此时c3仍然是最新的commit，因此HEAD不改变

当我们在dev分支上开发并提交了两个版本c4 , c5后，由于HEAD要指向最新的commit，因此会指向c5

![image-20230311093152250](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311093152250.png)



假如这时候dev开发完成，要和master分支合并，由于master没有另外迁出版本，与dev不冲突，那么就会直接将master指针指向最新版本c5，也就是Fast-forward合并，此时如果dev分支任务完成了，删除dev分支即可

![image-20230311093717592](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311093717592.png)



如果在dev开发两个版本后，在master版本也更新了c6 , c7的话，首先HEAD会指向最新一次commit，也就是c7

![image-20230311094123226](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311094123226.png)



此时要将dev合并进master分支，需要将c5 和 c7合并成一个c8版本，如果c5和c7的文件差别较大，需要手动处理好两个版本间的冲突才能继续合并

![image-20230311094504932](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311094504932.png)

##### 本地分支、追踪分支和远程分支

- **本地分支**：本地分支就是我们可以通过 `git branch` 查看到的分支，也就是我们自己Git仓库所拥有的分支，我们都可以利用。
- **远程分支**：远程分支是对远程仓库的分支的索引，它其实也是本地分支，只是我们无法移动它，必须要在和中心服务器交互根据服务器更新到本地来的代码移动的，远程分支的作用就是我们上次和中心服务器交互更新得到的最新版本，它也是个指针。
- **追踪分支**：追踪分支比较难理解，它**也是一个本地分支**，只是它**对应了一个远程分支**，如果我们本地的某个分支对应了一个特定的远程分支，那么它就是追踪分支，比如我们最初的master分支就是一个追踪分支，它对应远程分支origin/master，这里origin是远程仓库名，当我们在master分支里执行更新(fetch，pull)或是推送(push)，在不指定分支的情况下，默认就是从origin/master分支更新来或者提交到origin/master分支。

例如刚刚从远程拉下来的一个仓库

![image-20230311095210395](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311095210395.png)

此时，`HEAD` 指向最新一次commit 版本c3，本地分支`master` 指向c3， 远程分支 `origin/master` 也指向版本c3。

这里本地的 `master` 分支对应了远程的 `origin/master` 分支，因此他就是追踪分支

如果我们没有及时更新远程分支，自己在本地埋头苦干更新本地版本的话，就会是这样的

![image-20230311095621883](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311095621883.png)



当我们在本地开发的时候，已经有人开发完成并且推送到远程分支的话，可怕的事情就来了

![image-20230311100033773](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_first_class/image-20230311100033773.png)

当我们把远程分支更新后一看，别人都把远程推到c8了，如果要把我们本地的合并进最新的远程分支，又要处理一堆的冲突

因此建议大家在多人开发的时候一定要及时拉取最新的分支

#### remote

对远程仓库的操作

##### 添加远程仓库

```shell
git remote add [远程仓库名] [远程仓库地址]
```

例如，要添加一个掌上重邮远程仓库，指定仓库名为**origin**，指令如下：

```shell
   			   # 名称                 远程仓库地址
git remote add origin git@github.com:RedrockMobile/CyxbsMobile_Android.git
```

如果手误输错了仓库名，需要更改的话，可以使用 **rename** ，例如需要修改名称  orgin -> origin

```shell
				# 原名称 修改后名称
git remote rename orgin origin
```

##### 移除远程仓库

```shell
    	   	  #仓库名
git remote rm origin
```

##### 查看远程仓库

```shell
# 查看现有的仓库有哪些（一般只有一个origin仓库，这是默认的名称）
git remote
# 可以查看仓库的地址
git remote -v
```

#### fetch

更新本地分支的指针

```shell
# 这个命令查找 “origin” 对应的远程仓库，从中抓取本地没有的数据，并且更新本地数据，移动 origin/master 指针指向新的、更新后# 的位置。
git fetch origin
# 当然我们也可以直接fetch
git fetch
```

在更新远程分支后，如果想基于 `origin/master` 分支继续工作，就可以从该分支迁出新分支进行开发：

```shell
git checkout -b dev origin/master
```

如果本地已经有一个 `master` 分支，并且想将 `origin/master` 拉取下来的更新合并入该分支，需要手动合并：

```shell
# 首先需要切换到master分支
git checkout master
# 合并
git merge origin/master
```

#### pull

更新当前分支对应的远程分支，并将更新合并进来
```shell
git pull
```

上面的命令其实就相当于一并执行了 `fetch` 和 `merge` 两个指令:

```shell
# git fetch 会把所有的远端镜像更新到本地，然后更新缺少的commit，相当于是同步
git fetch
# git merge  会合并当前HEAD指向的分支，其余分支并不会
git merge origin/[对应的远程分支名]
```

#### push

前面提过了如何把远程仓库的更新拉取到本地并且合并进分支，`push` 操作则是将本地的更改提交到远程仓库上去。

```shell
# 会将某个分支推送到远程分支上
git push [远程主机名/仓库名] [本地分支名]:[远程分支名]
# 表示将当前分支推送到[远程主机名]的对应分支
git push [远程主机名/仓库名]
# 强行推送，会强行覆盖掉远程仓库，慎用！
git push -f
```

只有一个远程主机时，`git push` 后的远程主机名可以省略

如果有多个远程主机， 想要设置push的默认主机，可以使用

```shell
git push -u origin master
```

先push一次，后续可以直接使用 `git push` 默认push到远程主机 `origin` 上

![bbf9ac789c6d92a93f261b71d610de52.jpeg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/bbf9ac789c6d92a93f261b71d610de52.jpeg)

#### tag

当我们想标记一次重要的commit，例如App发布一个版本v6.0.1的时候，就需要用到 `tag` 操作进行一个标记

**编辑并提交tag（注意此时提交的tag还在本地）**

```shell
git tag -a [版本号] -m '版本信息'
```

**给之前的commit 打 tag**

```shell
git tag -a [tag名称] [commit的哈希值] -m '信息'
```

**把本地的tag推送上去**

```shell
# 全部推送
git push origin --tags
# 推送指定tag
git push origin tag名称
```

推送到远程仓库后我们就能看到对应的tag，例如GitHub：

![1690461007680.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690461007680.png)

**如果突然发现有严重bug，可以删除tag（注意此时也是删除的本地）**

```shell
git tag -d 版本号
```

**删除远程的tag**

```shell
git push origin :refs/tags/v1.1
```

同时，在一些情况下也可以使用 `tag` 来代替commit的哈希值使用

例如：

```shell
git checkout tag名称
git checkout -b new分支名称 tag名称
git pull --t tag名称
```

#### GitHub

~~GayHub~~ GitHub是 ~~全球最大的同性交友网站~~ 全球最大的代码托管平台，它提供了一个集中存储、版本控制、协作和代码管理的平台。它提供了强大的协作功能，允许多个开发者共同参与一个项目，进行代码的修改、审查和合并等等。

[GitHub](https://github.com/) 这是GitHub的官方网站，可以在这里注册账号并开始使用GitHub。

##### Pull requests

在把本地的开发分支推到云端后，我们可以向仓库提一个Pull requests来更加安全地将我们的分支合并进仓库主分支中。

![1690461413049.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690461413049.png)

选择需要合并的原分支和目的分支，创建pr

![1690511549622.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690511549622.png)

完善合并描述，提交

![1690511633370.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690511633370.png)

然后就可以等待仓库管理员对我们的pr进行合并/打回，我们也可以在pr下与管理员进行交流

![1690512578368.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690512578368.png)
