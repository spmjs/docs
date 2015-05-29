
# SPM 3.6 发布

大家好，

这个版本的性能、稳定性均有显著提升。而由于改动比较大，所以跳了一个版本，直接发 3.6 。

![](https://t.alipayobjects.com/images/T1x5RfXi4nXXXXXXXX.png)

主要有以下改动：

**(1) 基于 webpack 重新实现了 build**

- 性能更快：比如钉钉的项目从之前的 `200s` 缩短到 `52s`，经过配置后最后到 `38s`
- 功能更强大：比如公用包和文件的提取，动态依赖、循环引用、node 模块补丁等，详见 [配置项](https://github.com/spmjs/docs/blob/master/project/configuration.md) 和 [案例](https://github.com/spmjs/examples/tree/spm-webpack)
- 扩展性更好：比如这样配置 `"loader": {".js":"+./foo"}`，即可对所有 js 文件用本地的 `foo.js` 进行额外处理，[Demo](https://github.com/spmjs/examples/tree/spm-webpack/custom-loader)

**(2) doc, server 和 test 基于 build 实现**

之前是基于中间件实现的，和 build 的流方式是两套。所以，调整方案之后：

- 稳定性更好：不会存在调试通过后，构建出来的代码有问题的情况
- 维护成本更低：仅需维护一套方案
- 文档静态化：doc 生成的文档终于静态化了，可部署到任意地方

**此外，还有一些其他的变更点：**

- 内置 server ：不再需要额外安装命令就可进行项目调试了
- [spm-sea](https://github.com/spmjs/spm-sea)：spm 只内置 standalone 方式的打包，cmd 方式抽取成 spm-sea，不再内置
- css 包规则变更：`@import '~foo'` 表示 foo 模块，`@import 'foo'` 表示 foo 文件，[讨论](https://github.com/spmjs/spm-sea/issues/2)

**文档教程：**
- [升级到 3.6](https://github.com/spmjs/docs/blob/master/misc/upgrade-to-3.6.md)
- [例子](https://github.com/spmjs/examples/tree/spm-webpack#examples)
- [项目入门](https://github.com/spmjs/docs/blob/master/project/get-started.md)
- [组件入门](https://github.com/spmjs/docs/blob/master/package/get-started.md)

**感谢：**
- webpack

最后，有升级或迁移到 spm 的想法，都可以找 @云谦 聊下。

--

云谦

