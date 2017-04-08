---

title: "如何写简历"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/vue.jpg"
tags:
    - 面试技巧
preview: 如何写简历

---
## 复习
### git
- 管理代码，版本控制的一个软件
### 集中式、分布式
- git是分布式
### git两个概念
- 工作区、暂存区、仓库
- 分支
### git常用命令
- git init
- git commit -a -m "" 修改过的文件提交到仓库
- git add .
- git status红色
- git commit
- git branch 新的分支名
- git checkout 分支名
- git checkout master
- git merge
- 自动合并
- 冲突：手动
- git add --> git commit
- 全局配置git config --global user.name ,user.email
- git diff
- git log --oneline
- git reflog
- git reset --hard 版本号
- git remote add origin 远程地址  var origin = 远程地址
- git push -u origin master(第一情况用-u,第二情况不用-u,.git文件夹找一个.config文件)
- git push


### 课程安排
- git
- npm
- browser-sync
- gulp

太麻烦
--> 简化



博客
项目

push推 pull 拉



git init
git pull 远程地址 master
....
git pull 远程地址 master
git push



confilct冲突
二个版本文件同一行不一样

rejected：远程服务器上的代码比本地的代码要新，不管代码是不是一模一样

第一种情况：远程服务器代码和本地一模一样 --> 
第二种：同一个文件的同一行代码 冲突
第三种情况：改的是不同的文件 


toriseGit
toriseSVN
angular英语

1.2.x

vue --> 中文文档




### 使用小海龟
第一步、配置ssh puttygen(只需要一个电脑配置一次)

第二步、克隆代码
第三步、执行git同步 --> 拉取


git clone 远程地址
git pull



git add --> git commit --> git pull --> git push


鼠标

解决

第一步、去官网下最新版本
第二步、找破解方式

迅雷 --> npm
npm init初始化
npm install --save jquery 相当于 迅雷下载电影
用--save存到package.json里面去

用来下载前端工具、库、框架

node --> npm


jquery官网 --> npm docs 库/框架的名字


npm install 名字 --save ---> 项目中真的会用得上的库/框架
npm install 名字 --save-dev --> 用来下载一些压缩、优化我们当前项目代码的前端工具 --save-dev
npm install 名字 -g --> 安装一些前端工具 browser-sync,webpack
npm install -g browser-sync 

developement
<script src=""

webstorm

github
码云


配置
sublime配置

慢慢买 api是http协议 https协议 报错 跨域 
协议、域名、端口只有
api写死放到github上面

动手

can not get /
index.html



hot module reload 更新


gulp
作用：压缩js,css,html,less编译、sass编译、图片优化

task 指定任务名
src  指定要处理的文件
dest 把要处理的文件指定放到哪里
watch 监视