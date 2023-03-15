### Source

Git —— 分布式版本控制系统，一个工具。

Open Source | Linux  : 庞大、不好管理

集中式的版本控制系统：不好用，收费  带宽要大 不然不行

<img src="C:\Users\admin\Desktop\Sync\LearnGit\images\image-20230315194915999.png" alt="集中式管理系统" style="zoom:67%;" />

The name "git" was given by Linus Torvalds when he wrote the very first version. He described the tool as "the stupid content tracker" 
and the name as (depending on your way): 

  - random three-letter combination that is pronounceable, and not actually used by any common UNIX command.  The fact that it is a mispronunciation of "get" may or may not be relevant. 
  - stupid. contemptible and despicable. simple. Take your pick from the dictionary of slang. 
  - "global information tracker": you're in a good mood, and it actually works for you. Angels sing, and a light suddenly fills the room. 
  - `"g*dd*mn idiotic truckload of sh*t"`: when it breaks 

### Why ?

对文本数据，进行自动分析改动。

时空穿梭，可以回退任何版本。

### Installation

### 版本库

类似一个目录，在这个目录中的文件，Git可以进行追踪，包括修改，删除，以及在目录中添加文件。 追踪、还原。 ---回溯

**创建一个版文库**

1. 创建一个目录`Dirctory`,随后转到该目录；
   `mkdir  LearnGit`
   `cd LearnGit`
   通过`pwd`命令，可以查看一下当前所在的目录（Linux）, Windows下可以用`echo %cd% `
2. 上面所创建的目录仅仅是一个普通的目录，通过`git init`命令，使得该目录变为Git可以管理的仓库（Repository）
   `.git`目录：Git用来追踪的隐藏文件夹  可以通过`dir /a `(Windows）查看

把文件添加到版本库

`git add Readme.md`

`git add .  |   git add * ` 把当前目录，所有文件添加到仓库

用`git commit`告诉Git，把文件提交到仓库

```
git commit -m "wrote a readme file"
```

`-m`参数  后面跟着本次提交的一个说明。最好是有意义的。简明扼要的，一针见血的。

add commit 两步走 ？

> commit  一次可以提交多个文件
>
> add 可以分批量添加文件

形象化的说明：

```bash
git config 登记演出主办人和邮箱地址
git init   临时租用了一个场地作为演出区
git status 寻问各文件的状态，如新来的（add）、离开的（delete）、补妆的（modify）等。
git add    将补妆好的、新来的文件登记到演出准备（Staging Environment）名册中，注销演技老套、生病而离开的文件
git commit 便是把文件推到演出区进行录播，供万人在线随时欣赏；当文件临时补妆返场，也可通过 -a ，在寻问过文件 status 的情况下，跳过登记阶段，再次录播，并剪辑、更新原有录像。
git status 只列出变动的文件
git add    登记文件变动到文件名册
git rm     从文件名册中注销该文件，并删除工作区文件（delete）
git rm --cached 只从文件名册中注销该文件
git restore --staged  是若干次add、rm --cached的逆向回退操作，撤销之前的登记操作，直到最近一次的commit 提交。
git restore 撤销工作区未登记的文件的删除、修改和创建（撤销会使新创建的文件处于Untracked的状态，但不会删除该文件），直到最近一次的登记。
```

### 时光穿梭

