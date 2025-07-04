---
title: Git
date: 2020-02-23 19:07:58
categories:
- Git
tags:
- Git
---

# 基础
{% asset_img git1.png %}

How to change the URI (URL) for a remote Git repository?
git remote set-url origin new.git.url/here

yarn add https://github.com/fancyapps/fancybox [remote url]
yarn add ssh://github.com/fancyapps/fancybox#3.0  [branch]
yarn add https://github.com/fancyapps/fancybox#5cda5b529ce3fb6c167a55d42ee5a316e921d95f [commit]

## ubuntu 安装最新版本
[gitVersion](https://github.com/git/git/releases)
因为 Ubuntu 自带的源中，Git 版本就是这么低，所以需要加入一个源，带有最新 Git 版本的源
``` zsh
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## merge
cms垒哥没有merge 到 dev
seven：merge 本地；本地dev 分支需要拉一下

## 查看文件修改内容
git diff test.text

# 配置

### ssh 密钥
```
ssh-keygen
```

### github.com代理
选择 “编辑PAC用户自定规则” 会打开一个简单编辑器。
在其中添加自定义的PAC规则，每行一条，规则格式参考 https://adblockplus.org/en/filter-cheatsheet

简单来说 ||a.com 这条规则即可匹配 a.com/xxx x.a.com/xxx xx.x.a.com/xxx 这些url

### 全局配置
用户名
``` BASH
$ git config --global user.name "name"
```

邮箱
``` BASH
$ git config --global user.email "email@gmail.com"
```

验证连接
``` zsh
ssh -T git@github.com
Hi KilFront! You've successfully authenticated, but GitHub does not provide shell access.
```

### 单项目配置
git为不同的项目设置不同的用户名

每个git项目下都会有一个隐藏的.git文件夹

两种方式
open config 命令打开，添加如下配置：
[user]
    name = XXX(自己的名称英文)
    email = XXXX(邮箱)

命令：
git  config  user.name  "xxxxx"


### 代理
``` BASH
#只对github.com
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080

#取消代理
git config --global --unset http.https://github.com.proxy
```

#### 仅为 GitHub 设置代理
git 代理
设置 git config --global http.https://github.com.proxy socks5://127.0.0.1:1086
设置完成后, ~/.gitconfig 文件中会增加以下条目:

[http "https://github.com"]
    proxy = socks5://127.0.0.1:1086


ssh 代理
修改 ~/.ssh/config 文件

Host github.com
    User git
    ProxyCommand nc -v -x 127.0.0.1:1086 %h %p

## .gitconfig文件
.gitconfig文件是Git的全局配置文件，它保留了关于Git行为和外观的设置。这些设置是针对当前用户的所有Git仓库有效的。
文件通常位于主目录，例如在Linux或Mac系统中，其路径通常是 ~/ ，在Windows系统中，其路径通常是 C:\Users\你的用户名 。你可以使用命令行编辑这个文件，或者使用 git config --global 命令设置这个文件的内容。


```.gitconfig
# 用户信息：这包括你的用户名和邮箱地址，这些信息会用于所有的git提交操作
[user]
        name = Your Name
        email = your.email@example.com

# 别名：你可以在 .gitconfig 文件中定义命令的别名来简化命令行操作
[alias]
        st = status
        co = checkout
        ci = commit
        br = branch
# 这样，你就可以用 `git st` 来代替 `git status`。   

# 默认的编辑器或比较工具：你可以在 .gitconfig 文件中定义默认使用的文本编辑器或者文件比较工具。
[core]
        editor = vim
[diff]
        tool = vsdiffmerge
```

### 全局.gitignore文件
创建一个全局.gitignore文件：首先，你需要创建这个文件，并存放在你的主目录下，或者任何一个你能够记住的地方。例如，你可以创建一个文件路径为 ~/.gitignore_global。
添加规则：在这个.gitignore_global文件中，按照正常的.gitignore规则添加你想要在所有仓库中忽略的文件或文件夹模式。
配置Git使用这个文件作为全局.gitignore：接下来，你需要告诉Git使用你创建的这个文件作为全局忽略规则，通过运行以下命令：
 git config --global core.excludesfile ~/.gitignore_global
这会在你的 .gitconfig 文件添加相关设置，指定全局忽略文件的位置。执行这个命令后，.gitconfig 文件中会显示类似下面的配置：
[core]
    excludesfile = /path/to/your/.gitignore_global

```
.DS_Store
node_modules/
target/
```

## token
gitlab import github   授权
{% asset_img register.png%}

# 指令
git配置
git config --list

## 提交
git commit -am "some str"
git push

git commit -am 'str'命令只能提交已经追踪过且修改了的文件，新增文件就必须使用git add . && git commit -m 命令；

## 标签
标签可以标记特定的代码版本
git tag v1.0.0
git push origin v1.0.0

### 处理上传环境bug
bg：已经合并了功能分支到master，只是还没有部署。这时候生产上有bug了，如何处理。
通过使用 Git 标签（tag）来处理生产环境的 bug 修复是一种常见且有效的方法。标签可以帮助你标记特定的代码版本，并在需要时快速回滚到这些版本。
```zsh
# 生产分支，切一个tag标签
git tag v1.0.0
git push origin v1.0.0

# 创建新的修复分支
git checkout tags/v1.0.0 -b hotfix/bug-fix
# 修复bug后
git add .
git commit -m "Fix production bug"
# 创建新的标签并部署
git tag v1.0.1
git push origin v1.0.1

# 部署 v1.0.1 标签到生产环境。

# 合并修复到 master
git checkout master
git pull origin master
git merge hotfix/bug-fix
git push origin master
```

### 删除tag
```zsh
# 本地
$ git tag -d v1
# 远程
$ git push --delete origin v1
```

## 切换到指定commit ID
```zsh
git checkout <commit-id>
```

## 版本回滚
### revert
创建一个新的提交来撤销指定提交的更改。
git revert HEAD^

### reset
注意：回滚前先checkout 一个分支进行保留
``` zsh
git reset --hard ff19b5644e7470728d5a10f57f244f9754fb4d58
git add .
git commit -m update
git push origin dev -f
```

-f : force 暴力

Pushing to git@github.com:519ebayproject/519ebayproject.git
To git@github.com:519ebayproject/519ebayproject.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:519ebayproject/519ebayproject.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
我遇到造成这个问题的原因，一般是因为执行了git reset命令，版本回退后没有恢复，造成本地仓库的提交版本号落后于远端仓库的提交版本号。
可以执行 git push -f命令去强制提交


----
git fetch --all
git reset --hard origin/master
git pull //可以省略

### 回滚之后的操作
git log  找到想退回的版本

### 未暂存文件
git reset 3e5236a

### 暂存文件
git reset --hard 3e5236a

## 历史提交记录
git log

## 重置origin
git remote set-url origin git@github.com:ApowoGames/cordova-plugin-keyboard.git

## 删除远程已提交的文件
https://www.liaoxuefeng.com/wiki/896043488029600/900002180232448
首先删除本地 文件
git status
deleted:    test.txt

``` zsh
# 从上往下，这步可省略
git rm -r --cached 文件/文件夹名称
# 修改本地 .gitignore
git add .
git commit -m ''
git push origin master
```

git rm -r --cached xxx.iml　　//-r 是递归的意思   当最后面是文件夹的时候有用

### 从Git仓库中移除已经追踪的target目录，但保留本地的target目录（不删除本地文件）
git rm -r --cached target

## 放弃修改
### 文件修改
单个文件/文件夹
``` zsh
$ git checkout -- filename
```

所有文件/文件夹
``` zsh
git checkout .
```

### 新增文件
单个文件/文件夹
``` zsh
$ rm filename / rm dir -rf
```

所有文件/文件夹
``` zsh
$ git clean -xdf
```

### 本地修改/新增了一堆文件，已经git add到暂存区，想放弃修改。
单个文件/文件夹：
``` zsh
$ git reset HEAD filename
```

所有文件/文件夹：
``` zsh
$ git reset HEAD .
```

### 本地通过git add & git commit 之后，想要撤销此次commit
``` zsh
$ git reset HEAD~1
```

## 暂存
我们有时会遇到这样的情况，正在dev分支开发新功能，做到一半时有人过来反馈一个bug，让马上解决，但是新功能做到了一半你又不想提交，这时就可以使用`git stash`命令先把当前进度保存起来，然后切换到另一个分支去修改bug，修改完提交后，再切回dev分支，使用`git stash pop`来恢复之前的进度继续开发新功能。

git stash pop：从暂存区恢复最近的一次 stash，应用到工作目录，并删除该 stash。
git stash apply：从暂存区恢复最近的一次 stash，应用到工作目录，但不删除该 stash。

### 不小心在master分支写了代码，怎么切新分支
```bash
git add .
git stash
git checkout -b new_branch_name
git stash pop
```

#### 切分支
忘记切分支，没提交
git checkout -b new
git add .
git commit - m ''
git push origin new 


## 清除已删除的分支
### git branch -a 
命令可以查看所有本地分支和远程分支（git branch -r 可以只查看远程分支）
发现很多在远程仓库已经删除的分支在本地依然可以看到。
``` zsh
git branch -a
  alpha
* dev
feature_ng
  feature_pretty
  master
  test_top
  remotes/origin/alpha
  remotes/origin/alpha_feature_share
  remotes/origin/dev
  remotes/origin/develop
  remotes/origin/learn_pixi
  remotes/origin/master
  remotes/origin/temp_avatar
  ```

### git remote show origin
查看remote地址，远程分支，还有本地分支与之相对应关系等信息。
``` zsh
$ git remote show origin
* remote origin
  Fetch URL: git@code.apowo.com:PixelPai/platform-client.git
  Push  URL: git@code.apowo.com:PixelPai/platform-client.git
  HEAD branch: master
  Remote branches:
    alpha                                        tracked
    dev                                          tracked
    feature_ng                                   tracked
    feature_pretty                               tracked
    master                                       tracked
    refs/remotes/origin/game-core                stale (use 'git remote prune' to remove)
    refs/remotes/origin/learn_pixi               stale (use 'git remote prune' to remove)
    refs/remotes/origin/temp_avatar              stale (use 'git remote prune' to remove)
  Local refs configured for 'git push':
    alpha          pushes to alpha          (up to date)
    dev            pushes to dev            (up to date)
    feature_ng     pushes to feature_ng     (up to date)
    feature_pretty pushes to feature_pretty (up to date)
    master         pushes to master         (local out of date)
```

### git remote prune origin
prune 删除
那些远程仓库已经不存在的分支，根据提示，使用 git remote prune origin 命令：
``` zsh
$ git remote prune origin
Pruning origin
URL: git@code.apowo.com:PixelPai/platform-client.git
 * [pruned] origin/alpha_feature_share
 * [pruned] origin/develop
 * [pruned] origin/feature_maker_avatar
 * [pruned] origin/feature_new_game_cover
 * [pruned] origin/temp_avatar
```

## 再次添加gitlab分支
``` zsh
# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/cordova-plugin-android-keyboard on git:master o [16:56:02] 
$ git remote -v
origin  git@github.com:ApowoGames/cordova-plugin-android-keyboard.git (fetch)
origin  git@github.com:ApowoGames/cordova-plugin-android-keyboard.git (push)

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/cordova-plugin-android-keyboard on git:master o [16:56:07] 
$ git remote add gitlab git@code.apowo.com:opensource/cordova-plugin-android-keyboard.git

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/cordova-plugin-android-keyboard on git:master o [16:56:33] 
$ git status
On branch master
nothing to commit, working tree clean

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/cordova-plugin-android-keyboard on git:master o [16:56:36] 
$ git push gitlab master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 323 bytes | 323.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
To code.apowo.com:opensource/cordova-plugin-android-keyboard.git
   bab51cf..2d1bf8f  master -> master
```

## gitlab 添加插件
``` zsh
$ cordova plugin add git+https://code.apowo.com/opensource/cordova-plugin-android-keyboard 
Installing "cordova-plugin-android-keyboard" for android
Adding cordova-plugin-android-keyboard to package.json
```

## 依赖gitlab项目
yarn add git+https://code.apowo.com/PixelPai/gamecore_pkt.git

yarn add git+ssh://git@code.apowo.com:PixelPai/gamecore_pkt.git
ci 里面加的是ssh的key 来通过gitlab的验证的 你请求的是https://code.apwo.com  如果是你本地 会在命令行中弹出 输入账号密码的提示 来通过http的验证
那么问题来了 你要通过http来请求嘛 如果需要 你去研究一下 怎么通过gitlab 的access-token拉取代码 然后改下ci
如果不需要 就改成通过git请求的；git+ssh

## 丢包问题解决
mac终端
sudo vim /private/etc/hosts

配置域名
199.232.69.194 github.com
13.229.188.59 github.global.ssl.fastly.net

【20240219更新：hosts地址会变，下一次又访问慢】

# 错误
### index.lock
error:
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.

``` zsh
cd .git
rm index.lock
```
应该是windows对进程的管理有个上锁机制，正常情况下，会上锁，进程结束，然后解锁进程。但是由于我强制关闭了运行中的git,导致git崩溃，已经上锁的index.lock没有来得及解锁而仍然存在。当我再用git add的时候，git发现已经存在了index.lock这个文件，导致报错。

### vscode 使用git
error：
git push --set-upstream origin master
执行一下就行

error：
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

wsl 和 windows 的混淆
我不是在wsl code . 启动的vscode
wsl 中的密钥 无法在windows中使用
在windows 生成密钥；命令行提交验证一次，就可以了

### gitignore文件
$ git add .
warning: adding embedded git repository: tooqing-webapp
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint: 
hint:   git submodule add <url> tooqing-webapp
hint: 
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint: 
hint:   git rm --cached tooqing-webapp
hint: 
hint: See "git help submodule" for more information.

``` zsh
git rm --cached tooqing-webapp
git submodule add git@code.apowo.com:PixelPai/tooqing-webapp.git tooqing-webapp
git add .
git commit -m 'cache'
git pull origin dev
```

# vscoed 中应用
### push
#### 暂存所有更改
更改处 '+'

#### 提交已暂存文件
更多操作... > 提交已暂存文件
输入本次提交内容 描述文字

#### 推送 push
更多操作... > 推送

### pull
更多操作... > 拉取


# gitignore
忽略所有 .a 结尾的文件
*.a

但 lib.a 除外
!lib.a

仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO

忽略 build/ 目录下的所有文件
build/

会忽略 doc/notes.txt 但不包括 doc/server/notes.txt
doc/notes.txt

# 依赖git上的库
``` zsh
yarn add git+ssh://git@code.apowo.com:PixelPai/game-core.git#dev
```

# 子模块
## 自模块冲突
git submodule foreach git checkout master //所有子工程切换到master分支
git submodule foreach git pull          //所有子工程更新代码
git add 所有子工程目录
git commit -m "update submodule"      //这里的提交应该是更新commit id
//使其保持最新，与master相同


## 添加
``` zsh
$ git submodule add https://github.com/maonx/vimwiki-assets.git
```

### 指定分支
git submodule add -b rpc git@code.apowo.com:PixelPai/game-core.git src/game-core

## 初始化
``` zsh
$ git submodule update --init
```

## 删除
1、Delete the relevant section from the .gitmodules file.
2、Stage the .gitmodules changes:
   git add .gitmodules
3、Delete the relevant section from .git/config.
4、Remove the submodule files from the working tree and index:
   git rm --cached path_to_submodule (no trailing slash).
5、Remove the submodule's .git directory:
   rm -rf .git/modules/path_to_submodule
6、Commit the changes:
   git commit -m "Removed submodule <name>"
7、Delete the now untracked submodule files:
   rm -rf path_to_submodule



逆初始化模块，其中{MOD_NAME}为模块目录，执行后可发现模块目录被清空
git submodule deinit {MOD_NAME} 
删除.gitmodules中记录的模块信息（--cached选项清除.git/modules中的缓存）
git rm --cached {MOD_NAME} 
提交更改到代码库，可观察到'.gitmodules'内容发生变更
git commit -am "Remove a submodule." 


删除子模块
有时子模块的项目维护地址发生了变化，或者需要替换子模块，就需要删除原有的子模块。

删除子模块较复杂，步骤如下：

rm -rf 子模块目录 删除子模块目录及源码
vi .gitmodules 删除项目目录下.gitmodules文件中子模块相关条目
vi .git/config 删除配置项中子模块相关条目
rm .git/module/* 删除模块下的子模块目录，每个子模块对应一个目录，注意只删除对应的子模块目录即可
执行完成后，再执行添加子模块命令即可，如果仍然报错，执行如下：

git rm --cached 子模块名称

完成删除后，提交到仓库即可。

## 切换分支
git submodule set-branch --branch feature_apk tooqing-webapp

## 子模块中的子模块
```
# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/tooqing-cordova/tooqing-webapp on git:feature_ipad x [16:48:11] 
$ cd public/gdk 

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/tooqing-cordova/tooqing-webapp/public/gdk on git:571cb30 o [16:48:19] 
$ git remote -v
origin  https://code.apowo.com/PixelPai/apowo-jssdk (fetch)
origin  https://code.apowo.com/PixelPai/apowo-jssdk (push)

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/tooqing-cordova/tooqing-webapp/public/gdk on git:571cb30 o [16:48:22] 
$ git remote set url git@code.apowo.com:PixelPai/apowo-jssdk.git
error: Unknown subcommand: set
usage: git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>

    -v, --verbose         be verbose; must be placed before a subcommand


# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/tooqing-cordova/tooqing-webapp/public/gdk on git:571cb30 o [16:50:02] C:129
$ git remote set-url origin git@code.apowo.com:PixelPai/apowo-jssdk.git

# niekaifa @ niekaifadeMacBook-Pro in ~/workspace/apowo/tooqing-cordova/tooqing-webapp/public/gdk on git:571cb30 o [16:50:23] 
$ git remote -v
origin  git@code.apowo.com:PixelPai/apowo-jssdk.git (fetch)
origin  git@code.apowo.com:PixelPai/apowo-jssdk.git (push)
```

# runner
## update
Ubuntu上默认直接安装了gitlab-runner，但其实安装的版本为10.5.0

问题：ci成功，但是没有记录
This job does not have a trace.

原因：版本太低，需要升级
``` zsh
# For Debian/Ubuntu/Mint
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash

# For RHEL/CentOS/Fedora
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash
```
再安装最近版本的gitlab-runner:
apt install gitlab-runner

## commond
gitlab-runner list
ubuntu@gitlab-runner:~$ sudo gitlab-runner list
Runtime platform                                    arch=amd64 os=linux pid=5248 revision=775dd39d version=13.8.0
Listing configured runners                          ConfigFile=/etc/gitlab-runner/config.toml
office-docker-runner                                Executor=docker Token=ab4ebb4e3471ff403c3ea1660db90b URL=https://code.apowo.com/
office internal gitlab-runner on PVE                Executor=shell Token=xtpd6UJrwhKWGi9MXyNa URL=https://code.apowo.com/
pve-ubuntu-test-runner                              Executor=shell Token=dBbekMdeG8nDHLaK1KQU URL=https://code.apowo.com
meshtalk-ci                                         Executor=docker Token=32xMwemzbdqgmENUxePD URL=https://code.apowo.com/
only for android app build                          Executor=docker Token=uHD7nWC4NB12we3AGb5q URL=https://code.apowo.com/

## 安装
sudo curl --output /usr/local/bin/gitlab-runner "https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-darwin-amd64"
给权限
sudo chmod +x /usr/local/bin/gitlab-runner

## 注册
gitlab-runner register
{% asset_img register.png%}

Enter the GitLab instance URL (for example, https://gitlab.com/):
https://code.apowo.com/
Enter the registration token:
zwE8ePU2N8Ngcwanszgq
Enter a description for the runner:
[niekaifadeMacBook-Pro.local]: test
Enter tags for the runner (comma-separated):
test
Registering runner... succeeded                     runner=zwE8ePU2
Enter an executor: virtualbox, docker-ssh+machine, kubernetes, custom, docker-ssh, ssh, docker+machine, docker, parallels, shell:
shell
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 

## 启动
gitlab-runner install
gitlab-runner start

## start runner
``` yml
test-job1:
  tags: 
    - custom01   //一定要指定 tags ，runner注册的时候填的tags
  script:
    - echo "This job tests something"
```
{% asset_img runner.png%}

## unregister
gitlab-runner unregister --name test-runner

## verify
gitlab-runner verify
``` zsh
Verifying runner... is alive                        runner=fee9938e
Verifying runner... is alive                        runner=0db52b31
Verifying runner... is alive                        runner=826f687f
Verifying runner... is alive                        runner=32773c0f
```

### delete
``` zsh
ubuntu@ci-runner:~$ gitlab-runner verify --delete
Runtime platform                                    arch=amd64 os=linux pid=10756 revision=54944146 version=13.10.0
WARNING: Running in user-mode.
WARNING: The user-mode requires you to manually start builds processing:
WARNING: $ gitlab-runner run
WARNING: Use sudo for system-mode:
WARNING: $ sudo gitlab-runner...

ERROR: Verifying runner... is removed               runner=Sf9cFJ7R
Verifying runner... is alive                        runner=UmV1JciW
Updated /home/ubuntu/.gitlab-runner/config.toml
```



## yml 语法
https://segmentfault.com/a/1190000010442764

## CI/CD
CI：Continuous Integration
CD：Continuous Delivery
CD：Continuous Deployment 

## Basic CI/CD workflow
{% asset_img ci.png%}

``` yml
stages:
  - build_compiler
  - build
  - build_dev
  - merge_build_test
  - deploy


before_script:
  - echo "before_scipt"


test:
  stage:
    build_compiler
  tags:
    - test
  script:
    - echo "test"
```

## 本地执行
``` zsh
$  gitlab-runner exec shell test
Runtime platform                                    arch=amd64 os=darwin pid=58199 revision=775dd39d version=13.8.0
Running with gitlab-runner 13.8.0 (775dd39d)
Preparing the "shell" executor
Using Shell executor...
executor not supported                              job=1 project=0 referee=metrics
Preparing environment
Running on niekaifadeMacBook-Pro.local...
Getting source from Git repository
Fetching changes...
Initialized empty Git repository in /Users/niekaifa/workspace/apowo/ci-test/builds/0/project-0/.git/
Created fresh repository.
Checking out bd79ba14 as master...
Skipping Git submodules setup
Executing "step_script" stage of the job script
$ echo "before_scipt"
before_scipt
$ echo "test"
test
Job succeeded
```

## 线上打tag

## 问题
### gitlab: Runner is offline, last contact was about some hours ago
解决：
gitlab-runner restart

### 注册后 



# git-flow
brew install git-flow-avh

git flow version

初始化：
git flow init

Initialized empty Git repository in /Users/savokiss/demos/gitflow/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? [] v
Hooks and filters directory? [/Users/savokiss/demos/gitflow/.git/hooks]

开始新的功能分支
git flow feature start auth

一般都是先提交分支，测试通过后才finish

提交信息规范

提交信息应该描述 “做了什么” 和 “这么做的原因”，主要由 header， body，footer组成。
header的格式：<type>: <subject>

type 用于说明提交的类型：
feature： 新功能
fix: 问题修复
docs: 文档
style: 调整格式（不影响代码运行）
refactor: 重构
test: 增加测试
chore: 构建过程或辅助工具的变动
revert: 撤销以前的提交
scope 用于说明提交的影响范围，内容根据具体项目而定。

完成feature/auth分支
``` zsh
$ git flow feature finish auth
Switched to branch 'develop'
Updating e69b22c..f7f48e2
Fast-forward
 # gitflow | 0
 README.md | 4 ++++
 2 files changed, 4 insertions(+)
 create mode 100644 # gitflow
 create mode 100644 README.md
Deleted branch feature/auth (was f7f48e2).
```

Summary of actions:
- The feature branch 'feature/auth' was merged into 'develop'
- Feature branch 'feature/auth' has been locally deleted
- You are now on branch 'develop'

## 提交信息规范
提交信息应该描述 “做了什么” 和 “这么做的原因”，主要由 header， body，footer组成。
header的格式：<type>: <subject>

type 用于说明提交的类型：
1. feature： 新功能
2. fix: 问题修复
3. docs: 文档
4. style: 调整格式（不影响代码运行）
5. refactor: 重构
6. test: 增加测试
7. chore: 构建过程或辅助工具的变动
8. revert: 撤销以前的提交
9. scope 用于说明提交的影响范围，内容根据具体项目而定。


# 问题
## 提交代码，但github上的绿格子没有变绿
- 检查下在本仓库上的帐号与github上是否一致
- master分支

``` zsh
niekaifa @ Mac-mini in ~/ikyu/KilFront/vue-project on git:master o [15:58:05] 
$ git config user.email                      
kaifawebb@gmail.com

niekaifa @ Mac-mini in ~/ikyu/KilFront/vue-project on git:master o [15:58:02] C:130
$ git config user.email "kaifawebb@gmail.com"
```

## 警告
We found a potential security vulnerability in one of your dependencies
github上删除 package-lock.json

## push慢
https://v2ex.com/t/876241
git config --global http.proxy socks5h://127.0.0.1:7890
git config --global https.proxy socks5h://127.0.0.1:7890

git 底层使用 libcurl 发送 http 请求，而 libcurl 的代理使用 socks5://时会在本地解析 DNS ，应该改成 socks5h://
https://curl.se/libcurl/c/CURLOPT_PROXY.html

## 主机密钥被更改
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
remove with:
ssh-keygen -f "/home/kil/.ssh/known_hosts" -R "github.com"

删除主机根目录 .ssh文件下的 known_hosts
