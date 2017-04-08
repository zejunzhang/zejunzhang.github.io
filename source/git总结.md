title: "git总结"
date: 2017-04-02 18:00:00 +0800
update: 2017-04-02 18:00:00 +0800
author: zhengwei
cover: "-/images/github.jpg"
tags:
    - 前端工具
preview: Git是一款开源的版本控制管理工具，它以快速、高效的特点被广泛应用在项目代码的团队协作当中。GitHub是一个使用Git托管的开源代码技术社区，几乎所有我们知道的开源库(框架)都可以去GitHub上面找到相关的下载地址，使用并参与到GitHub上不仅可以帮助我们获取第一手的技术资料、了解最新的技术走向，而且还可以利用GitHub进行代码的托管和管理，对技术人员来说是一个绝佳的学习平台。本文内容将聚焦如何快速入门git和github,主要涉及到git相关概念的理解，常用命令的使用介绍,github网站的使用介绍,常见的git学习资源等

---

## 为什么要对代码进行版本控制

### 场景一
你现在去上班了，在做一个项目，你按照产品的需要说明完成了功能，然后你拿过去给你的产品经理看，产品经理看完以后感觉有些地方不是特别的满意，然后就让你进行修改，你按产品经理的意愿回去修改了几版，但是他最后说你这一版还不如前面那一版好看，不行就用前面一版吧，但是这个时候你发现，你之前改的代码你不记得是怎么写的了~~~

### 场景二
你现在去上班了，被公司的领导分配到了一个技术小组当中，你们团队五六个人一起在开发一个项目，每个人分配到不同的需求，同时在写代码，最后你们的代码写完了，悲剧的是，你们想合并一下代码，但是由于好多文件是由很多人同时在进行修改，不知道到底要用哪个代码，害怕把对方的代码覆盖掉了~~~

### 一个不太成熟的想法
![为什么要使用版本控制软件](-/images/git_01.png)

### 更科学的方式
把项目开发中的每个人的每一次微小的修改记录下来，这样可以根据记录的历史随意的切换到任意一个时间点的代码的状态：

版本 | 用户 | 说明 | 日期 | 修改的代码
---------|----------|---------|---------|---------
 001 | zhengwei | 2016-9-1 10:20 | 添加了首页component | `import HomePage from '@/Component/HomePage.vue'`
 002 | nll | 2016-9-1 10:22 | 添加了路由 | `Vue.use(router)`
 003 | yevon | 2016-9-2 11:33 | 添加了ajax代码 | `created:fetch('http://localhoast:8080/getData')`

### 通俗的理解
git就是一个时光机，我们可以随意的切换到代码的任意一个历史版本
![](-/images/timg.jpg)

## 常用的版本控制软件

### 按类型划分

