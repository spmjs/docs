
# 私有源

自搭私有源通常有两个目的：

- 保障研发流程的稳定性
- 保证业务组件的私有性

## 单向同步

![](https://t.alipayobjects.com/images/T1r7BcXglTXXXXXXXX.png)

私有源可开启来自公有源 (spmjs.io) 的单向同步。

## 搭建

详见：https://github.com/spmjs/spmjs.io 。然后可以修改 `config/base.yaml` 里的 `sync` 为 `on` 可开启来自 spmjs.io 的单向同步。

## 使用

spm 里所有和源操作相关的命令，都可以添加 `--registry` 参数来指定源路径，比如：

```bash
$ spm publish --registry http://path/to/your-private-registry
```

另外，如果不想每次都多输入 `--registry` 参数，也可以把配置到 spmrc 里：

```bash
$ spm config registry http://path/to/your-private-registry
```
