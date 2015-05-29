
# 应对不同的项目类型

由于业务类型的不同，以及前端技术的发展，我们现在要面对各种项目的类型。有些是单页应用，有些是多页应用，多页应用可能还要考虑页面之间的缓存共用，等等。

而针对这些问题，SPM 提供了 `include` 和 `ignore` 这两个构建参数(详见：[buildArgs](../package.json/buildArgs.md) )。通过他们的组合，理论上可以满足各种项目类型的需要。

## 单页应用和不太在意性能的多页应用

推荐用 `--include standalone`，这种方式会把所有的依赖都打包到一起，并且可以自运行且无需 loader 。

HTML 里的使用方法：

```html
<script src="entry.js"></script>
```

## 在意性能的多页应用

上面这种方式处理多页应用时会有一定量的冗余。

比如有两个页面，每个页面都依赖 jQuery，用上面的方式会把 jQuery 打包到各自的输出文件里，这样 jQuery 就不能在两个页面间公用缓存了。

这时推荐用 `--include all --ignore jquery`，构建时会打包除 jquery 外的所有依赖为 CMD 模块，通过 seajs 载入运行。ignore 的 jquery 可以通过 seajs 的 alias 配置指定具体的版本。

HTML 里的使用方法：

```html
<script src="seajs/2.2.0/seajs.js,jquery/1.7.2/jquery.js"></script>
<script>
seajs.config({
  alias: {
    'jquery': 'jquery/1.7.2/jquery.js'
  }
});
seajs.use('entry.js');
</script>
```

## 其他

- 还可以选择 `--include relative` 的方式，构建时只会包含相对目录的本地文件，不会包含依赖。所以所有的依赖组件都需要被发布到 cdn 上。

## 延伸阅读

- [standalone 支持 umd 方案整理](https://github.com/spmjs/spm/issues/892)
