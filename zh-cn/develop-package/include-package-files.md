
# 引入组件内部文件

在 spm 里，一个组件只允许有一个单一出口，这在某些情况下并不能完全满足需求。

比如 [bootstrap](http://spmjs.io/package/bootstrap) 组件，入口是 `js/bootstrap.js`，而如果要引入 CSS 文件，则需要：

```css
@import 'bootstrap/css/bootstrap.css';
```

或者你仅需要他的 tooltip 功能：

```javascript
require('bootstrap/js/tooltip');
```

比如 CSS 组件 [anima-ui](http://spmjs.io/package/anima-ui)，由很多模块组成，如果用户需要单独引入某一个模块：

```css
@import 'anima-ui/build/util/flexbox.css';
```
