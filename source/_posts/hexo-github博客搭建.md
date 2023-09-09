---
title: hexo-github博客搭建
date: 2023-09-08 17:32:57
tags:
---

## 搭建步骤

### step1:创建github仓库

```
在Github上创建一个以yourname.github.io为名字的仓库，在填写地址的时候注意，这个地址是就是你的域名，以github.io结尾
```

<img src="./hexo-github博客搭建/创建github仓库.png" style="zoom: 67%;" />

### step2:安装Hexo

```shell
$ mkdir hexo
$ cd hexo
$ npm install -g hexo-cli

注意：需要先安装npm和node.js环境
```



### step3:搭建博客

```shell
$ hexo init myblog # myblog博客项目名称
$ cd myblog
$ npm install
```

新建完成后，生成如下目录

```
myblog/ 
|-- node_modules/   # 放置npm的包
|-- scaffolds/      # 储存文章模板
|-- source/			# 储存文章和部分资源
|-- themes/			# 储存主题
|-- _config.xxx.yml # 是肢体的plus版配置文件（xxx须更改文主题名）
|-- _config.yml		# hexo的主要配置文件
|-- package.json    # npm依赖的包json
|-- package-lock.json
```

### step4:配置

> 因为使用markdown写博客的时候，有时候会插入图片，需要做如下配置才能解决图片不展示问题

```shell
# 1.安装依赖
$ npm install https://github.com/CodeFalling/hexo-asset-image --save

# 2.修改_config.yml中的post_asset_folder设为true
这个配置的意思是每次new post一个博客，会增加一个和博客同名的文件夹

# 3.将博客文章使用的图片放到上面的同名文件夹下
![图片描述]（./文件夹名称/NO1.jpg）

#生成静态文件
$ hexo g 

https://blog.csdn.net/qq_34243930/article/details/109046120
https://blog.csdn.net/kantaiyang/article/details/129159055
https://blog.csdn.net/time888/article/details/70249241
https://www.cnblogs.com/bzsheng/p/13802829.html
```

### step5:新建博客

```shell
#1.创建文章
$ hexo new "hexo-github博客搭建"

#2.进入source\_posts\hexo-github博客搭建.md编辑文章

#3.发布
$ hexo clean  # 清理,但不会删除.deploy_git里的静态文件
$ hexo g #会在public文件夹生成静态博客文件
$ hexo s #本地预览效果  http://localhost:4000/
$ hexo d #会把这个public文件夹的东西拷贝到.deploy_git文件夹里，并把该文件夹里的文件全部推送push到远程库。

#4.访问地址可查看文件（有一定的延迟）
https://29shadow.github.io
```

## 扩展

### 1.Hexo实现多端同步

> 两个电脑，公司一个，家里一个，如何同步写博客？？？

实现方法：使用github来同步博客，将本地的博客内容推送到master分支，多个客户端修改后pull和push

```shell
A客户端将本地博客提交到github的master上
(1)目录下添加.gitignore，添加/.deploy_git和/public
(2)初始化,然后关联远程仓库，然后提交文件到远程仓库
$ git init
$ git remote add origin 远程仓库地址
$ git add .
$ git commit -m "更新说明"
$ git push -u origin master

B客户端拉取远程仓库
(1)同样先安装好node、git、hexo，新建项目文件夹
(2)同步github项目
$ git init
$ git remote add origin 远程仓库地址
$ git fetch
$ git reset --hard origin/master


在多个客户端编辑博客发布后都要进行同步操作
$ git add 
$ git commit -m "更新信息"  
$ git push -u origin master 

同步管理
每次想写博客时，先执行
$ git pull
```



注意

```
推送到github报如下错，需要使用token，不能使用密码了
remote: Support for password authentication was removed on August 13, 2021.

去github的 用户 -> Settings -> Developer Settings -> Personal access tokens -> Generate new token
创建token，将token复制保存，提交的时候，密码输入token就可以了
```

