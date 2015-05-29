
# spm-server ([source](https://github.com/spmjs/spm-server))

> 如果不喜欢本地启 server 的调试方法，可以试下 [seajs-wrap](https://github.com/seajs/seajs-wrap) 。

基于 [serve-spm](https://github.com/spmjs/serve-spm) 的 SPM3 本地调试工具，同时也内置了一些路径映射，可以很方便地进行线上调试。

## DEMO

在`我的支付宝`页面调试 `arale-tip` 组件：

![](https://t.alipayobjects.com/images/T10QJcXodWXXXXXXXX.gif)

## 安装

```bash
$ npm install spm-server -g
```

## 特性

- 支持 `??` 协议的 `combo` 解析和代理
    
    比如请求 `/??a.js,b.js`，本地只有 `a.js`，没有 `b.js`，则会从 CDN 上获取 `b.js`，和 `a.js` 合并后输出。

- 支持 `livereload`

    通过添加参数 `--livereload` 开启，需和 [Livereload Chrome 插件](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei) 配合使用。

- 支持 `https`

    通过添加参数 `--https` 开启。线上 assets 服务器是 https 协议，且需要调试线上问题时使用。

- 支持 `less` 和 `coffeescript`

    比如，请求 `/a.css` 时会检查 `/a.less` 是否存在，然后实时编译返回。

## 用法

```bash
$ spm-server [OPTIONS]
```

## 选项

- `-p, --port <port>`, 端口号, 默认为：`8000`
- `-b, --base <path>`, base path to access package in production
- `--idleading <idleading>`, 模块名前缀, 默认为：`{{name}}/{{version}}`
- `--https`, 同时开启 https proxy
- `--livereload`, 开启 livereload，需和 [livereload Chrome 插件](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei) 配合使用

## 使用场景

- relative/all
    - [内链引入 seajs，通过 seajs.use 载入所有模块](https://github.com/spmjs/spm-server/blob/master/test/fixtures/normal/normal.html)
    - [内链 combo 引入 seajs 和依赖模块，通过 seajs.use 载入入口模块](https://github.com/spmjs/spm-server/blob/master/test/fixtures/normal/combo_deps.html)
    - [内链 combo 引入 seajs 和所有模块，通过 seajs.use 初始化入口模块](https://github.com/spmjs/spm-server/blob/master/test/fixtures/normal/combo_all.html)
- standalone
    - [单独引入入口模块](https://github.com/spmjs/spm-server/blob/master/test/fixtures/standalone/normal.html)
    - [combo 引入入口模块和其他 JS 文件](https://github.com/spmjs/spm-server/blob/master/test/fixtures/standalone/combo.html)
    - [base 不是根目录](https://github.com/spmjs/spm-server/blob/master/test/fixtures/standalone/taobao.html)，运行 `spm-server` 时指定 `base`

## 路径规则

详见：[spmjs/serve-spm#2](https://github.com/spmjs/serve-spm/pull/2)

```
# 目录结尾，自动查找 index.htm 和 index.html
- /$ -> index.htm, index.html

# 当前 pkg 的 dist 目录下的文件，代理到源码
- ^/dist/curr_name/curr_version/a.js -> /a.js

# 依赖模块的请求，先找 dist 下的(基于性能上的考虑)，再照 spm_modules 下的
- ^/name/version/a.js -> /dist/name/version/a.js
- ^/name/version/a.js -> /spm_modules/name/version/a.js

# handlebars 处理
- ^handlebars-runtime.js, ^/dist/cjs/handlebars.runtime.js -> hanelebars.runtime.js

# js require css 和 tpl 文件的处理
- a.css.js^ -> a.css, a.tpl.js -> a.tpl, ...

# 预编译语言，目前支持 less 和 coffeescript
- a.js^ -> a.coffee
- a.css^ -> a.less
```


## FAQ

* 部分文件我不想加 cmd wrap 怎么办? 

    url 添加 `nowrap` 参数，比如 `/a.js?nowrap`。

* 和 `spm doc watch` 有什么区别?

    `doc watch` 面向组件开发。基于 nico，所以支持 markdown 解析，启动时会先生成 _site 目录，然后基于 _site 目录启动服务器。`spm-server` 面向应用开发。不生成额外的目录，支持一些常用的应用开发功能，比如 `livereload`, `https server`, `cdn combo proxy` 等。

