
# 组件入门

下面会一步步教你如何通过 [spm](https://github.com/spmjs/spm) 来开发一个组件。

## 脚手架

```bash
$ mkdir now
$ cd now
$ spm init
```

```bash
Creating a spm package:
[?] Package name: (now)
[?] Version: (1.0.0)
[?] Description:
[?] Author: afc163 <afc163@gmail.com>

Initialize a spm package Succeccfully!
```

这样，你就有了一个叫 now 的组件。

## 安装依赖

先安装默认依赖：

```bash
$ spm install
```

然后我们需要 moment 依赖，这里 有他的详细信息。

```
$ spm install moment --save
```

## 开发

编辑 index.js ，和在 nodejs 里一样：

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
var now = require('now');
alert(now); // add this
````
</pre>

## 本地调试

执行 `spm doc` 开启一个文档服务 127.0.0.1:8000 ：

```bash
$ spm doc
```

然后在浏览器里打开 [http://127.0.0.1:8000/examples/](http://127.0.0.1:8000/examples/) 即可看到结果。

你可以在 Markdown 文件里用 3 个 &#96; 来引用代码，也可以用 4 个 &#96; 。

这是一条特殊规则，引用的代码首先会高亮显示，然后还会被插入一个 script 标签来同步执行。这一点非常有用，在调试 demo 的同时，还可以写出优雅的文档。

如果想在 demo 中插入 iframe，需声明代码为 frame 类型：

<pre>
````iframe:600
I am in a iframe of 600px high
````
</pre>

如果不想用 `spm doc` 来调试代码，你还可以试试 spm server 来调试开发模式下的 CommonJS 代码。

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

![](https://t.alipayobjects.com/images/T1GjRfXiBaXXXXXXXX.png)

你也可以在浏览器里打开 [http://127.0.0.1:8000/tests/runner.html](http://127.0.0.1:8000/tests/runner.html) 查看结果。

此外，还可以打开 `coverage/lcov-report/index.html` 查看测试覆盖率。

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

文件名请使用中划线或下划线作为连接符

```
// bad
examples/beforePageCount.md
// good
examples/before-page-count.md
// good
examples/before_page_count.md
```
