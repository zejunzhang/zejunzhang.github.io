title: "打包sea.js"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
tags:
    - 前端工具
preview: 打包sea.js代码

---
<!-- TOC -->

- [github源码地址](#github源码地址)
- [说明](#说明)
- [package.json示例如下：](#packagejson示例如下)
- [开发阶段代码如下](#开发阶段代码如下)
    - [index.html代码示例](#indexhtml代码示例)
    - [包装jquery.js](#包装jqueryjs)
    - [主模块main.js](#主模块mainjs)
    - [第三方模块a.js代码如下：](#第三方模块ajs代码如下)
- [上线打包阶段](#上线打包阶段)

<!-- /TOC -->
## github源码地址
https://github.com/black-pony/seajs-gulp-pack
## 说明
大家先把我的代码下载下来，对着这篇文档搞明白了再去玩自己的项目，否则会遇到问题的

## package.json示例如下：
```json
{
  "name": "iheima",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.1.1",
    "seajs": "^3.0.2"
  },
  "devDependencies": {
    "gulp": "^3.9.1",
    "gulp-cmd-pack": "^1.0.9",
    "gulp-uglify": "^2.0.0"
  }
}

```

## 开发阶段代码如下
### index.html代码示例
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script src="./node_modules/seajs/dist/sea-debug.js"></script>
    <script>
        seajs.config({
            base:'./js',
            alias:{
                jquery:'../node_modules/jquery/dist/jquery'
            }
        });
        seajs.use('main');
    </script>
</body>
</html>
```

### 包装jquery.js
这块直接拷贝我包装好的文件，不要自己尝试去修改，否则打包好了会报错的

### 主模块main.js
```javascript
define(function(require,module,exports){
    "use strict";
    var a = require('./a');
    $(document).click(function(){
        alert('1');
    });
    console.log(2322);
    console.log(a);
});
```

### 第三方模块a.js代码如下：
```javascript
define(function(require,exports,module){
    "use strict";
    module.exports = {title:22};
});
```

## 上线打包阶段
1. 修改index.html代码如下：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script src="./node_modules/seajs/dist/sea-debug.js"></script>
    <script>
        // seajs.config({
        //     base:'./js',
        //     alias:{
        //         jquery:'../node_modules/jquery/dist/jquery'
        //     }
        // });
        // seajs.use('main');

         seajs.config({
            base:'./dist/'
        });
        seajs.use('main')

    </script>
</body>
</html>
```
2. gulpfile.js如下：

```javascript
"use strict";
var gulp = require('gulp');
var cmdPack = require('gulp-cmd-pack');
var uglify = require('gulp-uglify');
 
gulp.task('cmd', function () {
    gulp.src('./js/main.js') //main文件 
        .pipe(cmdPack({
            mainId: 'main', //初始化模块的id 
            base: './js', //base路径 
            alias: {
                jquery: '../node_modules/jquery/dist/jquery'
            }
        }))
        .pipe(uglify({ //压缩文件，这一步是可选的 
            mangle: {
                except: ['require']
            }
        }))
        .pipe(gulp.dest('./dist'));//输出到目录 
});
 ```