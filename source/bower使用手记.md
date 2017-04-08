title: "bower使用手记"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/bower-logo.svg"
tags:
    - 前端工具
preview: bower是一个用来下载前端的库(框架)的下载器

---
<!-- TOC -->

- [安装](#安装)
- [初始化(交互式创建，默认一路按回车即可)](#初始化交互式创建默认一路按回车即可)
- [安装jquery](#安装jquery)
    - [安装特定版本的jquery](#安装特定版本的jquery)
    - [根据`bower.json`来安装依赖项](#根据bowerjson来安装依赖项)

<!-- /TOC -->
## 安装
```
$ npm install -g bower
```

## 初始化(交互式创建，默认一路按回车即可)
```
$ bower init
```

然后会发现文件夹当中会多出来一个bower.json的文件

```
{
  "name": "demo1",
  "authors": [
    "zhengwei1949 <zhengwei1949@qq.com>"
  ],
  "description": "",
  "main": "",
  "license": "MIT",
  "homepage": "",
  "ignore": [
    "**/.*",
    "node_modules",
    "bower_components",
    "test",
    "tests"
  ],
  "dependencies": {
    "jquery": "^3.2.1"
  }
}
```

## 安装jquery
```
$ bower install jquery
```

### 安装特定版本的jquery
```
$ bower install jquery@1.11.2
```

### 根据`bower.json`来安装依赖项
```
$ bower install
```