title: "browser-sync总结"
date: 2017-04-03 9:00:00 +0800
update: 2017-04-03 9:00:00 +0800
author: zhengwei
cover: "-/images/brower-sync.jpg"
tags:
    - 前端工具
preview: browser-sync是一个用来提高我们异步测试浏览器兼容性的工具。

---
<!-- TOC -->

- [安装](#安装)
- [演示代码](#演示代码)
- [使用命令](#使用命令)
- [测试](#测试)
- [使用注意事项](#使用注意事项)

<!-- /TOC -->
## 安装
```
npm install -g browser-sync
```

## 演示代码
index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
    <style>
        #demo{
            display: none;
        }
    </style>
</head>
<body>
    <input type="button" value="点击弹框" id="btn">
    <div id="demo">
        点击显示隐藏内容
    </div>
    <script>
        window.onload = function(){
            var oDemo = document.querySelector('#demo');
            var oBtn = document.querySelector('#btn');
            oBtn.addEventListener('click',function(){
                oDemo.style.display = 'block';
            },false);
        }
    </script>
</body>
</html>
```

style.css
```css
body{
    background:red;
}
```

## 使用命令
```
browser-sync start --server --files "*.*"
```

## 测试
1. 点击按钮
2. 把style.css中的background改成其他颜色，观察页面的反应

## 使用注意事项
- 文件名一定要用双引号，不要用单引号
- html文件一定要有骨架结构