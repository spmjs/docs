
# 升级到 3.6

## 规则变更

- css import 规则变更，@import '~foo' 表示 foo 模块，@import 'foo' 表示 foo 文件，[详](https://github.com/spmjs/spm-sea/issues/2)

比如：

```css
@import 'alice-base';
```

要改成 ：

```css
@import '~alice-base';
```


## 组件开发

主要是 markdown 文件写法变更：

- 只能使用 commonjs 写法，不再支持 cmd 的方式
- 不能 require 相对文件，只能 require 包

比如：

```
seajs.use('./index', 'jquery', function(Dialog, $) {
  new Dialog($('#el'));
});
```

要修改成：

```
var Dialog = require('dialog');
var $ = require('jquery');

new Dialog($('#el'));
```

## 项目开发

主要是配置项变更：

- build 相关的配置项全部移到 build 属性下
- output 中不支持写 css 文件，需通过 `extractCSS` 属性来解决，[Demo](https://github.com/spmjs/examples/tree/spm-webpack/react)
- 更多详见：[配置项](../project/configuration.md)

另外：

- 项目调试使用 `spm server` 而不是 `spm-server`，详见：[调试](../project/debug.md)

