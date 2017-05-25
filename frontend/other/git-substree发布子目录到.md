### 使用GIT SUBTREE集成项目到子目录

> 使用场景
例如，在项目Game中有一个子目录AI。Game和AI分别是一个独立的git项目，可以分开维护。为了避免直接复制粘贴代码，我们希望Game中的AI子目录与AI的git项目关联，有3层意思：
+ AI子目录使用AI的git项目来填充，内容保持一致。
+ 当AI的git项目代码有更新，可以拉取更新到Game项目的AI子目录来。
+ 反过来，当Game项目的AI子目录有变更，还可以推送这些变更到AI的git项目。
+ 用git subtree可以轻松满足上面的需求。

#### 对比git submodule

如果你没有用过git submodule，你甚至可以不用了解git submodule是什么，submodule的基本介绍也不在本文的说明范围内。虽然它满足了上述差不多的需求，但是复杂难用，以至于需要这么长一篇教程才能说清楚用法。

如果你的项目正在使用git submodule，你应该知道用submodule有多么麻烦，这里还有一篇文章专门解释git submodule的缺点，可以参考前面教程里的最后一段来删除submodule（是的，连删除步骤都非常麻烦）。

使用git subtree之后，管理、更新都更加方便。

#### 什么是git subtree

> git subtree是一条git子命令，本质上subtree是一种合并策略，从git v1.5.2，官方就推荐使用subtree代替submodule，所以它并不需要保存.submodule这样的元信息。

#### git subtree的前提条件

> subtree子命令很晚才集成到git中，请确保你的git版本（使用git --version查看） > v1.8.0.0。有些文章中说v1.7.11就已经集成了，实际上没有，如果直接执行会看到这样的结果：

#### $git subtree  
git: 'subtree' is not a git command. See 'git --help'.
如果你是在OS X下使用git，推荐用homebrew来安装新版本

> $brew install git  
`git --version  `
`git version 1.8.3.4`

#### git subtree用法

针对第一段的3条需求，我分别说明具体的命令。

### 1. 第一次添加子目录，建立与git项目的关联

建立关联总共有2条命令。

语法：`git remote add -f <子仓库名> <子仓库地址>`

解释：其中-f意思是在添加远程仓库之后，立即执行fetch。

语法：`git subtree add --prefix=<子目录名> <子仓库名> <分支> --squash`

解释：--squash意思是把subtree的改动合并成一次commit，这样就不用拉取子项目完整的历史记录。--prefix之后的=等号也可以用空格。

示例

`$git remote add -f ai https://github.com/aoxu/ai.git  `
`$git subtree add --prefix=ai ai master --squash`

### 2. 从远程仓库更新子目录

更新子目录有2条命令。

语法：git fetch <远程仓库名> <分支>

语法：git subtree pull --prefix=<子目录名> <远程分支> <分支> --squash

示例

`$git fetch ai master  `
`$git subtree pull --prefix=ai ai --squash`
3. 从子目录push到远程仓库（确认你有写权限）

推送子目录的变更有1条命令。

语法：git subtree push --prefix=<子目录名> <远程分支名> 分支

示例

`$git subtree push --prefix=ai ai master`
参考资料：

speackerdeck
atlassian
pro git



#### 实践
+ 1.自己的项目 在根目录下新建一个新的目录 叫 dist
+ 2.在github或gitlab仓库上新建一个工程，取名叫publish
+ 3.建立关联关系,并取名为publish。 `git remote add -f publish git@gitlab:kkk.publish.git`
+ 4.建立子目录关系 git subtree add --prefix dist publish master --squash
+ 5.将自己项目的打包目标指向dist目录，然后打包新的文件并commit
+ 6.最后push到新的仓库 git subtree push --prefix=dist publish master 



