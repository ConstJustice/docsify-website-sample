# package.json

## main
定义了项目的入口点，通常是用于启动项目的文件。它的值通常是项目根目录中的 index.js 文件，但也可以是你选择作为包的主入口的任何文件。如
```
"main": "src/index.js",
```

## name
代表模块的名称，必须字段
 - 可以使用`validate-npm-package-name`来检测模块命名是否规范
 - 可以 npm view  packageName 来查看模块是否被使用
注意：react-router-dom 已经存在，react.router.dom、reactrouterdom 都不可以再创建

## version
版本号，必须字段
SemVer 规范，采用X.Y.Z的格式，其中 X、Y 和 Z 均为非负的整数，且禁止在数字前方补零

 - X 是主版本号(major)：修改了不兼容的 API
 - Y 是次版本号(minor)：新增了向下兼容的功能
 - Z 为修订号(patch)：修正了向下兼容的问题

## description、keywords
description是项目的描述、keywords是项目关键字。当使用npm检索时，会对此两个字段进行检索

## files
files用于描述npm publish 命令后推送到 npm 服务器的文件列表

## private
定义为私有模块，避免发布到公共npm上

## bin
 - bin 字段用来指定各个内部命令对应的可执行文件的位置。
 - 当package.json 提供了 bin 字段后，即相当于做了一个命令名和本地文件名的映射。
 - 调用时需要加入node前缀，如果需要简写，可在执行文件中第一行加入解析声明
```js
#!/usr/bin/env node
```