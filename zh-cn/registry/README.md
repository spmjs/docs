# 源

## 什么是源? 

这里的源指的是 spm 的服务端，即：http://spmjs.io 。所有源上的包都是以 commonjs 或 umd 的形式存在。

## SPM 为什么选择自搭源?

这里有具体的讨论和分析：https://github.com/spmjs/spm/issues/718

另外，个人觉得自搭源最重要的优势是`稳定性`，尤其是对于大公司来说。很难想象研发流程的链路上需要依赖一个外部的不稳定服务，比如随时可能被墙的 github，有速度问题的 npm 。

出于这个考虑，SPM 的源提供了`同步机制`，自己搭建的私有源可以从 spmjs.io 上定时同步。比如在支付宝，就有搭建自己的私有源，从而保证研发流程的稳定。

## 组件池构成

![](https://t.alipayobjects.com/images/T1rANcXhlAXXXXXXXX.png)

如上图。目前源上的组件池主要包含以下 3 部分：

- 业界优秀开源模块 (持续推广和迁移中，详见：[awesome-javascript](https://github.com/sorrycc/awesome-javascript))
- 个人发布模块
- 团队和公司的产品 (通常带前缀，比如 arale-dialog)

欢迎共建组件池。

附：https://github.com/spmjs/spm/wiki/迁移业界优秀模块到-spmjs.io-并反推的简易教程




