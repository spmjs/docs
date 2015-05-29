# 引入 CSS

> spmjs.io 上有不少 CSS 组件，比如 [normalize.css](http://spmjs.io/package/normalize.css) 和 `alice` 系列的 UI 组件。

和 JS 一样，你可以通过 `@import` 引入源上的 CSS 组件或本地的 CSS 文件。

```css
@import 'normalize.css';
@import './layout/layout.css';

body {
  color: teal;
  background: url('./background-image.jpg');
}
```

此外，spm 还提供了在 JS 里引入 CSS 的功能。

```javascript
@require('alice-box');
@require('./theme/basic.css');
```

> 通过这种方式引入 CSS 之后，构建时候会自动安装 [import-style](http://spmjs.io/package/import-style)，来加载 CSS 。

