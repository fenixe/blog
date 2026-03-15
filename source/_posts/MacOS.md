---
layout: mac
title: OS
date: 2020-03-23 09:33:26
categories:
- MacOS
tags:
- MacOS
---

# Base
## .zshrc
```zsh
# 设置
export OPENAI_API_KEY='your-api-key-here'

# 验证
echo $OPENAI_API_KEY
```

## 工作区设置
### 输入法切换
系统默认快捷键切换
1、Control + 空格键：这是 macOS 默认的快捷方式，能快速在最近使用的两种输入法间切换，比如之前用英文、当前切换后就能直接切到中文。
2、设置大写锁定键切换：若习惯用大写锁定键，可先打开 “系统设置”，找到 “键盘” 选项；在右侧 “文字输入” 中点击 “编辑”，开启 “使用大写锁定键切换（上次所用的拉丁输入法）和当前输入法”，之后按大写锁定键就能快速在英文和中文间切换。
### 鼠标
大屏幕，鼠标跟踪速度调高一点。
系统偏好设置 》 鼠标 》跟踪速度

### 滚动
修改滚动方向，跟windows操作习惯一样。
系统偏好设置 》 鼠标 》滚动方向：自然（不勾选）

### 查看文件图片
点击图片 + 空格键，快速预览图片、视频、PDF等文件。

## 指令
## 打开某软件
open *QQ*

### 在xcode中打开
open platforms/ios/UpdateDemo.xcodeproj

## 中文输入法无选择框
pkill -f SCIM.app

# 系统更新
{% asset_img mac_os.jpeg %}

