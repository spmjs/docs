# 环境配置

## 环境准备

### 安装 node

作为一个前端，你需要 node 环境。

推荐使用 [nvm](https://github.com/creationix/nvm) 来安装：

```bash
$ curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | bash
$ nvm install 0.10.24
$ nvm alias default 0.10.24
```

另外，也可以在[官方下载](http://nodejs.org/download/)或[通过包管理工具安装](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager)。

### 去除 sudo

**如果你是用 nvm 来安装的 node，请跳过步骤。**

使用 npm 安装模块的时候经常要输入 sudo，还要输入密码，这点很让人烦躁。下面你可以简单粗暴的去除 sudo（看看作者的[软文](http://howtonode.org/introduction-to-npm)）

``` bash
$ sudo chown -R $USER /usr/local
```

### 安装 git

版本管理工具也是必须的，可以先[了解 git 的相关内容](http://rogerdudler.github.com/git-guide/index.zh.html) 。

git 下载地址如下

 -  [git for mac](https://code.google.com/p/git-osx-installer/downloads/list?can=3&q=&sort=-uploaded&colspec=Filename+Summary+Uploaded+Size+DownloadCount)
 -  [git for windows ](https://code.google.com/p/msysgit/downloads/list?q=full+installer+official+git)

### 安装 spm

```bash
$ npm install spm -g
```

## windows 环境

推荐使用 windows 的包管理工具 [chocolatey](https://github.com/chocolatey/chocolatey)。

安装 nodejs 和 git ：

```
c:\> cinst git.install
c:\> cinst nodejs.install
```

设置环境变量：

```
PATH = C:\Users\{{username}}\AppData\Roaming\npm
NODE_PATH = C:\Users\{{username}}\AppData\Roaming\npm\node_modules
```

