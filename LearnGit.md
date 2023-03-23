### Source

Git —— 分布式版本控制系统，一个工具。

Open Source | Linux  : 庞大、不好管理

集中式的版本控制系统：不好用，收费  带宽要大 不然不行

<img src="https://cdn.jsdelivr.net/gh/c1ata/imgbed2020/imgimage-20230315194915999.png" alt="集中式管理系统" style="zoom:67%;" />

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

`git status` 查看当前仓库的状态

`git diff` 查看修改的内容

`git log` 查看历史记录

`git log --pretty=oneline` 简明的显示信息 

`git reset --hard HEAD^^`

`git reflog` 查看命令历史，以便确定回到哪个版本

### 工作区和暂存区

**工作区**：电脑上能直接看到的目录 （Workding Directory）

**版本库**：工作区中有一个隐藏的目录`.git` (Repository)

- `暂存区`(Stage | Index)
- First Branch -- `main`   HEAD 指向当前分支

 ![git-repo](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/img0.jpg)

多次`git add`操作，相当于把文件放到了暂存区，`git commit` 操作相当于一次性处理完暂存区的所有文件。

没有`add`的文件，通过`git status`会显示 **Untracked Files**

### 远程仓库

`git branch -r` 显示远程仓库

`git remote show`

`git remote -v` 查看远程项目地址

`git remote show origin` 查看当前项目所有信息

`git diff`        查看工作区和暂存区差异

`git diff --cached`查看暂存区和仓库差异，

`git diff HEAD` 查看工作区和仓库的差异，

`git add`的反向命令`git checkout`，撤销工作区修改，即把暂存区最新版本转移到工作区，

`git commit`的反向命令`git reset HEAD`，就是把仓库最新版本转移到暂存区。

### 管理修改

Track的不是文件，而是修改。修改：增加了一行文字，甚至一个字符；添加了一个新文件，都算是修改。删除，替换...

每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中

### 撤销修改

**Working Directory**

把文件恢复到上一个版本的状态

`git checkout -- file` 可以丢弃工作区的修改，让这个文件恢复到最近一次`add` 或 `commit`的状态

上面的 `--` 必须要有

`git restore file `也能达到同样的效果

**Stage**

`git restore --staged <file>...`  to unstage

 `git reset HEAD readme.txt`   unstage 

**场景**

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file` (git restore file)。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，

第一步用命令`git reset HEAD <file>`  (git restore --staged <file>)，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

### 删除文件

删除文件的话，如果要还原：`git retore file` | `gir checkout -- file` 

删除的话：`git rm file `  记得要 `git commit -m "xxx"` 一下

如果提交到版本库的话，还原的话只会还原到最新的那一版本。以前的未提交到版本库的内容则会丢失

### 远程仓库（!）

分布式：同一个**Git Repository**,可以分布再不同的机器上；

有一台机器充当服务器的**Role** 

Github: 为 Git Repository 提供托管服务

#### `SSH` 密钥管理

1. 检查现有SSH密钥
   Git Bash -> `ls -al ~/.ssh`

   - id_rsa.pub
   - id_ecdsa.pub
   - id_ed25519.pub

2. 生成SSH密钥
   Git Bash -> `ssh-keygen -t ed25519 -C "your_email@example.com"`

   - 将以提供的电子邮件地址为标签创建新 SSH 密钥
     （若以前存在密钥，可以自定义密钥名称）
   - 设置安全密码

3. 添加到SSH-Agent

   - 确保 ssh-agent running
     `start the ssh-agent in the background`
     
     ```shell
        $ eval "$(ssh-agent -s)"
        > Agent pid 59566
     ```
     
   - 将 SSH 私钥添加到 ssh-agent
     `ssh-add ~/.ssh/id_ed25519`
     
   - 将 SSH 密钥添加到 GitHub 上的帐户

     1. 复制SSH公钥
        `clip < ~/.ssh/id_ed25519.pub`
     2. Settings -> SSH and GPG keys -> New SSH key

4. 测试SSH连接
   `git -T git@github.com`

#### 远程仓库 URL的切换

将远程URL 从 HTTPS 切换到 SSH

- 查看当前远程仓库的信息
  `git remote -v`
- `git remote set-url origin git@github.com:USERNAME/REPOSITORY.git`

#### 添加或删除远程库

本地库和远程库的名称要一致 

**添加远程库**

`git remote add origin git@github.com:USERNAME/REPOSITORY.git`

**删除远程库**

`git remote rm origin`

**推送分支**

第一次：`git push -u origin main` 把本地的分支和远程的分支 **绑定**

`git push origin main`

#### 从远程库克隆

`git clone git@github.com:USERNAME/REPOSITORY.git`

ssh 速度最快

### 分支管理

平行宇宙

 ![learn-branches](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/branch.png)

#### 创建与合并分支

一条时间线就是一个分支

 ![image-20230319195505165](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230319195505165.png)

`main`指向最新提交，`HEAD`指向`main` 

每`commit`一次，Git 用 `main` 指向最新的 `commit`, 再用 `HEAD` 指向 `main`

随着不断的提交，main分支的线会越来越长

  ![image-20230319200056196](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230319200056196.png)

创建了一个新的分支`Dev`,Git 会新建一个指针` Dev`,指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上

相当于切换了分支

 ![image-20230319200440969](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230319200440969.png)

Now,工作区的修改和提交都是针对Dev分支，main指针不变，Dev指针向前移动一步

最简单的合并：main 指向 Dev的最新提交

 ![image-20230319201705000](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230319201705000.png)

Dev分区也可以删除

创建`Dev` 分支，切换到`Dev`分支

```shell
$ git checkout -b Dev
Switched to a new branch 'Dev'
```

`git checkout`命令加上`-b`参数表示**创建并切换**

相当于：

```bash
$ git branch Dev
$ git checkout Dev
```

利用`git branch` 常看当前分支

```shell
$ git branch
* Dev
  main
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号

