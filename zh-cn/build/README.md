# 构建

> 如果你不喜欢 cmd ，还可以自行写构建工具实现基于模块规范的输出

## `$ spm build`

目前内置的 `spm build` 命令适用于组件和简单项目，功能包含：

- 转换 commonjs 为 cmd 模块 ([gulp-transport](https://github.com/popomore/gulp-transport))
- [spm-standalonify](https://github.com/spmjs/spm-standalonify)
- [uglifyjs](https://github.com/mishoo/UglifyJS2)
- [cssmin](https://github.com/jakubpawlowicz/clean-css)
- ...

## 使用

```bash
$ spm build
```

## 扩展

对于有自定义需求的复杂项目，或者使用了预编译语言比如 less, coffee 的项目，则需自行基于 spm 提供的基础库实现构建流程。

附：[一个构建的例子](https://gist.github.com/sorrycc/809594fa344ad4a30a42) ，功能包含：

- less, coffee 的预编译支持
- pathmap 自定义输出路径
- 自定义任务和流
- autoprefixer
- ...
