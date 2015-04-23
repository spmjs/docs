# 指定依赖

package.json 中 `spm.build.global` 指定依赖，他们不会被解析，但会被替换为 window 下的全局变量。

比如：

```js
var $ = require('jquery');
```

配置 `"global":{"jquery":"jQuery"}` 后被构建成：

```js
var $ = window['jQuery'];
```

你可以利用 global 避免打包一些基础模块，比如 `jQuery`  `underscore.js` 。

## 开发指定依赖 jQuery 项目


### 创建目录和文件
```
$ mkdir build-global && cd build-global
$ touch index.html index.js package.json
```
> Windows 用户请创建 build-global 目录，进入 build-global目录创建 `index.html` 、 `index.js` `package.json` 文件

### 准备HTML
在 index.html 写上基本的页面结构和样式：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>使用 spm 开发指定依赖 jQuery 的项目</title>
    <style>
        #box {
            width: 100px;
            height: 100px;
            background-color: #ABCDEF;
        }
    </style>
</head>
<body>
    <div id="box"></div>
	<script src="lib/jquery.min.js"></script>
    <script src="index.js"></script>
</body>
</html>
```

### 声明依赖

在 `package.json` 中写入：

```js
{
  "spm": {
    "build": {
      "global": {
        "jquery": "jQuery"
      }
    }
  }
}
```

### 下载 jquery.min.js 至 lib 目录
[https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js](https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js)

此时目录结构为：
```
└── lib/
│   └── jquery.min.js
├── index.html
├── index.js
└── package.json
```
### 编写 index.js

```
var $ = require('jquery');
$(function (){
    $('#box').hide(333).show(333);
})
```

### 调试代码

调试开发模式下的 CommonJS 代码：
```
$ spm server
```
打开 [http://127.0.0.1:8000/](http://127.0.0.1:8000/) 预览效果

### 构建项目
开发完毕，一行命令构建：

```
$ spm build index.js index.html
```

构建后的目录结构为：
```
└── dist/
	├── index.html
    └── index.js
└── lib/
│   └── jquery.min.js
├── index.html
├── index.js
└── package.json
```

[dist/index.js](https://github.com/spmjs/examples/blob/master/build-global/dist/index.js) 文件内容为:

```js
!function(r){function o(e){if(t[e])return t[e].exports;var n=t[e]={exports:{},id:e,loaded:!1};return r[e].call(n.exports,n,n.exports,o),n.loaded=!0,n.exports}var t={};return o.m=r,o.c=t,o.p="",o(0)}([function(r,o,t){var e=t(1);e(function(){e("#box").hide(333).show(333)})},function(r,o,t){r.exports=jQuery}]);
```

[查看更多配置项](https://github.com/nimojs/docs/blob/master/project/configuration.md)