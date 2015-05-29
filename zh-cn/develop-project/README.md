# 项目开发

> 由于目前 spm 更侧重于解决组件方面的问题，项目开发的工具（比如 [spm-server](https://github.com/spmjs/spm-server) 、部署、项目的脚手架等) 并没有内置到 spm 中，需额外安装。

## 演示

![](http://gtms04.alicdn.com/tps/i4/TB1iN.pGXXXXXa3XpXXDs3XUXXX-699-360.gif)

## 基本流程

1. 建 package.json
2. 开发和用 `spm install` 安装依赖
3. 用 `spm-server` 调试
4. 部署和发布

## 目录结构

```
helloworld
  ├─ dist/         (构建生成的目录，用于发布和部署)
  ├─ spm_modules/  (依赖组件安装后所在目录)
  ├─ index.js
  ├─ index.css
  ├─ index.html
  ├─ package.json  (配置文件，详见 package.json/README.html)
```

## 开发

编辑 `package.json`：

```javascript
{
  "name": "helloworld",
  "version": "0.1.0",
  "spm": {
    "output": [
      "index.js",
      "index.css"
    ],
    "buildArgs": "--include standalone"
  }
}
```

> output 用于声明哪些文件需要构建，buildArgs 用于配置构建选项，详见 [package.json](../package.json/README.md) 。

编辑 `index.js`：

```javascript
var $ = require('jquery');
$('body').append('<div>Hello World!</div>');
```

编辑 `index.css`：

```css
@import 'normalize.css';
div {
  color: red;
}
```

编辑 `index.html`：

```html
<link rel="stylesheet" href="index.css" />
<script src="index.js"></script>
```

## 安装依赖

在项目目录中执行命令：

```bash
$ spm install jquery normalize.css --save
```

spm install 命令会从 `源：spmjs.io` 上下载依赖的组件，并保存到 `spm_modules` 下，结构如下：

```
spm_modules
  ├─ jquery/2.1.1/
  ├─ normalize.css/3.0.1/
```

## 本地调试

`spm-server` 是 spm 的本地调试工具之一，封装了不少常用的调试功能。比如 `livereload`, `https`，`less` 和 `coffee` ，详见 [spm-server 文档](spm-server.md) 。

```bash
$ npm install spm-server -g
$ spm-server
         server: listen on 8000
```

启动成功后，在浏览器里打开 http://localhost:8000 即可看到效果。

> 通过 `spm-server --livereload` 可开启 livereload 模式 (监听文件改动并自动刷新)

## 构建

在项目目录中执行命令：

```bash
$ spm build
```

该命令会分析 package.json，对 output 中指定的文件进行 CMD 转换、压缩等处理，然后输出到 `dist` 目录。

构建后 `dist` 的目录结构如下：

```bash
dist
  ├─ helloworld/0.1.0/
    ├─ index-debug.css
    ├─ index-debug.js
    ├─ index.css
    ├─ index.js
```

> `dist` 目录路径中会包含版本号，通过版本化的非覆盖式发布可解决静态资源缓存更新、灰度发布、快速回滚、保留历史版本等问题。

## 部署和发布

`dist` 下的文件是用于发布的，把里面的文件传到服务器上即可。

> 如果需要 zip 包，可执行 `spm build --zip` 命令，在构建之后自动压缩 dist 目录。

## Congratulation

至此，你应该已学会如何用 spm 构建一个简单的项目了吧。继续阅读：

* [应用 bootstrap](develop-project/using-bootstrap.md)
* [spm-server 使用文档](develop-project/spm-server.md)

