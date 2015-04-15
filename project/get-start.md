
# 项目入门

春节快要来了，工程师接到一个显示春节倒计时的需求。

工程师开始新建页面：

```bash
$ mkdir countdown && cd countdown
$ touch index.html index.js
```

在 index.html 写上基本的页面结构和样式：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新春倒计时</title>
    <style>
      #count-down-text {
        margin: 200px auto;
        text-align: center;
        color: #F33838;
        font-size: 36px;
      }
    </style>
  </head>
  <body>
    <div id="count-down-text"></div>
    <script src="index.js"></script>
  </body>
</div>
```

工程师对这个需求进行了简单的系分，发现需要用到日期处理模块 [moment](http://spmjs.io/package/moment) 和一个 [util.format](http://spmjs.io/package/util) 格式化方法。这些模块在 [spmjs.io](http://spmjs.io) 上都可以找到，于是他通过 spm 直接安装模块到本地。

```bash
$ spm install moment util --save
```

依赖会保持到 package.json 中：

```javascript
{
  "spm": {
    "dependencies": {
      "moment": "2.9.0",
      "util": "0.10.3"
    }
  }
}
```

然后工程师就可以打开 index.js 进行 JS 应用的编写，文件使用 CommonJS 的格式，使用熟悉的 `require` 引入安装的依赖模块。

```javascript
var moment = require('moment');
var util = require('util');

var newYear = moment([2015, 2, 19]);

calculate();
setInterval(calculate, 1000);

function calculate() {
  // 计算还差几天
  var now = moment();
  var diff = moment.duration(newYear.diff(now));

  document.getElementById('count-down-text').innerHTML =
    util.format(
      '距 2015 年春节还有 %s 月 %s 天 %s 时 %s 分 %s 秒',
      diff.months(),
      diff.days(),
      diff.hours(),
      diff.minutes(),
      diff.seconds()
    );
}
```

接着可以运行 `spm server` 启动服务，并访问 http://127.0.0.1:8000 就可以看到页面了。现在你可以直接修改 index.js 里的内容进行调试（甚至可以调试依赖模块）。

开发完毕，一行命令构建：

```
$ spm build index.js index.html
```

然后会在 `./dist` 目录下得到可运行的 index.js 和 index.html 文件。

实例查看：http://jsfiddle.net/j7d3Ld9x/

以上只是一个极简单的例子。spm 支持各类开发模式和前端语言包括 css、预编译样式语言、模板、React 等，支持通用模块的演示文档部署及内网的源部署方案，对前端的各类调试开发部署模式有很多探索和积淀。对于前端团队还是个人开发者都很友好，值得一试。

