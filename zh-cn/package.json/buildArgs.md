# buildArgs

## 参数列表

Field | Description |
----- | ----------- |
dest | 输出目录，默认为 `dist`
include | 指定打包策略，可选 relative、all、standalone、umd，默认为 `relative`
ignore | 指定不进行 transport 的依赖
skip | 指定不进行分析的依赖
idleading | 模块名前缀，默认为 `{{name}}/{{version}}`
withDeps | 同时打包所有依赖，默认为 `false`

## include

Field | Description |
----- | ----------- |
relative | 打包相对依赖
all | 打包所有依赖
standalone | 打包所有依赖并可自运行
umd | 在 standalone 基础上再添加 `umd wrap`

### 举例说明

比如有一个组件 `a/0.1.0/index.js`：

```javascript
require('./relative');
require('b');
```

include 为 `relative` 时，打包出来是：

```javascript
define('a/0.1.0/index.js', ['a/0.1.0/relative', 'b/0.1.0/index.js'], function() {});
define('a/0.1.0/relative.js', function() {});
```

include 为 `all` 时，打包出来是：

```javascript
define('a/0.1.0/index.js', ['a/0.1.0/relative', 'b/0.1.0/index.js'], function() {});
define('a/0.1.0/relative.js', function() {});
define('b/0.1.0/index.js', function() {});
```

include 为 `standalone` 时，打包出来是：

```javascript
(function(){
var a_0_1_0_index_js, a_0_1_0_relative_js, b_0_1_0_index_js;
b_0_1_0_index_js = (function() {})();
a_0_1_0_relative_js = (function() {})();
a_0_1_0_index_js = (function() {})();
})();
```

include 为 `umd` 时，打包出来是：

```javascript
(function(){
var a_010_index_js, a_010_relative_js, b_010_index_js;
b_010_index_js = (function() {})();
a_010_relative_js = (function() {})();
a_010_index_js = (function() {})();

// umd wrap
if (typeof exports == "object") {
  module.exports = a_010_index_js;
} else if (typeof define == "function" && define.amd) {
  define([], function(){ return a_010_index_js });
} else {
  this["a"] = a_100_indexjs;
}
})();
```

## ignore

还是上面的例子，如果 include 为 `relative` 并且 ignore 为 `b`，打包出来是：

```javascript
define('a/0.1.0/index.js', ['a/0.1.0/relative', 'b'], function() {});
define('a/0.1.0/relative.js', function() {});
```


