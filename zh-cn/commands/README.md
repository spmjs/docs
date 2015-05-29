
# 命令行

`spm` 有一系列的命令来管理组件的生命周期。

下面是简单的列表，你可以执行 `spm help [command]` 查看详细信息。

![](http://gtms01.alicdn.com/tps/i1/TB1x4aMGFXXXXXLXVXXM_30QpXX-830-704.png)

## spm init
通过模板生产组件的脚手架。

## spm login
登录，获取组件发布权限。

## spm install `[name[@version]]`
安装依赖到本地目录。

## spm publish
发布组件。

## spm unpublish `[name[@version]]`
撤销组件发布。

## spm tree
显示组件的依赖树。

## spm info `[name[@version]]`
通过名字查询组件信息。

## spm search `[query]`
搜索组件。

## spm test
通过 phantomjs 跑测试用例。

## spm doc `[build|watch|publish]`
文档管理工具集。

* spm doc build

  构建文档到 `_site` 文件夹。

* spm doc watch

  构建文档，并启动监听服务，地址是：http://127.0.0.1:8000 。

* spm doc publish

  发布 `_site` 文件夹到 [spmjs.io](http://spmjs.io/) ， Demo url 是 `http://spmjs.io/docs/{{package-name}}` 。

## spm build
构建组件。

* -O [dir] `output directory, default: dist`
* --include [include] `determine which files will be included, optional: relative, all, standalone`
  - relative `default`

    Only contain relative dependencies. Absolute dependencies should also be deployed so that it can run on Sea.js.
    ```js
    // would load abc, and abc's dependencies separately.
    seajs.use('abc');
    ```
  - all

    Contain relative and absolute dependencies.
    ```js
    // only need to load abc.
    seajs.use('abc');
    ```
  - standalone

    Build a standalone package that could be used in script tag way without any loader.
    ```html
    <script src="path/to/abc.js"></script>
    ```

* --ignore [ignore] `determine which id will not be transported`
* --idleading [idleading] `prefix of module name, default: {{name}}/{{version}}`

## spm completion
spm 命令自动完成脚本，可通过 `npm completion >> ~/.bashrc  (or ~/.zshrc)` 安装。

