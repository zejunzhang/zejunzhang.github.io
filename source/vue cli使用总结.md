title: "vue cli使用总结"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/vue.jpg"
tags:
    - 前端工具
preview: vue项目脚手架

---

<!-- TOC -->

- [安装](#安装)
- [罗列可以使用的starter项目](#罗列可以使用的starter项目)
- [安装webpack-simple类型的starter](#安装webpack-simple类型的starter)
- [安装webpack类型的starter](#安装webpack类型的starter)

<!-- /TOC -->

## 安装
```
npm install -g vue-cli
```

## 罗列可以使用的starter项目
```
vue list
```

```
C:\Users\Administrator>vue list

  Available official templates:

  ★  browserify - A full-featured Browserify + vueify setup with hot-reload, linting & unit testing.
  ★  browserify-simple - A simple Browserify + vueify setup for quick prototyping.
  ★  simple - The simplest possible Vue setup in a single HTML file
  ★  webpack - A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.
  ★  webpack-simple - A simple Webpack + vue-loader setup for quick prototyping.

```

## 安装webpack-simple类型的starter
```
vue init webpack-simple myApp
```

## 安装webpack类型的starter
```
vue init webpack myApp
```