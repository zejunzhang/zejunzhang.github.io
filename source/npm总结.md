title: "npm总结"
date: 2017-04-02 18:00:00 +0800
update: 2017-04-02 18:00:00 +0800
author: zhengwei
cover: "-/images/npm.svg"
tags:
    - 前端工具
preview: npm可以作为前端库(框架)的下载工具，也可以作为Node.js项目的包管理工具。

---
<!-- TOC -->

- [概念理解](#概念理解)
- [what is package](#what-is-package)
- [what is module](#what-is-module)
- [package和module的关系](#package和module的关系)
- [常见命令总结](#常见命令总结)
- [升级node](#升级node)
    - [mac电脑](#mac电脑)
    - [windows电脑](#windows电脑)
- [npm用不了怎么办](#npm用不了怎么办)
- [semantic versioning](#semantic-versioning)
    - [a.b.c的含义](#abc的含义)
- [在package.json中的体现](#在packagejson中的体现)
- [package.json说明](#packagejson说明)
- [解决下载npm包慢的问题](#解决下载npm包慢的问题)
    - [方式一 使用taobao源](#方式一-使用taobao源)
    - [使用步骤](#使用步骤)
    - [方式二 使用nrm](#方式二-使用nrm)

<!-- /TOC -->
> 本文翻译自`https://docs.npmjs.com`

## 概念理解
- package 是一个被`package.json`描述文件或者文件夹
- module  是一个可以通过`Node.js`的`require`来引用的文件或者文件夹(当然前端的直接通过script引入这里不提)

## what is package
- 一个包含`package.json`的文件夹
- 一个已经放到`npmjs.org`上面的，可以通过`npm install --save <name>@<version>`下载的东西

## what is module
- 包含`package.json`且里面带有`main`属性的的一个文件夹
- 包含`index.js`的文件夹
- 一个JavaScript文件

## package和module的关系
大部分时候我们说二者是等价的，但有一些cli工具型的package不包含main属性是作为前端工具来使用的，所以不算是module

## 常见命令总结

命令 | 含义 
---------|----------
 npm init | 交互式的创建`package.json`文件
 npm init -y| 默认创建`package.json`文件 
 npm install packageName --save、-S | 安装库(框架)、node第三方包,也可以写成npm install --save packageName
 npm install packageName --save-dev、-D | 安装当前项目的前端构建工具等(gulp,babel)
 npm install -g packageName | 全局安装前端工具(browser-sync,gulp-cli,vue-cli,react-cli之类)
 npm uninstall -g、--save|--save-dev | 卸载包
 npm docs packageName | 查看某库(框架)、Node第三方包的官网、描述信息
 npm install -g npm@latest | 更新npm版本到最新(自己没测过，不知是否有效)
 npm shrinkwrap | 锁定你当前安装的npm包的版本
 npm ls | 打印出来所有当前电脑安装的npm包
 npm config list | 我主要是用来查看当前电脑所使用的源地址(registry)
 npm root | 打印出来当前项目文件夹的node_modules的路径
 npm cache clean | 清除npm的缓存
 npm update | 升级本地包
 npm outdated | 查看哪些本地包有更新的版本
 npm update -g packageName | 升级全局包
 npm outdated -g --depth=0 | 查看哪些包有更新的版本


## 升级node
### mac电脑
```
brew install node
```
### windows电脑
直接卸载旧的，安装最新的msi文件

## npm用不了怎么办
重装node的msi软件

## semantic versioning
### a.b.c的含义
- 主版本号.次版本号.修订号
- Bug修复及极其小的改动 --> 增加最后一个数字 1.0.0 --> 1.0.1
- 添加了新的功能特性，但没有破坏旧的API --> 增加中间的数字 1.0.0 --> 1.1.0
- 完全重构，不能向后兼容 --> 增加首尾数字 1.0.0 --> 2.0.0

## 在package.json中的体现
- 打补丁 --> 1.0,1.0.x,~1.0.4
- 小的改动 --> 1,1.x,^1.0.4
- 大的改动 --> * , x

![semver对照表](-/images/semver.png)


## package.json说明

配置项 | 配置说明
---------|----------
 name | 当前包的名字，不能超过214个字符，不能包含.,_,不能有大写字符，不能和核心模块重名，
 version | 当前包的版本号，在npmjs.org上面，名字@版本号一定是唯一的标识，版本号必须符合semver
 description | 关于当前包的功能的描述
 keywords | 当前包的描述的关键词，有利于在npmjs.org进行搜索的时候可以搜索出来 
 homepage | 当前包的官网
 bugs | 如果你的包有bug,别的用户可以在这里提交issue
 license | 指定你的包使用的证书类型
 author | 作者
 contributors | 贡献者 
 files | 指定你的包必须包含的一些文件
 bin | npm会软链接到./node_modules/.bin下面
 main | 指定入口文件，如果没写默认是index.js
 repository | 指定你的包的仓库地址
 scripts | 指定可以执行的脚本 
 config | 可以在scripts的脚本当中，通过npm_package_config_xxx变量来访问 
 dependencies | 依赖项
 devDepencies | 像一些编译coffeescript,less,sass的包都安装在这里面

## 解决下载npm包慢的问题
### 方式一 使用taobao源
[taobao镜像](https://npm.taobao.org/)一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。
### 使用步骤
1. 执行`npm install -g cnpm --registry=https://registry.npm.taobao.org`
2. 把以前`npm install packageName`替换成`cnpm install packageName`

### 方式二 使用nrm
1. 执行`npm install -g nrm`
2. 执行`nrm test`测试哪个镜像源下载速度最快
```
C:\Users\Administrator>nrm test

*  npm ---- Fetch Error
  cnpm --- 364ms
  taobao - 159ms
  nj ----- Fetch Error
  rednpm - 256ms
  npmMirror  Fetch Error
  edunpm - Fetch Error
```
3. 通过测试我们发现，taobao是快，把镜像切换到taobao
```
nrm use taobao
```
4. 以后使用的时候，还是执行`npm install packageName`,但是下载的时候默认会从淘宝镜像去下载

