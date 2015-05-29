# Package.json

`spm` 使用和 `npm` 基本一致的 `package.json` 来描述组件。除了包含一些特殊配置的 `spm` 域之外，其他都和 `npm` 保持一致。

### Fields

Field | Description |
------------ | ------------- |
name* | 组件名，全部小写，以 `-` 或 `.` 分隔单词
version* | 语义化的版本号，比如 1.0.0
description | a brief description of your package
keywords | an array contains keywords
homepage | url of your package's website
author | author of this package: `Hsiaoming Yang <me@lepture.com>` or `{ "name": "Hsiaoming Yang", "email": "me@lepture.com" }`
maintainers | an array of maintainers, just like author
repository | Specify the place where your code lives. `{ "type": "git", "url": "http://github.com/isaacs/npm.git" }`
bugs | The url to your project's issue tracker and / or the email address to which issues should be reported.
license | license
**spm*** |
spm.main | 组件的唯一入口，默认为 `index.js`，如果是一个 css 组件，可以设置为 `index.css`
spm.output | 指定构建输出的文件，以数组表示，支持 glob 格式：`src/**/*.js`
spm.dependencies | 指定依赖组件
spm.devDependencies | 指定开发状态下的依赖组件
spm.tests | 指定测试文件，支持 glob 格式：`tests/*-spec.js`
spm.buildArgs | 配置 `spm build` 的命令行参数
spm.registry | 指定组件发布的目标源，默认为 `http://spmjs.io`
spm.ignore | 发布到源上时需要忽略的文件，以数组表示，功能同 `.spmignore`

### 一个简单的例子

```json
{
  "name": "arale-calendar",
  "version": "1.1.0",
  "description": "Calendar widget.",
  "keywords": [
    "widget",
    "month",
    "datepicker"
  ],
  "author": "Hsiaoming Yang <me@lepture.com>",
  "maintainers": [
    "hotoo <hotoo.cn@gmail.com>",
    "shengyan <shengyan1985@gmail.com>"
  ],
  "homepage": "http://aralejs.org/calendar/",
  "repository": {
    "type": "git",
    "url": "https://github.com/aralejs/calendar.git"
  },
  "bugs": {
    "url": "https://github.com/aralejs/calendar/issues"
  },
  "license": "MIT",
  "spm": {
    "main": "calendar.js",
    "dependencies": {
      "jquery": "1.7.2",
      "moment": "2.6.0",
      "arale-base": "1.1.0",
      "arale-position": "1.1.0",
      "arale-iframe-shim": "1.1.0",
      "handlebars": "1.3.0",
      "arale-widget": "1.2.0"
    },
    "devDependencies": {
      "expect.js": "0.3.1"
    },
    "tests": "tests/*-spec.js",
    "ignore": [
      "dist",
      "_site"
    ],
    "buildArgs": "--ignore jquery"
  }
}
```
