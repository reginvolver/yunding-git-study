## 从零开始的Git学习

### 啥是Git？为啥要学Git？

Git是一种分布式版本控制系统，用于跟踪文件和代码的变化。它被广泛用于软件开发项目中，可以帮助多人协作开发、管理代码的版本、回滚代码等。

学习Git的原因有以下几点：

1. 版本控制：Git可以帮助你跟踪文件和代码的变化，记录每次修改、添加或删除的内容。这使得你可以轻松地查看文件的历史记录，并且可以随时回滚到之前的版本。对于团队协作开发或个人项目管理来说，版本控制是非常重要的。
2. 多人协作：Git支持多人同时对同一个项目进行开发，并能够合并各自的修改。它提供了分支和合并的功能，允许团队成员在独立的分支上进行开发，最后将所有修改合并到主分支上。这种方式能够有效地协调团队成员之间的工作，避免冲突和覆盖他人的修改。
3. 代码管理：Git提供了一个中央仓库和本地仓库的结构，你可以将代码保存在本地仓库中，并将其推送到中央仓库上。这样，你可以方便地备份代码、恢复代码、共享代码等。Git还提供了分支管理、标签管理等功能，可以帮助你更好地组织和管理代码。
4. 开源社区：Git已经成为开源软件开发的事实标准，许多知名的开源项目都使用Git进行版本控制。学习Git可以使你更好地参与开源社区，贡献自己的代码或从其他人的代码中学习。

上班都用git！！！不会你就凉凉辣！

### 这玩意咋使？

#### Git！安装！

Mac: 终端输入git 会自动安装

Win：安装

配置环境变量（除git bash之外也可以使用git）

Win + R (运行) windows cmd / powershell

#### Git！配置！

##### 设置用户名和邮件地址。

这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改：

```bash
git config --global user.name "John Doe" 

git config --global user.email johndoe@example.com 
```

再次强调，如果使用了 --global 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事 情， Git 都会使用那些信息。 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 --global 选项的命令来配置。 很多 GUI 工具都会在第一次运行时帮助你配置这些信息。

查看配置

```bash
git config -l
```

##### 生成/添加ssh公钥

Gitee 提供了基于SSH协议的Git服务，在使用SSH协议访问仓库之前，需要先配置好账户/仓库的SSH公钥。

你可以按如下命令来生成 sshkey:

```
ssh-keygen -t ed25519 -C "xxxxx@xxxxx.com"  
# Generating public/private ed25519 key pair...
```

> 注意：这里的 `xxxxx@xxxxx.com` 只是生成的 sshkey 的名称，并不约束或要求具体命名为某个邮箱。
> 现网的大部分教程均讲解的使用邮箱生成，其一开始的初衷仅仅是为了便于辨识所以使用了邮箱。

按照提示完成三次回车，即可生成 ssh key。通过查看 `~/.ssh/id_ed25519.pub` 文件内容，获取到你的 public key

```
cat ~/.ssh/id_ed25519.pub
# ssh-ed25519 AAAAB3NzaC1yc2EAAAADAQABAAABAQC6eNtGpNGwstc....
```

