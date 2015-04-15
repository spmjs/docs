
# 环境准备

## 安装 Node

`Node.js` 支持 >= 0.10.29, 建议安装 >= 0.12.0

#### osx, linux 环境

```bash
$ git clone git@github.com:creationix/nvm.git ~/.nvm
$ source ~/.nvm/nvm.sh
# 安装
$ nvm install v0.12.0
# 显示当前本地安装的所有 Node.js
$ nvm ls 
# 显示服务器所有可用的 Node.js
$ nvm ls-remote
# 本地可用的 Node.js 中使用 0.12.0
$ nvm use 0.12.0
# 设置每次启动默认版本
$ nvm alias default 0.12.0
```

### window 环境

这里假设大家都使用 `d:\git` 目录存放 git 项目。

```bash
$ d:
$ cd git
$ git clone git@github.com:nanjingboy/nvmw.git
# 设置 d:\git\nvmw 墓道到 PATH 环境变量
$ set "PATH=d:\git\nvmw;%PATH%"
# 安装
$ nvmw install 0.12.0
# 显示当前本地安装的所有 Node.js
$ nvmw ls 
# 显示服务器所有可用的 Node.js
$ nvmw ls-remote
# 本地可用的 Node.js 中使用 0.12.0
$ nvmw use 0.12.0
# 设置每次启动默认版本
$ nvmw switch 0.12.0
```

## 安装 SPM

```bash
$ npm i spm -g
```

如遇因网速原因导致的安装失败，可尝试使用 [cnpm](http://cnpmjs.org/) 的源加速安装。

```bash
$ npm i spm -g -r http://r.cnpmjs.org/
```

