# 组件开发

下面会一步步教你如何通过 [spm](https://github.com/spmjs/spm) 来开发一个组件。

```
$ spm -v
3.x.x
```

开始前，请确保安装了 spm@3.x 。

## init

```bash
$ mkdir now
$ cd now
$ spm init
```

```
Creating a spm package:
[?] Package name: (now)
[?] Version: (1.0.0)
[?] Description:
[?] Author: afc163 <afc163@gmail.com>

Initialize a spm package Succeccfully!
```

这样，你就有了一个叫 `now` 的组件。

## 安装依赖

先安装默认依赖：

```bash
$ spm install
```

然后我们需要 [moment](http://momentjs.com) 依赖，[这里](http://spmjs.io/package/moment) 有他的详细信息。

```bash
$ spm install moment --save
```

## 开发

编辑 `index.js` ，和在 nodejs 里一样：

```javascript
var moment = require('moment');
var now = moment().format('MMMM Do YYYY, h:mm:ss a');

module.exports = now;
```

然后编辑 `examples/index.md`:

<pre>
# Demo

---

## Normal usage

````javascript
seajs.use('index', function(now) {
  alert(now); // add this
});
````
</pre>

## 本地调试

执行 `spm doc watch` 开启一个文档服务 `127.0.0.1:8000` ：

```bash
$ spm doc watch
```

然后在浏览器里打开 [http://127.0.0.1:8000/examples/](http://127.0.0.1:8000/examples/) 即可看到结果。

你可以在 Markdown 文件里用 3 个 &#96; 来引用代码，也可以用 4 个 &#96; 。

这是一条特殊规则，引用的代码首先会高亮显示，然后还会被插入一个 script 标签来同步执行。这一点非常有用，在调试 demo 的同时，还可以写出优雅的文档。

如果想在 demo 中插入 iframe，需声明代码为 `frame` 类型：

<pre>
````iframe:600
I am in a iframe of 600px high
````
</pre>


> 如果不想用 `spm doc watch` 来调试代码，你还可以试试 [seajs-wrap](https://github.com/seajs/seajs-wrap) 或 [spm-server](https://github.com/spmjs/spm-server/) 来调试开发模式下的 `CommonJS` 代码。

## 添加测试用例

编辑测试文件 `tests/now-spec.js`，我们默认引用了一个断言方案 [expect.js](http://spmjs.io/package/expect.js) 。

```javascript
var expect = require('expect.js');
var now = require('../index');

describe('now', function() {

  it('normal usage', function() {
    expect(now).to.be.a('string');  // add this
  });

});
```

看看测试结果：

```bash
$ spm test
```

你也可以在浏览器里打开 [http://127.0.0.1:8000/tests/runner.html](http://127.0.0.1:8000/tests/runner.html) 查看结果。

## 发布

现在你已拥有一个包含完整功能和完善测试用例的组件里，尝试把他发布到 [spmjs.io](http://spmjs.io/) 吧。

```bash
$ spm publish
```

你应该要先执行 `spm login` 来获取权限，否则会提示验证失败。

```bash
$ spm login
```

`username` 是你的 github 账号，而 `authkey` 可以在你登陆后在 http://spmjs.io/account 找到。

> 当然，组件 `now` 是我发布的。你应该先改个名字然后重新试一次。

## 文档

spmjs.io 可以托管组件文档。你只需要编辑 `README.md` 和 `examples` 目录，通过 `spm doc watch` 预览，然后发布到 spmjs.io.

```bash
$ spm doc publish
```

最新版文档的 url 是 `http://spmjs.io/docs/{{name}}/` ，也可以通过 `http://spmjs.io/docs/{{name}}/{{version}}/` 访问到所有版本。

比如：http://spmjs.io/docs/now/ 。

## 构建

```bash
$ spm build
```

`spm build` 命令会构建 `spm.main` 和 `spm.output` 声明的文件到 `dist` 目录。`spm.buildArgs` 会作为参数传入。

默认的构建结果是可以被部署到 cdn 上的包。然后可以通过 [Sea.js](https://github.com/seajs/seajs/) 来引用他。比如：[seajs@2.2.1](https://raw.githubusercontent.com/seajs/seajs/2.2.1/dist/sea.js) 。


```html
<script src="http://cdn.example.com/path/to/sea.js"></script>
<script src="http://cdn.example.com/path/to/seajs-combo.js"></script><!-- If your need that -->
<script>
  seajs.config({
    base: 'http://cdn.example.com/',
    alias: {
      now: 'now/1.0.0/index.js'
    }
  });
  // load http://cdn.example.com/??now/1.0.0/index.js,moment/2.6.0/moment.js
  seajs.use(['now'], function(now) {
    console.log(now);
  });
</script>
```

你也可以添加参数来构建 [standalone](/documentation/spm-commands#spm-build) 的包。

```bash
$ spm build --include standalone
```

```html
<!-- use it without loader -->
<script src="http://cdn.example.com/path/to/standalone.js"></script>
```

## Congratulation

至此，你应该已学会如何用 spm 开发一个组件，欢迎发布组件到这里！继续阅读：

* [引入 CSS](develop-package/include-css.md)
* [引入模板](develop-package/include-template.md)
* [引入组件内部文件](develop-package/include-pkg-files.md)