![SSH生成](https://images.gitee.com/uploads/images/2021/0827/165113_8e58f0e1_551147.png)

![输入图片说明](https://images.gitee.com/uploads/images/2021/0827/165455_ec7dbd09_551147.png)

复制生成后的 ssh key，通过仓库主页 **「管理」->「部署公钥管理」->「添加部署公钥」** ，添加生成的 public key 添加到仓库中。

![添加部署公钥](https://images.gitee.com/uploads/images/2018/0814/233212_29a62378_551147.png)

添加后，在终端（Terminal）中输入

```
ssh -T git@gitee.com
```

首次使用需要确认并添加主机到本机SSH可信列表。若返回 `Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access.` 内容，则证明添加成功。

![SSH添加提示](https://images.gitee.com/uploads/images/2018/0814/170837_4c5ef029_551147.png)

添加成功后，就可以使用SSH协议对仓库进行操作了。

Github同理

##### 如何测试公钥是否添加成功？

使用ssh链接 clone一个仓库 能clone成功就成功辣！



git clone + 链接（https / ssh）. ssh配置后免密

git clone git@github.com:reginvolver/recruit-backend.git

git clone https://gitee.com/xiaoWenZhuo/full-stack.git

// 连接不到主机

#### Git！启动！





### 来学一些基本知识？

#### 啥是版本控制？

版本控制是一种`记录一个或若干文件内容变化`，以便将来查阅特定版本修订情况的系统。

是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，

#### 主流版本管理工具有啥？

Git 分布式 每个仓库都是一个完整备份

SVN 集中化 有个中央服务器 一个炸了都炸了！

#### Git的一些基本概念

Git本地有三个工作区域：

`工作目录`（Working Directory）文件夹 不会被git管理 本地

`暂存区`(Stage/Index)。git真正管理的地方。本地

如果在加上`远程的git仓库`(Remote Directory)  Github/gitee

就可以分为四个工作区域。

文件在这四个区域之间的转换关系如下：

Workspace：工作区，就是你平时存放项目代码的地方

Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息

Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数 据。其中HEAD指向最新放入仓库的版本

Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据 交换

<img src="https://gitee.com/xiaoWenZhuo/picgo/raw/master/imgs/image-20220116171035317.png" alt="image-20220116171035317" style="zoom:50%;" />

#### 工作流程

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域；

３、将暂存区域的文件提交到git仓库。

因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

• 已修改表示修改了文件，但还没保存到数据库中。

• 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。

• 已提交表示数据已经安全地保存在本地数据库中。

<img src="https://gitee.com/xiaoWenZhuo/picgo/raw/master/imgs/image-20220116171653855.png" alt="image-20220116171653855" style="zoom:50%;" />





### 怎么交作业？

==== 从始至终记住 Git的管理基本单位是仓库 也就是文件夹 所有的git操作路径 请务必在你的仓库文件夹进行 ====

==== 不要在e盘 c盘 或者各种奇奇怪怪的路径 执行各种奇奇怪怪的git命令 ====

- 获取一个可爱的Git远程仓库（从GitHub/Gitee新建然后薅一个）

  克隆仓库的命令是 git clone

  比如，要克隆 Git 的链接库 libgit2，可以用下面的命令：

  ```bash
   git clone https://github.com/libgit2/libgit2 
  ```

  这会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 .git 文件夹(隐藏)，从远程仓库拉取下所有数据放入 .git 文件夹，然后从中读取最新版本的文件的拷贝。

  如果你进入到这个新建的 libgit2 文 件夹，你会发现所有的项目文件已经在里面了，准备就绪等待后续的开发和使用。

- 三板斧

  ​	git status   查看当前git 仓库的状态



- git add   未管理 -> 管理

  本地文件夹 -> 暂存区 （git管理了）

  将文件纳入git的管理

  ````
  git add <file1> <file2> ...  # 添加修改的文件
  将`<file1> <file2> ...`替换为你要添加的文件列表，
  git add . （将当前目录的所有文件 全部纳入管理） 注意执行的路径 （文件夹）
  ````

- git commit -m  拍照片 （快照）


    ```
    git commit -m "Commit message"  # 提交修改并附上提交信息
    `"Commit message"`替换为对提交的简要描述。
    ```

    提交至本地

- git push （注意push之前 确保本地的文件夹是干净的 没有未commit的文件）

  push之前 使用git pull 命令 看一眼有没有坏蛋改你代码

  merge

  发布至远程

  ````
  git push <remote> <branch_name>  # 将本地分支推送到远程仓库
  ```
  
  将`<remote>`替换为远程仓库的名称（通常是`origin`），`<branch_name>`替换为你的分支名称。
  ````

### 	

​		-

### 不想敲黑框框了肿么办

- VsCode
    - 推荐插件 GitLens
- JetBrains系全家桶 （Idea、Webstorm、Pycharm等）
    - 万能的IDE早已为你准备好了超级好用的Git插件

### 企业开发常见操作

- 分支 - 平行宇宙

  在软件开发中，使用分支是一种常见的代码管理策略，可以帮助团队更好地组织和协作开发。下面是分支的一般用途以及操作流程的概述：

    - 生产环境分支（Production Branch）master ：
        - 用途：生产环境分支包含了已经通过测试并准备发布到生产环境的代码。
        - 操作流程：
            1. 从主分支或预发环境分支创建生产环境分支。
            2. 确保生产环境分支上的代码已经通过了所有必要的测试和验证。
            3. 将生产环境分支的代码部署到生产环境中。

    - 开发分支（Develop）：
        - 用途：开发分支是用于日常开发工作的分支，包含最新的开发代码。团队成员可以在该分支上进行功能开发、Bug修复等工作。
        - 操作流程：
            1. 从主分支创建开发分支。
            2. 在开发分支上进行开发和修改。
            3. 定期将最新的主分支合并到开发分支，以确保开发代码与稳定代码保持同步。
            4. 当开发分支上的功能开发完成并经过测试后，可以将其合并回主分支。
    - 预发环境分支（Pre-production Branch）：
        - 用途：预发环境分支用于将代码部署到类似于生产环境的测试环境中进行最终的测试和验证。
        - 操作流程：
            1. 从主分支或开发分支创建预发环境分支。
            2. 将代码部署到预发环境进行测试。
            3. 验证代码在预发环境中的功能和性能。
            4. 如果存在问题，可以在预发环境分支上进行修复，并重新进行测试。
            5. 当预发环境验证通过后，可以将预发环境分支合并回主分支或开发分支。

##### 在公司如何合并分支？ 我该合并哪个分支？

- master （生产环境分支）
- pre（预发环境分支）
- xiaowenzhuo_1126_fixsomebug (个人开发分支) - 从 master （生产环境分支）

##### 如何拉取他人的代码？

- git pull 命令

##### 合并有代码冲突怎么办？

- 解决冲突

##### commit了但是commit错分支了怎么办？

不要使用git push -f

- 未提交至远程仓库
    - 本地 undo commit
- 提交至远程仓库
    - revert 之后提交 无法抹除你罪恶的踪迹

### 如何进行团队开发？

- GitHub/Gitee
    - 创建团队/拥有同一个仓库的权限
        - 相当于本地开发 三板斧 + pull + 分支
    - 开源项目/无权限
        - fork仓库 提PR 等待仓库所有者同意后并入仓库

### IDEA/VsCode演示

### Github-全球最大的通行交友网站

- 上面有啥 怎么用？



.gitignore文件 用于忽略不提交的内容