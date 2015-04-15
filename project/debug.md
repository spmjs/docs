
# 项目调试

spm3 一个较大的改变是源码书写规范从 CMD 变为 CommonJS ，带来的好处是和社区打通，更接近 nodejs 的开发体验。坏处是 CommonJS 的源码不能像 CMD 一样在浏览器里直接加载，从而影响线下的调试体验。

CommonJS 和 CMD 写法上最大的区别就是 `define(function(require, exports, module) {})` 的包裹，只要在调试阶段无缝的加入这个包裹，就可以比较方便的加载调试了。在 spm 3.6 之前的都是通过这个思路去解决的。

不过，这种方案有个比较大的问题，调试和构建方案不一致。所以潜在的会有调试通过但构建不通过的问题，并且维护上成本也比较高。所以在 spm 3.6 里，我们把调试方案基于构建来实现了。

有两个方案可供选择：

1. `spm build --watch`
2. `spm server`

第一种方案不需要开 server，适用于不方便开 server 的场景；第二种方案需要开 server ，功能更强大。

> @spm-server 老用户：spm server 和 spm-server 不是同一个东西。spm server 是 spm-webpack-server 。

下面主要介绍第二种方案。

## 本地调试

本地调试没啥好说的，就是进入到一个 spm3 的项目目录中，执行 `spm server`。

![](https://t.alipayobjects.com/images/T12PJfXktbXXXXXXXX.png)

然后可以通过参数开启各种附加功能。

![](https://t.alipayobjects.com/images/T15OBfXgNsXXXXXXXX.png)

### livereload

通过 `spm server --livereload` 开启。

![](https://t.alipayobjects.com/images/T1rPReXjpvXXXXXXXX.png)

这时 spm-server 会做两件事：

1. 开启 livereload 服务器
2. 访问 html 页面时会插入 livereload 脚本，用于和服务器通讯实时刷新页面

### weinre

通过 `spm server --weinre` 开启。

![](https://t.alipayobjects.com/images/T1ij0eXcRmXXXXXXXX.png)

和 livereload 一样，spm-server 会做两件事：

1. 开启 weinre 服务器
2. 访问 html 页面时会插入 weinre 脚本，用于和服务器通讯

然后就可以在 weinre 页面上看到当前绑定的设备了：(端口是 8989)

![](https://t.alipayobjects.com/images/T15j4eXoNcXXXXXXXX.png)

关于 weinre 的使用这里就不展开了，可以访问 [weinre 的官网文档](http://people.apache.org/~pmuellr/weinre/docs/latest/UserInterface.html) 来了解。

## 线上调试

线上调试主要是通过 anyproxy 实现。

```bash
## spm server 不直接依赖 anyproxy ，所以第一次使用前需要手动安装
$ npm install anyproxy -g

## 启动 spm server 和 (any)proxy
$ spm server --proxy
```

然后应该能看到下图的提示：(包含 GUI 和 HTTP 代理的端口)

![](https://t.alipayobjects.com/images/T1nPNfXdlcXXXXXXXX.png)

> 注意：第一次使用时应该会提示你安装根证书。

然后就是通过各种方式把请求配置到 HTTP 代理上去，比如 Chrome：

### Chrome

推荐使用扩展程序 [Proxy SwitchySharp](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm?hl=zh-CN)，可以很方便地定制大力规则和情景模式。安装完成后，添加一个情景模式比如 spm：

![](https://t.alipayobjects.com/images/T1jjVeXgpsXXXXXXXX.png)

然后到切换到“切换规则”面板，启用规则切换，加入一条对 alipayobjects.com 的代理规则的配置：

![](https://t.alipayobjects.com/images/T1h68eXd0cXXXXXXXX.png)

> 根据项目的不同，这里可能需要加上你对应的开发环境的代理规则

OK，接下来选择开启 SwitchSharp 的“自动切换模式”，代理的配置就完成了：

![](https://t.alipayobjects.com/images/T1i6VeXidsXXXXXXXX.png)

然后访问 https://a.alipayobjects.com/ ，如果在页面上看到项目目录下的文件列表了，就说明本地环境启动成功了：

![](https://t.alipayobjects.com/images/T1Hn4eXjJXXXXXXXXX.png)

同时在 anyproxy 的监控页面也会看到一条请求记录：

![](https://t.alipayobjects.com/images/T1.PVeXftnXXXXXXXX.png)

### 移动端

1. 常规方法

  ![](https://t.alipayobjects.com/images/T1eP0eXgdmXXXXXXXX.png)

1. 代理 app，比如 Andriod 的 [ProxyDroid](https://play.google.com/store/apps/details?id=org.proxydroid)

