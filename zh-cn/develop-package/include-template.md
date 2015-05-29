
# 引入模板

SPM 支持在 JS 文件里直接引入两种模板：

1. tpl
1. handlebars

以 handlebars 为例，使用步骤为：

1. 新建 `a.handlebars`，编辑模板内容
1. 在 JS 文件里 `require("./a.handlebars");`
1. 调试(spm doc watch 或 spm-server) 和构建时会预编译 `a.handlebars`
1. 构建时如果发现有 require `handlebars` 文件，则会自动安装 `handlebars-runtime` 并保存到 `spm/dependencies`