# brew
[Homebrew](https://github.com/Homebrew/brew)是一款自由及开放源代码的软件包管理系统，用以简化macOS系统上的软件安装过程

brew 是从下载源码解压然后 ./configure && make install ，同时会包含相关依存库。并自动配置好各种环境变量，而且易于卸载。
这个对程序员来说简直是福音，简单的指令，就能快速安装和升级本地的各种开发环境。

而 brew cask 是 已经编译好了的应用包 （.dmg/.pkg），仅仅是下载解压，放在统一的目录中（/opt/homebrew-cask/Caskroom），省掉了自己去下载、解压、拖拽（安装）等蛋疼步骤，同样，卸载相当容易与干净。这个对一般用户来说会比较方便，包含很多在 AppStore 里没有的常用软件。

install
``` zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

版本
``` zsh
$ brew -v
Homebrew 3.6.12
Homebrew/homebrew-core (git revision 250e2930521; last commit 2022-11-29)
```

更新自己
``` zsh
brew update
```

更新某个包时，查看更新信息
``` zsh
brew upgrade -d yarn
```

两种方式安装包
``` zsh
brew install yarn 
curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --version 1.13.0
```

apps path
``` zsh
cd /Applications
```

安装java
``` zsh
brew cask install --verbose --debug java
```

## 安装软件
brew install ffmpeg
brew install wget

## 卸载软件
brew uninstall wget

## 问题
### Updating Homebrew...
解决办法
#### 关闭自动更新
在.zshrc文件中加入下方命令：
``` zsh
export HOMEBREW_NO_AUTO_UPDATE=true
```

#### 替换镜像源加速
我们平时执行brew命令安装软件的时候，跟这三个仓库有关：
```
1.brew.git
2.homebrew-core.git
3.homebrew-bottles
```

使用阿里的Homebrew镜像源代替可以进行加速

##### 替换brew.git
``` zsh
cd "$(brew --repo)"
git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git
```

还原：
``` zsh
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git
```

##### 替换homebrew-core.git
``` zsh
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git
```

还原：
``` zsh
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```

##### 替换homebrew-bottles访问地址
``` zsh
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

还原的话就是删除HOMEBREW_BOTTLE_DOMAIN，上面的是zsh的命令，如果是bash的话请写在.bash_profile文件中。

更新后成功：
``` zsh
$ brew upgrade yarn
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/cask).
==> Updated Casks
karabiner-elements ✔               hex-fiend                          qownnotes
115browser 
```

### instail慢
#### 替换代理
``` zsh
# niekaifa @ niekaifadeMacBook-Pro in ~ [14:40:01] C:130
$ brew cask install adoptopenjdk8 --debug
==> Downloading https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u265-b01/OpenJDK8U-jdk_x64_mac_hotspot_8u265b01.pkg
==> Downloading from https://github-production-release-asset-2e65be.s3.amazonaws.com/140418865/6444de00-d246-11ea-8be7-50169d929f88?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F2
##################                                                        25.7%^C

# niekaifa @ niekaifadeMacBook-Pro in ~ [14:54:50] C:130
$ export ALL_PROXY=127.0.0.1:1087 【注意：该设置仅在当前zsh有效】

# niekaifa @ niekaifadeMacBook-Pro in ~ [14:55:55]
$ brew cask install adoptopenjdk8 --debug
==> Downloading https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u265-b01/OpenJDK8U-jdk_x64_mac_hotspot_8u265b01.pkg
==> Downloading from https://github-production-release-asset-2e65be.s3.amazonaws.com/140418865/6444de00-d246-11ea-8be7-50169d929f88?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20200810%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20200810T065610Z&X-Amz-Expires=300&X-
######################################################################## 100.0%
==> Verifying SHA-256 checksum for Cask 'adoptopenjdk8'.
==> Installing Cask adoptopenjdk8
==> Running installer for adoptopenjdk8; your password may be necessary.
==> Package installers may write to any location; options such as --appdir are ignored.
Password:
installer: Package name is AdoptOpenJDK
installer: Installing at base path /
installer: The install was successful.
package-id: net.adoptopenjdk.8.jdk
version: 1.8.0_265-b01
volume: /
location: Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk
install-time: 1597042784
🍺  adoptopenjdk8 was successfully installed!
```

## 安装gradle
brew install gradle     一直失败

该用二进制文件安装
``` zsh
❯ mkdir /opt/gradle
❯ unzip -d /opt/gradle gradle-6.6-bin.zip
❯ ls /opt/gradle/gradle-6.6
LICENSE  NOTICE  bin  README  init.d  lib  media
```

## 另一种安装APP的方式
```
# 1. 订阅本仓库的 Tap
brew tap lbjlaq/antigravity-manager https://github.com/lbjlaq/Antigravity-Manager

# 2. 安装应用
brew install --cask antigravity-tools
```


# hosts系统文件
Hosts是一个没有扩展名的系统文件，可以用记事本等工具打开，其作用就是将一些常用的网址域名与其对应的IP地址建立一个关联“数据库”，当用户在浏览器中输入一个需要登录的网址时，系统会首先自动从Hosts文件中寻找对应的IP地址，一旦找到，系统会立即打开对应网页，如果没有找到，则系统会再将网址提交DNS域名解析服务器进行IP地址的解析。
``` zsh
sudo vi /etc/hosts

127.0.0.1	www.163.com
```

# 清理内存
sudo purge

# 快捷键
## 显示隐藏文件
shift + command + .

## 截图
截全屏并保存到剪贴板：Shift + Cmmand  + 3  ++ Control
截取选择区域并保存到剪贴板：Shift + Cmmand  + 4  ++ Control

### 自定义截图按键
「苹果图标」→「系统设置」→「键盘」→ 右侧找到「快捷键」→ 点击左侧「屏幕截图」。
Alt + S （S = Screenshot，截图）

# 清理mac
Finder>前往>资源库（按alt显示）

~/Library/Caches

# Xcode
## 问题
## iPhone is not available. Please reconnect the device
Before you debug with iPhone, follow this mapping table about the version of Xcode and iOS：

Xcode 12.2 → iOS 14.2

Xcode 12.1 → iOS 14.1

Xcode 12 → iOS 14

Xcode 11.7 → iOS 13.7

Xcode 11.6 → iOS 13.6

Xcode 11.5 → iOS 13.5

Xcode 11.4 → iOS 13.4

Download at https://developer.apple.com/download/more/.

# 环境变量
``` zsh
# niekaifa @ niekaifadeMacBook-Pro in ~ [16:07:33]
$ printenv
TERM_SESSION_ID=w0t0p0:B9D213B1-A345-4B37-B004-59FF4A1C2236
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.HQ60wnWS6K/Listeners
LC_TERMINAL_VERSION=3.4.4
COLORFGBG=7;0
ITERM_PROFILE=Default
XPC_FLAGS=0x0
LANG=zh_CN.UTF-8
PWD=/Users/niekaifa
SHELL=/bin/zsh
SECURITYSESSIONID=186a7
TERM_PROGRAM_VERSION=3.4.4
TERM_PROGRAM=iTerm.app
PATH=/usr/local/sbin:/usr/local/bin:/Users/niekaifa/bin:/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin:/Users/niekaifa/.oh-my-zsh/custom/plugins/nali:/Users/niekaifa/Library/Android/sdk/tools:/Users/niekaifa/Library/Android/sdk/platform-tools:/bin:/opt/gradle/gradle-6.6/bin
LC_TERMINAL=iTerm2
COLORTERM=truecolor
COMMAND_MODE=unix2003
TERM=xterm-256color
HOME=/Users/niekaifa
TMPDIR=/var/folders/2y/w_dvhyrj543fn4qjvglt4gxh0000gn/T/
USER=niekaifa
XPC_SERVICE_NAME=0
LOGNAME=niekaifa
LaunchInstanceID=41F6AEA0-4EDD-45B6-83B1-CC77E675EB94
__CF_USER_TEXT_ENCODING=0x0:25:52
ITERM_SESSION_ID=w0t0p0:B9D213B1-A345-4B37-B004-59FF4A1C2236
SHLVL=1
OLDPWD=/Users/niekaifa/ikyu/code/cordova-hot-code-push
ZSH=/Users/niekaifa/.oh-my-zsh
PAGER=less
LESS=-R
LC_CTYPE=zh_CN.UTF-8
LSCOLORS=Gxfxcxdxbxegedabagacad
HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles
http_proxy=http://127.0.0.1:1080
https_proxy=http://127.0.0.1:1080
_=/usr/bin/printenv
```

查看terminal 使用的那个
``` 
echo "zsh loaded"
```

# 制作可引导盘
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/Samsung_T5

# nginx
``` zsh
brew -v
brew update
brew install nginx

 /usr/local/etc/nginx/nginx.conf
```

查看nginx的配置信息
brew info nginx

安装目录：/usr/local/Cellar/nginx/1.21.6 (26 files, 2.2MB) *
根目录：Docroot is: /usr/local/var/www
配置文件及默认端口：The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that

nginx将在servers目录下加载所有文件，可以在此目录下启动nginx服务：
nginx will load all files in /usr/local/etc/nginx/servers/.

To restart nginx after an upgrade:
  brew services restart nginx
Or, if you don't want/need a background service you can just run:
  /usr/local/opt/nginx/bin/nginx -g daemon off;

查看nginx安装目录
open /usr/local/etc/nginx/

nginx安装到了哪里？
open /usr/local/Cellar/nginx

work address
/opt/homebrew/etc/nginx/servers/

home address
/usr/local/etc/nginx/servers

## 启动
brew services start nginx // 重启的命令是: brew services restart nginx

brew services reload nginx

http://localhost:8080/
Welcome to nginx! 

# Tools
## Microsoft remote desktop
传输mac和windows之间的文件
https://blog.csdn.net/Xuxiuyun0611/article/details/94432230
{% asset_img img_rd_0.png %}
{% asset_img img_rd_1.png %}
{% asset_img img_rd_2.png %}


# issues
## MacBook M1 brew安装其他软件遇到问题（Error: Cannot install in Homebrew on ARM processor in Intel default prefix (/usr/local)!）的处理方法

打开Finder-> 打开应用程序->打开实用工具->终端
找到终端.app(找到自己用的终端，或者iTerm)，显示简介，把使用 Rosetta打开勾选上，然后重启终端，再运行brew install ，

最后装好了别忘了去掉勾

"departmentId": 9,
"departmentName": "普通内科",
"doctorEthNo": "8623777",
"doctorName": "AAA",
"doctorTitle": "高级",
"doctorTitleId": 3,
"hospitalId": 225471,
"hospitalName": "上海乐静门诊部",
"imgs": [{"url": "https://dev-digilink-cdn.oss-cn-shanghai.aliyuncs.com/2022-05-11/6ce51e1b-b361-4983-942b-05922ab72b72"}],
"msgMobile": null,
"status": "NoSubmit"

## 打不开xxx,因为Apple无法检查其是否包含恶意软件
{% asset_img software.jpg %}

安全性与隐私 -> 允许从以下位置下载的应用 -> 任何来源
如果 “任何来源”被隐藏，输入指令：
sudo spctl --master-disable

## 绕过安全验证（无法安装cocos 1.9.3）
问题：无法打开（App的授权已撤销）
删除软件上的安全验证信息，来达到绕过 MacOS 安全验证。
``` bash
sudo xattr -rd com.apple.quarantine /Users/qkil/Downloads/CocosCreator_v1.9.3_20180704.dmg
```

另外一种方法：重置签名
```bash
sudo codesign --force --deep --sign - <app-path>
成功：<app-path>: replacing existing signature
失败：<app-path>: resource fork,Finder information,or similar detritus not allowed
# 先执行
xattr -cr <app-path>
# 再执行
sudo codesign --force --deep --sign - <app-path>
```

## “CocosCreator”将对您的电脑造成伤害。您应该将它移到废纸篓
解决：访达 -> 应用程序 xxx.App -> 右键 -> 显示简介 -> 勾选 “覆盖恶意软件保护”。

## 删除Microsoft AutoUpdate
访达，“前往”——“前往文件夹”
/Library/Application Support/Microsoft/
直接删除文件夹“MAU2.0”
