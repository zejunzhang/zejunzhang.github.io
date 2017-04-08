title: "gulp总结"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/iruTC031_400x400.png"
tags:
    - 前端工具
preview: gulp是一个用来前端的工作流构建工具。

---

<!-- TOC -->

- [四大api](#四大api)
- [使用gulp的步骤](#使用gulp的步骤)
- [使用gulp压缩css --> gulp-cssnano 或者 gulp-cssmin](#使用gulp压缩css----gulp-cssnano-或者-gulp-cssmin)
- [使用gulp合并css --> gulp-concat](#使用gulp合并css----gulp-concat)
- [使用gulp 压缩合并css](#使用gulp-压缩合并css)
- [使用gulp压缩js --> gulp-uglify](#使用gulp压缩js----gulp-uglify)
- [使用gulp合并js --> gulp-concat](#使用gulp合并js----gulp-concat)
- [使用gulp压缩合并js --> gulp-uglify + gulp-concat](#使用gulp压缩合并js----gulp-uglify--gulp-concat)
- [使用gulp压缩html --> gulp-htmlmin](#使用gulp压缩html----gulp-htmlmin)
- [使用gulp进行监视文件的改变 --> gulp.watch](#使用gulp进行监视文件的改变----gulpwatch)
- [常用gulp插件](#常用gulp插件)

<!-- /TOC -->

![gulp功能一览图](-/images/1245223-f1682d270e570f41.jpg)

## 四大api
- gulp.src 指定要处理的文件的路径

```javascript
gulp.src('client/templates/*.jade')
    .pipe(jade())
    .pipe(minify())
    .pipe(gulp.dest('build'));
```

```javascript
gulp.src('client/*.js','client/bad.js'')
```

- gulp.dest 指定把处理的文件放到哪个文件夹
- gulp.task 指定任务名

```javascript
gulp.task('someTaskName',function(){

});
```

- gulp.watch 类似于事件，当监视的文件发生改变的时候，触发后面的回调函数

## 使用gulp的步骤
![gulp工作流](-/images/gulp-cli.png)

## 使用gulp压缩css --> gulp-cssnano 或者 gulp-cssmin
[文档地址](https://github.com/chilijung/gulp-cssmin/)

```javascript
var gulp = require('gulp');
var cssmin = require('gulp-cssmin');
gulp.task('default',function(){
    gulp.src('src/**/*.css')
        .pipe(cssmin())
        .pipe(gulp.dest('dist'));
});
```
## 使用gulp合并css --> gulp-concat

```javascript
var concat = require('gulp-concat');
gulp.task('scripts',function(){
    gulp.src('./lib/*.js')
        .pipe(concat('all.js'))
        .pipe(gulp.dest('./dist/'));
});
```

## 使用gulp 压缩合并css 
顺序：先合并再压缩

## 使用gulp压缩js --> gulp-uglify

## 使用gulp合并js --> gulp-concat

## 使用gulp压缩合并js --> gulp-uglify + gulp-concat

## 使用gulp压缩html --> gulp-htmlmin

## 使用gulp进行监视文件的改变 --> gulp.watch

## 常用gulp插件

插件名称 | 作用 
---------|----------
 gulp-uglify  | js压缩
 gulp-minify-css | css压缩 
 gulp-minify-html | html压缩
 gulp-jshint | js代码检查
 gulp-concat | 文件合并
 gulp-less | 编译less
 gulp-sass | 编译sass
 gulp-imagemin | 压缩图片
 gulp-autoprefixer | css自动加前缀
  