可以在Dev分支上修改文件，然后切换到main分支上，发现修改已经消失

```shell
$ gir checkout main
```



 ![git-br-on-master](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/0.png)

**分支的合并**

把`dev`分支的工作成果合并到`main`分支

```shell
$ git merge Dev
Updating 323e803..14c503b
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

`Fast-forward`：直接把`main`指向`dev`的当前提交

**删除分支**

```shell
$ git branch -d Dev
Deleted branch Dev (was 14c503b).
```

使用`git branch`查看分支

```bash
$ git branch
* main
```

PS.

`git switch` 命令

创建并切换分支 ：`git switch -c Dev`

切换分支： `git switch Dev`

#### 解决冲突

**Preparations**：

new branch: `feature1`

```shell
# 创建并切换到 feature1 这个分支
git switch -c feature1
```

![fff](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230321150037037.png)

无法快速合并，出现冲突（`conflict`）

```shell
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

使用`git status`也可查看冲突

```shell
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   readme.txt
```

可以直接查看冲突文件的内容：

```
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```

Git 使用 `<<<<<<<` , `=======` , `>>>>>>>` 标记不同分支

修改之后再提交

 ![image-20230321151300385](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230321151300385.png)

使用`git log` 查看分支合并的情况:`git log --graph`命令可以看到分支合并图

```shell
$ git log --graph --pretty=oneline --abbrev-commit
*   4ea7d21 (HEAD -> main) fix conflict
|\
| * 8b509ec (feature1) AND simple
* | a6251d0 & simple
|/
```

最后，删除`feature1`分支

```shell
$ git branch -d feature1
Deleted branch feature1 (was 8b509ec).
```

#### 分支管理策略

在`Fast  forward`模式下，删除分支后会丢失分支信息

禁用`Fast Forward`模式，`merge`后会提交一个`commit`，需要`-m`参数，添加描述

```shell
git merge --no-ff -m "merge with --no-ff" dev
Merge made by the 'ort' strategy.
 readme.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```
`--no-ff`参数，表示禁用`Fast forward`

`git log --graph --oneline`查看合并信息

```shell
$ git log --graph --oneline
*   a608261 (HEAD -> main) merge with --no-ff
|\
| * 11cd736 (dev) add haaaaaaaaa
|/
```

 ![image-20230321154012482](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/image-20230321154012482.png)

**分支策略**

`main` 稳定，仅仅用来发布新版本

`dev` 不稳定，开发

每个人有自己的分支，然后合并到`dev`分支上

 ![git-br-policy](https://cdn.jsdelivr.net/gh/c1ata/imagebed2023/img/git-strategy.png)

#### Bug分支

场景：面临bug需要来修复

先在dev分区保留工作现场:  `git stash`

切换到出现bug的分支： `git switch main`

创建问题分支： `git switch -c issue-101`

修复bug并提交： `git add bug-files` `git commit -m "Fix bug"`

切换回bug分支 ：`git switch main`

合并问题分支：`git merge --no-ff -m "fix issue101" issue-101`

删除`issue-101` 分支： `git branch -d issue-101`

回到`dev`分区继续开发,恢复工作现场：

- `git stash list`:查看保存的工作现场（git将工作现场stash到某个地方了）
- git stash apply
- git stash drop
- git stash pop
- git stash apply stash@{0}

修复 dev  分区的bug

`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支