
# 配置项

> spm 的项目可通过修改 package.json 来配置构建参数。

所有参数：

```js
{
  "name": "",
  "version": "",

  "spm": {

    "build": {
      // -- 依赖解析
      // 指定不解析的模块或文件
      "global": {
        "react": "React",
        "./a": "AAA"
      },
      // 开启或禁用 node 模块的 polyfills
      "node": {
        "global": false
      },

      // -- 性能
      // 提取依赖为 vendor.js
      "vendor": ["jquery", "underscore"],
      // 提取公共 chunk 为 common.js
      "common": true,
      "base64": {},

      // -- 语言类
      "babel": {},
      "uglify": {},
      "autoprefixer": {},
      "less": {},
      "coffee": {},
      "jsx": {},
      "handlebars": {},

      // -- 输出
      "dest": "./build",
      "hash": true,
      // 提取入口 js 文件依赖链中的 CSS chunk，输出和入口文件同名的 css 文件
      "extractCSS": true,
      // 输出的包名
      "library": "",
      // this, umd, common, amd, var 等等
      "libraryTarget": "",
      // 等同于 libraryTarget: umd, library: Foo
      "umd": "Foo",

      // -- 扩展
      "loader": {
        ".js": "+jsdc-babel"
      },

      // -- 调试
      "define": {
        "DEBUG": false
      }
    },

    "server": {
      "devtool": "#eval",
      "define": {
        "DEBUG": false
      }
    },

    "registry": ""
  }
}
```

## build 配置

### global

指定依赖，他们不会被解析，但会被替换为 window 下的全局变量。

比如：

```js
var $ = require('jquery');
```

配置 `"global":{"jquery":"jQuery"}` 后被构建成：

```js
var $ = window['jQuery'];
```

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/build-global)

### node

配置是否引入 node 相关的补丁。

默认值：

```js
{
  console: false,
  process: true,
  global: true,
  Buffer: true,
  __filename: "mock",
  __dirname: "mock"
}
```

### vendor

配置是否提取依赖包为 vendor.js，默认关闭。

比如：有一个页面 a 依赖了 jquery 和 underscore，配置 `"vendor": ["jquery"]`，则会输出 a.js (包含 underscore) 和 vendor.js (包含 jquery) 。

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/common-pkg)

### common

配置是否提取公用 chunks，默认关闭。

比如：有两个页面 a 和 b，他们同时依赖了 c 。配置 `"common": true` 之后，会输出 a.js, b.js 和 common.js 。

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/common-file)

### base64

配置是否把图片和字体文件转成 base64 ，默认关闭。

举例：

- `"base64": true`，全部转换
- `"base64": {"limit":10000}`，只在文件大小小于 10kb 时转换

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/base64)

### babel

指定 ES6 转换器 babel 的配置项，默认关闭。

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/es6)

注：如果要支持 ie8，一些特性需要额外载入 es5-shim + es5-sham 可以。

- http://babeljs.io/docs/usage/caveats/#internet-explorer

### uglify

配置 uglify 压缩器的选项。

默认值：

```js
sourceMap: false,
output: {
  ascii_only: true,
  comments: false
}
```

### autoprefixer

配置 autoprefixer 的选项。

### dest

配置输出目录，默认为 `./dist` 。

比如：

 - `"dest": "./build"`

### hash

配置输出文件名是否带 hash 后缀。

比如：

- `"hash": true`

### extractCSS

提取 js 入口文件依赖链上的所有 CSS 为同名 CSS 文件，默认关闭。

比如：

- `"extractCSS": true`

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/react)

### library

如果配置了，则作为类库输出，library 为类库名，默认关闭。

### libraryTarget

配置输出格式，默认 "var" 。可选 "var", "this", "commonjs", "commonjs2" "amd", "umd"

### umd

配置输出格式为 umd，并指定类库名。

比如：`"umd": "Foo"` 等同于 `"library": "Foo"` 和 `"libraryTarget": "umd"`

### loader

配置扩展 loader。

比如要对 js 文件做额外处理，处理的文件是 ./loader.js，那么配置：

```js
"loader": {
  ".js": "+./loader"
}
```

比如：

- `"loader": {".js": "+./loader"}`，对 js 文件用 .loader 做额外处理
- `"loader": {".js": "+./loader$"}`，对 js 文件用 .loader 做预处理
- `"loader": {".js": "./loader"}`，对 js 文件只用 .loader 进行处理
- `"loader": {".js": "-jsx2"}`，不对 js 文件进行 jsx 处理

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/custom-loader)

### define

定义环境变量，和 "server" 下的 "define" 配合使用，可区分开发和生产环境。

比如：

```js
"build": {
  "define": {"DEBUG":false}
},
"server": {
  "define": {"DEBUG":true}
}
```

然后代码里：

```js
if (DEBUG) {
  console.log('debug mode');
} else {
  console.log('production mode');
}
```

这样就可以在调试环境下输出 `debug mode`，在生产环境下输出 `production mode` 。

[Demo](https://github.com/spmjs/examples/tree/spm-webpack/define)

## server 配置 

### devtool

默认是 `"devtool": "#sourcemap"` 。

## scripts 配置

## registry 配置

强制指定源，比如 `"registry": "http://private.registry"`

