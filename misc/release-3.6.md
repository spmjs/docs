
# SPM 3.6 发布

这个版本的性能、稳定性均有显著提升。而由于改动比较大，所以跳了一个版本，直接发 3.6 。

**修改记录：**
- build 基于 webpack 重新实现
- server, doc 和 test 基于构建重新实现，代替之前使用中间件的方式
- 内置 server
- 只支持 standalone 的打包方式，cmd 方式抽取成 spm-sea，不再内置
- css import 规则变更，@import '~foo' 表示 foo 模块，@import 'foo' 表示 foo 文件，[详](https://github.com/spmjs/spm-sea/issues/2)
- 抽取 spm-argv，统一处理配置参数

**文档：**
- [升级到 3.6](https://github.com/spmjs/docs/blob/master/misc/upgrade-to-3.6.md)
- [例子](https://github.com/spmjs/examples/tree/spm-webpack#examples)
- [项目入门](https://github.com/spmjs/docs/blob/master/project/get-started.md)
- [组件入门](https://github.com/spmjs/docs/blob/master/package/get-started.md)

**感谢：**
- webpack

--

云谦

