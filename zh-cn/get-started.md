
# 新手入门

## 介绍

[spm](https://github.com/spmjs/spm) 是一套完整的浏览器端组件管理解决方案，包含对于 JavaScript、CSS 和模板的处理。

![SPM LOGO](https://i.alipayobjects.com/i/localhost/png/201404/2YQxOTYoFp.png)

所有 `源：spmjs.io` 上的组件都是以 CommonJS 的方式组织，并可以通过 [seajs](http://seajs.org/) 加载运行。同时，我们基于 [spm](https://github.com/spmjs/spm) 提供了一套完整的组件生命周期管理方案，包含以下特性：

- 初始化
- 依赖安装
- 本地开发
- 发布到 [spmjs.io](http://spmjs.io/)
- 单元测试
- 文档服务
- 构建

[spmjs.io](http://spmjs.io/) 是针对 spm 的组件管理服务。你可以在这里搜索需要的组件，也可以发布组件到这里。如果需要，你还可以搭建自己的私有源服务或镜像。

## 安装

```bash
$ npm install spm -g
```

> 如果遇到安装问题，请先确认 [环境配置](environment.html) 是否正确，以及搜索下 [别人踩过的安装坑](https://github.com/spmjs/spm/search?q=install&type=Issues&utf8=%E2%9C%93)。

## 使用

> 以下是组件开发的使用入门，你也可以直接跳到[项目开发](develop-project/README.html)。

初始化组件：

```bash
$ mkdir example
$ cd example
$ spm init
```

安装依赖：

```bash
$ spm install jquery --save
$ spm install moment@2.6.0 --save
```

发布到 [spmjs.io](http://spmjs.io/)

```bash
$ spm publish
```

> 你可能需要先执行 `spm login` 来获取权限，登录 [spmjs.io](http://spmjs.io) 之后在 http://spmjs.io/account 可以找到 `authkey`。

如果组件包的尺寸过大，可以添加 `.spmignore` 来过滤掉不需要的文件，格式同 [.gitignore](http://git-scm.com/docs/gitignore)。

## 贡献

欢迎通过以下方式来贡献 spm ：

- [Bug reports](https://github.com/spmjs/spm/issues)
- [Feature requests](https://github.com/spmjs/spm/issues)
- [Pull requests](https://github.com/spmjs/spm/pulls)
- 推广 spm 到你的朋友圈