#### 集中式
![集中式版本控制](-/images/centralized.png)
##### 常见的代表
svn(如果对svn感兴趣或者以后公司用得上的可以参考[svg资料](http://pan.baidu.com/s/1c2zPt9Q))
#### 分布式
![分布式版本控制](-/images/distributed.png)
##### 常见的代表
git

## 集中式 vs 分布式
- 集中式严重依赖于版本控制服务器，如果不能上网或者服务器挂了，则当前的代码不能进行版本管理，相反，分布式可以在当前的电脑进行版本控制
- 如果服务器挂了，则集中式的代码好多将永久性损坏，而分布式只要有一台电脑是好的，大部分代码是可以找回来的

## git安装
### windows电脑安装
[git安装](http://jingyan.baidu.com/article/90895e0fb3495f64ed6b0b50.html)
### mac电脑
mac电脑内置了git软件

### git bash使用注意事项
- 打开方式：在当前项目文件夹中，右键 --> git bash打开
- 可以按住ctrl+鼠标滚轮进行放大缩小 

## 配置用户信息
为了标识出每一个小的修改是谁修改的，我们需要在使用git之前做一些配置
```
$ git config --global user.name "zhengwei1949"
$ git config --global user.email zhengwei1949@qq.com
```

### 注意
- 上面的$大家在敲命令的时候，一定不要输
- 用户名如果没有空格隔开，不需要加双引号
- 建议加上--global配置项，这是一个你的电脑全局性的配置，以后任何项目文件夹在初始化git的时候都不用管这个了

### 查看是否设置正确
```
git config user.name
```

and

```
git config user.email
```

or

```
git config --list
```

## 创建git项目
```
git init
```

![初始化git仓库](-/images/git_init.png)

## 将代码提交到仓库当中
### 工作区、暂存区、仓库
![](-/images/areas.png)

### 一个文件的生命周期
![一个文件的生命周期](-/images/lifecycle.png)

### 将代码提交到仓库的步骤
1. 执行`git add a.html`
2. 执行`git commit "添加a.html到仓库当中"`

### 查看当前代码的状态
```
git status
```

#### 如何知道是哪个状态
- 看颜色法：红色代表处于工作区、绿色代表片于暂存区、白色代表添加到了仓库
- 看单词
    + untracked files --> 处于工作区(新增文件)
    + changes not staged for commited --> 文件被修改，未保存到暂存区
    + changes to be committed --> 处于暂存区，尚未添加到仓库当中

#### 命令简化
- `git add .` --> 添加所有处于工作区文件到暂存区
- `git commit -a -m "添加所有修改的文件直接从工作区到仓库"`

## git忽略文件
把一些没有必要添加到仓库的文件在`.gitignore`当中设置一下

```
.idea
.temp
```

## 版本回退

### 理解版本
![分支](-/images/fenzhi.png)
### 文件差异对比
1. 以工作区为基准，如果暂存区当中添加这个文件但尚未添加到仓库，则比较的是工作区与暂存区，如果暂存区的添加到了仓库，则比较工作区与仓库
```
git diff
```

2. 比较暂存区与仓库代码的区别
```
git diff --cached
```

### 日志的查看
```
git log
```

### 版本回退
![版本回退图](-/images/git-reset.jpg)
![版本回退图](-/images/git_reset.gif)
```
git reset --hard HEAD~0 --> 放弃所有的当前工作区与暂存区代码，回退到与仓库代码一致
git reset --hard HEAD~1 --> 切换到上一次仓库代码
git reset --hard HEAD~2 --> 切换到上上一次仓库代码
```

### 查看所有的版本号
```
git reflog
```
### 根据版本号进行对比
```
git diff 版本号1 版本号2
```

### 根据版本号进行回退
```
git reset --hard 版本号
```

## 配置别名
```
$ git config --global alias.st status
$ git config --global alias.ci commit
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

## 分支
![分支模型](-/images/lr-branches-2.png)
在版本回退里，每次提交，Git会把它们串成一条时间线，这条时间线就是一个分支。截止目前，只有一条时间线，在Git里，这条分支叫主分支，即`master`分支。HEAD严格来说不是指向提交，而是指向`master`,`master`才是指向提交的，所以`HEAD`指向的就是当前分支。
一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用HEAD指向`master`,就能确定当前分支，以及当前分支的提交点。

### 创建分支
```
git branch 分支名
```

### 切换分支
```
git checkout 分支名
```

#### 注意：
切换分支的时候，一定要把当前的仓库的不是在仓库里面的代码提交到仓库(工作区、暂存区)

### 删除分支
```
git branch -d 分支名
```

### 创建并切换分支
```
git checkout -b 分支名
```

## 合并分支
```
git merge 分支名
```

### 如何判断出现了冲突
```
CONFLIT   
```

#### 冲突的原因
两个不同的分支修改了同一个文件的同一行代码，当他们需要合并(git merge)的时候，就会有冲突

#### 冲突什么情况下会出现？
- git merge的时候 --> 也就是分支进行合并的时候，对比两个文件有没有修改同一行代码

### 本地模拟冲突
#### 实验一
a分支上面没有这一行代码，b分支上多了这一行 --> 不会冲突
#### 实验二
a分支和b分支上都多了这一行，但是代码是相同的 --> 不会冲突
#### 实验三
a分支和b分支上都多了这一行，但是代码是不同的 --> 冲突

#### 如何解决冲突
1. 确定我们最终要的代码
2. 执行`git add .`
3. 执行`git commit -m '提交信息'`

## git练习
- 可以玩下level 1就行了 [git在线练习](https://www.codeschool.com/learn/git)

## github
[使用github](http://jingyan.baidu.com/article/f7ff0bfc7181492e27bb1360.html)

## github工作流
```
git init
git add .
git commit -m '代码提交注释'
git remote add origin 仓库地址
git push -u origin master
```

## github配置ssh
[配置github的ssh](http://jingyan.baidu.com/article/a65957f4e91ccf24e77f9b11.html)

## github工作流(更通用版)
```
git clone 仓库地址(或者git init + git remote add origin 仓库地址 + git pull)
git add .
git commit -m '代码提交注释'
git push -u origin master
```

## 推送到远程服务器的时候出现拒绝(rejected)

### 本地代码能推送的前提
- 本地的项目必须是基于远程Repository代码的基础上修改的

### 提交到github被拒绝
#### 什么情况下出现rejected
- 本地代码很旧了，线上的代码有了最新其他的用户提交的最新的代码

#### 解决的办法
- 将远程Repository中的代码git pull拉取到本地(git pull会给我们自动做一个merge,如果出现冲突会提示)
- 然后再进行Push，即可完成代码提交

#### 远程模拟冲突
1. 创建一个github仓库
2. 克隆到本地
3. 在本地创建一个新的文件
4. 推送到服务器上面
5. 在服务器上改代码
6. 尝试修改本地代码，推送到服务器上面

#### 如何解决rejected
1. 执行`git pull origin master`
2. 执行`git add .`
3. 执行`git commit -m 'abc'`
4. 执行`git push`

## tortoiseGit的使用
### 优点
`git add .`,`git commit -m 'wfe'`,`git push`合并成一步 ==> 右键 --> git提交

## git常见问题汇总
[git常见问题汇总](https://github.com/zhengwei1949/git-tips)

## git常用命令汇总

命令 | 含义
---------|----------
 git init | 初始化仓库
 git add . | 把工作区中未保存的文件保存到暂存区
 git commit -m '注释' | 把文件从暂存区提交到仓库
 git status | 查看当前仓库的状态(红色代表的工作区有代码未保存到暂存区，绿色代表有代码未提交到仓库)
 git diff | 查看工作区与暂存区、仓库代码的区别
 git diff --cached | 查看暂存区与仓库代码的区别
 git diff 版本号1 版本号2 | 对比两个版本号的区别 
 git log | 查看提交日志
 git reset --hard HEAD | 撤销当前工作区、暂存区的修改 
 git reset --hard HEAD~0 | 撤销当前工作区、暂存区的修改 
 git reset --hard HEAD~1 | 切换到上一次提交的代码状态
 git reset --hard 版本号 | 切换到某版本号的提交
 git branch 分支名 | 创建分支
 git checkout 分支名 | 切换分支
 git branch -d 分支名 | 删除分支
 git merge 分支名 | 合并分支
 git remote add origin 远程服务器地址 | 提交到远程服务器
 git push -u origin master | 简写push命令(第一次提交)
 git push | 简写push命令(以后的提交)